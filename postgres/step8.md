# A deeper look - Postgres pod

The Postgres configuration enables SSL and configures a path for the
certificates and key which are provided by spiffe-helper:

`cat postgres/postgresql.conf`{{execute}}

The `pg_hba.conf` configuration disables remote connections without SSL and
forces SSL connections to use a client certificate:

`cat postgres/pg_hba.conf`{{execute}}

The `spiffe-helper` configuration specifies where the certificates and key are
placed. The `certDir` directory is shared by both the `postgres` and `spiffe-helper`
containers within the pod:

`cat postgres/spiffe-helper.conf`{{execute}}

The `reloadCertificates.sh` script causes Postgres to do a configuration reload,
which refreshes the certificates. This is done by exposing the Postgres UNIX
domain socket from the `postgres` container into the `spiffe-helper`.
This `kubectl` command cats the two line `reloadCertificates.sh` script:

`kubectl exec $(kubectl get pods --selector=app=postgres --output=jsonpath="{..metadata.name}") --container=spiffe-helper cat /opt/spiffe-helper/reloadCertificates.sh`{{execute}}
