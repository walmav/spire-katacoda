Get latest SPIRE release tar:
 `wget https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Extract the tar:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Configure jwt issues configuration:
Set `jwt_issuer = ` value to https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/

`sed 's/<JWT_ISSUER>/https:\/\/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g server.conf`{{execute HOST1}} 