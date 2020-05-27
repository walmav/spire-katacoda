# Providing dynamic service identities to Envoy workloads through SPIRE

Envoy is a popular open-source service proxy that, among other things, is widely used to provide abstracted, secure, authenticated and encrypted communication between services. Envoy enjoys a rich configuration system that allows for flexible third-party interaction.
One component of this configuration system is the Secret Discovery Service protocol or SDS. Envoy uses SDS to retrieve and maintain updated “secrets” from SDS providers. In the context of authentication, these secrets are the TLS certificates, private keys, and trusted CA certificates Envoy uses to provide secure TLS communication between services.

When Envoy connects to the SDS server the SPIRE Agent attests Envoy and determines which service identities and CA certificates it should make available to Envoy over SDS.

The `customer service` backend is serving static content using NGINX to simulate Customer Service JSON API. The
`webapp` frontend is configured to fetch data from the JSON API exposed by the `customer service`. Envoy is deployed to proxy requests on behalf of the `customer service`.

The `webapp` frontend is written in `go` and uses the native `go-spiffe` library to obtain its [x509 SVID](https://github.com/spiffe/spiffe/blob/master/standards/X509-SVID.md) and Establishing mutually authenticated TLS (mTLS) with the `customer service` backend. 
 Although out of scope in this context, the detailed documentation of using go-spiffe library is here: [go-spiffe v2 documentation and examples](https://pkg.go.dev/github.com/spiffe/go-spiffe/v2?tab=overview)


![Scenario diagram](assets/scenario-diagram.png)
