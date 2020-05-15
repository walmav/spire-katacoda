# Register SPIRE workloads

The following script will create workload and node attestation registration
entries in SPIRE. Workloads are registered on spire-server:

`cat spire/register_workloads`{{execute}}

Note that workload entries are created with a TTL of 60 seconds. This means
that certificates will have a 60 second lifecycle and will be rotated prior to
expiration.

Run the script:

`bash spire/register_workloads`{{execute}}

Show the registration entries:

`kubectl exec -n spire spire-server-0 -- /opt/spire/bin/spire-server entry show`{{execute}}
