# Launch nginx

nginx is being used to simulate an application with a JSON API that the
`webapp` application uses to fetch data. An envoy proxy will be deployed in
the next step to proxy requests from the webapp to nginx.

`docker-compose up customer-service >customer-service.log &`{{execute}}

# Wait for container to start

`./waitfor customer-service`{{execute}}

# Logs

To view the `nginx` (customer-service component) log:

`cat customer-service.log`{{execute}}
