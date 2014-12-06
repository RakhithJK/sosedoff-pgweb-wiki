Build the image:

```
docker build -t pgweb .
```

Start container:

```
docker run [OPTIONS of docker] pgweb [OPTIONS of pgweb]
```

### Example

Run postgresql container:

```
docker run -d \
           --name="postgresql" \
           -p 5432:5432 \     
           -e USER="testuser" \
           -e DB="testdb" \
           -e PASS="test123" \
           paintedfox/postgresql
```

Run pgweb container:

```
docker run -d \
           -p 8080:8080 pgweb \
           --url postgres://testuser:test123@your-ip:5432/testdb \
           --bind 0.0.0.0
```

Then open [http://your-ip:8082](#) in your browser.