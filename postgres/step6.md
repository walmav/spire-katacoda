# Provision Database

We will now create a database for the application, create the application
DB user, and seed the database with some test data.

# Create `symbank` tablespace:

`postgres/run /usr/lib/postgresql/12/bin/createdb -U postgres symbank`{{execute}}

# Create `symuser` DB user with a random password

Note that the password is never saved or used anywhere, as the application is
using client certificate authentication. We don't even echo the password here.

```
user_pass=$(openssl rand -base64 32)
echo " \
  CREATE USER symuser WITH encrypted password '$user_pass'; \
  GRANT ALL privileges ON database symbank TO symuser; \
" | postgres/run psql -U postgres
```{{execute}}

# Create `customers` table and populate with test data

```
echo " \
  CREATE TABLE customers (id bigserial primary key, name varchar(40) NOT NULL, address text NOT NULL); \
  GRANT ALL privileges ON table customers TO symuser; \
  GRANT ALL privileges ON sequence customers_id_seq TO symuser; \
  INSERT INTO customers (name, address) VALUES ('Scrooge McMoneypants', '123 Main Street, Anytown USA.'); \
  INSERT INTO customers (name, address) VALUES ('Tiny Timothy', '987 Nowhere Street, AnotherTown USA.'); \
" | postgres/run psql -U postgres symbank
```{{execute}}

