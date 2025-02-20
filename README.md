# Solana

## Quick Installation

```
curl \
  --proto '=https' \
  --tlsv1.2 \
  -sSfL ]
  https://raw.githubusercontent.com/solana-developers/solana-install/main/install.sh \
  | bash
```

Returns:

```
Installed Versions:
Rust: rustc 1.84.1 (e71f9a9a9 2025-01-27)
Solana CLI: solana-cli 2.1.14 (src:3ad46824; feat:3271415109, client:Agave)
Anchor CLI: anchor-cli 0.30.1
Node.js: v23.8.0
Yarn: 0.32+git

Installation complete. Please restart your terminal to apply all changes.
```

### Update PATH

```
export PATH="/home/<USER>/.local/share/solana/install/active_release/bin:$PATH"
```

### Solana CLI

```
solana --version
```

Returns:

```
solana-cli 2.1.14 (src:3ad46824; feat:3271415109, client:Agave)
```

#### Create Wallet

```
solana-keygen new
```

Returns:

```
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none): 

Wrote new keypair to /home/<USER>/.config/solana/id.json
===========================================================================
pubkey: H9XUYsgDG4Fr83roHNnM3XGdNJVyGtdCQv7frLCzmzYD
===========================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
volcano account oven toast truth canyon fitness crowd clap claim bind march
===========================================================================
```

**Warning: Never share your Secret/Private Key like that. This is just an
 example for you to see.**

If a wallet already exists, you can always force the creation of a new wallet
 with the `--force` option. **Warning: Be very careful with that as you will
 override the existing keys file.**

#### Show Public Key (Account Address)

```
solana-keygen pubkey
```

Returns:

```
H9XUYsgDG4Fr83roHNnM3XGdNJVyGtdCQv7frLCzmzYD
```

#### Show Balance

##### Mainnet:

```
solana balance
```

##### Devnet

```
solana balance --url devnet
```

#### Airdrop 2 Devnet SOL (Lamports)

```
solana airdrop 2 H9XUYsgDG4Fr83roHNnM3XGdNJVyGtdCQv7frLCzmzYD --url devnet
```

Returns:

```
Requesting airdrop of 2 SOL

Signature: 4jHrrksJsrwZvoTvbPKbfNvpZnLgAStnnLRP8RvVTVykg9jcJSwVy9QtitSAgRvGntB3wfXPkpcXzWZ4BvbYJn81

2 SOL
```

### Solana Explorer

The Solana Explorer (Beta) is available at: https://explorer.solana.com

### Solana Program Library (SPL)

```
cargo install spl-token-cli
```

#### Create Token

```
spl-token create-token --url devnet
```

Returns:

```
Creating token 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F under program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA

Address:  5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F
Decimals:  9

Signature: hWuei7La2gz7meDsdjL8jKd1ta3cw9iFuicwDwrpPacT1ZrvJeyqJvNcvETxgfX6QfgpccpUWg34BBXukSVprH8
```

`5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F` is referred to as the "Token
 Address".

#### Create Account for Token

```
spl-token create-account 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F --url devnet
```

Returns:

```
Creating account 2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj

Signature: 5ktbEL5kcRLHyzRfdbjaUS6U4KztPPRMcVVtTDw32wfYWpUJh7kvmdZMutYQd5yLWKnyvcNf6gsZ3zAvXneXUb8p
```

`2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj` is referred to as the "Account
 Token Address".

#### Get Token Balance

```
spl-token balance 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F --url devnet
```

Returns:

```
0
```

#### Mint Token (1,000)

```
spl-token mint 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F 1000 --url devnet
```

Returns:

```
J7HC3oh3MC9F 1000 --url devnet
Minting 1000 tokens
  Token: 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F
  Recipient: 2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj

Signature: 3xxMnsKs4UXweXe9DKnzFx6nUhLBumdGvPHUW8VFFsXraFJKVeT4ahAhe2zrJuG4eHVb4a5aePsxES1wn66R9btN
```

#### Check current Circulating Supply

```
spl-token supply 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F --url devnet
```

Returns:

```
1000
```

#### Disable (revoke) Minting Authority

In order to create a limited supply of your token, you can disable or revoke the
 authority of minting new token that only you have.

```
spl-token authorize 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F mint --disable --url devnet
```

Returns:

```
Updating 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F
  Current mint: H9XUYsgDG4Fr83roHNnM3XGdNJVyGtdCQv7frLCzmzYD
  New mint: disabled

Signature: 55pahufVq9v8KN5eemjNfHzvGbukVUUTTPgfkmBLT8pB99q7oRYK6n3K8zoV3NkngPxa8X7GPGLJi5riR5BFUT5e
```

Attempting to mint additional token using:

```
spl-token mint 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F 1000 --url devnet
```

Will result in the following error:

```
Minting 1000 tokens
  Token: 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F
  Recipient: 2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj
Error: Client(Error { request: Some(SendTransaction), kind: RpcError(RpcResponseError { code: -32002, message: "Transaction simulation failed: Error processing Instruction 0: custom program error: 0x5", data: SendTransactionPreflightFailure(RpcSimulateTransactionResult { err: Some(InstructionError(0, Custom(5))), logs: Some(["Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]", "Program log: Instruction: MintToChecked", "Program log: Error: the total supply of this token is fixed", "Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4147 of 4147 compute units", "Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA failed: custom program error: 0x5"]), accounts: None, units_consumed: Some(4147), return_data: None, inner_instructions: None, replacement_blockhash: None }) }) })
```

#### Burn own Token

You can only burn token from your own token account, that is the reason why
 here, we are going to use your token account address:

```
spl-token burn 2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj 100 --url devnet
```

Returns:

```
Burn 100 tokens
  Source: 2eNkoxGS5gyhMBV4owYa4E7htZDg2he9NpwpQzN4jedj

Signature: 5EbU9C3ERk1xxPrdtBhZUVYLrbWAioppcqcdguFZY6V3mCa7yKAfRF6qLWsVW6UcCucPGe9GY5SMX8JZwZAQodSF
```

Checking the account token balance again:

```
spl-token balance 5LSuWnxMAAgZuefifAoVoJhxPobXtb2oJ7HC3oh3MC9F --url devnet
```

Returns:

```
900
```

