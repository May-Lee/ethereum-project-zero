# 1.) Intro to Ethereum and Solidity

## What is the history of Bitcoin and Ethereum?
* Original BTC whitepaper written in 2008 to describe P2P payments without an intermediary (such as a bank) and, similar to cash, with no chance to charge back.

* Ethereum whitepaper published in 2013 "Ethereum: The Ultimate Smart Contract and Decentralized Application Platform"
    * Introduces the idea of "smart contracts" as entties sending and receiving money
    * Can therefore build DACs - Decentralized Autonomous Corporations
    * Essentially allows for programmatic control over transactions

* The main difference between Bitcoin and Ethereum is that Bitcoin is non-programmatic

## How do nodes and an Ethereum network work?
* Ethereum networks are used to transfer money and store data
* Anyone can run a node, and a node is just a computer running an Ethereum client
* Each node can store a full copy of the blockchain - a database that stores a record of every transaction that has ever taken place
* There are many different networks, and they are formed by one or more nodes
* However, there is one main Ethereum network, Mainnet

## How do we connect with Ethereum to send money, store data, deploy contracts etc.?
* Developers can use web3.js and consumers can use Metamask or Mist browser
* Explain Metamask to a beginner.
    * How do you install it?
        * It's a Chrome extension
        * You enter a password
        * Account address, public key, private key (all hexadecimal numbers)
    * What do you need to remember when you use it?
        * address vs. account
        * seed phrase
        * abandoning the wallet
            * there is no shortage of wallets; you can create a many as you wish
    * What are the different networks in Metamask?
        * Ropsten, Kovan, Rinkeby, Mainnet etc.
    * One account (address) will work across all the networks 
* How do you use a wallet?
* What happens when you send and receive Ether?
    * Sending:
        * Clicks 'submit' on form
        * Address is sent to backend server
        * Backend server uses web3 library to create a 'transaction' object
            * What does a transaction contain?
                * nonce - how many transactions sent from that address
                * to - address it's being sent to
                * value - amount of ether being sent
                * gasPrice - amount of ether sender is willing to pay per unit gas to process transaction
                * startGas/gasLimit - Units of gas that this transaction can consume
                * v, r, s - cryptographic pieces of data, generated from the sender's private key, that can be used to generate the sender's account address
                    * verifies legitimacy of transaction
                    * cannot be back-generated
        * Backend server sends 'transaction' object to network (here Rinkeby)
        * Backend server waits for 'transaction' to be confirmed
            * Transaction gets sent to a node in the network, to start
                * Multiple transactions get sent and the node has the entire blockchain
                * Multiple transactions get collected into a block
                * The validation logic - "mining" - run by the node on the block, causes the delay
                * This is block time
        * Backend server sends success message back to browser

## So what is a blockchain and what is POW?
(See sections 13 and 14)

## What are smart contracts?
* What are some important points to remember?
* What is the `pragma` statement and why is it important?
* What is the constructor function?
    * What are some common patterns?
* What are common functions?
    * Pair each function with a common pattern and an explanation of the use of
    that pattern.
* What is the difference between storage and local variables and how they are used? 