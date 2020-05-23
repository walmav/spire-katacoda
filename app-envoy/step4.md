# Envoy Configuration
When Envoy connects to the SDS server the SPIRE Agent attests Envoy and determines which service identities and CA certificates it should make available to Envoy over SDS.
As service identities and CA certificates are rotated, updates are streamed back to Envoy, which can immediately apply them to new connections without interruption or downtime and without the private keys ever having to touch the disk. In other words, SPIRE’s rich methods of defining and attesting services can be used to target the Envoy process, define an identity for it, and provide it with X.509 certificates and trust information that Envoy can use for TLS communication.


## Configure SPIRE Agent Cluster:
Envoy must be configured to communicate with the SPIRE Agent by configuring a cluster that points to the Unix domain socket the SPIRE Agent provides.
The connect_timeout influences how fast Envoy will be able to respond if the SPIRE Agent is not running when Envoy is started or if the SPIRE Agent is restarted.

<pre class="file" data-filename="envoy.yaml" data-target="insert" data-marker="#ADD_SPIRE_AGENT_CLUSTER">

  - name: spire_agent
    connect_timeout: 0.25s
    http2_protocol_options: {}
    hosts:
      - pipe:
          path: /run/spire/sockets/agent.sock
</pre>

## Configure TLS Context
To obtain a TLS certificate and private key from SPIRE, you can set up an SDS configuration within a TLS context.
The name of the TLS certificate is the SPIFFE ID of the service that Envoy is acting as a proxy for.
<pre class="file" data-filename="envoy.yaml" data-target="insert" data-marker="#ADD_TLS_CONTEXT">
      tls_context:
        common_tls_context:
          tls_certificate_sds_secret_configs:
          - name: "spiffe://example.local/customer-service"
            sds_config:
              api_config_source:
                api_type: GRPC
                grpc_services:
                  envoy_grpc:
                    cluster_name: spire_agent
</pre>

## Configure Validation Context
Envoy uses trusted CA certificates to verify peer certificates. Validation Contexts provide these trusted CA certificates. SPIRE can provide a validation context per trust domain.
To obtain a validation context for a trust domain, you can configure a validation context within the SDS configuration of a TLS context, setting the name of the validation context to the SPIFFE ID of the trust domain.
<pre class="file" data-filename="envoy.yaml" data-target="insert" data-marker="#ADD_VALIDATION_CONTEXT">
          combined_validation_context:
            # validate the SPIFFE ID of incoming clients
            default_validation_context:
              verify_subject_alt_name:
                - "spiffe://example.local/webapp"
            # obtain the trust bundle from SDS
            validation_context_sds_secret_config:
              name: "spiffe://example.local"
              sds_config:
                api_config_source:
                  api_type: GRPC
                  grpc_services:
                    envoy_grpc:
                      cluster_name: spire_agent
          tls_params:
            ecdh_curves:
              - X25519:P-256:P-521:P-384

# Launch Envoy

Next, we'll deploy the envoy proxy, which handles all the SPIFFE/SPIRE work
such as SVID, certificate rotation, terminating mTLS, and so on.

`docker-compose up customer-service-envoy >customer-service-envoy.log &`{{execute}}

# Wait for container to start

`./waitfor customer-service-`{{execute}}

# Logs

To view the `envoy` (customer-service component) log:

`cat customer-service-envoy.log`{{execute}}
