## Configure SPIRE Agent Cluster

Click **envoy.yaml** in the frame to the right of this text to
display the Envoy configuration file.

Envoy must be configured to communicate with the SPIRE Agent by configuring a cluster that points to the Unix domain socket the SPIRE Agent provides.
The `connect_timeout` for `spire-agent` influences how fast Envoy will be able to respond if the SPIRE Agent is not running when Envoy is started or if the SPIRE Agent is restarted.

Click **Copy to Editor** to insert the `connect_timeout` for
`spire-agent` configuration into the Envoy configration file.

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

Click **Copy to Editor** to insert the SDS configuration into the
Envoy configuration file.

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

Click **Copy to Editor** to insert the validation context configuration into the
Envoy configuration file.

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
</pre>

## Launch Envoy

Next, we'll deploy the Envoy proxy, which handles all the SPIFFE/SPIRE work
such as SVID management, certificate rotation, terminating mTLS, and so on.

Start Envoy by running the following `docker-compose` command:

`docker-compose up customer-service-envoy >customer-service-envoy.log &`{{execute}}

You can immediately run the following command to wait for the container to start:

`./waitfor customer-service-`{{execute}}

Check the Envoy log to ensure Envoy has started:

`cat customer-service-envoy.log`{{execute}}

At the end of the log, you should see `all dependencies initialized. starting workers`.
