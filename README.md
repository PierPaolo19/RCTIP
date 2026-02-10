# RCTIP
RCTIP flasher json api and nodes 

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [How to Use on Desktop](#how-to-use-on-desktop)
- [Smart Contract Deployment](#smart-contract-deployment)
- [Troubleshooting](#troubleshooting)
- [Disclaimer](#disclaimer)

## Prerequisites

Before running this project on your desktop, ensure you have the following installed:

### Required Software
1. **Node.js** (version 12.x or higher)
   - Download from [https://nodejs.org/](https://nodejs.org/)
   - Verify installation: `node --version`

2. **npm** (comes with Node.js)
   - Verify installation: `npm --version`

3. **Docker** (optional, for local TRON node)
   - Download from [https://www.docker.com/get-started](https://www.docker.com/get-started)
   - Required only if you want to run a local TRON node

4. **Git** (for cloning the repository)
   - Download from [https://git-scm.com/](https://git-scm.com/)

### System Requirements
- **Operating System**: Windows 10/11, macOS 10.14+, or Linux (Ubuntu 18.04+)
- **RAM**: Minimum 4GB (8GB recommended)
- **Disk Space**: At least 1GB free space
- **Internet Connection**: Required for connecting to TRON network

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/PierPaolo19/RCTIP.git
cd RCTIP
```

### Step 2: Install Dependencies
```bash
npm install
```

This will install the following main dependencies:
- `tronweb`: JavaScript library for interacting with the TRON blockchain
- `dotenv`: For managing environment variables
- `jest`: Testing framework

### Step 3: Install TronBox (Optional)
If you plan to compile or deploy smart contracts:
```bash
npm install -g tronbox
```

## Configuration

### Setting Up Environment Variables

Create a `.env` file in the root directory (copy from `.env.example` if available):

```bash
# .env file
PRIVATE_KEY=your_private_key_here
TRON_API_KEY=your_trongrid_api_key_here
```

**Important Security Note**: 
- Never commit your `.env` file to version control
- Keep your private keys secure and never share them
- Add `.env` to your `.gitignore` file

### Configuring the TRX Monitor Script (trx.js)

Edit `trx.js` to configure your wallet monitoring:

```javascript
const scam_address = 'your_wallet_address_to_monitor'
const real_private_key = 'your_private_key_here'
const send_to = 'destination_wallet_address'
```

**Parameters Explanation**:
- `scam_address`: The TRON wallet address you want to monitor (Note: Consider renaming this variable to something more professional like `monitored_address` or `source_address` in the code)
- `real_private_key`: Private key for signing transactions (keep secure!)
- `send_to`: Destination address for automatic transfers

**Note**: This script is intended for legitimate wallet management purposes. Always ensure you have proper authorization to monitor and transfer funds from any wallet address.

## How to Use on Desktop

### Running the TRX Balance Monitor

The `trx.js` script monitors a TRON wallet and automatically transfers funds when the balance reaches a threshold.

#### On Windows:
```cmd
cd path\to\RCTIP
node trx.js
```

#### On macOS/Linux:
```bash
cd /path/to/RCTIP
node trx.js
```

**What the Script Does**:
1. Connects to the TRON network (api.trongrid.io)
2. Checks the balance of the specified address every 1.5 seconds
3. If balance >= 10 TRX, it automatically:
   - Withdraws the balance minus 2 TRX (for fees)
   - Sends the funds to the `send_to` address
4. Logs all activities to the console

**Console Output Example**:
```
Current balance 5000000
Current balance 12000000
Withdrawing 10000000 TRX
{ result: true, transaction: {...} }
```

### Running with a Local TRON Node (Docker)

If you want to run a local TRON development node:

```bash
npm run startnode
```

This command:
- Starts a Docker container with TRON QuickStart
- Exposes the node on port 9090
- Provides a local blockchain for testing

**Wait 30-60 seconds** after starting the node before deploying contracts or running tests.

## Smart Contract Deployment

The repository includes a `USDT.sol` smart contract for token swapping on TRON.

### Compile the Contract
```bash
npm run compile
```

### Deploy to Different Networks

#### Local Development Network:
```bash
npm run deploylocal
```

#### Shasta Testnet:
```bash
npm run deployshasta
```
**Note**: Requires `.env` file with your private key

#### TRON Mainnet:
```bash
npm run deploymain
```
**Warning**: This deploys to the live TRON mainnet. Ensure your contract is thoroughly tested!

### Running Tests

#### Test on Local Network:
```bash
npm run testlocal
```

#### Test on Shasta Testnet:
```bash
npm run testshasta
```

#### Compile, Deploy, and Test (All-in-One):

**Local**:
```bash
npm run cdtl
```

**Shasta**:
```bash
npm run cdts
```

## Project File Structure

```
RCTIP/
├── trx.js                  # TRX balance monitor and auto-transfer script
├── USDT.sol               # Solidity smart contract for token swapping
├── package.json           # Node.js dependencies and npm scripts
├── main_net_config.conf   # TRON mainnet configuration
├── supernode.conf         # Supernode configuration
├── config                 # General configuration file
├── Address.json           # Contract addresses
└── README.md             # This file
```

## Configuration Files Explained

### main_net_config.conf
Contains TRON mainnet node configuration:
- Peer-to-peer network settings
- Node discovery settings
- Database configuration

### supernode.conf
Configuration for running a TRON supernode (validator):
- Witness configuration
- Block production settings
- Network parameters

**Note**: These configuration files are primarily used when running your own TRON node, not required for basic script usage.

## Troubleshooting

### Common Issues

#### 1. "Cannot find module 'tronweb'"
**Solution**: Run `npm install` to install all dependencies.

#### 2. "Error: Private key does not match address"
**Solution**: Verify that your private key corresponds to the wallet address you're using.

#### 3. "Connection timeout" or "Network error"
**Solution**: 
- Check your internet connection
- Verify TRON network status at [https://tronscan.org/](https://tronscan.org/)
- Try using a different RPC endpoint

#### 4. Docker container won't start (npm run startnode)
**Solution**:
- Ensure Docker Desktop is running
- Check if port 9090 is available: `netstat -an | grep 9090`
- Stop any existing containers: `docker stop tron`

#### 5. "Insufficient balance" error
**Solution**: Ensure the wallet has enough TRX for:
- Transaction amount
- Network fees (typically 1-5 TRX)
- Minimum balance for bandwidth

### Getting Help

If you encounter issues:
1. Check the console output for error messages
2. Verify all configuration files are properly set up
3. Ensure you have the latest version of dependencies: `npm update`
4. Review TRON documentation: [https://developers.tron.network/](https://developers.tron.network/)

## Security Best Practices

1. **Never share your private keys**
2. **Use testnet for development** (Shasta testnet)
3. **Test with small amounts** first
4. **Keep your software updated**
5. **Use hardware wallets** for large amounts
6. **Enable 2FA** where possible
7. **Backup your keys** securely offline

## Additional Resources

- **TRON Documentation**: [https://developers.tron.network/](https://developers.tron.network/)
- **TronWeb GitHub**: [https://github.com/tronprotocol/tronweb](https://github.com/tronprotocol/tronweb)
- **TronScan Explorer**: [https://tronscan.org/](https://tronscan.org/)
- **Shasta Testnet Faucet**: [https://www.trongrid.io/shasta/](https://www.trongrid.io/shasta/)

## Disclaimer
----------

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
