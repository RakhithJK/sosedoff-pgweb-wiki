Exposing Pgweb interface to public internet poses a huge risk, especially if not properly secured. A common use case is providing an easy UI for developers/data folks, and let them run ad-hoc queries in the UI instead of connecting directly to the database, which most likely is not available without VPN access. Distributing database credentials is also a bad idea in general.

Pgweb by itself does not provide any means of authenticating users based on identity providers such as Google or Github, and only supports HTTP basic authentication out of the box, via `--auth-user` and `--auth-pass` CLI options. This may work for one-off setups, but not very scalable on organization level (we still need to share password, etc).

## Auth proxy

A tool like [oauth2-proxy](https://oauth2-proxy.github.io/oauth2-proxy/) comes very handy for a use case like that! We could easily integrate with over 10 identity providers in a generic way. Most folks would use Google, so that's what we're going to use as an example moving forward.

## Testing locally

Follow these steps to configure Google OAuth for locally running Pgweb.

1. Make sure to download the latest `oauth2-proxy` release. Head over to Github: https://github.com/oauth2-proxy/oauth2-proxy/releases
2. Next, we need to create and configure a new Google project, head over to [Developer Console](https://console.cloud.google.com/apis/dashboard). Once you create a new project, you must configure `Oauth Concent screen`, this is where you can pick `Internal` or `External` user type. Pick `Internal` if your Google organization permits (that'll allow logging in only with corp email), otherwise `External` will be okay for testing. Follow prompts for application setup.
3. Switch to `Credentials` section and click on `Create Credentials`. From the dropdown, pick `OAuth Client ID`. Next, enter `Web Application` in the `Application Type` dropdown.
4. On the same page, enter `http://localhost:4180/oauth2/callback` into `Authorized redirect URIs` input field. Hit `Create`.
5. On the next screen you will be prompted the OAuth client ID and secret ID, save these values as we will need them to configure our OAuth in the next step.

To start the proxy, replace `--client-id`, `--client-secret` and `--cookie-secret` values:

```bash
./oauth2-proxy \
  --skip-provider-button=true \
  --provider=google \
  --client-id=<REPLACE ME: OAUTH_CLIENT_ID> \
  --client-secret=<REPLACE ME: OAUTH CLIENT SECRET> \
  --cookie-secret=<GENERATE RANDOM STRING> \
  --cookie-expire=4h0m0s \
  --email-domain='*' \
  --http-address=0.0.0.0:4180 \
  --upstream=http://localhost:8081 \
  --redirect-url=http://localhost:4180/oauth2/callback
```

Keep in mind, the `--email-domain='*'` setting will allow ANY Google email, which is okay for testing, but should be swapped out for real deployments.

Next, in the new terminal window, start pgweb process:

```bash
pgweb --db=my-awesome-database --bind=0.0.0.0
```

If everything configured correctly, you should be able to hit the endpoints:

- `http://localhost:8081` - Pgweb UI, should work if your database exists, make sure you have it running first before trying to authenticate with Google
- `http://localhost:4180` - On the first visit you will be redirected to Google OAuth consent page, you can choose any Google account from there.

You're all set. For any additional information on provider setup, visit [official documentation](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/oauth_provider#google-auth-provider).

## Troubleshooting

A few things may go wrong with the setup, common issues are:

- Not adding the correct redirect URL in the `Authorized redirect URIs` in Google Developer Console. Make sure to add new URLs when deploying OAuth proxy on multiple domains/endpoints.
-  Not setting up the correct `--upstream` with Pgweb. Pgweb DOES NOT listen on `0.0.0.0` address (any network interface) by default, you should enable that option with `--bind=0.0.0.0` .This is only necessary if your `oauth2-proxy` process is not running on the same machine as `pgweb`. 