## Creating a Decentralized Twitter dApp with Embark
### Intro
In this [workshop](https://github.com/status-im/embark-dtwitter-workshop/tree/start/instructions), we'll explore how can we use Embark to simplify the development of a decentralised Twitter dApp (or DTwitter), and we'll be showing off some of the killer features of Embark v3.2. We will start off using an Embark Docker image to quickly bootstrap our Embark environment, then we'll download the DTwitter dApp template and off we go! Next, we'll walk through developing our DTwitter dApp using test-driven development.

The final code for this dApp can be found in the [Embark DTwitter Workshop repository](https://github.com/status-im/embark-dtwitter-workshop), however we will be kicking things off using the [`start` branch](https://github.com/status-im/embark-dtwitter-workshop/tree/start) as a starting point for our workshop. This branch contains some "missing" code that we will be adding together in this workshop as we follow the steps outlined in the  [instructions](https://github.com/status-im/embark-dtwitter-workshop/tree/start/instructions).

This dApp uses [React](https://reactjs.org/), but getting in to React details is out of scope for this workshop, so don't worry, we will only be focussing on the pieces that Embark helps us build the dApp. In reality, any JS framework can be used with Embark.

## What is Embark?
Embark is a fast, simple and powerful framework to help you develop and deploy fully decentralized applications. Embark allows developers to leverage all decentralised technologies for building dApps, facilitated by  code-generating contract objects and an `EmbarkJS` javascript API for use in your dApp. Embark is fully configurable, and can leverage as many or as few decentralized technologies as required. Embark can:
* Automatically run a blockchain node.
* Automatically run an IPFS or Swarm node and make these available via the `EmbarkJS API`. Embark can also upload your entire dApp to IPFS or Swarm.
* Compile and deploy Ethereum smart contracts (solidity, vyper, or bamboo) as you write them. Embark will also code generate your contracts, and will make them available via a JS object.
* Webpack and deploy your dApp assets as you write them.
* Integrate with `ENS`, available via the `EmbarkJS` API (coming in 3.2).
* Write and run contract unit tests