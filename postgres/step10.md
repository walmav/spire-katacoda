# A deeper look - DB user

During provisioning of the DB, we set the user to a random password, which
we didn't save - if you go back to that step you'll note the password wasn't
even displayed.

We can reset the user password all we like, and the application will continue
to function as we are using client certificates for authentication.

# Set password to a new random value

```
user_pass=$(openssl rand -base64 32)
db_cmd=$(echo "ALTER USER symuser WITH encrypted password '$user_pass';")
echo $db_cmd
echo $db_cmd | postgres/run psql -U postgres
```{{execute}}

Exercise the API via curl - note that the application continues to function:

`curl $(kubectl get service customer -o jsonpath="{..spec.clusterIP}"):8000/customers/1`{{execute}}


# Disable user

Note that standard postgres privileges still apply. The following will deny
`symuser` from logging in to the DB:

`echo "ALTER USER symuser WITH NOLOGIN" | postgres/run psql -U postgres`{{execute}}

The application will now return an error.

#Re-enable user

`echo "ALTER USER symuser WITH LOGIN" | postgres/run psql -U postgres`{{execute}}


