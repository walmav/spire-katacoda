Get latest OIDC Discovery Provider:
`wget https://storage.googleapis.com/download.scytaleio.com/tar/scytale-oidc-discovery-provider-latest-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Untar:
`tar -xvf scytale-oidc-discovery-provider-latest-linux-x86_64-glibc.tar.gz`{{execute HOST1}}

Configure Trust Domain:
`sed -i 's/<TRUST_DOMAIN>/[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/g' oidc-discovery-provider.conf`{{execute HOST1}}





