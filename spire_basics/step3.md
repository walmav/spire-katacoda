Now that both SPIRE Server and SPIRE Agent are up and running, you want to see how SPIRE works in action and check how workloads are identified. 

The next step is to register a SPIFFE ID and a set of selectors that need to matched to obtain that SPIFFE ID. This is the SPIFFE ID of a workload that would start in this environment and retrieve its identity after being attested. To identify this workload,  we will define selectors that will be mapped to a target SPIFFE ID. For the purpose of this exercise, the selectors use will be unix kernel based. 

1. Create a user with uid 1001. The uid will be registered as a selector of the workload's SPIFFE ID. During kernel based attestation the workload process will be interrogated for the registered uid.
`useradd -mu 1001 workload`{{execute}} 

2. Create Workload Registration Entry:
`/opt/spire-0.9.1/bin/spire-server entry create \
-spiffeID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/workload \
-parentID spiffe://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/clientnode \
-selector unix:uid:1001`{{execute}} 

3. As a way to simulate the workload API interaction and retrieve the workload SVID bundle a workload would obtain you can run the following api subcommand in the agent. Run the command as a user "workload" created in step 1 with uid 1000:
`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 " workload`{{execute}} 

4. Examine the output. 

5. Optionally, you may write the SVID and key retrieved to disk with -write in order to examine in more detail.

`su -c "/opt/spire-0.9.1/bin/spire-agent api fetch x509 -write ~/" workload`{{execute}} 

`su -c "openssl x509 -in ~/svid.0.pem -text -noout"  workload`{{execute}} 
