# Using Envoy to Provide Dynamic Service Identity using SPIRE

Envoy is a popular open-source service proxy that, among other things, is widely used to provide abstracted, secure, authenticated and encrypted communication between services. Envoy enjoys a rich configuration system that allows for flexible third-party interaction.
One component of this configuration system is the Secret Discovery Service protocol or SDS. Envoy uses SDS to retrieve and maintain updated “secrets” from SDS providers. In the context of authentication, these secrets are the TLS certificates, private keys, and trusted CA certificates Envoy uses to provide secure TLS communication between services.

When Envoy connects to the SDS server the SPIRE Agent attests Envoy and determines which service identities and CA certificates it should make available to Envoy over SDS.

The `customer service` backend is serving static content using NGINX to simulate Customer Service JSON API. The
`webapp` frontend is configured to fetch data from the JSON API exposed by the `customer service`. Envoy is deployed to proxy requests on behalf of the `customer service`.

#Deploy `customer service` application

### Start  `customer service` application by running the following docker compose command:

`docker-compose up customer-service >customer-service.log &`{{execute}}

### Wait for the container to start:

`./waitfor customer-service`{{execute}}

### Check the NGINX Logs to ensure  `customer service` is started:

To view the `nginx` (customer-service component) log:

`cat customer-service.log`{{execute}}
