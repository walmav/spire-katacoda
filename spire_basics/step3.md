
The next step is to register a SPIFFE ID with a set of selectors. We will use unix kernel selectors that will be mapped to a target SPIFFE ID.

Create a user with uid 1001. The uid will be registered as a selector of the workload's SPIFFE ID. During kernel based attestation the workload process will be interrogated for the registered uid.
`useradd -u 1001 workload`{{execute}} 

Create Workload Registration Entry:
`/opt/spire-0.9.1/bin/spire-server entry create \
-spiffeID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/workload \
-parentID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/clientnode \
-selector unix:uid:1001`{{execute}} 

Simulate the workload API interaction and retrieve the workload SVID bundle by running the api subcommand in the agent. Run the command as user workload created in earlier with uid 1000
`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 " workload`{{execute}} 

Examine the output. Optionally, you may write the SVID and key to disk with -write in order to examine them in detail.
`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 -write ~/" workload` {{execute}} 

`su -c "openssl x509 -in ~/svid.0.pem -text -noout"  workload`{{execute}} 