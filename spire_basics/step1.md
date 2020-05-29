Download the SPIRE tarball:
`wget --no-verbose --show-progress https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute}}

Extract the tarball:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz -C /opt/`{{execute}}

The tarball includes: 
* The spire-agent and spire-server binaries
* Configuration files for the SPIRE Agent and Server

Before we install the server, let's see the server configuration file:
`cat server.conf`{{execute}}

Configure the `trust_domain` of the SPIRE Server in server.conf. The value corresponds to the host part of the authority component of the URI as defined in the SPIFFE standard: https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE-ID.md#21-trust-domain

`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' server.conf`{{execute}}

Note: The trust domain represents to the trust root of a system. A trust domain can be an individual, organization, environment or department running their own independent SPIFFE infrastructure. All workloads identified in the same trust domain are issued identity documents that can be verified against the root keys of the trust domain.

Make any other necessary modifications to the server file. For the purpose of this exercise we won't be making any other changes.

Next, start SPIRE Server:

`/opt/spire-0.9.1/bin/spire-server run -config server.conf &`{{execute}}
