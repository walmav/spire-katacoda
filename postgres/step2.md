# Deploy SPIRE

Deploy spire-server and spire-agent:

`kubectl apply -k spire`{{execute}}

# Wait for SPIRE to start

Wait for both spire-agent and spire-server to be in Running state before
continuing:

`kubectl get pods -n spire`{{execute}}

**Keep running the above `kubectl get` command until both pods are in the `Running`
state.**

# SPIRE logs

To look at spire-server logs:

`kubectl logs -n spire --selector app=spire-server`{{execute}}

To look at spire-agent logs:

`kubectl logs -n spire --selector app=spire-agent`{{execute}}

**It will take about 30 seconds for SPIRE pods to start.**

# When SPIRE pods are Running, continue to the next step
