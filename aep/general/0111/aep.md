# Planes

Systems such as software-defined networks and public clouds have distinct sets
of APIs which are crucial for accomplishing a full user journey. For example,
in networking, a user must:

1. Configure the network to determine how data will flow (e.g. defining network
   interfaces, gateways)
2. Send data through the network.

The API and operations for these steps can be divided into layers known as
_planes_, indicating the role that the API plays in data.

The AEPs define the following planes:

- Management plane: contains AEP-compliant, resource-oriented APIs that
  primarily configure and allow retrieval of resources. APIs in the management
  plane generally do no accept nor interact with user data directly.
- Data plane: a heterogenous API (ideally resource-oriented) that reads and
  writes user data. Often connects to entities provisioned by the management
  plane plane, such as virtual machines.

## Guidance

### Management Plane

Management resources and methods exist primarily to provision, configure, and
audit the resources that the data plane APIs operates on.

For example, the following are considered management resources for a cloud
provider:

- virtual machines
- virtual private networks
- virtual disks
- a blob store instance
- a project or account

### Data Plane

Methods on the data plane operate on user data in a variety of data formats,
and generally interface with a resource provisioned via a management plane API.
Examples of data plane methods include:

- writing and reading rows in a table
- pushing to or pulling from a message queue
- uploading blobs to or downloading blobs from a blob store instance

Data plane APIs **may** not comply to AEPs due to requirements including high
throughput, low latency, or the need to adhere to an existing interface
specification (e.g. ANSI SQL).

- For convenience, resources and methods that operate on the data plane **may**
  expose themselves via resource-oriented management APIs. If so, those
  resources and methods **must** adhere to the requirements of the management
  plane as specified in the other AEPs.

### Major distinctions between management and data plane

- [Declarative clients][] operate on the management plane exclusively.
- Data planes are often on the critical path of user-facing functionality, and
  therefore:
  - Have higher availabilty requirements than management planes.
  - Are more peformance-sensitive than management planes.
  - Require higher-throughput than management planes.

[Declarative clients]: ./0003.md#declarative-clients

## Changelog

- **2024-01-27**: initial fork of this AEP from https://google.aip.dev/111.