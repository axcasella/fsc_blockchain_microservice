# Docusign FSC Hackathon Submission

## App 3 - Greeblocks Blockchain Microservice

## Overview

Simply relying on an centralized database such as Microsoft Dynamics isn't enough. We have decided to take advantage of blockchain technology and add an immutable source of truth for each certificate issued by the FSC.

Our blockchain microservice is built on top of Hyperledger Fabric. Hyperledger Fabric is an open source private permissioned blockchain framework. The microservice's server is built with Node.js and Express. The server side code is written in Typescript. The server calls Hyperledger Fabric's Contract APIs to communicate with the blockchain network.

The smart contract chaincode is written in Typescript as well. It is ready to be hosted on a managed blockchain service such as the Amazon Managed Blockchain service.

Certificate object in the blockchain ledger:

```
@Object()
export class Certificate {
  @Property()
  public certificateID: string;
  public type: string;
  public company: string;
  public issuer: string;
  public issuanceDate: string;
  public status: string;
}
```

The microservice server exposes **REST APIs**, called by the backend server:

```
Add a certificate to the blockchain ledger
POST api/blockchain/certificates
```

We have made it optional for the backend server to connect to the blockchain microservice. In the backend server, the config setting is the `enable_blockchain` field in `src/config/config.ts`. After the chaincode is deployed to a managed blockchain service, this option can be turned on, and the microservice's server can be started. When this is enabled, the backend server can call the `POST api/blockchain/certificates` API when updating the certificate's status to "issued" in Microsoft Dynamics. This creates a certificate in the immutable ledger.

## Try it out

To start up the microservice server in local machine, run the following commands:

```
npm install
npm run server
```

The microserver APIs will not work without a blockchain network.

To run a local network, you can install this [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=IBMBlockchain.ibm-blockchain-platform) and follow the guide there to set up a local blockchain environment, then deploy the `chaincode` directory to that network.

To run a network in the cloud, you can use one of the following options:

[Amazon Managed Blockchain](https://aws.amazon.com/managed-blockchain/)

[IBM Blockchain Platform](https://www.ibm.com/blockchain/platform)

## Links to the rest of the app

[Frontend repo](https://github.com/axcasella/docusign_fsc_ui)

[Backend server repo](https://github.com/axcasella/docusign_fsc_server)

Checkout our demo video on [Youtube](https://www.youtube.com/watch?v=NoS7zAkZ2Gc&feature=youtu.be)!
