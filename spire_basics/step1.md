Download the SPIRE tarball:
`wget --no-verbose --show-progress https://github.com/spiffe/spire/releases/download/0.9.1/spire-0.9.1-linux-x86_64-glibc.tar.gz`{{execute}}

Extract the tarball:
`tar -xvf spire-0.9.1-linux-x86_64-glibc.tar.gz -C /opt/`{{execute}}

The tarball includes:
* The spire-agent and spire-server binaries
* Configuration files for the SPIRE Agent and Server

Let's see the server configuration file:
`cat server.conf`{{execute}}

Before we run the server, we'll need to set the `trust_domain` in `server.conf`.

A trust domain is an arbitrary identifier for a group of entities that expect to communicate securely. The group can be an organization or a set of hosts, such as the host of an application and the host of a database. Each SPIRE server has a single, unique trust domain.

The trust domain is the root element in a SPIFFE ID. A SPIFFE ID is a URI in the format `spiffe://trust domain/workload identifier` that uniquely identifies a workload for SPIRE authentication.

So let's set our trust domain:
`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' server.conf`{{execute}}

We'll verify the change:
`grep katacoda server.conf`{{execute}}

For this demo, the trust domain is set to the Katacoda host name.

The other Spire Server configuration options are OK as is for this simple demo. If you are really curious about them, see [Server configuration file](https://github.com/spiffe/spire/blob/master/doc/spire_server.md#server-configuration-file).

Start the SPIRE Server:
`/opt/spire-0.9.1/bin/spire-server run -config server.conf &`{{execute}}
Since we haven't set a `log_file` or redirected the output, log messages from SPIRE Server are printed to the console.
