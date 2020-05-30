# Test Service

Run the customer service application to list a customer in the Postres database:

`curl $(kubectl get service customer -o jsonpath="{..spec.clusterIP}"):8000/customers/1`{{execute}}

The `customer` API is very simple:

+ Fetch all customers: `/customers`
+ Fetch a single customer by ID: `/customers/ID`

In the previous step, we seeded the database with two customers, having IDs `1` and
`2`.

# Revisit logs

This is a good time to review all the log
files.

+ The spire-server and spire-agents logs will show SVID creation and rotation, and
  workload attestation.
  
  `kubectl logs -n spire --selector app=spire-server`{{execute}}

+ The postgres logs will show configuration reloads as certificates are rotated.
  
  `kubectl logs --selector app=postgres --container=postgres`{{execute}}

+ The customer logs will show the connection string used to access postgres.
  
  `kubectl logs --selector app=customer --container=customer`{{execute}}

+ The spiffe-helper logs will show output from the commands executed when
  certificates are rotated.
  
  `kubectl logs --selector app=customer --container=spiffe-helper`{{execute}}

  Certificates are rotated based on the expiration time, which is controlled
  by the TTL value in SPIRE registration entries.
