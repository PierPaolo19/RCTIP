# Quick Desktop Setup Guide

This is a condensed guide for getting RCTIP running on your desktop computer quickly.

## 🚀 Quick Start (5 Minutes)

### 1. Prerequisites Check
```bash
# Check if Node.js is installed
node --version  # Should show v12.x or higher

# Check if npm is installed
npm --version   # Should show 6.x or higher
```

**Don't have Node.js?** Download from [nodejs.org](https://nodejs.org/)

### 2. Clone and Install
```bash
# Clone the repository
git clone https://github.com/PierPaolo19/RCTIP.git
cd RCTIP

# Install dependencies
npm install
```

### 3. Configure Your Settings

Edit `trx.js` and replace the empty strings:

```javascript
const scam_address = 'YOUR_MONITORING_WALLET_ADDRESS'  // Wallet to monitor
const real_private_key = 'YOUR_PRIVATE_KEY'            // Your private key
const send_to = 'DESTINATION_WALLET_ADDRESS'           // Destination wallet
```

**Note**: Only monitor wallets you have authorization to access.

### 4. Run the Script
```bash
node trx.js
```

You should see output like:
```
Current balance 5000000
Current balance 5000000
...
```

## 📝 What Each File Does

| File | Purpose |
|------|---------|
| `trx.js` | Monitors TRON wallet and auto-transfers funds when balance ≥ 10 TRX |
| `USDT.sol` | Smart contract for token swapping on TRON |
| `package.json` | Defines project dependencies and npm commands |
| `main_net_config.conf` | TRON mainnet node configuration |
| `supernode.conf` | Settings for running a TRON supernode |

## 🎯 Common Use Cases

### Use Case 1: Monitor a Wallet
Just run `node trx.js` after configuring the addresses. The script will:
- Check balance every 1.5 seconds
- Auto-transfer when balance reaches 10+ TRX
- Keep 2 TRX for transaction fees

### Use Case 2: Deploy Smart Contract (Local Testing)
```bash
# Start local TRON node
npm run startnode

# Wait 30 seconds, then compile and deploy
npm run compile
npm run deploylocal
```

### Use Case 3: Deploy to Testnet
```bash
# Create .env file with your key
echo "PRIVATE_KEY=your_key_here" > .env

# Deploy to Shasta testnet
npm run deployshasta
```

## ⚠️ Important Notes

1. **Security**: Never commit your private keys to Git
2. **Testing**: Always test on Shasta testnet before mainnet
3. **Fees**: Ensure wallet has TRX for transaction fees
4. **Backup**: Keep secure backups of your private keys

## 🆘 Quick Troubleshooting

| Problem | Solution |
|---------|----------|
| `Cannot find module 'tronweb'` | Run `npm install` |
| `Connection timeout` | Check internet connection and TRON network status |
| `Insufficient balance` | Add more TRX to your wallet |
| Docker won't start | Make sure Docker Desktop is running |

## 📚 Need More Details?

See the main [README.md](README.md) for:
- Detailed installation instructions
- Complete configuration guide
- Advanced troubleshooting
- Security best practices

## 🔗 Useful Links

- [TRON Documentation](https://developers.tron.network/)
- [TronScan Explorer](https://tronscan.org/)
- [Shasta Testnet Faucet](https://www.trongrid.io/shasta/)
- [TronWeb on GitHub](https://github.com/tronprotocol/tronweb)

---

**Ready to go?** Just run `node trx.js` and you're live! 🎉
