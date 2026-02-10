# RCTIP
RCTIP flasher json api and nodes - A TRON blockchain development toolkit for smart contract deployment and TRX monitoring.

## Table of Contents
- [Description](#description)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Running TRX Monitoring Script](#running-trx-monitoring-script)
  - [Smart Contract Development](#smart-contract-development)
  - [Available NPM Scripts](#available-npm-scripts)
- [Project Structure](#project-structure)
- [Disclaimer](#disclaimer)

## Description

RCTIP is a TRON blockchain toolkit that provides:
- TRX balance monitoring and automated withdrawal functionality
- Smart contract development and deployment tools using TronBox
- Integration with TRON mainnet and Shasta testnet
- USDT/TRC20 token contract examples

## Prerequisites

Before using this project, ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v12 or higher recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [Docker](https://www.docker.com/) (optional, for local TRON node)
- [TronBox](https://developers.tron.network/docs/tronbox-installation) (for smart contract development)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/PierPaolo19/RCTIP.git
   cd RCTIP
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Install TronBox globally (if not already installed):
   ```bash
   npm install -g tronbox
   ```

## Configuration

### TRX Monitoring Script Configuration

Edit the `trx.js` file and configure the following variables:

```javascript
const scam_address = ''      // Address to monitor
const real_private_key = ''  // Private key for signing transactions
const send_to = ''           // Destination address for withdrawals
```

**⚠️ Security Warning:** Never commit private keys to version control. Use environment variables or secure key management systems in production.

### Smart Contract Configuration

The project includes configuration files for different TRON networks:
- `main_net_config.conf` - Mainnet configuration
- `supernode.conf` - Supernode configuration
- `config` - General configuration file

For deployment to testnet/mainnet, create a `.env` file with your private key:
```bash
PRIVATE_KEY=your_private_key_here
```

## Usage

### Running TRX Monitoring Script

The `trx.js` script monitors a TRON address and automatically withdraws funds when the balance exceeds 10 TRX:

```bash
node trx.js
```

**How it works:**
1. Checks the balance of `scam_address` every 1.5 seconds
2. When balance reaches ≥10 TRX, it withdraws the amount minus 2 TRX (fee buffer)
3. Sends withdrawn TRX to the `send_to` address
4. Logs all transactions and errors to console

**Note:** The 2 TRX buffer is hardcoded in the script (`withdraw_amount = balance - 2000000`). You can adjust this value based on actual network fees if needed.

### Smart Contract Development

#### Start Local TRON Node

```bash
npm run startnode
```

This starts a Docker container with a local TRON development node on port 9090.

#### Compile Smart Contracts

```bash
npm run compile
```

Compiles all Solidity contracts in the project.

#### Deploy to Local Network

```bash
npm run deploylocal
```

#### Deploy to Shasta Testnet

```bash
npm run deployshasta
```

Make sure your `.env` file is configured with your private key.

#### Deploy to Mainnet

```bash
npm run deploymain
```

**⚠️ Warning:** Deploying to mainnet will use real TRX. Ensure thorough testing before mainnet deployment.

### Available NPM Scripts

| Script | Description |
|--------|-------------|
| `npm run startnode` | Start local TRON development node in Docker |
| `npm run compile` | Compile all smart contracts |
| `npm run deploylocal` | Deploy contracts to local development network |
| `npm run deployshasta` | Deploy contracts to Shasta testnet |
| `npm run deploymain` | Deploy contracts to TRON mainnet |
| `npm run testlocal` | Run tests on local network |
| `npm run testshasta` | Run tests on Shasta testnet |
| `npm run cdtl` | Compile, deploy, and test on local network |
| `npm run cdts` | Compile, deploy, and test on Shasta testnet |
| `npm run specs` | Run Jest test specifications |

## Project Structure

```
RCTIP/
├── trx.js                    # TRX monitoring and withdrawal script
├── USDT.sol                  # USDT/TRC20 token smart contract
├── package.json              # Node.js dependencies and scripts
├── main_net_config.conf      # Mainnet configuration
├── supernode.conf            # Supernode configuration
├── config                    # General configuration
├── Address.json              # Address storage
└── README.md                 # This file
```

## Disclaimer

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE. 
