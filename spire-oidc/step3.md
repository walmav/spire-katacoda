Get latest SPIRE release tar:
 `wget https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST2}}

Extract the tar:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST2}}

Set `trust_domain` to [[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com in agent.conf
`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' agent.conf`{{execute HOST2}}

Set `server_address` to [[HOST_SUBDOMAIN]]-8081-[[KATACODA_HOST]].environments.katacoda.com in agent.conf
`sed -i 's/<SPIRE_SERVER>/[[HOST_SUBDOMAIN]]-8081-[[KATACODA_HOST]].environments.katacoda.com/g' agent.conf`{{execute HOST2}}

Generate token for Join Token based attestation on the SPIRE Server: 
`./spire-0.9.1/bin/spire-server token generate -spiffeID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/clientnode`{{execute HOST1}}

Create Workload Registration Entry:
`./spire-0.9.1/bin/spire-server entry create -spiffeID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/oidc-test-workload -parentID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/clientnode -selector unix:uid:1001`{{execute HOST1}} 

Start SPIRE Agent
Run the command below on Host 2 Terminal replacing the <JOIN_TOKEN> placeholder with the token generated earlier
`./spire-0.9.1/bin/spire-agent run -config agent.conf -joinToken <JOIN_TOKEN> &`{{copy}}
