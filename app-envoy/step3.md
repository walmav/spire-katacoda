# Deploy Customer Service

Deploy NGINX serving static content to simulate Customer Service JSON API. The
`webapp` application uses the JSON API to fetch data. We deploy Envoy proxy in the next step to proxy requests from the webapp to NGINX.

`docker-compose up customer-service >customer-service.log &`{{execute}}

# Wait for container to start

`./waitfor customer-service`{{execute}}

# Logs

To view the `nginx` (customer-service component) log:

`cat customer-service.log`{{execute}}
