# Register SPIRE workloads

The following script creates attestation registration entries on the
SPIRE Server for the nodes (hosts), Postgres database, and the
sample application:

`cat spire/register_workloads`{{execute}}

Note that workload entries are created with a TTL of 60 seconds. This means
that certificates will have a 60 second lifecycle and will be rotated prior to
expiration.

Run the script:

`bash spire/register_workloads`{{execute}}

The output shows the three SPIFFE IDs created and the selectors used
to uniquely identify each registration entry.

To see the registration entries again at a later time, you can run the following command:

`kubectl exec -n spire spire-server-0 -- /opt/spire/bin/spire-server entry show`{{execute}}
