## Launch webapp

Launch the webapp:

`docker-compose up webapp >webapp.log &`{{execute}}

You can immediately run the following command to wait for the container to start:

`./waitfor webapp`{{execute}}

When you see `Creating root_webapp_1 ... done`, view the `webapp` log:

`cat webapp.log`{{execute}}

You should see a line similar to the following in the log:
 `webapp_1                  | 2020/06/02 20:33:07 Server "0.0.0.0:8080"`
