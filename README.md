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
* Create new account.
* Send some Ether
* Start a miner
* Deploy a Smart Contract
* Interact with contract using truffle

# Install Geth:

Geth is an Ethereum client written in Go. This means running Geth turns a computer into an Ethereum node. To install it on a linux, run the following commands:

`sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum`

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

`{

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
    
}`
The given JSON represents a configuration file for a private Ethereum network. Let's go through each key and its purpose:

"config": This section defines various configuration parameters for the network.

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


"alloc": This section defines the initial account balances for specific addresses.

"0x55860Df9065F504b79BF599FCf0Ce1340fD065d8": This address is assigned a balance of "9999999999999999999999999" wei.
"0x1496d986cc5194b39f82ea89A61c1b31Cf33F57e": This address is also assigned a balance of "9999999999999999999999999" wei.

# Create node:







 
