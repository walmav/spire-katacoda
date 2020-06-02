Now that both SPIRE Server and SPIRE Agent are running, let's see how SPIRE works in action and how workloads are identified.

The next step is to register a SPIFFE ID for a workload using one or more unique environment characteristics called "selectors". Selectors can be a Unix UID, Unix group, AWS IID, etc. These selectors form a kind of fingerprint for one or more workloads.

Create a user with a UID of 1001:
`useradd -mu 1001 workload`{{execute}}

Register the UID of 1001 as a selector on the SPIRE Server:
`/opt/spire-0.9.1/bin/spire-server entry create \
-spiffeID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/workload \
-parentID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/clientnode \
-selector unix:uid:1001`{{execute}}
You will see the output from the command first showing the newly created SPIFFE ID and its parent ID, followed by log messages from the SPIRE Server that show the registration occurring.

Later, when a workload requests authorization, SPIRE verifies the authenticity of the workload by introspecting the kernel for the workload's UID and comparing it with the registered UID value associated with the SPIFFE ID.

To simulate the workload API interaction and retrieve the workload SVID bundle that a workload would obtain, run the following api option using the SPIRE Agent binary:
`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 " workload`{{execute}}
A workload proves its identity to a resource or caller using an SVID (SPIFFE Verifiable Identity Document). An SVID contains the workload's SPIFFE ID in cryptographically-verifiable certificate or token.

The output from the previous command displays the TTL of the SVID, which are typically kept short for security purposes.

To show what the SVID looks like, first save the SVID and key to disk:
`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 -write ~/" workload`{{execute}}

Then, decode and print the SVID:
`su -c "openssl x509 -in ~/svid.0.pem -text -noout"  workload`{{execute}} 
