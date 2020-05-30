# Register SPIRE workload entries

We create two workload entries in SPIRE Server - one for the
`customer-service` Envoy container, and another for the `webapp` front-end.

Create entry for `customer-service-envoy` container:

`docker-compose exec spire-server /opt/spire/bin/spire-server entry create \
-spiffeID spiffe://example.local/customer-service \
-parentID spiffe://example.local/node \
-selector unix:path:/usr/local/bin/envoy \
-ttl 30`{{execute}}

Create an entry for `webapp` container:

`docker-compose exec spire-server /opt/spire/bin/spire-server entry create \
-spiffeID spiffe://example.local/webapp \
-parentID spiffe://example.local/node \
-selector unix:path:/opt/symbank-webapp/symbank-webapp \
-ttl 30`{{execute}}
