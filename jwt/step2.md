# Register SPIRE workload entries

We need to create a workload entry in spire-server - This will allow
spire-agent to be a workload itself where it's CLI can be used to obtain a
JWT.

# Create workload entry for spire-agent CLI

`docker-compose exec spire-server /opt/spire/bin/spire-server entry create \
-spiffeID spiffe://example.local/spire-agent \
-parentID spiffe://example.local/node \
-selector unix:path:/opt/spire/bin/spire-agent`{{execute}}
