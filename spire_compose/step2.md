# Launch SPIRE agent

Copy the trust domain certificate bundle from SPIRE server into SPIRE agent
(`/tmp/spire-agent` will be mounted in the SPIRE container as `/run/spire`).

`docker-compose exec spire-server /opt/spire/bin/spire-server bundle show > /tmp/spire-agent/bootstrap.crt`{{execute}}

Create a join token, and copy to the SPIRE container directory:

`TOKEN=$(docker-compose exec spire-server /opt/spire/bin/spire-server token generate -spiffeID spiffe://example.local/node | awk '{print $2}' | tr -d '\r')`{{execute}}

`echo $TOKEN`{{execute}}

`sed -i "s/TOKEN/${TOKEN}/" /tmp/spire-agent/agent.conf`{{execute}}


Start SPIRE agent container:

`docker-compose up spire-agent &`{{execute}}
