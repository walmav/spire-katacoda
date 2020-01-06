Get latest SPIRE release tar:
 `wget https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Extract the tar:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Set `trust_domain` to [[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com in server.conf

`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' server.conf`{{execute HOST1}}


Set `jwt_issuer`  config to https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com in server.conf

`sed -i 's/<JWT_ISSUER>/https:\/\/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' server.conf`{{execute HOST1}}

Start SPIRE Server:

`./spire-0.9.1/bin/spire-server run -config spire-0.9.1/conf/server/server.conf &`{{execute HOST1}}