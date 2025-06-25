# Simple Blockchain
Welcome to Simple Blockchain, a lightweight and educational implementation of a blockchain network built with Python and Flask. This project demonstrates the core concepts of blockchain technology, including proof-of-work, distributed consensus, and transaction management, in an easy-to-understand way.

## Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [How It Works](#how-it-works)
- [License](#license)

## Features
- **Proof-of-Work (PoW)**: Implements a simple PoW algorithm for mining new blocks.
- **Distributed Network**: Supports multiple nodes with chain synchronization.
- **Transaction Management**: Add and validate transactions across the blockchain.
- **RESTful API**: Built with Flask to interact with the blockchain via HTTP requests.
- **Genesis Block**: Initializes the blockchain with a genesis block.
- **Chain Validation**: Ensures the integrity of the blockchain across nodes.

## Tech Stack
- **Python 3.x**: Core programming language.
- **Flask**: Lightweight web framework for API development.
- **Requests**: For handling HTTP requests between nodes.
- **Hashlib**: For SHA-256 hashing of blocks.
- **JSON**: For encoding and decoding block data.

## Installation
Follow these steps to set up the project locally:
1. **Clone the Repository**:
   ```
   git clone https://github.com/RaihanFerdy/Simple-Blockchain.git
   cd Simple-Blockchain
   ```
2. **Create a Virtual Environment**:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. **Install Dependencies**:
   ```
   pip install -r requirements.txt
   ```
4. **Run the Application**:
   Start a node by specifying a port (e.g., 5000):
   ```
   python blockchain.py 5000
   ```
5. **Run Multiple Nodes** (optional):
   Open new terminal windows and run additional nodes on different ports:
   ```
   python blockchain.py 5001
   python blockchain.py 5002
   ```

## Usage
Once the nodes are running, you can interact with the blockchain using the provided API endpoints. Use tools like **cURL**, **Postman**, or a web browser to send HTTP requests.
### Example: Adding a Transaction
```
curl -X POST -H "Content-Type: application/json" -d '{"sender":"04d0988bfa799f7d7ef9ab3de97ef481","recipient":"cd0f75d2367ad456607647edde665d6f","amount":50}' http://localhost:5000/transactions/new
```
### Example: Mining a Block
```
curl http://localhost:5000/mine
```
### Example: Adding a Node
```
curl -X POST -H "Content-Type: application/json" -d '{"nodes":["http://localhost:5001"]}' http://localhost:5000/nodes/add_nodes
```
### Example: Syncing the Blockchain
```
curl http://localhost:5000/nodes/sync
```

## API Endpoints
| Endpoint                | Method | Description                              |
|-------------------------|--------|------------------------------------------|
| `/blockchain`           | GET    | Retrieve the full blockchain.            |
| `/mine`                 | GET    | Mine a new block.                        |
| `/transactions/new`     | POST   | Add a new transaction to the blockchain. |
| `/nodes/add_nodes`      | POST   | Register new nodes to the network.       |
| `/nodes/sync`           | GET    | Synchronize the blockchain with peers.   |
### Request/Response Examples
**POST /transactions/new**
- Request:
  ```
  {
    "sender": "04d0988bfa799f7d7ef9ab3de97ef481",
    "recipient": "cd0f75d2367ad456607647edde665d6f",
    "amount": 50
  }
  ```
- Response:
  ```
  {
    "message": "Transaction will be added to block 2"
  }
  ```

**GET /mine**
- Response:
  ```
  {
    "hash_of_previous_block": "986b701e70e2737f7e221a5415c6257f0f56300441e792ac4bb4815b656dc6a2",
    "index": 2,
    "message": "A new block has been mined",
    "nonce": 83056,
    "transaction": [
        {
            "amount": 1,
            "recipient": "d779fe7e959d499d979661b538718e02",
            "sender": "0"
        }
    ]
  }
  ```

## How It Works
1. **Genesis Block**: The blockchain starts with a genesis block, hashed with SHA-256.
2. **Proof-of-Work**: Miners solve a computational puzzle to find a nonce that produces a hash starting with a specified number of zeros (difficulty target).
3. **Transactions**: Users submit transactions, which are stored in a block and validated during mining.
4. **Consensus**: Nodes synchronize their chains by adopting the longest valid chain in the network.
5. **Node Network**: Multiple nodes can join the network, and the blockchain ensures consistency across them.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
