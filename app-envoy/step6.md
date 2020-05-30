# View the webapp in another browser tab

Click https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com to open the Scrooge
McBank webapp in a new browser tab.
The page automatically refreshes. You should be looking at a bank transaction log for
"Jacob Marley".

# Delete registration entry

Click the following command to revoke the workload entry for the
`customer-service-envoy` container:

`./revoke_envoy`{{execute}}

We have configured a 30 second TTL for SVIDs, so after that time the
application will stop working. After the SVID expires, the Scrooge
McBank application tab refreshes automatically and the following error
message is displayed:

`ERROR Could not get transaction data: Unable to create TLS
connection: x509: certificate has expired or is not yet valid`

Go back to the browser tab containing the Scrooge McBank application
to check for this error. After seeing the error, return to the
Katacoda demo tab.

# Re-create registration entry

If you go back to step 2 and re-run the first  command ("Create entry for
customer-service-envoy container") the application will start to work
again once the entry is registered and the workload is re-attested.

Switch back to the Scrooge McBank tab to verify that the page is
displayed properly after re-running the first command in step 2.
