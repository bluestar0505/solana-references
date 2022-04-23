
# 1. Solana CLI
For instance, we can check the current network (and other) configuration with this command:
```
solana config get

# output
Config File: /Users/user/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: /Users/user/.config/solana/id.json
Commitment: confirmed
```

We can change the network like so:
```
# set to localhost
solana config set --url localhost

# set to devnet
solana config set --url devnet
//or
solana config set --url https://api.devnet.solana.com
```

We can also use the CLI to see our current local wallet address:
```
solana address
```

And then get the full details about an account:
```
solana account <address from above>
```

Start the local network. This is going to be a local Solana node that we can deploy to for testing:
```
solana-test-validator
```

Once the local network is running, you can airdrop tokens to your account.<br>
With the network running, open a separate window and run the following command:
```
solana airdrop 100
```

You can the check the balance of your wallet:
```
solana balance

# or

solana balance <address>
```

#2. Building Anchor app


## Anchor manual
① Document<br>
https://docs.rs/anchor-lang/0.16.1/anchor_lang/#modules

② anchor tutorial source explain<br>
https://project-serum.github.io/anchor/getting-started/introduction.html

③ TweetAccount<br>
https://lorisleiva.com/create-a-solana-dapp-from-scratch/structuring-our-tweet-account


## 2-1. Creating Anchor App
[Anchor Install](https://project-serum.github.io/anchor/getting-started/installation.html#install-rust)

Create new anchor project and change into the new directory:
```
anchor init solana_app --javascript

cd solana_app
```

To compile this program, we can run the Anchor build command:
```
anchor build
```

Fixing errors of anchor version 
 ```
//1. maybe Rust can fix itself:
rustup update

//2. explicitly add a toolchain: 
 rustup toolchain install stable

//3. reinstall rustup:
rustup self uninstall
// and then go back through the instructions at https://www.rust-lang.org/tools/install
``` 

Change Node Version
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

nvm install <version>       Download and install a <version>
nvm use <version>           Modify PATH to use <version>
nvm ls                      List versions (installed versions are blue)


nvm alias default 8.1.0     Set default node version on a shell
```

We can now deploy the program. Be sure that solana-test-validator is running:
```
anchor deploy

anchor deploy --provider.cluster devnet
```

##2-2 Creating React App

In the root of the Anchor project, create a new react app to overwrite the existing app directory:
```
npx create-react-app app
```
Next, install the dependencies we'll need for Anchor and Solana Web3:

```
cd app

npm install @project-serum/anchor @solana/web3.js
```

We'll also be using Solana Wallet Adapter to handle connecting the user's Solana wallet. Let's install those dependencies as well:
```
npm install @solana/wallet-adapter-react \
@solana/wallet-adapter-react-ui @solana/wallet-adapter-wallets \
@solana/wallet-adapter-base
```
<br>
Before we can interact with a program on the <strong>localhost</strong> network, we must switch our Phantom wallet to the proper network.
<br>
<br>
Next, open your terminal and run this command (be sure solana-test-validator is running):

```
solana airdrop 10 <address>
```

Change into the app directory and run the following command:
```
npm start
```