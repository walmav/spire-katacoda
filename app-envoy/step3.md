
# Deploy customer service application

### Start  `customer service` application by running the following docker compose command:

`docker-compose up customer-service >customer-service.log &`{{execute}}

### Wait for the container to start:

`./waitfor customer-service`{{execute}}

### Check the NGINX Logs to ensure  `customer service` is started:

To view the `nginx` (customer-service component) log:

`cat customer-service.log`{{execute}}
