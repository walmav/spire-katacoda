# Obtain a JWT token

We will now use the spire-agent CLI to obtain a JWT token. This uses the
workload API.

`docker-compose exec spire-agent /opt/spire/bin/spire-agent api fetch jwt -audience foo -socketPath /run/spire/sockets/agent.sock >/tmp/spire-jwt`{{execute}}

# Dump the JWT and EC key coordinates

`cat /tmp/spire-jwt`{{execute}}
