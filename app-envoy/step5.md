## Launch webapp

Launch the webapp:

`docker-compose up webapp >webapp.log &`{{execute}}

You can immediately run the following command to wait for the container to start:

`./waitfor webapp`{{execute}}

When you see `Creating root_webapp_1 ... done`, view the `webapp` log:

`cat webapp.log`{{execute}}

You should see `Status: Downloaded newer image for
us.gcr.io/scytale-registry/symbank-webapp-go-api:1.0.1` in the log.
