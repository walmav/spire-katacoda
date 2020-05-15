# A deeper look - customer pod

The customer API application configuration contains information about connecting
to the database, as well as a path for the certificates and key, which are
provided by spiffe-helper:

`cat customer/customer.conf`{{execute}}

The spiffe-helper configuration specifies where the certificates and key are
placed (this directory is shared by both the `customer` and `spiffe-helper`
containers within the pod):

`cat customer/spiffe-helper.conf`{{execute}}

Note that the customer API application does not use connection pooling and
reloads the certificates on each connection, so no action is required by
`spiffe-helper` to request cert reload by the application.
