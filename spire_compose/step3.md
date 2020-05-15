# Examine SPIRE workload entries

The join token created a node entry for `spire://example.local/spire/node`
as specified when we generated the token. Examine this entry with:

`docker-compose exec spire-server /opt/spire/bin/spire-server entry show`{{execute}}
