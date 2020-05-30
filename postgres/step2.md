# Deploy SPIRE

Deploy spire-server and spire-agent:

`kubectl apply -k spire`{{execute}}

# Wait for SPIRE to start

Use the following command to check that both spire-agent and spire-server are in a Running state:

`kubectl get pods -n spire`{{execute}}

Keep running the above `kubectl get` command until both pods are displayed as `Running`
underneath `STATUS`.

**It will take about 30 seconds for the SPIRE pods to start.**

# SPIRE logs

As you go through this demo, you may want to check the SPIRE Server
and Agent logs to see how various actions affect each of them.

To look at spire-server log:

`kubectl logs -n spire --selector app=spire-server`{{execute}}

In the SPIRE Server log you should see a line similar to the following
to indicate that SAT attestation has completed:
`time="2020-05-30T00:13:12Z" level=info msg="Node attestation request completed" address="10.32.0.1:43428" attestor=k8s_sat method=node_api spiffe_id="spiffe://example.k8s.local/spire/agent/k8s_sat/example.k8s.local/642ae7cd-77af-4c95-99bd-ea815dd998a2" subsystem_name=node_api`

To look at spire-agent log:

`kubectl logs -n spire --selector app=spire-agent`{{execute}}

In the SPIRE Agent log you should see a line similar to the following
to indicate that SAT attestation has completed:
`time="2020-05-30T00:13:12Z" level=debug msg="No pre-existing agent SVID found. Will perform node attestation" path=/run/spire/agent_svid.der subsystem_name=attestor`

# When SPIRE pods are Running, continue to the next step
