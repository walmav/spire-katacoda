# Launch webapp

Launch the webapp

`docker-compose up webapp >webapp.log &`{{execute}}

# Wait for container to start

`./waitfor webapp`{{execute}}

# Logs

To view the `webapp` log:

`cat webapp.log`{{execute}}
