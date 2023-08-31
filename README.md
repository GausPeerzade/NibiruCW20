# Smart Contract Deployment Guide

This guide outlines the steps to deploy the CW20-based smart contract using the Nibid blockchain. The contract allows for the creation and management of tokens following the CW20 standard.

## Prerequisites

Before you begin, make sure you have the following:

Nibid blockchain environment set up
Nibid CLI installed
Access to a Nibid account with sufficient funds

## Deployment Steps

Set the necessary variables in your terminal:

export KEY_NAME=<your_key_name>

Store the CW20 base contract using the following command:
nibid tx wasm store cw20_base.wasm --from=$KEY_NAME --gas 8000000 --fees 200000unibi
Save the generated transaction hash and code ID for reference.

Check the raw log of the transaction using the transaction hash:
nibid q tx <transaction_hash> | grep raw_log

Retrieve information about the smart contract code using the code ID:
nibid query wasm code-info <code_id>

Prepare the initialization parameters for the smart contract instance. Modify the init variable according to your requirements:
init='{"name":"UTSA_test","symbol":"UTSA","decimals":6,"initial_balances":[{"address":"nibi1m2mm7kzvw6m3464h94ryqg8xvr6tyeyywa9c6n","amount":"13000000"}],"mint":{"minter":"nibi1m2mm7kzvw6m3464h94ryqg8xvr6tyeyywa9c6n"},"marketing":{}}'

Instantiate the smart contract using the following command:
nibid tx wasm instantiate <code_id> $init --label "UTSA cw20_base" --no-admin --from=$KEY_NAME --gas 8000000 --fees 200000unibi -y

Congratulations! You've successfully deployed the CW20-based smart contract on the Nibid blockchain.

Please make sure to replace <your_key_name>, <transaction_hash>, <code_id>, and adjust the init variable as needed for your specific use case.
