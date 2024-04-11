# Upgrading from a Full-Node to a Validator Node on Cosmos
Upgrading your node from a full-node to a validator node is an essential step for participating in the consensus 
and governance of a Cosmos-based network. This guide provides a concise overview of the upgrade process, 
focusing on crucial commands and flags for an easy-to-follow experience. 

## Prerequisites
Before proceeding with the upgrade, ensure that:

- Your node is fully synchronized with the mainnet.
- You understand the responsibilities and risks of being a validator, including potential slashing for downtime or double signing.

## Upgrade Process
### 1. Create Your Validator
Convert your full-node into a validator node by staking tokens and declaring your node as a validator with the following command:
```
gaiad tx staking create-validator \
  --amount=1000000uatom \
  --pubkey=$(gaiad tendermint show-validator) \
  --moniker="your_moniker" \
  --chain-id="your_chain_id" \
  --from="your_key_name"
```
Important Flags:
- '--amount' : The amount of native tokens to stake. This determines your voting power and the risk level.
- '--pubkey' : Your validator's public key, identifying your node on the network.
- '--moniker' : A human-readable name for your validator. Choose something memorable.
- '--chain-id' : The unique identifier of the blockchain you wish to validate for.
### 2. Edit Validator Description
Update your validator's description to provide more information to potential delegators:
```
gaiad tx staking edit-validator \
  --moniker="new_moniker" \
  --website="https://yourwebsite.com" \
  --identity="16_digit_keybase_id" \
  --details="About your validator" \
  --from="your_key_name" \
  --chain-id="your_chain_id"
```

Important Flags:
- '--website' : URL of your validator's website for more information.
- '--identity' : A Keybase identity for validator identity verification.
- '--details' : A brief description of your validator for potential delegators.
- '--from' : The account name used to sign transactions, indicating the source of the command.
### 3. Confirm Your Validator is Running
Ensure your validator is active and properly configured:
```
gaiad query tendermint-validator-set | grep "$(gaiad tendermint show-address)"
```
This command checks if your validator's address is part of the current validator set.

# Editing Validator's On-Chain Information
Use the following CLI command to edit your validator's information:
```
gaiad tx staking edit-validator \
  --moniker="new_moniker" \
  --website="https://yourwebsite.com" \
  --identity="your_keybase_id" \
  --details="your_validator_details" \
  --from="your_key_name" \
  --chain-id="your_chain_id"
```
Important Flags:
- '--moniker': This is your validator's name on the network. 
Choose a memorable name that represents your validator's identity or mission.

- '--website': Your validator's website URL. It's a resource for potential delegators 
to learn about your team, security measures, and contributions to the ecosystem.

- '--identity': A 16-digit Keybase identity hash obtained upon registering with Keybase.io. 
It links your validator's profile picture from Keybase to enhance recognition and trust.

- '--details': A short description of your validator. Highlight your mission, values, and contributions,
offering insight to both potential and current delegators.
### Additional Considerations
- Updating your validator's information might require a small amount of the network's native tokens to cover transaction fees.
- Make sure your descriptions and URLs are concise and informative, as these are public and contribute to your validator's reputation.
