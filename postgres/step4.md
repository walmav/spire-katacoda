# Deploy Postgres

Apply the Postgres deployment:

`kubectl apply -k postgres`{{execute}}

Use the following command to check that the Postgres pod is in a Running state:

`kubectl get pod --selector=app=postgres`{{execute}}

Keep running the above `kubectl get` command until the pod is displayed as `Running`
underneath `STATUS`.

**It will take about 30 seconds for the pod to start.**

Two containers in this pod are launched - `postgres` for the database,
and `spiffe-helper` which handles TLS certificates and rotation. To
verify these containers, run:

`kubectl get pods -l app=postgres -o jsonpath='{.items[*].spec.containers[*].name}{"\n"}'`{{execute}}

# Postgres logs

As you go through this demo, you may want to check the Postgres and
the Postgres `spiffe-helper` logs to see how various actions affect
each of them.

To look at Postgres log:

`kubectl logs --selector app=postgres --container=postgres`{{execute}}

It's normal to see `received SIGHUP, reloading configuration files` in
the Postgres log at this point in the demo.

To look at spiffe-helper log:

`kubectl logs --selector app=postgres --container=spiffe-helper`{{execute}}

# When the postgres pod is Running, continue to the next step
