# Private Network

The following guide provides detailed instructions on how to set up a private Ethereum blockchain on your local computer for testing purposes. It encompasses the necessary steps for installation and also includes guidance on deploying a basic smart contract.

For deploying and running the Ethereum blockchain we will use go-ethereum, aka geth, and for deploying the smart contract we will use Truffle.
The following are link to  download geth client based on the os:
https://geth.ethereum.org/docs/getting-started/installing-geth

The following are link to download truffle:
https://trufflesuite.com/docs/truffle/how-to/install/

The below points are steps that to be followed for creating etherum private network:
* Install geth
* Install truffle
* Configure genesis block
* Create nodes
* Generate accounts for nodes
* Initialize and start node
* Connect to the node from command line
* Create new account via command line
* Transfer some Ether to new account
* Start miner
* Deploy a Smart Contract
* Interact with contract using truffle

# Install Geth:

Geth is an Ethereum client written in Go. This means running Geth turns a computer into an Ethereum node. To install it on a linux, run the following commands:

`sudo add-apt-repository -y ppa:ethereum/ethereum`

`sudo apt-get update`

`sudo apt-get install ethereum`

For other versions follow this link :https://geth.ethereum.org/docs/getting-started/installing-geth

# Install Truffle:
A development environment, testing framework and asset pipeline for blockchains using the Ethereum Virtual Machine (EVM), aiming to make life as a developer easier by providing built-in smart contract compilation, linking, deployment and binary management.

prerequisite:
   * Node.js v14 - v18
   * Windows, Linux, or macOS

In terminal, run following command :

`npm install -g truffle `

To check whether it is installed properly or not, run the following:

`truffle version`

# Configure genesis block:

The genesis block refers to the initial block in a blockchain network. It serves as the foundation or starting point of the entire blockchain. The genesis block is unique and distinct from subsequent blocks as it does not reference any previous block. It usually contains special parameters or data that establish the basic configuration of the blockchain, such as the timestamp of creation, the initial set of transactions, and other essential information. Each node in the network will be initialized with same genesis block.

Following are the step to be followed for creating genesis block:
* Create folder called privateNetwork(name could be changed based on the preference)
* Create three more directories inside of the privateNetwork
* Now, create a file in the  privateNetwork as a genesis.json.

which includes the following config details in the file.

     {
         "config": {
    
        "chainId": 8888,
        
        "homesteadBlock": 0,
        
        "eip150Block": 0,
        
        "eip155Block": 0,
        
        "eip158Block": 0,
        
        "byzantiumBlock": 0,
        
        "constantinopleBlock": 0
        
    },
    
    "difficulty": "200000",
    
    "gasLimit"   : "21000000",
    
    "gas price"  : "0",
    
    "alloc": {
    
        "0x55860Df9065F504b79BF599FCf0Ce1340fD065d8": { "balance": "9999999999999999999999999" },
        
        "0x1496d986cc5194b39f82ea89A61c1b31Cf33F57e" : {"balance": "9999999999999999999999999"}
        
    }    
    }
The given JSON represents a configuration file for a private Ethereum network. Let's go through each key and its purpose:

"config": 

This section defines various configuration parameters for the network.

"chainId": 

It is a unique identifier that represents a specific blockchain network within the Ethereum ecosystem. It serves as an identifier for a particular blockchain and distinguishes it from other networks.In this case, the chainId is set to 8888. The chain ID can be assigned with any number of digit expect from 0 to 10 which are assigned to the existing network number such as the mainnet, testnets (e.g., Ropsten, Rinkeby, Kovan).

"homesteadBlock": 

Indicates the block number at which the Homestead protocol rules are enabled.The value in the Ethereum configuration, it indicates that the specified block number or higher is considered part of the Homestead phase, and the associated protocol rules and features should be enabled.


"eip150Block": 

Indicates the block number at which the EIP-150 protocol rules are enabled.EIP-150 introduced gas cost changes to address certain DoS (Denial-of-Service) attacks and mitigate the impact of spam transactions. It adjusted the gas costs for various operations to make them more efficient and discourage potential attack vectors. The EIP150Block value indicates the block number at which these gas cost changes took effect.


"eip155Block": 

Indicates the block number at which the EIP-155 protocol rules are enabled.EIP-155 introduced a standardized format for transaction signatures to prevent replay attacks across different Ethereum chains. It included a chain ID in the transaction's signature, making each transaction unique to a specific chain and preventing the replay of transactions on different networks. The EIP155Block value represents the block number from which transactions must adhere to this new signing format.


"eip158Block": 

Indicates the block number at which the EIP-158 protocol rules are enabled.EIP-158 was an update related to storage gas refunds. Prior to EIP-158, when a contract deleted data from storage, it still incurred gas costs. EIP-158 introduced gas refunds, allowing contracts to recover some gas costs when they cleared data from storage. The EIP158Block value indicates the block number from which gas refunds for storage clearing were enabled.


"byzantiumBlock": 

Indicates the block number at which the Byzantium protocol rules are enabled.Support for zk-SNARKs: Byzantium included precompiled contracts that enable the use of zk-SNARKs (zero-knowledge proofs) on the Ethereum network. This allows for more efficient and private transactions.Repricing of the SSTORE opcode: Byzantium adjusted the gas costs associated with the SSTORE opcode, which is used for storage operations. This change aimed to make certain operations more cost-effective and encourage better usage of storage.


"constantinopleBlock": 

Indicates the block number at which the Constantinople protocol rules are enabled.Constantinople further adjusted the gas costs for certain opcodes, making certain operations cheaper and more efficient. This aimed to optimize the usage of gas on the Ethereum network.
Introduction of new opcodes: Constantinople introduced new opcodes such as CREATE2, which allows the creation of contracts at deterministic addresses based on their bytecode and initialization parameters. It also introduced EXTCODEHASH, which provides a way to retrieve the hash of a contract's code.

"difficulty": 

Mining difficulty in Ethereum refers to the level of computational effort required to mine new blocks and add them to the blockchain. It is a measure of how hard it is to find a valid block hash that satisfies the network's consensus rules.Specifies the difficulty level of mining new blocks in the network. In this case, the difficulty is set to "200000".


"gasLimit": Sets the maximum amount of gas that can be used in a block. The gas limit is set to "21000000".


"gas price": Specifies the price of gas in wei units. Here, the gas price is set to "0", indicating that transactions can be executed without any cost.


"alloc": 

This section defines the initial account balances for specific addresses.

"0x55860Df9065F504b79BF599FCf0Ce1340fD065d8": This address is assigned a balance of "9999999999999999999999999" wei.
"0x1496d986cc5194b39f82ea89A61c1b31Cf33F57e": This address is also assigned a balance of "9999999999999999999999999" wei.

# Create node:

For the purpose of this private blockchain, we will create some nodes locally in our machine.

Create 3 new directories. Each of them will represent a single node in the blockchain:

`mkdir node01 node02 node03`

# Generate the account for node :

Let’s create Ethereum accounts in the first node, so that later we can do some transactions for testing purposes:

`geth --datadir "/PATH_TO_NODE01/" account new`

You will be prompted for a secret password. Write down the address of the created accounts and save the password in the file as password.txt inside of the node(node01, node02, node03) folder.
Now go back to genesis file, over there paste this account along with balance under alloc key.

     alloc:{
    
        "generatedAccount1": { "balance": "9999999999999999999999999" },
        
        "generatedAccount2" : {"balance": "9999999999999999999999999"}
        
     }

# Initialize and start the nodes :
 
 The first step is to initialize each node with the genesis file previously created. For this, run this command for each of the nodes, replacing   with your system path:

`geth --datadir "/PATH_TO_NODE/" init /PATH_TO/genesis.json`

Then start each node by running the following command for each of them.


A bootnode, short for bootstrap node, is a special type of node in the Ethereum network that serves as a discovery mechanism for other nodes to join the network. Its main purpose is to facilitate the initial connection and peer discovery process for new nodes.


The command "bootnode -genkey boot.key" is used to generate a private key file for a bootnode in the Ethereum network.

`bootnode -genkey boot.key`

By executing this command, the bootnode will start and begin its role as a discovery mechanism for other nodes in the Ethereum network. Other nodes can connect to this bootnode using the provided address and port, obtain a list of known peers, and join the Ethereum network.

`bootnode -nodekey boot.key -addr :30306`

output : ![image](https://github.com/Manasamahesh/privateNetwork/assets/25504822/ec30eb38-9b17-40f5-853f-1f89b0ffc3f9)

The term "enode address" refers to the Ethereum Node Identifier. It is a unique identifier assigned to each node in the Ethereum network. An enode address consists of several components that provide information about the node's network location and capabilities.

The enode address has the following format:

`enode://<node-id>@<ip-address>:<port>?discport=<discovery-port>`
  
Let's break down the components of an enode address:

node-id: This is a unique identifier for the node, typically represented as a combination of letters and numbers. It serves as a globally unique identifier for the node in the Ethereum network.

ip-address: This represents the IP address of the node. It specifies the network location where the node can be reached.

port: This is the port number on which the node is listening for incoming connections. It is used to establish network communication with the node.

discport=discovery-port: This component specifies the discovery port, which is used for the node's peer discovery mechanism. It allows other nodes to find and connect to the node.
  
To bring up the private network using geth run below commands
 
`geth --datadir node01 --port 30306 --bootnodes enode://7ace3d114e928ab51cf399286eb2eceb3eb286f22c1b418053def3203e2368586320b20fd07401fe49b48353441e5c403b00e83cbd78da21639eae9f4a4405aa@127.0.0.1:0?discport=30307 --unlock 0x55860Df9065F504b79BF599FCf0Ce1340fD065d8 --password password.txt --authrpc.port 8551  --authrpc.addr 127.0.0.1 --authrpc.vhosts * --rpc.enabledeprecatedpersonal --http --http.api  "web3,eth,personal,net,miner" --http.corsdomain "*" --http.vhosts "*" --http.port 8552 --allow-insecure-unlock --miner.etherbase "0x55860Df9065F504b79BF599FCf0Ce1340fD065d8"  --rpc.allow-unprotected-txs --mine`

The command you provided is a command-line instruction for running a Geth node with various configurations and options. Let's break down the different parts of the command:

- `--geth`: It is the command to start the Geth Ethereum client.

- `--datadir node01`: Specifies the data directory for the Geth node, where the blockchain data and other node-related files will be stored.

- `--port 30306`: Sets the port number on which the node will listen for incoming connections from other nodes.

- `--bootnodes`: Specifies the list of bootstrap nodes that the current node should connect to for peer discovery and network synchronization. In this case, it provides an enode URL for a bootnode with authentication credentials.

- `--unlock`: Unlocks the specified Ethereum account, allowing it to sign transactions. Here, `0x55860Df9065F504b79BF599FCf0Ce1340fD065d8` is the address of the account to be unlocked. This account name `0x55860Df9065F504b79BF599FCf0Ce1340fD065d8` should be replace with your system generated account name, which is generated for your nodes.

- `--password password.txt`: Specifies the path to a file containing the password to unlock the account.

- `--authrpc.port`, `--authrpc.addr`, `--authrpc.vhosts`: Configures the RPC (Remote Procedure Call) server to listen on the specified port and address with virtual host support.

- `--rpc.enabledeprecatedpersonal`: Enables the deprecated personal API for interacting with Ethereum accounts and managing transactions.

- `--http`: Enables the HTTP-RPC server, allowing remote interaction with the Geth node via HTTP.

- `--http.api`: Specifies the APIs to enable for the HTTP-RPC server. Here, "web3,eth,personal,net,miner" enables the Web3, Ethereum, Personal, Network, and Miner APIs.

- `--http.corsdomain`, `--http.vhosts`, `--http.port`: Configures CORS (Cross-Origin Resource Sharing) domain, virtual host support, and the port number for the HTTP-RPC server.

- `--allow-insecure-unlock`: Allows insecure unlocking of the account by accepting plaintext passwords over HTTP.

- `--miner.etherbase`: Sets the Ethereum address that will receive mining rewards when mining is enabled. This account name `0x55860Df9065F504b79BF599FCf0Ce1340fD065d8` should be replace with your system generated account name, which is generated for your nodes. 

- `--rpc.allow-unprotected-txs`: Allows unprotected (non-encrypted) transactions over the RPC interface.

- `--mine`: Enables mining on the node, which means the node will participate in the process of validating and adding new blocks to the blockchain.

Overall, this command starts a Geth node with specified configurations, connects to bootnodes, unlocks an Ethereum account, enables various APIs and services, and allows mining and transaction processing. It provides a way to interact with the Ethereum network via RPC and perform mining operations.

![image](https://github.com/Manasamahesh/privateNetwork/assets/25504822/d4d79e48-0479-4ebb-a17d-74f501358d8e)

 # Connect to the node from command line :
 
 In order to interact with the nodes you need to open a terminal and use geth to attach to it. Run the following command for each of the nodes,    in a separate terminal and use the correct port number for each of them.
 
 `geth attach http://127.0.0.1:8552`
 
 ![image](https://github.com/Manasamahesh/privateNetwork/assets/25504822/aba60d5d-c5e2-4341-809c-93b56ad3067b)
 
 ## Create new account through cli: 
 
 The following are command to create new Account through command line interface:
  
  `personal.newAccount()`
  
  ## Transfer some ether to new account:
   
  `eth.accounts`
 
 Then check the balance of the first account:
 `eth.getBalance(eth.accounts[0])`
 
 Now unlock the first account in order to start a transaction from it:
 
 `personal.unlockAccount(eth.accounts[0])`
 Now send some Ether:
 
 `eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:1000})`
 
 Now you will get the prompt for entering the password which was generated at the time of account creation.
 The next step is to start a miner so that this transaction is actually processed and persisted in the blockchain.
 
 ##  Start a miner
The first thing to do is to set an account to receive the mining awards. This is called the etherbase account. 
Go to the console attached to it and run the following command:
`miner.setEtherbase(eth.accounts[0])`

Then run the following command:
 
 `miner.start()`
 
 You should see null as a response, once this command got executed successfully, and then in the other console where you started the node you should see the progress of the mining that you just started.

You can now verify the balance of the account and check that the transfer was done properly.
 
 `eth.getBalance(eth.accounts[1])`
 
 
# Deploy a Smart Contract
In this section we will create and deploy a simple smart contract into our network. For this we will be using Truffle, which is a development framework for Ethereum.

Run the following command to install the Truffle library:

`npm install -g truffle`

Next we will initialize a new Truffle project by running this command in a new folder:

`truffle init`

After the creation of initial files and directories, you'll need to update the truffle-config.js file to ensure Truffle can establish a connection with your network. Modify the file with the following content, making sure to replace the port number with the one corresponding to your first node's running port. Additionally, provide the complete address of the first account created in that node for the from address field.

      networks: {

      private: {
         host: "127.0.0.1",
         port: 8552,
         network_id: "*",
         gas: "800000", // (default: 6721975)
         from: "0x55860Df9065F504b79BF599FCf0Ce1340fD065d8", // (give the account number which is generated as part of node creation)
        chainId: 8888,
       },
       } 
Next, open the contracts folder and create a new file called calculator.sol. Complete it with the following code, which is a simple contract written in the Solidity language:

`pragma solidity ^0.8.0;

 contract Calculator {

  function add(uint256 a, uint256 b) public pure returns (uint256) {
  
    return a + b;
    
  }
  
  function subtract(uint256 a, uint256 b) public pure returns (uint256) {
  
    return a - b;
    
  }
  
  function multiply(uint256 a, uint256 b) public pure returns (uint256) {
  
    return a * b;
    
  }
  
  function divide(uint256 a, uint256 b) public pure returns (uint256) {
  
    require(b != 0, "Division by zero");
    
    return a / b;
    
  }
  
  function square(uint256 a) public pure returns (uint256){
  
      return a^2;
      
  }
  
 }`

The next step is to update the migrations file so that Truffle knows that it needs to compile and migrate the contract that we just created. Open the 1_deploy_contract.js file located in the migrations folder and modify its content to match the following:

`const Calculator = artifacts.require("Calculator");

module.exports = function (deployer) {

deployer.deploy(Calculator);

};`
Now, we can utilize Truffle to compile our contract and deploy it to our network. It's important to note that Truffle will also compile and deploy its migrations contract. The migrations contract serves the purpose of tracking the deployed versions of our contracts and ensuring they remain up to date.

Go to the contracts folder and run the following command:

`truffle compile`

Next we need to unlock the account in the node, as we are going to deploy the contract using that account. Go to the terminal that is attached to that node and run this command:

`personal.unlockAccount(eth.accounts[0])`

Finally, go back to the contracts folder and run this command to deploy the contract:

`truffle migrate`

The contract should now be deployed in your network in a new address.

![image](https://github.com/Manasamahesh/privateNetwork/assets/25504822/be8117a8-7144-43d1-8928-32ab714d5ef3)


# Interact with contract using truffle

The following command is connect with deployed contracts:

`truffle console`
       
`let MyContract = artifacts.require('Calculator');`       

With the contract instance available, you can now interact with its functions and state variables. You can call contract functions using the instance's method calls. For example:

`let result = await myContractInstance.myFunction();` // Replace 'myFunction' with the actual function name

`console.log(result);` // Output the result or perform further actions 

Here example from deployed contract is,

`let result = await MyContract.add(4,3);`

`console.log(result);`


 
 
 
