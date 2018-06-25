## Coding: DTwitter contract
We can start updating our `/contracts/DTwitter.sol` contract code and watch as Embark watches and recompiles everything for us as we go.
### Functions
Let’s begin by writing some of our contract functions.
###### Create account
The `createAccount` function will be used for creating users in the contract. We need to add the new user to the user/address mapping so we can keep track of the address that created the user.
1. Add a user to the `users` mapping and populate details (`creationDate`, `owner`, `username`, `description`)
    ```
    users[usernameHash].creationDate = now; // 'now' is not recommended for accuracy
    users[usernameHash].owner = msg.sender;
    users[usernameHash].username = username;
    users[usernameHash].description = description;
    ```
    > Note: we are using the block timestamp `now` to specify a creation date for the user (and also for the tweet time as we'll see later on). This application of `now` is fine, as ther are no reliances on this block timestamp for randomness. Please see the [Solidity documentation](https://solidity.readthedocs.io/en/v0.4.25/units-and-global-variables.html) for more information.
2. Add an entry to our `owners` mapping so we can retrieve a user by their address. This will be useful for when we need to find out if our current address is associated with a user.
    ```
    owners[msg.sender] = usernameHash;
    ```
###### Edit account
We will be updating the user's profile in the `editAccount` function, so we need to be able to update the user's description and picture in the contract.
1. Update the description (could be empty):
    ```
    users[usernameHash].description = description;
    ```
2. Only update the user's picture if the hash passed in is not empty or null        (essentially disallows deletions):
    ```
    if (bytes(pictureHash).length > 0) {
       users[usernameHash].picture = pictureHash;
    }
    ```
###### User exists
The `userExists` function is used for checking if a user exists in the `users` mapping stored in the contract.
1. In Solidity, we can see if an item in a `struct` exists by checking that a property of an item is not set to it's default value. For example, we can check if a specific user exists in the `users` mapping by see if the user's `creationDate` is not `0` (the default value in Solidity for the block timestamp which is a `uint`).
    ```
    return users[usernameHash].creationDate != 0;
    ```
###### Tweet
For the `tweet` function to work, we need to add the tweet to the user in the `users` mapping. First, we need to get the user associated with the address who initiated the contract call (the `msg.sender`). Then, we can store the tweet in the `users` mapping against that user. Finally, we can emit an event that a tweet occurred. Later, we will subscribe to this event to get tweets as they are added to the contract in real time.
1. Get our user from the `usernameHash`
    ```
    User storage user = users[usernameHash];
    ```
2. Get our new tweet index
    ```
    uint tweetIndex = user.tweets.length++;
    ```
3. Update the user's tweets at the tweet index
    ```
    user.tweets[tweetIndex] = content;
    ```
4. Emit the tweet event and notify the listeners
    ```
    emit NewTweet(usernameHash, content, now);
    ```