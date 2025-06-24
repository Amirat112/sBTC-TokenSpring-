

##  README

###  sBTC-TokenSpring

This Clarity smart contract implements a **token vesting system with built-in fungible token capabilities**. The contract allows the contract owner to:

* Initialize a SIP-010-compliant fungible token with a fixed supply.
* Create configurable vesting schedules for multiple recipients.
* Release vested tokens over time or according to milestone-based schedules.

Recipients can then call the `release` function to claim their vested tokens as they become available.

---

### ✨ Key Features

✅ **Token Creation and Configuration**
The contract supports creating a fungible token that follows the SIP-010 standard (`get-name`, `get-symbol`, `get-decimals`, `get-token-uri`, etc.).

✅ **Vesting Schedules**
Each recipient can have a customized schedule defined by:

* `total-amount`: Total number of tokens vested.
* `start-block`: Block height when vesting begins.
* `cliff-blocks`: Cliff period length before vesting can begin.
* `duration-blocks`: Total vesting duration.
* `milestones`: A list of milestone dates and their percentage vesting.

✅ **Milestone Support**
Optional milestone-based vesting for more granular token release.

✅ **Safe Arithmetic**
Dedicated `safe-add`, `safe-sub`, `safe-mul`, and `safe-div` prevent overflows.

✅ **Ownership Control**
Only the `contract-owner` can initialize the contract and create new vesting schedules.

---

### 🧠 Core Functions

#### 📜 Public

* `initialize(name, symbol, decimals, uri, initial-supply)`:
  Sets up the token and mints the total supply to the owner.
* `create-vesting-schedule(...)`:
  Creates a new vesting schedule for a recipient.
* `release()`:
  Allows a recipient to withdraw their vested tokens.

#### 📖 Read-Only

* `get-vesting-schedule(recipient)`:
  Fetches the vesting schedule of a recipient.
* `get-vested-amount(recipient)`:
  Retrieves the amount vested so far.
* `get-releasable-amount(recipient)`:
  Retrieves the amount that can be claimed immediately.
* `get-name()`, `get-symbol()`, `get-decimals()`, `get-token-uri()`:
  SIP-010 standard getters.
* `get-balance(account)`, `get-total-supply()`:
  Fungible token getters.

---

### 🧮 Error Codes

* `err-owner-only (u100)`: Unauthorized sender.
* `err-already-initialized (u101)`: Contract already initialized.
* `err-no-schedule (u103)`: No schedule found for recipient.
* `err-insufficient-balance (u105)`: Insufficient vested tokens to withdraw.
* … and more.
  (See source for full list.)

---

### 🏗️ Usage Flow

1. Owner calls `initialize()` to set up token parameters.
2. Owner calls `create-vesting-schedule()` for each recipient.
3. Recipients wait for cliff or milestones to pass.
4. Recipients call `release()` to receive their vested tokens.

---
