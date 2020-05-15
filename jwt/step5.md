# Validate JWT token with pyjwt

We will dump the JWT token with a 3rd party tool this time, using `pyjwt` to
dump the contents of the JWT (without verification, as pyjwt doesn't have the
key).

First, install `python-jwt` which has a JWT decode utility:

`apt install -y python-jwt`{{execute}}

Next, decode the JWT, parsed out of the CLI output:

`jwt --no-verify $(grep eyJ /tmp/spire-jwt | tr -d '\r')`{{execute}}
