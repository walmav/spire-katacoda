# Launch envoy

Next, we'll deploy the envoy proxy, which handles all the SPIFFE/SPIRE work
such as SVID, certificate rotation, terminating mTLS, and so on.

`docker-compose up customer-service-envoy >customer-service-envoy.log &`{{execute}}

# Wait for container to start

`./waitfor customer-service-`{{execute}}

# Logs

To view the `envoy` (customer-service component) log:

`cat customer-service-envoy.log`{{execute}}
