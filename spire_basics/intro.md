SPIRE (the SPIFFE Runtime Environment) is a tool-chain for establishing trust between software systems across a wide variety of hosting platforms. Concretely, SPIRE exposes the SPIFFE Workload API, which can attest running software systems and issue SPIFFE IDs and SVIDs to them. This in turn allows two workloads to establish trust between each other, for example by establishing an mTLS connection or by signing and verifying a JWT token. Or for a workload to securely authenticate to a secret store, a database, or a cloud provider service.

This scenario will guide you through the basic steps of setting up SPIRE: 
 - Run SPIRE Server 
 - Attest SPIRE Agent using Join Token Node Attestation
 - Create Workload Registration Entry
 - Simulate the workload API interaction and retrieve workload SVID
 

