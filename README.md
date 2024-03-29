# MonoBlockchain

MonoBlockchain is a decentralised proof of work blockchain with the backend written in Python. 

The cryptocurrency individually is referred to as an _MB Coin_ (Mono Block Coin).

[Preview Video](#preview-video)



<p align="center">
    <img width="238" alt="MonoBlockchain Preview" src="https://user-images.githubusercontent.com/10171446/177392317-24968898-0c8f-4944-8d33-5f0c6681ae64.png">
</p>

<p align="center">
</p>

# Features

- Immutable Ledger
- Distributed P2P Network
- Proof of Work (SHA-256)
- Consensus Protocol
- Easy to Use Transaction System
- HTML User Interface
- Developer Friendly:
  - API-Based Backend
  - Frameworks: Bootstrap, DataTables, FontAwesome, jQuery



# Table of Contents
- [Setup and Usage](#setup-and-usage)
  - [Python Version](#python-version)
  - [Dependencies](#dependencies)
  - [Initialising Servers](#initialising-servers)
- [Blockchain Concepts](#blockchain-concepts)
  - [Proof of Work](#proof-of-work)
  - [Hashing Algorithm](#hashing-algorithm)
  - [Immutable Ledger](#immutable-ledger)
  - [Distributed P2P](#distributed-p2p)
  - [Mining](#mining)
  - [Consensus Protocol](#consensus-protocol)
- [Programming Logic](#programming-logic)
  - [How Mining Works (Technical)](#how-mining-works-technical)
  - [User Interface](#user-interface)
  - [Encoding](#encoding)
  - [Verification](#verification)
- [Preview Images of the Blockchain Client](#preview-images-of-the-blockchain-client)
  - [Alice Generating a Wallet](#alice-generating-a-wallet)
  - [Bob Generating a Wallet](#bob-generating-a-wallet)
  - [Making a Transaction](#making-a-transaction)
  - [Successful Transaction](#successful-transaction)
  - [Viewing Transactions](#viewing-transactions)
- [Preview Images of the Blockchain Server](#preview-images-of-the-blockchain-server)
  - [Viewing Transactions to be Mined](#viewing-transactions-to-be-mined)
  - [Mining](#mining)
  - [Configuring the Blockchain](#configuring-the-blockchain)
  - [Consensus Between Nodes Blockchain](#consensus-between-nodes-blockchain)
- [Preview Video](#preview-video)

# Setup and Usage

## Python Version

    $ python3.10
    Python 3.10.5


## Dependencies



### Node (Server)
    pip3.10 install Crypto \
                    Flask \
                    Flask_CORS \ 
                    PyCryptoDome


### Client
    pip3.10 install Crypto \
                    Flask \
                    PyCryptoDome

## Initialising Servers

Initialisation can be done in two ways. One is via PyCharm the other is running multiple Python instances via the command line.

### PyCharm

#### Node1 (Server)

Within PyCharm under _Run/Debug Configurations > Add New Configuration > Python_, the following Configuration should be chosen:

  - Name: Node1
  - Script path: ~/PycharmProjects/MonoBlockchain/blockchain/blockchain.py
  - Parameters: -p 5001
  - Python interpreter: Python 3.10

  <p align="center">
  <img width="1156" alt="PyCharm Configuration Node1" src="https://user-images.githubusercontent.com/10171446/177368870-a389d38d-8d70-47d7-a7ab-58efa73eb58e.png">
  </br>
  <b>PyCharm Configuration Node1</b>
</p>

#### Node2 (Server)

  - Name: Node2
  - Script path: ~/PycharmProjects/MonoBlockchain/blockchain/blockchain.py
  - Parameters: -p 5002
  - Python interpreter: Python 3.10

#### Alice (Client)

  - Name: Alice
  - Script path: ~/PycharmProjects/MonoBlockchain/blockchain_client/blockchain_client.py
  - Parameters: -p 8081
  - Python interpreter: Python 3.10

<p align="center">
  <img width="1196" alt="PyCharm Configuration Alice" src="https://user-images.githubusercontent.com/10171446/174770596-5742d253-496b-4357-a4a0-698de77659f8.png">
  </br>
  <b>PyCharm Configuration Alice</b>
</p>

#### Bob (Client)

  - Name: Bob
  - Script path: ~/PycharmProjects/MonoBlockchain/blockchain_client/blockchain_client.py
  - Parameters: -p 8082
  - Python interpreter: Python 3.10

<p align="center">
  <img width="1196" alt="PyCharm Configuration Bob" src="https://user-images.githubusercontent.com/10171446/174770973-8e59cb41-9e6b-4e30-a6f0-40350dd86935.png">
  </br>
  <b>PyCharm Configuration Bob</b>
</p>

#### Running the Configuration

<p align="center">
  <img width="1326" alt="PyCharm Configurations" src="https://user-images.githubusercontent.com/10171446/174771586-566e19c6-fb7c-4ddb-8dd8-31a17f7ac28e.png">

  </br>
  <b></b>
</p>

PyCharm Configurations are outlined in greater detail [here](https://www.jetbrains.com/help/pycharm/configuring-python-interpreter.html#packages).


### Command-Line

CMD.exe / Terminal / Shell

#### Node1 (server)

    $ python3 ~/MonoBlockchain/blockchain/blockchain.py


#### Alice (client)

    $ python3 ~/MonoBlockchain/blockchain-client/blockchain-client.py -p 8081

#### Bob (client)

    $ python3 ~/MonoBlockchain/blockchain-client/blockchain-client.py -p 8082


# Blockchain Concepts

## Proof of Work

MonoBlockchain is based on Proof of Work (PoW).

  - [Investopedia](https://www.investopedia.com/terms/p/proof-work.asp)
  - [Wikipedia](https://en.wikipedia.org/wiki/Proof_of_work#:~:text=Proof%20of%20work%20(PoW)%20is,minimal%20effort%20on%20their%20part.)

## Hashing Algorithm

PoW relies on SHA256 due to requiring:
  - One-way function
    - [The avalanche effect](https://www.cryptovision.com/en/glossary/avalanche-effect/#:~:text=The%20Avalanche%20Effect%20refers%20to,show%20a%20strong%20avalanche%20effect.)
    - [Deterministic](https://www.sqlite.org/deterministic.html#:~:text=A%20deterministic%20function%20always%20gives,input%20X%20is%20the%20same.)
  - Fast computation
  - Must withstand collisions (SHA-256 has 2<sup>256</sup> combinations)

## Immutable Ledger

The idea of an immutable ledger is to ensure the previous hash is linked cryptographically to the last block. Which then can be traversed back to the genesis (initial) block.

<p align="center">
  <img width="640" alt="Immutable Ledger Example" src="https://user-images.githubusercontent.com/10171446/172579310-c11ca268-f185-4560-8b89-5388aa17dabb.png">
  </br>
  <b>Immputable Ledger</b>
</p>

If _block 2_ were to be maliciously altered, the previous hash on _block 3_ would reflect this alteration. As the hash of _block 2_ would not be equal to the previous hash of _block 3_.

## Distributed P2P

### Explanation of Distributed P2P

A distributed peer-to-peer (P2P) network ensures that the blockchain ledger's network is not centralised. 

<p align="center">
  <img width="575" alt="image" src="https://user-images.githubusercontent.com/10171446/172582471-6d101052-4e95-4482-b3f8-6c6bd120bf1e.png">
  </br>
  <b>Distributed P2P Network: Showing Computers (Servers) as Nodes</b>
</p>

Having a decentralised network provides several benefits:
  - More nodes in the network
  - Potentially faster as not relying on a single node
  - More secure as the ledger has no single point of failure


<p align="center">
  <img width="681" alt="Distributed P2P Network Showing Blocks" src="https://user-images.githubusercontent.com/10171446/172584273-9f9cdf41-b5d2-4727-b232-eebe8802473c.png">
  </br>
  <b>Distributed P2P Network Showing Blocks</b>
</p>

### Attacking Distributed P2P Network

Because of the immutable ledger, the attack must modify earlier blocks to reflect the hash change. Which requires much processing power as the SHA-256 algorithm is computationally demanding.

The attack vector of computing forged blocks is demonstrated below:

<p align="center">
  <img width="682" alt="Distributed P2P Network Being Attacked" src="https://user-images.githubusercontent.com/10171446/172584901-121923b0-2890-41ad-8f0f-d78d8d447461.png">
  </br>
  <b>Distributed P2P Network Being Attacked</b>
</p>

However, for the example above, seven nodes maintain an independent version of the ledger. The attacker has successfully modified blocks and forged the ledger cryptographically to reflect an action that did not occur. However, the attacker did this for a single node. As the attacker only makes up 14% of the distributed P2P network. For the attacker to successfully perform their attack, they must control 51% or more of the network's nodes. 

See, [51% attack](https://www.investopedia.com/terms/1/51-attack.asp#:~:text=A%2051%25%20attack%20is%20an,other%20miners%20from%20completing%20blocks.).

## Mining

Mining is the competitive process that verifies and adds new transactions to the Blockchain for a cryptocurrency that uses the proof of work (PoW) method. The miner that wins the competition is rewarded with some amount of the currency and/or transaction fees - [source](https://www.pcmag.com/encyclopedia/term/crypto-mining#:~:text=(CRYPTOcurrency%20mining)%20The%20competitive%20process,currency%20and%2For%20transaction%20fees.).

Consider further reading [PoW - Wikipedia](https://en.wikipedia.org/wiki/Proof_of_work).

The main point with mining is _hard to solve, easy to verify_.


### Explanation of How Mining Works (Abstract)
[Bitcoin Mining in 4 Minutes - Computerphile](https://www.youtube.com/watch?v=wTC31ZI6QM4) will give a ver clear outline of Bitcoin mining. MonoBlockchain is based on the same concept, and the PoW hashing algorithm is also SHA-256. So, there is little difference from a mining perspective between Bitcoin and MonoBlockchain.

[Nonce](https://en.wikipedia.org/wiki/Cryptographic_nonce) (number once) is an arbitrary number that can be used just once in a cryptographic communication. The nonce is used to ensure old communications cannot be reused.

<p align="center">
  <img width="464" alt="Abstract Overview of a Block" src="https://user-images.githubusercontent.com/10171446/172814804-7b06b2ad-6641-44d7-9034-cdc395bd8867.png">
  </br>
  <b>Abstract Overview of a Block</b>
</p>



### Why is Mining Necessary?

The short answer is to prevent abuse of the network. Requiring computational power to _prove work_ is a logical method for mitigating DoS attacks while still keeping the usage of the network feasible.


## Consensus Protocol

A consensus protocol aims to achieve agreement between nodes regarding what a blockchain should contain at a given time (including new blocks).

### First Challenege

Referring back to _Attacking Distributed P2P Network_, we saw the attacker achieved a tampered version of the Blockchain but only contributed 14% of the entire distributed network. The other 86% naturally outnumbered the malicious blockchain node. 


### Second Challenege

Because each node in the distributed P2P network will mine the next block independently, a problem arises; overlapping nodes during synchronisation.

<p align="center">
  <img width="661" alt="Second Challenege to Overcome" src="https://user-images.githubusercontent.com/10171446/173308045-ce98925e-ed15-4c2d-a586-6266bbd8b0fb.png">
  </br>
  <b>Consensus Protocol - Second Challenege: Overlapping Nodes</b>
</p>

The consensus to avoid overlapping nodes is to wait for a new block to be mined before synchronising with other nodes in the network. Once a node has mined a new block, the other nodes will be asked to add it to their blockchain.

Essentially, _the longest chain wins_ is a consensus between nodes.

#### Orphan Block

Another issue to consider as a blockchain PoW network user is orphan blocks.

An [orphan block](https://www.investopedia.com/terms/o/orphan-block-cryptocurrency.asp#:~:text=An%20orphan%20block%20is%20a,the%20shorter%20chain%20are%20orphaned.) is a block that has been solved within the blockchain network but was not accepted by the network.

An orphan block can occur because _there can be two miners who solve valid blocks simultaneously. The network uses both blocks until one chain has more verified blocks. Then, the blocks in the shorter chain are orphaned._

Ideally, to avoid falling victim to an orphan block, users would be advised to wait for 4-6 blocks after their transaction was verified before considering the transaction as 'fully' verified.

# Programming Logic

## How Mining Works (Technical)
This section is still under development.

The backend code is be viewed in `blockchain/blockchain.py`.

### Mining Values

Within `blockchain/blockchain.py` the following values are assigned:

    MINING_SENDER = "Blockchain - Miner Reward"
    MINING_REWARD = 1
    MINING_DIFFICULTY = 2

A possible future development could include writing functions to progressively change the `MINING_REWARD` and `MINING_DIFFICULTY`. However, for now the values are constant.

### Hash Calculation

### Proof of Work

`def proof_of_work(self):` 


## User Interface

To reduce development time with the user interface (UI), I have opted for using HTML with frameworks and host via HTTP using the [render_template](https://flask.palletsprojects.com/en/2.1.x/quickstart/#rendering-templates) function in the `Flask` library.



### JavaScript

Within `blockchain_client/static/js/script.js` is the location for user-written JavaScript, which is contained within the `blockchain_client/templates/*`. The same logic applies to `blockcahin/static/js/script.js`.

#### Blockchain Frontend

Because of the length of a public key `30819f300d06092a864886f70d010101050003818d00308189028181009f148fb25857801a51cb3a294af9707b27ce92e99a7c65604210a4675b855dc7166127a651bc2ae47f38ce726e3b9aeb978b869d67fb0b4ed24bfbd31c8cc8fb289a8f986eca64a993db4426f6307f307e3139d648d44ad7428b487a79642a2c43783f48bf60f9795a848f182459b14bb9c41553f4d3363732b7786eb2589d270203010001` I decided to use JavaScript to render public keys longer than 25-characters using ellipsis for the transactions table.

The following logic can be found in `blockchain/static/js/script.js`:

    columnDefs: [{targets: [1,2,3,4,5], render: $.fn.dataTable.render.ellipsis(25)}]

##### Transactions on the Blockchain

Within `blockchain/static/js/script.js` is the timestamp for transactions.

    formattedTimestamp = date.toLocaleTimeString('en-GB', options);

Currently, the timezone is configured to British English `en-GB`, but feel free to change this, possibly to `UTC`.

An outline of the `toLocaleTimeString()` function available via [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleTimeString).

##### Transactions on the Blockchain Client

Similar behaviour is seen within `blockchain_client/static/js/script.js`

    var formattedDateTime = date.toLocaleTimeString("en-GB", options);

### Frameworks

The following frameworks are used:

  - Bootstrap v4.0.0 
  - DataTables 1.10.16
  - Font Awesome 4.7.0 
    - Font Awesome webfont
  - jQuery JavaScript Library v3.3.1

### CDNs and SRI Hashes

CDNs have been used and where the CDN did not provide an SRI Hash for integrity checks of the href/src I manually created the [SRI Hash](https://www.srihash.org/).

_Possibly_ in a future revision, CDN files will be loaded locally via './static/vendor/' and have a local copy instead.

### Specifying Node on Client-Side

Within `blockchain-client/template/make_transactions.html` the input tag contains `value="http://127.0.0.1:5001"`

Do chnage the `value=""` as necessary.

    <div class="row">
      <label class="col-sm-12">Blockchain Node URL:</label>
      <div class="col-sm-12">
        <input type="text" name="node_url" id="node_url" rows="2" class="form-control" value="http://127.0.0.1:5001">
      </div>
    </div>


The `value` is changeable when generating a transaction, as the client allows choosing which node to send the transaction to.

<p align="center">
  <img width="483" alt="Confirm Transaction Details" src="https://user-images.githubusercontent.com/10171446/175831064-0dd92807-06b9-4aac-b082-6458395c0af0.png">

  </br>
  <b>Make Transaction page displaying Confirm Transaction Details</b>
</p>

## Encoding
Throughout the project, communication between the node (server) and client data is passed via JSON. Because of this, data is converted into a String and then encoded.

### Public-key

Here the `hexlify` function is used.

### Hash

SHA-256 hashes are encoded using UTF-8, as indicated within `blockchain/blockchain.py`

    def verify_transaction_signature(self, sender_public_key, signature, transaction):
      ...
      h = SHA.new(str(transaction).encode('utf8'))

## Verification
Because MonoBlockchain was developed for educational purposes, some lightweight basic validation choices were made, which do not offer real-world protection.

### New Transaction
Within `blockchain/blockchain.py`, the following logic for validating a new transaction has been implemented.

    def new_transaction():
        values = request.form
        required = ['confirmation_sender_public_key', 'confirmation_recipient_public_key', 'transaction_signature',
                    'confirmation_amount']
        if not all(k in values for k in required):
            return 'Missing values', 400

Please take care with `if not all(k in values for k in required):` as the logic was only to check if all values were present, nothing more. Erroneous values can be entered into the blockchain.


# Preview Images of the Blockchain Client

## Alice Generating a Wallet


<p align="center">
  <img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177380333-2307962e-1afd-46a4-b3e3-ec7980c8b916.png">
  </br>
  <b></b>
</p>

## Bob Generating a Wallet


<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177380535-cc431931-883c-46fe-9742-41400db6c597.png">
  </br>
  <b></b>
</p>

## Making a Transaction

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177380770-9b6bdac2-b9b7-441a-98d1-e0063ed9fef3.png">

</br>
  <b>Alice Sending Bob 100 MB Coin</b>
</p>

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177380964-6cbcc98b-9ec8-483f-ac18-013e54ee0839.png">


<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177380770-9b6bdac2-b9b7-441a-98d1-e0063ed9fef3.png">
</br>
  <b></b>
</p>


## Successful Transaction


<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177381046-49c9118f-f1ae-4ae9-988b-5f6bc2bf83b6.png">
</br>
  <b>The Prompt of a Successful Transaction</b>
</p>

## Viewing Transactions

Onced mined transactions for the specified node are displayed.

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177382893-08fd67ab-81f6-44ea-bf8a-e07bb7e8c580.png">
</br>
  <b>Bob Viewing Transactions on Node1</b>
</p>


# Preview Images of the Blockchain Server

## Viewing Transactions to be Mined

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177381322-38aa44e0-5295-48ba-b4af-6a6e1dd704a9.png">

</br>
  <b>Viewing Transactions to be Mined on Node1</b>
</p>

## Mining

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177381754-a8aac3ed-7823-405c-be8e-84c8d6aad069.png">
</br>
  <b>Mining Transaction on Node1</b>
</p>

## Configuring the Blockchain

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177381969-dbb9550e-8e91-43f9-8200-6a1361cd2ec7.png"></br>
  <b>Configuring the Blockchain Node</b>
</p>

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177382117-04e51abc-a54e-45df-9ff0-fded7c311580.png">  
<b>Configuring the Blockchain Node</b>
</p>

## Consensus Between Nodes Blockchain

<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177382265-c3cb437b-c81d-4c07-a6e8-f379546c7bda.png">
<b>Consensus Between Node 1 and Node 2</b>
</p>


<p align="center">
<img width="1392" alt="image" src="https://user-images.githubusercontent.com/10171446/177382362-30d7e2a6-30cd-4c48-b4a1-6b1a41573c63.png">
<b>Consensus Between Node 1 and Node 2</b>
</p>


# Preview Video
[MonoBlockchain Preview | YouTube](https://www.youtube.com/watch?v=I5-dnr9fH-Q)
