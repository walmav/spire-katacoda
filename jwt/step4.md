# Validate JWT token with spire-agent

We will again use the spire-agent CLI, this time to valide the JWT token
obtained in the previous step. The JWT is parsed out of the CLI output from
the previous step.

`docker-compose exec spire-agent /opt/spire/bin/spire-agent api validate jwt -audience foo -socketPath /run/spire/sockets/agent.sock -svid $(grep eyJ /tmp/spire-jwt)`{{execute}}
