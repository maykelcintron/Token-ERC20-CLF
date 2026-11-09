# My Cyfrin CLF Token (CLF)

A secure and modular ERC20 token smart contract developed in Solidity using the **OpenZeppelin** framework. This contract implements a role-based access control system (`AccessControl`) instead of a single owner (`Ownable`), enabling more granular management of minting permissions.

---

## 🚀 Features

- **ERC20 Standard:** Compatible with any standard Ethereum wallet, exchange, or smart contract.
- **Role-Based Access Control (`AccessControl`):** Separates administrative privileges from operational privileges using cryptographic roles (`DEFAULT_ADMIN_ROLE` and `MINTER_ROLE`).
- **Controlled Minting:** Only authorized accounts with the minter role can create new tokens.
- **OpenZeppelin v5.2.0:** Utilizes the ecosystem's most secure and audited contract libraries.

---

## 📋 Technical Specifications

- **Solidity Version:** `^0.8.26`
- **Libraries:** `@openzeppelin/contracts@5.2.0`
- **Token Name:** `My Cyfrin CLF Token`
- **Symbol:** `CLF`
- **Decimals:** `18` (default for ERC20)

---

## 🔐 Role System

The contract manages two main roles that are automatically assigned to the creator (`msg.sender`) during deployment in the constructor:

1. **`DEFAULT_ADMIN_ROLE`:** Global contract administrator. Can grant or revoke both the admin and minter roles to other addresses.
2. **`MINTER_ROLE`:** Role with exclusive permissions to execute the `mint` function and create new tokens in circulation.

---

## 💻 Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

import {ERC20} from "@openzeppelin/contracts@5.2.0/token/ERC20/ERC20.sol";
import {AccessControl} from "@openzeppelin/contracts@5.2.0/access/AccessControl.sol";

contract MyERC20 is ERC20, AccessControl {
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");

    constructor() ERC20("My Cyfrin CLF Token", "CLF") {
        _grantRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _grantRole(MINTER_ROLE, msg.sender);    
    }

    function mint(address to, uint256 amount) public onlyRole(MINTER_ROLE) {
        _mint(to, amount);
    }
}
```

---

## 🛠️ Installation and Compilation

If you are using development frameworks like **Foundry** or **Hardhat**, make sure to install the specified OpenZeppelin dependencies:

### With Foundry:
```bash
forge install OpenZeppelin/openzeppelin-contracts@v5.2.0
```

### With Hardhat (npm):
```bash
npm install @openzeppelin/contracts@5.2.0
```

---

## 📜 License

This project is licensed under the [MIT](LICENSE) license.
