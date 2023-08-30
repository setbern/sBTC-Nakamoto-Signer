# What is this
Draft documentation for sBTC Signer specifically for the Nakamoto [release](https://stacks-network.github.io/sbtc-docs/sbtc-roadmap.html)

The readers of this are assumed to be anyone who is looking to run a sBTC Signer with minimal custom configuration.


## Prerequisites
Rust - [To install](https://www.rust-lang.org/tools/install).

Accessible Stacks node  - A Stacks node running the stackerDB instance which is used for signer communication and transaction monitoring and broadcasting.

Accessible Bitcoin node  - A Bitcoin node used for transaction monitoring and broadcasting.

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
The signer takes a TOML config file with the following expected properties

| Key.                 	| Required | Description                                                                                                                                              	     |
| ------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `private_key`        	| `true`   | Stacks private key of the signer, used for signing sBTC transactions.                                                                                    	     |
| `stacks_node_rpc_url`	| `true`   | Stacks node RPC URL that points to a node running the stackerDB instance which is used for signer communication and transaction monitoring and broadcasting.    |
| `bitcoin_node_rpc_url`   | `true`   | Bitcoin node RPC URL used for transaction monitoring and broadcasting.                                                                                       |
| `network`            	| `false`  | One of `['Mainnet', 'Testnet','Devnet' ]`. Defaults to `Testnet`                                                                                         	|
| `signer_api_server_url`  | `false`  | Url at which to host the signer api server for transaction monitoring. Defaults to "http://localhost:3000".                                              	|
| `auto_deny_block`    	| `false`  | Number of blocks before signing deadline to auto deny a transaction waiting for manual review. Defaults to 10.                                           	|
| `auto_approve_max_amount`| `false`  | Maximum (btc?) amount of a transactions that will be auto approved                                                                                       	|
| `auto_deny_addresses_btc`| `false`  | List of bitcoin addresses that should trigger an auto deny                                                                                               	|
| `auto_deny_addresses_stx`| `false`  | list of stx addresses that should trigger an auto approve                                                                                                	|

### Example TOML file
```toml
# config.toml

# Mandatory fields

# Note: Replace 'MY_PRIVATE_KEY' with the actual private key value
signer_private_key = "MY_PRIVATE_KEY"
stacks_node_rpc_url = "http://localhost:9776"
bitcoin_node_rpc_url = "http://localhost:9777"

# Optional fields

auto_approve_max_amount = 500000
network = "Devnet"
# Note: replace "BTC_ADDRESS_*" with actual BTC addresses you wish to deny
auto_deny_addresses_btc = [
	"BTC_ADDRESS_1",
	"BTC_ADDRESS_2"
]
# Note: replace "STX_ADDRESS" with an actual STX address you wish to deny
auto_deny_addresses_stx = [
	"STX_ADDRESS"
]
```


 ## Running the binary
 After installing and creating a config file to run the binary
 
```console
stacks-signer-mini --config conf/signer.toml
```

 ## Monitor Transactions
 The signer binary operates a web server/client and it can be navigated to by default at http://localhost:3000/ (unless otherwise specified from config). Here you can see pending transactions and manually review and sign transactions that cannot be automatically signed on your behalf. Note that manual review is triggered based on the options you have set in your configuration file.


