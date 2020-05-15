# Deploy Postgres

Apply the deployment:

`kubectl apply -k postgres`{{execute}}

Wait for Postgres to start:

`kubectl get pod --selector=app=postgres`{{execute}}

Two containers in this pod are launched - `postgres` for the database, and
`spiffe-helper` which handles TLS certificates and rotation.

# Postgres logs

To look at postgres logs:

`kubectl logs --selector app=postgres --container=postgres`{{execute}}

To look at spiffe-helper logs:

`kubectl logs --selector app=postgres --container=spiffe-helper`{{execute}}

**It will take about 30 seconds for the postgres pod to start.**

# When the postgres pod is Running, continue to the next step
