# 💸 Expense Tracker App

A decentralized application (dApp) built with **Solidity** and **React**, allowing users to track expenses on the blockchain. It includes features like updating/displaying a user name and converting ETH to INR.

---

## 🚀 Features

- Update user name on the blockchain (Solidity)
- Display user name in frontend (React)
- Real-time ETH to INR conversion

---

## 🛠 Tech Stack

- **Solidity** (Smart Contract)
- **ReactJS** (Frontend)
- **Ether.js / Web3.js** (Blockchain Interaction)
- **CoinGecko API** (for ETH-INR conversion)

---

## 📦 Smart Contract: Update Name Feature (Solidity)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ExpenseTracker {
    string public name;

    constructor(string memory _name) {
        name = _name;
    }

    function updateName(string memory _newName) public {
        name = _newName;
    }

    function getName() public view returns (string memory) {
        return name;
    }
}
💻 Frontend: Display Name (JavaScript / React)
javascript
Copy
Edit
import { useEffect, useState } from "react";
import { ethers } from "ethers";
import ExpenseTrackerABI from "./abis/ExpenseTracker.json";

const CONTRACT_ADDRESS = "0xYourContractAddressHere";

function DisplayName() {
  const [name, setName] = useState("");

  useEffect(() => {
    const fetchName = async () => {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const contract = new ethers.Contract(CONTRACT_ADDRESS, ExpenseTrackerABI.abi, provider);
      const currentName = await contract.getName();
      setName(currentName);
    };

    fetchName();
  }, []);

  return <div>Your Name: {name}</div>;
}

export default DisplayName;
💱 ETH to INR Converter (JavaScript)
javascript
Copy
Edit
import { useEffect, useState } from "react";

function EthToInrConverter() {
  const [ethPrice, setEthPrice] = useState(null);

  useEffect(() => {
    const fetchEthPrice = async () => {
      const res = await fetch("https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=inr");
      const data = await res.json();
      setEthPrice(data.ethereum.inr);
    };

    fetchEthPrice();
  }, []);

  return (
    <div>
      1 ETH = ₹{ethPrice ? ethPrice.toLocaleString() : "Loading..."}
    </div>
  );
}

export default EthToInrConverter;
📌 Setup
bash
Copy
Edit
# Clone the repo
git clone https://github.com/yourusername/expense-tracker-app.git

# Navigate into the frontend
cd frontend

# Install dependencies
npm install

# Run the app
npm start
