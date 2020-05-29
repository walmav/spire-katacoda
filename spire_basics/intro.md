SPIFFE and SPIRE (the SPIFFE Runtime Environment) are a set of APIs and associated tooling that provides a uniform language for describing service identity in a wide range of workloads (including orchestration systems), verifying that identity, and providing a workload with documents that serve as proof of that identity. The identities are in turn used for establishing trust between software systems across a wide variety of hosting platforms.

Concretely, SPIRE exposes the SPIFFE Workload API, which can attest running software systems and issue SPIFFE IDs and SVIDs to them. This in turn allows two workloads to establish trust between each other, for example by establishing an mTLS connection or by signing and verifying a JWT token. Or for a workload to securely authenticate to a secret store, a database, or a cloud provider service.

This scenario provides a walk through of installing the components that make up a SPIRE deployment installation and a basic demonstration of its functionality in action. During the exercise you will:

 * Install and start a SPIRE Server 
 * Attest SPIRE Agent using Join Token Node Attestation
 * Create a Workload Registration Entry
 * Simulate the workload API interaction and retrieve workload SVID
 

