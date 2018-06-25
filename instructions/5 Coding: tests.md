## Contract tests
Now that we have our contract written, we can use the code generation provided by [`EmbarkJS`](https://github.com/embark-framework/EmbarkJS/) to write our contract unit test cases for test-driven development. Embark will code generate a `DTwitter` javascript object for us from our contract and make it accessible in our dApp by way of the `DTwitter` object. 
> Additionally, `EmbarkJS` allows us to interact with decentralised storage (IPFS and Swarm) and decentralised communication (Whisper), which are all configurable in config files. 
###### Create account transaction should be successful
Our [first test](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L33-L40) is to ensure that our `createAccount` transaction is sent successfully. Let's fill in the code that calls our `createAccount` contract function:
```
// do the create account tx
const createAccountTx = await DTwitter.methods.createAccount(username, description).send();
```
> Notice the `.send()` at the end. This is required when we are sending a transaction that will modify the state of contract. In this case, we are modifying the state by adding a user to the `users` mapping.
###### Should create user
After our successful `createAccount` transaction, this should have created a user. In [our test](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L42-L49), let's fill in the code to retrieve a user from the contract.
```
// Get user details from contract
const user = await DTwitter.methods.users(web3.utils.keccak256(username)).call();
```
> This time we used a `.call()`. Why? Because in this case we are not modifying the state of the contract, and simplying querying data from it. Changing state costs gas, so we use `.send()`, while querying state is free, so we use `.call()`.
###### Should create owner for default account
The `createAccount` function should have also created an entry in the `owners` mapping with our `defaultAccount`, which we check in the [next test](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L51-L57). This is how we retrieve an owner from the `owners` mapping:
```
// read from the owners mapping the value associated with the defaultAccount
const usernameHash = await DTwitter.methods.owners(web3.eth.defaultAccount).call();
```
###### User exists should be true
We can use our `userExists` function in the contract to check if a `usernameHash` exists. This will later be used for username validation in the dApp. Our [test for `userExists`](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L59-L65) can be completed using:
```
// Check the usernamehash exists
const exists = await DTwitter.methods.userExists(usernameHash).call();
```
###### Edit Account should update user details
After a call to `editAccount`, our user's details should be updated. [This unit test](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L68-L79) can be completed by adding the following:
1. Call edit account
    ```
    await DTwitter.methods.editAccount(usernameHash, updatedDescription, updatedImageHash).send();
    ```
2. Then fetch the user details with the usernamehash
    ```
    const updatedUserDetails = await DTwitter.methods.users(usernameHash).call();
    ```
###### Tweet event should fire when there is a tweet
We need to ensure that our contract events subscription works correctly when someone creates a new tweet via the `tweet` function. In our [unit test](https://github.com/status-im/embark-dtwitter-workshop/blob/cryptolife/start/test/dtwitter_spec.js#L81-L94), we can add the following:
1. Subscribe to the `NewTweet` event
    ```
    DTwitter.events.NewTweet({
        filter: { _from: usernameHash },
        fromBlock: 0
   })
   .on('data', (event) => {
        assert.equal(event.returnValues.tweet, tweetContent);
    });
    ```
2. Do the tweet
    ```
    await DTwitter.methods.tweet(tweetContent).send();
    ```
### Run tests
Let's run the tests to ensure they are all passing. Type `quit` in the Embark consle, then run:
```
run_embark test
```
###### Test results
Your test results should appear similar to the following:
```
DTwitter contract
    ✓ transaction to create a dtwitter user 'testhandle' with description 'test description' should be successful (114ms)
    ✓ should have created a user 'testhandle' (60ms)
    ✓ should have created an owner for our defaultAccount
    ✓ should know 'testhandle' exists (49ms)
    ✓ should be able to edit 'testhandle' user details (186ms)
    ✓ should be able to add a tweet as 'testhandle' and receive it via contract event (54ms)
```
> Note: there is a known error with `ganache` that sometimes causes last test does to fail with the error `ERROR: The returned value is not a convertible string`. We are currently investigating this issue.
