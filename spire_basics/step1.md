Get latest SPIRE release tar:
 `wget https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute}}

Extract the tar:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz -C /opt/`{{execute}}

Look at all the files in the untar directory:
`ls -lrt spire-0.9.1`{{execute }}

Look at the server configuration file:
`cat server.conf`{{execute}}

TRUST DOMAIN:
The trust domain corresponds to the trust root of a system. A trust domain could represent an individual, organization, environment or department running their own independent SPIFFE infrastructure. All workloads identified in the same trust domain are issued identity documents that can be verified against the root keys of the trust domain.

Configure the `trust_domain` of the SPIRE Server in server.conf, This can be set to any arbitrary host part of the authority component of the URI as defined in the SPIFFE standard: https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE-ID.md#21-trust-domain

`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' server.conf`{{execute}}

Start SPIRE Server:

`/opt/spire-0.9.1/bin/spire-server run -config server.conf &`{{execute}}