# Connect Backend

Pgweb offers a way to create new connection with credentials obtained from a third
party API. This is a useful feature for people who run Pgweb for their clients and
need the ability to setup connections without any UI interactions. It is possible
now with the new Connect Backend Feature.

## Overview

Let say you are running a service that in an addition to it's main features also
has a page for users to access their database. The database browsing experience 
is powered by Pgweb, so you would have an url like `https://pgweb.awesomecorp.com/connect/:token`,
where `token` is something that you generate for each of your customers.

Now, the user could visit their postgres resources using `https://pgweb.awesomecorp.com/connect/test` 
and under the hood pgweb will make a HTTP (HTTPS supported too) call to the internal API to obtain
the database credentials based on the token in the url. If you're running pgweb behind an [oauth2-proxy](https://github.com/bitly/oauth2_proxy) or any other similar software you could also pass through a set
of headers (authentication, etc) for any extra validations. Once the credentials are obtained, pgweb
will setup a new session that will only work in a single browser tab. This is how the existing
multi-session support is implemented.

## Usage

To start the pgweb with connect backend feature use the following flags:

```
--connect-backend= Enable database authentication through a third party backend
--connect-token=   Authentication token for the third-party connect backend
--connect-headers= List of headers to pass to the connect backend
```

Connect backend feature work only when `--sessions` flag is provided since pgweb
runs in a single session mode by default.

Example:

```bash
pgweb \
  --sessions \
  --connect-backend=http://localhost:4567/my-endpoint \
  --connect-token=api-token
```

Next, you will need to setup your connect api endpont. Here's an example in Sinatra:

```ruby
require "sinatra"

# Authentication token
$token = "test"

# List of all availble resources
$resources = {
  "id1" => "postgres://localhost:5432/db1?sslmode=disable",
  "id2" => "postgres://localhost:5432/db2?sslmode=disable",
  "id3" => "postgres://localhost:5432/db3?sslmode=disable"
}

helpers do
  def error(code, message)
    halt(code, JSON.dump(error: message))
  end
end

before do
  content_type :json
end

post "/" do
  req = JSON.load(request.body)

  # Check the resource
  resource = $resources[req["resource"]]
  if !resource
    halt 404
  end
  
  # Return connection credentials
  JSON.dump(
    database_url: resource
  )
end
```

Copy and paste the code above into `app.rb` and then run:

```
ruby app.rb
```

Good, now your API is up and running.

Every time user visit the connect url, like `https://pgweb.yourcopr.com/connect/resource_id`, pgweb
will generate a JSON payload. Example request:

```json
{
  "resource": "resource_id",
  "token": "api-token",
  "headers": {
    "x-forwarded-access-token": "...",
    "x-forwarded-email": "...",
    "x-forwarded-user": "..."
  }
}
```

By default headers will not be included in the payload. To enable pass-through of the headers,
list them in as a CLI argument:

```
--connect-headers=X-Forwarded-Access-Token,X-Forwarded-Email,X-Forwarded-User
```

Header name intended for the passthrough will be converted to the converted to the lower case. 
Header values will be left untouched.

In order to establish the connection on pgweb's side, your API must respond with HTTP status 200.
Any other error codes will trigger the connection error and be aborted.
