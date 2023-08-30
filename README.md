# What is this
Draft documenation for sbtc Signer specifically for the Nakamoto [release](https://stacks-network.github.io/sbtc-docs/sbtc-roadmap.html)

The readers of this are assumed to be anyone who is looking to run a sBTC Signer with minimal custom configuration.


## Prerequisites
Rust - [To install](https://www.rust-lang.org/tools/install).

Accesible Stacks node  - A Stacks node running the stackerDB instance which is used for signer communication and transaction monitoring and broadcasting.

Accesible Bitcoin node  - A Bitcoin node used for transaction monitoring and broadcasting.

A Stacks Address - Identify your address as a Signer

## Installing

### Building from Source
If you wish to compile the default binary from source, follow the steps outlined below. Otherwise, download the binary directly (below)

1. First, clone the Stacks sBTC mono repository:  
```console
git clone https://github.com/Trust-Machines/stacks-sbtc.git
```
2. Next, navigate to the stacks-signer-mini directory:  
```console
cd stacks-sbtc/stacks-signer-mini
```
3. Checkout the appropriate release branch you wish to use if you are not using the default main branch
```console
git checkout main
```
4. Compile the signer binary:  
Note the binary path defaults to `target/release/stacks-signer-mini`.
```console
cargo build --release
```

### Downloading the Binary
1. First, download the precompiled default [TODO: signer binary](LINK).

2. Untar the file
```console
tar -xvf signer_binary.tar
```
3.  Check Extracted Files:
After running the untar command, the contents of the tar file should be extracted to the current directory. You should see the signer binary (stacks-signer-mini) and the configuration file (signer.toml) listed among the extracted files.

2. Next, install the signer.
```console
cargo install --path stacks-signer-mini
```

## Configuration

| Key.                   | Required | Description                                                                                                                                                  | 
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `private_key`          | `true`   | Stacks private key of the signer, used for signing sBTC transactions.                                                                                        |
| `stacks_node_rpc_url`  | `true`   | Stacks node RPC URL that points to a node running the stackerDB instance which is used for signer communication and transaction monitoring and broadcasting. |
| `bitcoin_node_rpc_url` | `true`   | Bitcoin node RPC URL used for transaction monitoring and broadcasting.                                                                                       |

