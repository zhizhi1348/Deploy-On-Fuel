# Deploy Contract On Fuel
![Just A pic](https://github.com/zhizhi1348/Deploy-On-Fuel/blob/main/Fuel_Logo_White_RGB.png)
## Install Dependecies
```ruby
sudo apt-get update && apt-get upgrade -y
sudo apt-get install git-all -y
sudo apt-get install curl screen -y
```

## Install Rust

```ruby
curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh
source "$HOME/.cargo/env"
rustup install stable
rustup update stable
rustup default stable
```

## Install Fuel ToolChain
```ruby
# Install Fuel
curl https://install.fuel.network | sh
# Press y then Enter

source /root/.bashrc

# Set fuelup testnet
fuelup toolchain install latest
fuelup self update
fuelup update
fuelup default latest
fuelup default testnet

# Check version
fuelup --version
```
## Create project
```ruby
# Create project
mkdir fuel-project
cd fuel-project
forc new counter-contract

# Edit Contract
nano counter-contract/src/main.sw

# Delete everything and Paste this code
contract;
 
storage {
    counter: u64 = 0,
}
 
abi Counter {
    #[storage(read, write)]
    fn increment();
 
    #[storage(read)]
    fn count() -> u64;
}
 
impl Counter for Contract {
    #[storage(read)]
    fn count() -> u64 {
        storage.counter.read()
    }
 
    #[storage(read, write)]
    fn increment() {
        let incremented = storage.counter.read() + 1;
        storage.counter.write(incremented);
    }
}

# Build Contract
cd counter-contract
forc build
```
## Deploy Contract
**First Download Fuel Walet extension from [Here](https://wallet.fuel.network/docs/install/)**

**Second get faucet from [Here](https://faucet-testnet.fuel.network/)**
```ruby
# Import seed phrase and create password
forc wallet import

# Create account
forc wallet account new

# Check your address
forc wallet accounts

# Deploy Contract , Enter password , Enter 0 , Enter y
forc deploy --testnet

# You get a Contract ID in your Terminal like this, Save it!
Contract counter-contract Deployed!

Network: https://testnet.fuel.network
Contract ID: 0x8342d413de2a678245d9ee39f020795800c7e6a4ac5ff7daae275f533dc05e08
Deployed in block 0x4ea52b6652836c499e44b7e42f7c22d1ed1f03cf90a1d94cd0113b9023dfa636
```

# Now you deployed your first contract successfuly⛽ Tweet @fuel_network letting them to know you just deployed a smart contract on the Fuel network
