## First run
Now let’s run Embark on our dApp to see what it can do for us, and take a quick tour of skeleton dApp.
```
run_embark run
```
You should see the Embark console and it's components. 
* *Contracts* - the top left shows which contracts are deployed and their address. * Modules loaded and running - the top right shows the status of the loaded modules running (or not running) in Embark. 
* *Log* - the middle shows log output. 
* *Console* - on the bottom row there is a console that will let us interact with `web3` and `ipfs` (try it out by typing `help` to see available commands).

### Embark output
You’ll notice from the logs and from the modules that Embark has started Go-ethereum and IPFS processes, compiled and deployed our contract, and webpacked our website for us. 
> The contract warnings in orange will disappear once we "complete" our contract.

### Take a tour of the barebones DTwitter site
The website has several features that *are not yet hooked up to our contract*, but let’s take a look around at the website anyway. Launch `http://localhost:8000` in your browser.

Functionality we'll see:
* Create an account
* Edit account
* Tweet
* Search and view user's tweets

Later, we'll hook this functionality up to a contract.