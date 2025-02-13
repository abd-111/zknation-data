# Airdrop Claim Instructions

This README provides instructions for different types of eligible entities involved in the airdrop. There are four categories of eligibility, each corresponding to specific datasets of addresses and entities.

## Eligibility Categories

1. `eligibility_list.csv` - This includes a list of eligible blockchain addresses, encompassing:

    - Externally Owned Accounts (EOAs)
    - Native ZKsync smart contract wallets
    - ZKsync smart contracts (including Safes and DAOs)
    - Ethereum smart contracts (including Safes and DAOs)

2. `external_project_list.csv` - Contains the names of external projects that have been allocated part of the airdrop.

3. `github_repo_list.csv` - Lists GitHub repositories that are eligible for the airdrop.

4. `zksync_native_project_list.csv` - Features a list of ZKSync native projects that received an allocation.

## Table of Contents

- [Github accounts](#github-accounts)
- [L2 Addresses](#l2-addresses)
- [L1 Smart Contracts Addresses](#l1-smart-contracts-addresses)

## Github accounts

For GitHub repositories eligible for the airdrop as listed in `github_repo_list.csv`, each eligible GitHub account must be associated with a ZKsync or Ethereum address. After association, the address will be added to the final Merkle tree of eligible addresses, which is stored onchain. Users can claim through the official fronted using the provided address or manual instruction from this repo.

### Associating Your GitHub Account

To associate your GitHub account with your ZKsync or Ethereum address, please follow these steps:

1. Visit the Official Frontend:
    - Go to [Claim ZK nation Airdrop](https://claim.zknation.io).

2. Log in with GitHub:
    - Use your GitHub credentials to log into the frontend.

3. Link Your Blockchain Address:
    - Once logged in, follow the prompts to link your ZKsync or Ethereum address to your GitHub account.

### Deadlines for Association

There are two key deadlines for associating your GitHub account:

- First Deadline: June 14th, 15:00:00 CEST. Accounts associated before this date are added to the first Merkle distributor contract onchain, allowing claims to be started as early as June 17th.
- Second Deadline: June 24th 23:59:59 CEST. If your GitHub account completes the association before this date, your address will be added into the second claim period.

**Important**: After the second deadline, unassociated GitHub accounts will NOT be able to claim airdrop tokens, and their allocation may be forfeited.

## L2 Addresses

### Standard EOA Accounts

For standard externally owned accounts (EOAs), please use the official frontend for claiming your airdrop tokens. You can access the claiming interface at:

[Claim ZK nation Airdrop](https://claim.zknation.io)

### L2 Multisig or DAO Contracts

If you are claiming from an L2 multisig or DAO contract address, you need to make L2 transaction following these steps:

#### Contract Call Preparation:

Find the required transaction data in the pregenerated instructions. You can submit `claim` transaction using raw calldata or function parameters.

1. Clone the GitHub Repository and navigate to the `/claim-instructions` directory:
    - Run the following command in the terminal
    ```
    git clone https://github.com/ZKsync-Association/zknation-data.git && cd zknation-data/claim-instructions
    ```
2. Generate Transaction Parameters:
    - Install dependencies and run the script to generate L2 contract claim transaction parameters:
    ```
    yarn && yarn generate-l2-contract-claim-tx <address>
    ```

![alt text](instructions-l2.png)

#### Claiming Process:

1. Use the [block explorer](https://era.zksync.network/address/0x66Fd4FC8FA52c9bec2AbA368047A0b27e24ecfe4#writeContract) frontend or suitable wallet interfaces that support contract interactions.
2. Execute the contract call with the generated calldata.

For example, if you are using Safe mutltisig, you can craft the transaction using the raw calldata in the Transaction Builder:

![alt text](safe.png)

## L1 Smart Contracts Addresses

If you are claiming from an L1 multisig, L1 DAO contract address, or other L1 smart contract address, you need to make an L1 transaction by following these steps:

#### Contract Call Preparation:

To claim tokens for an L1 contract, you need to first generate calldata. Unlike L2 execution, L1 to L2 calldata and the price for the transaction execution depend on network conditions. Therefore, use the provided script to generate the transaction parameters.

1. Clone the GitHub Repository and navigate to the `/claim-instructions` directory:
    - Run the following command in the terminal
    ```
    git clone https://github.com/ZKsync-Association/zknation-data.git cd zknation-data/claim-instructions
    ```
2. Generate Transaction Parameters:
    - Install dependencies and run the script to generate L1 contract claim transaction parameters:
    ```
    yarn && yarn generate-l1-contract-claim-tx <address> [--l1-gas-price] [--l1-json-rpc]
    ```
    - `l1-gas-price` should be not less than the L1 gas price when transaction will be executed.
    - `l1-json-rpc` - optional parameter to specify L1 node RPC.

![alt text](instructions-l1.png)

#### CLI Output Description:

When you run the script, the CLI will output the following data:

- `address`: The address which claims.
- `to`: The address to call on L1.
- `function`: The name of the smart contract function to call.
- `params`: A JSON object detailing the transaction parameters and specifying the function to call.
- `l1_raw_calldata`: The calldata to be sent with the transaction.
- `value`: The amount in wei to send with the transaction.
- `gas_price`: The minimum gas price to send transaction with.

#### Claiming Process:

1. Use the [block explorer](https://etherscan.io/address/0x303a465B659cBB0ab36eE643eA362c509EEb5213#writeProxyContract) frontend or suitable wallet interfaces that support contract interactions.
2. Execute the contract call with the generated calldata.

For example, if you connect your wallet on Etherscan, you can call the contract directly from the UI:

![alt text](etherscan.png)
