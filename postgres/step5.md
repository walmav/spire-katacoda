# Deploy Customer Service

The customer service is a JSON API that retrieves customer information from the
Postgres DB.

Apply the deployment:

`kubectl apply -k customer`{{execute}}

Wait for the customer service to start:

`kubectl get pod --selector=app=customer`{{execute}}

Two containers in this pod are launched - `customer` for the customer service,
and `spiffe-helper` which handles TLS certificates and rotation.

# Customer logs

To look at customer logs (note there is no output unless an error occurs):

`kubectl logs --selector app=customer --container=customer`{{execute}}

To look at spiffe-helper logs:

`kubectl logs --selector app=customer --container=spiffe-helper`{{execute}}

**It will take about 30 seconds for the application pod to start.**

# When the customer pod is Running, continue to the next step
