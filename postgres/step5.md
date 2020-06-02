# Deploy Customer Service

The customer service application is a JSON API that queries the
Postgres DB for customer information.

Apply the deployment:

`kubectl apply -k customer`{{execute}}

Wait for the customer service pod to start:

`kubectl get pod --selector=app=customer`{{execute}}

Keep running the above `kubectl get` command until the pod is displayed as `Running`
underneath `STATUS`.

**It will take about 30 seconds for the pod to start.**

Two containers in this pod are launched - `customer` for the customer
service, and `spiffe-helper` which handles TLS certificates and
rotation. To show these containers, run:

`kubectl get pods -l app=customer -o jsonpath='{.items[*].spec.containers[*].name}{"\n"}'`{{execute}}

# Customer logs

As you go through this demo, you may want to check the application log
and application `spiffe-helper` log to see how various actions affect each of
them.

To look at customer service API log (note there is no output unless an error occurs):

`kubectl logs --selector app=customer --container=customer`{{execute}}

To look at `spiffe-helper` log:

`kubectl logs --selector app=customer --container=spiffe-helper`{{execute}}

# When the customer pod is Running, continue to the next step
