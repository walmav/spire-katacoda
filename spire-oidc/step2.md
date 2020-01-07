Get latest OIDC Discovery Provider:
`wget https://storage.googleapis.com/download.scytaleio.com/tar/scytale-oidc-discovery-provider-latest-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Untar:
`tar -xvf scytale-oidc-discovery-provider-latest-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Configure Trust Domain:
`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' oidc-discovery-provider.conf`{{execute HOST1}}

Allow the OIDC Discovery Provider binary to listen on port 443:
`setcap CAP_NET_BIND_SERVICE+eip opt/scytale/bin/oidc-discovery-provider`{{execute HOST1}}

Start OIDC Discovery Provider:
`opt/scytale/bin/oidc-discovery-provider &`{{execute HOST1}}


