# DTwitter template download
Now that we have Embark Docker setup, we can leverage Embark to download and install a dApp template for us. We can use any of the [Embark templates](https://embark.status.im/templates/), but in our case we will use the `start` branch from our repo and use it as the skeleton of our dApp. This template is a website built using React (don't worry if you don't know React, we are not focussing on this part). 

## Let's go
First, let's make sure our `pwd` is in the parent folder of where we want our dApp to be. For example, if we want our dApp to live in our home directory (`~`), make sure we're in our home directory:
```
cd ~
```
Now, let's download the template in to a `~/dtwitter` folder:
```
run_embark new dtwitter --template https://github.com/status-im/embark-dtwitter-workshop#start
cd dtwitter
```
Embark will create new dApp called `dtwitter` and install all dependencies for us!
Let’s take a moment to open the template in our favorite IDE and take a tour of the file structure of a standard Embark dApp:
* `/app` - contains all our assets for the website. These will get webpacked according to our settings in `/embark.json`.
* `/config` - contains all our configuration
    * Blockchain - configures options for running geth
    * Communication - configures whisper options
    * Contracts - configures options for deploying contracts from Embark, as well as the connection to make to geth from the dApp
    * Namesystem - configures ENS support (coming in 3.2)
    * Storage - configures decentralised storage for IPFS and Swarm. Includes a section for uploading the dApp as well as a dApp connection that can be used in the dApp.
    * Webserver - configuration options for the webserver that serves the dApp during development.
* `/contracts` - contains our contacts
* `/test` - contains our mocha tests for testing our contracts
* `embark.json` - configures dapp asset file locations, webpack options, and library versions to use