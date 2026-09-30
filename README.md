# SC6113-Class-Example-ChatGPT

A minimal Flask + HTML + CSS DApp for a `SimpleStorage` smart contract.

- Contract: `0xab32bd19c1a369b9a949aa7ff2bd0ef5a2518b76`
- **Read** (`get()`): Flask calls the contract through `RPC_URL` (falls back to MetaMask).
- **Write** (`set(uint256)`): signed in the browser by the user's MetaMask wallet.
  The server never holds a private key.

## Project structure

```
app.py               Flask backend (reads the contract via web3.py)
requirements.txt
Procfile             gunicorn entry point for cloud hosts
templates/index.html Frontend (ethers.js + MetaMask)
static/styles.css
```

## Run locally

```bash
pip install -r requirements.txt
export RPC_URL="https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY"
python app.py
```

Open http://localhost:5000. Make sure MetaMask is on the same network the contract is deployed to.

## Environment variables

| Name               | Required | Description                                      |
|--------------------|----------|--------------------------------------------------|
| `RPC_URL`          | yes      | RPC endpoint of the network the contract is on   |
| `CONTRACT_ADDRESS` | no       | Override the default contract address            |
| `SECRET_KEY`       | no       | Flask secret key                                 |
| `PORT`             | no       | Port for `python app.py` (default 5000)          |

Do not commit your RPC API key — set it as an environment variable on your host.

## Deploy (Render / Railway)

- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn app:app` (already in `Procfile`)
- Add `RPC_URL` in the service's environment settings.
