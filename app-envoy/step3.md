## Start customer service application

Start the `customer-service` application by running the following
`docker-compose` command:

`docker-compose up customer-service >customer-service.log &`{{execute}}

You can immediately run the following command to wait for the container to start:

`./waitfor customer-service`{{execute}}

When you see `Creating root_customer-service_1 ... done` and the
`host01 $` prompt, check the NGINX log to ensure `customer service`
is started:

`cat customer-service.log`{{execute}}

The log should contain the phrase `Configuration complete; ready for start up`.
