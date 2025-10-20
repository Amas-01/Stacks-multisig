# Stacks Multisig Wallet

This project provides a multisig (multi-signature) wallet smart contract for the Stacks blockchain. It allows a group of owners to manage shared crypto assets, requiring a minimum number of signatures to approve and execute transactions.

## Overview

The multisig wallet is designed to enhance security for holding and transferring assets like STX and SIP-010 fungible tokens. Instead of a single private key controlling an account, control is distributed among multiple signers. A transaction is only executed if a pre-defined number of signers (the "threshold") approve it.

## Features

- **Shared Asset Management**: Securely manage STX and any SIP-010 fungible tokens.
- **Configurable Security**: The contract is initialized with a list of authorized signers and a minimum signature threshold.
- **On-Chain Transactions**: All proposals, approvals, and executions are recorded on the Stacks blockchain.
- **Two-Step Transaction Process**:
    1. A signer submits a transaction proposal.
    2. Other signers provide their signatures.
    3. Once the threshold is met, any signer can execute the transaction.

## Smart Contracts

### 1. `contracts/multisig.clar`

This is the core logic for the multisig wallet.

- **Initialization**: `(initialize (list principal) uint)`: Sets up the wallet with an initial list of signers and the required signature threshold. Can only be called once by the contract deployer.
- **Transaction Submission**: `(submit-txn uint uint principal (optional principal))`: A signer can propose a new transaction. It supports two types:
    - `type 0`: STX transfer.
    - `type 1`: SIP-010 fungible token transfer.
- **Transaction Execution**:
    - `(execute-stx-transfer-txn uint (list 100 (buff 65)))`: Executes an STX transfer after verifying that the signature threshold has been met.
    - `(execute-token-transfer-txn uint <ft-trait> (list 100 (buff 65)))`: Executes a SIP-010 token transfer after verifying signatures.

### 2. `contracts/mock-token.clar`

This is a simple implementation of the SIP-010 fungible token trait. It is used for development and testing to demonstrate the multisig wallet's ability to manage token assets.
