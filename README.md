CapituCoin/
├── contracts/
│   └── CapituCoin.sol
├── migrations/
│   └── 1_deploy_contract.js
├── test/
│   └── CapituCoin.test.js
├── package.json
├── truffle-config.js
├── README.md

1. **contracts/CapituCoin.sol**:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";

contract CapituCoin is ERC20, ERC20Burnable, Ownable, Pausable {
    uint256 public constant INITIAL_SUPPLY = 10_000_000_000_000 * 10**18;

    constructor(address owner) ERC20("CapituCoin", "CAPITU") {
        transferOwnership(owner);
        _mint(owner, INITIAL_SUPPLY);
    }
}
```

2. **migrations/1_deploy_contract.js**:
```javascript
const CapituCoin = artifacts.require("CapituCoin");

module.exports = function (deployer, network, accounts) {
  deployer.deploy(CapituCoin, accounts[0]);
};
```

3. **test/CapituCoin.test.js**:
```javascript
const CapituCoin = artifacts.require("CapituCoin");

contract("CapituCoin", (accounts) => {
  it("should deploy successfully", async () => {
    const instance = await CapituCoin.deployed();
    assert(instance.address !== "");
  });
});
```

4. **package.json**:
```json
{
  "name": "capitucoin",
  "version": "1.0.0",
  "description": "CapituCoin ERC-20 Token",
  "main": "truffle-config.js",
  "scripts": {
    "test": "truffle test"
  },
  "author": "",
  "license": "MIT",
  "dependencies": {
    "@openzeppelin/contracts": "^4.9.2",
    "truffle": "^5.9.0",
    "@truffle/hdwallet-provider": "^2.1.13"
  }
}
```

5. **truffle-config.js**:
```javascript
module.exports = {
  networks: {
    bscTestnet: {
      provider: () => new HDWalletProvider(
        "<YOUR_MNEMONIC>",
        "https://data-seed-prebsc-1-s1.binance.org:8545"
      ),
      network_id: 97,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true,
    },
  },
  compilers: {
    solc: {
      version: "^0.8.0",
    },
  },
};
```

6. **README.md**:
```markdown
# CapituCoin

CapituCoin is an ERC-20 token deployed on Binance Smart Chain. It is inspired by the character "Capitu" from Brazilian literature.

## Requirements
- Node.js
- Truffle
- Ganache
- MetaMask

## Deploy Instructions
1. Install dependencies:
   ```bash
   npm install
   ```

2. Compile the smart contracts:
   ```bash
   truffle compile
   ```

3. Deploy to BSC Testnet:
   ```bash
   truffle migrate --network bscTestnet
   ```

4. Run tests:
   ```bash
   truffle test
   ```

## License
MIT
