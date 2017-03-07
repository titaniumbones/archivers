# List of Services

** **

### Archive-Gen
URL-to-Archive server that crawls the web injesting raw data into the library with digital provenance.

### Archive-Cron
Pluggable service that executes containerized custom scripts that extract datasets unreachable by archive-gen or archiver-coordinator.

### Archive-Coordinator
A service that integrates data hosts.

### Archive-IPFS
A service that makes Library content available on the IPFS network.

### Identity-Mgmt
A service that hosts keypairs for web-based contribution.

### Identity-Info
A service that hosts volunteered information (for example, name, email, location) about an identity, eventually also publishing this information over IPFS. It may also support grouping identities for key rotation.

### Context
A service for volunteers to write metadata about content hosted anywhere within the library.

### Package-Gen
A server that generates packages in various formats for package-oriented data hosts on-demand

### Metablocks
A Spec for tracking metadata.