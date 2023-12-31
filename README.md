# ChatDKG Developer Tooling

Polyflow team will use our internally developed tooling to bring Knowledge Graph support & ChatDKG support to millions of Web2 developers, hiding all complexities of interacting with blockchain.

## The Challenge

* dkg-client is a JS SDK which enables developers to integrate Knowledge Graphs into their apps. 
* It abstracts away the process of creating an NFT & publishing a new version of the Knowledge Graph.
* However, dkg-client still requires the developer to have some Web3 specific knowledge or the user to have a Web3 wallet installed. This greatly limits developer & user accessibility.

## The Solution

Integrate Polyflow SDK & Transaction Processing Backend as an extension SDK to the dkg-client SDK!

Benefits
* Developers don’t need to know anything about blockchain development to integrate dkg-client!
* Users can be logged in via email or phone number, instead of wallet address!
* Out-of-the box analytics for all transactions & graph updates/queries!
* Transactions are processed automatically by a backend process.

## The Impact

### AI Developers

* Develop extensions & plugins for AI developer tools with Knowledge Graph.
* Enable AI backends to write updates into the Knowledge Graph through a simple HTTP call.
* Hide the complexity of blockchain & transaction signing.

### Web2 Developers

* Develop plugins for frontend frameworks, which feed data automatically into the Knowledge Graph (e.g. Wordpress, Shopify, Angular, React).
* Enable frontend actions to update the Knowledge Graph with a simple HTTP call.

### Users

* Log-in to tools which interact with Knowledge Graph with their email or phone. 
* Get subsidized gas & token costs or pay them with a simple credit card tx.
* Hide the blockchain from users.

## Milestones

### Milestone #1 | SDK Wrapper around dkg-client functions

Time: 30 days

Description: We will build a wrapper around dkg-client which exposes all the functionality of the dkg-client SDK, but doesn't require the developer to add transaction signing and provides custodial wallet support, gasless transactions, full transaction-oriented analytics & human readable transaction previews.

### Milestone #2 | HTTP-based backed signer & TX manager

Time: 30 days

Description: We will build an HTTP-based signer, which enable teams to automate the interaction with Knowledge Graphs through any HTTP-enabled device, including mobile apps, bakend apps, IoT/Hardware devices, etc... 

# Case / Example

In this example, we will demonstrate the abilities of the Polyflow Code SDK wrapper & infra on an example from the 3rd ChatDKG Office Hours. We will explore the case of adding the pamphlet information for the imaginary drug `yewmakerol` to the Knowledge Graph - but this time, from a perspective of an AI engineer (or any other Web2 developer) who is not familiar with anything blockchain related.

The example is very simple:

1. The developer will create a new Polyflow Code project - and get an API Key
2. The developer will use `npm` to install the `polyflow` SDK and the `origintrail` extension.
3. The developer calls the exposed methods.

```js
import Polyflow from '@polyflow/core'
import DKG from '@polyflow/origintrail'

const sdk = new Polyflow('api-key')

// The DKG SDK is now created as a wrapper around the Polyflow SDK. The developer uses the Polyflow
// dashboard to set up RPC endpoints, DKG enpoints and selects the signer.
//
// The signer can be a frontend widget signer *or* a backend signer. The frotnend signer is great for native
// Web3 apps, while the backend signer is great for backend apps, bot automation & frontend apps which want to use
// existing user role management and auth systems.
const dkg = new DKG(sdk)

const yewmakerol = JSON.parse('./path/to/yewmakerol.json')

dkg.asset.create(yewmakerol, { epochsNum: 5 }).then(result => {
  // this callback is called after the asset has been signed, added to the DKG and updated on the blockchain
  console.log(result)
})

```

## Signers

The developer uses the Polyflow dashboard to choose between several signer types. A signer will take a raw blockchain transaction, sign it and deploy it to the blockchain. It will then wait for the transcation to finish and tell the SDK that the action is complete.

![Polyflow Architecture](https://github.com/0xpolyflow/ChatDKG-Tooling/assets/129866940/3bc799cf-8bdf-4c40-bda8-18aa94342a86)

The developers have a choice between two types of signers:
* Polyflow SDK Widget Signer - Frontend
* Backend/HTTP Signer

### Widget Signer

The SDK Widget signer will take all the heavy lifting from the developer and open a user-friendly widget to users when they need to sign the blockchain transaction. The widget also supports many user friendly features:
* Login with email
* Autofunding (Gasless transactions)

In this way, the widget can hide the complexity of blockchain interaction from both the user and developer. All the complex heavy lifting is handled by Polyflow.

<img width="351" alt="Screenshot 2023-07-25 at 18 42 04" src="https://github.com/0xpolyflow/ChatDKG-Tooling/assets/129866940/c4f08678-1c01-4234-a2ef-f2d77b2716ed">

### Backend/HTTP signer

The backend signer enables any developer to send raw transactions to a signer which holds the private keys for one or more accounts. The signer then signs those transactions, deploys them to the blockchain and fetches the result.

This is great for people building backends which interact with blockchain, builing bots which automate interactions with blockchain *or* who are builing frontend apps, but want to authorize their users with their own auth, instead of blockchain private keys.


