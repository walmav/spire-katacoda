# Test Service

`curl $(kubectl get service customer -o jsonpath="{..spec.clusterIP}"):8000/customers/1`{{execute}}

The `customers` API is very simple:

+ Fetch all customers: `/customers`
+ Fetch a single customer by ID: `/customers/ID`

In the previous step, we seeded the DB with two customers, having IDs `1` and
`2`.

# Revisit logs

This is a good time to go back to the previous steps and review all the log
files.

+ spire-server and spire-agents logs will show SVID creation and rotation, and
  workload attestation.
+ postgres logs will show configuration reloads as certificates are rotated.
+ customer logs will show the connection string used to access postgres.
+ spiffe-helper logs will show output from the commands executed when
  certificates are rotated.

Certificates are rotated based on the expiration time, which is controlled
by the TTL value in SPIRE registration entries.
