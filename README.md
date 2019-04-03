# HelloEOS (for MacOS)

> HelloEOS is a modified project building flow of deploying an EOS smart contract to Jungle Testnet base on the official tutorial on https://developers.eos.io/eosio-home/docs. 
>
> I've followed the official tutorial but end up encountering some problems, which is why this project flow is written.

## Detailed Steps
### Step 1: Generate Keys
- Generate the public key and private key pair for your testnet account.
- example website: https://nadejde.github.io/eos-token-sale/ 
- Remember the public key and private key you just generated.
> Since we are generating the keys only for testnet, the security issue is not that serious when you generate the keys on web.  
### Step 2: Download Scatter
- Get the desktop verison: https://get-scatter.com/
- Or, add it to Google: https://chrome.google.com/webstore/detail/scatter/ammjpmhgckkpcamddpolhchgomcojkle?hl=zh-TW
- Create your wallet and remember your password & mnemonic carefully.
- Import the private key in Step 1 to your wallet.

### Step 3: Create Account on Jungle Testnet 
- https://monitor.jungletestnet.io/#home

- Create Account
	- Enter account name and the public key generated in Step 1.
	- You might get error if the account name was already used, just think of another one.

- Faucet
	- Get some free EOS for your testnet account (100 EOS at a time).

- Block Explorer
	- Login by Scatter.
	- View account -> Wallet: You can buy some CPU/Net/RAM with the EOS you just got from the faucet.
	
### Step 4: Set Up Environment
> Version: 
>
> eosio: 1.7.0, eosio.cdt: 1.6.0

- Install eosio
	```
	brew tap eosio/eosio
	brew install eosio
	```
- Install eosio.cdt
	```
	brew tap eosio/eosio.cdt
	brew install eosio.cdt
	```
- Setup development wallet
	- First, go to Jungle Testnet website and click "API endpoints", copy any one of it (ex: http://jungle2.cryptolions.io:80).
	
	- Check your account
		```
		cleos --url http://jungle2.cryptolions.io:80 get account [account_name]
		```
		- Suppose my account name is "ktgincottest", `cleos --url http://jungle2.cryptolions.io:80 get account ktgincottest`.
		- You should see some account info in console.
	
	- Create default wallet
		```
		cleos --url http://jungle2.cryptolions.io:80 wallet create --to-console
		```
		- You should see a password for this wallet. Remember it.
	
	- Open and unlock the wallet
		```
		cleos --url http://jungle2.cryptolions.io:80 wallet open
		cleos --url http://jungle2.cryptolions.io:80 wallet unlock
		cleos --url http://jungle2.cryptolions.io:80 wallet list
		```
		- You should see something like ` Wallets: ["default *"] `
	
	- Import private key
		```
		cleos --url http://jungle2.cryptolions.io:80 wallet import
		```
		- Paste the private key generated in Step 1.
		
### Step 5: Hello World!
- Clone this project or download the hello.cpp in this repository.

- Compile hello.cpp
	```
	eosio-cpp -o hello.wasm hello.cpp --abigen
	```
	- If some warning like "empty ricardian clause file" or "action <hi> does not have a ricardian contract" appears, just ignore it.
	
- Set contract
	```
	cleos --url http://jungle2.cryptolions.io:80 set contract [account_name] . -p [account_name]@active
	```
	- Suppose my account name is "ktgincottest", cleos --url http://jungle2.cryptolions.io:80 set contract ktgincottest . -p ktgincottest@active
	- If you see some error such as "Error 3080001: Account using more than allotted RAM usage", go buy some RAM on the Jungle Testnet for your account.
	
- Block Explorer on Jungle Testnet
	- Login and view your account.
	- You should see a new button "</>Contract" appear beside "Account", and the function "hi" would appear below.
	- You can click "hi" to push a new transaction, then scatter should jump out and ask for permission.
	- Done! You've set up your first EOS smart contract!
