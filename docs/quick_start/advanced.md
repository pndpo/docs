# Advanced: Build & run a local DevNet node

"DevNet" is a single-node "blockchain" that runs WebAssembly and state transition without actually running the full blockchain/consensus functionality. Essentially, you can interact with it as if it was a multi-node blockchain for the purposes of writing and testing code.

You can run your own DevNet locally by installing and running a node, which will produce blocks. The core NEAR node client is written using the [Rust language](https://www.rust-lang.org/), which uses [Cargo](https://github.com/rust-lang/cargo) to manage packages \(similar to NPM\).

## 1. Setup Rust & dependencies

The most up-to-date procedure for installing and running a node is provided in the [README for the nearcore library on Github](https://github.com/nearprotocol/nearcore).

Follow the steps in that README to get Rust, Cargo and the nearcore library set up.

## 2. Run the node

Once everything is installed, you should be able to run DevNet with:

```bash
cargo run --package=devnet
```

## 3. Deploy your app to DevNet

After you have an app locally developed, you can deploy it to the local DevNet.

Download near cli tools

```text
npm install -g near-shell
```

Navigate to your source directory in command line, and do the following:

1. Create an account for your contract

```bash
near create_account --account_id <yourcontractname>
```

1. Build your contract

```bash
near build
```

1. Deploy your contract to DevNet

```bash
near deploy --contract_name <yourcontractname>
```

For help using cli tools, you can use `near help`.

## 4 \(Optional\). Play with your node!

Execute the following in the `nearcore` folder to run some Python scripts which will help you test that your DevNet is working properly:

```bash
# Install pynear
cd pynear
# sudo may be required if you are not testing with a python virtual environment
python setup.py develop

# See usage of rpc helper script
pynear --help

# Get usage of sub command
pynear send_money --help

# Send money
pynear send_money -r bob.near -a 1

# Create a new account for the contract
pynear create_account test_contract 1

# Deploy code for the smart contract account
pynear deploy test_contract tests/hello.wasm

# Call method 'setValue' for contract 'test_contract' and pass arguments
pynear schedule_function_call test_contract setValue --args '{"value":"testtest"}'

# Call view function 'getValue' for contract 'test_contract'
pynear call_view_function test_contract getValue

# Call view function 'benchmark_sum_n' for contract 'test_contract' and pass n=500000
pynear call_view_function test_contract benchmark_sum_n --args='{"n":500000}'

# View state for Bob's account
pynear view_account -a bob.near

# Create an account
pynear create_account cindy 1

# View full state db of the contract
pynear view_state test_contract
```

