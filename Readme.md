Assalamu Alaikum Wa Rahmatullah

Today, we will see how to make a private Blockchain using geth. Geth is a go implementation of Ethereum. Geth can be downloaded from this link: [GETH](https://www.gns3.com/software/download/). If you are following this tutorial then I would recommend downloading version 1.10.26. Otherwise some of the commands I am going to use here will not work.

To download version 1.10.26 first go to the download page then go down and keep clicking **Show Older Releases** under stable version list untill you find version 1.10.26. You can find 32-bit, 64-bit, ARMv5, ARMv6, ARM64, ARMv7 versions. Download the one which will be supported in your system. In my case it is 64-bit. A file named **geth-linux-amd64-1.10.26-e5eb32ac.tar.gz** will be downloaded.

After downloading

### For Linux
Open terminal by clicking ```ctrl+alt+T``` then navigate to the folder where the file is downloaded. Then run the following commands.

to unzip the file run this command:
```
sudo tar -xvf geth-linux-amd64-1.10.26-e5eb32ac.tar.gz
```

<br>Navigate to the extracted folder:
```
cd geth-linux-amd64-1.10.26-e5eb32ac
```

<br>Make the geth file executable:
```
sudo chmod +x geth
```

<br>Copy the geth file to /usr/local/bin directory
```
sudo cp geth /usr/local/bin
```

<br>to check the geth version:
```
geth version // to check the geth version
```
<br>If the installation is successful it will show<br>
```
Geth
Version: 1.10.26-stable
Git Commit: e5eb32acee19cc9fca6a03b10283b7484246b15a
Git Commit Date: 20221103
Architecture: amd64
Go Version: go1.18.5
Operating System: linux
GOPATH=
GOROOT=go
```
<br><br>

After finishing the installation create a folder anywhere in your machine then create a json file named **genesis.json** inside that folder. Put the following in the json file:
```
{
    "config": {
        "chainId": 257,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0
    },
    "nonce": "0x0000000000000042",
    "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x00",
    "gasLimit": "0x8000000",
    "difficulty": "0x400",
    "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "alloc": {
        "0x0000000000000000000000000000000000000001": {
            "balance": "1000000000000000000"
        }
    }
}
```

<br>
This json file defines our genesis block which is the first block of our Blockchain. The part inside **alloc** of the **genesis.json** file can be changed.<br>

Here, ```0x0000000000000000000000000000000000000001``` is an account which will probably work as the coinbase. And ```"balance": "1000000000000000000"``` is the balance of the coinbase. You can change the values inside "alloc" as you like. But don't change the other values.<br><br>

After doing that open terminal and run the following commands:
```
geth --datadir=/home/mohammadrokib/Codes/Private_BlockChain_2 init /home/mohammadrokib/Codes/Private_BlockChain_2/genesis.json
```

With this command I am initializing the blockchain inside datadir (a folder) with **genesis.json** as the genesis/first block. For me the directory of datadir (the folder) is ```/home/mohammadrokib/Codes/Private_BlockChain_2``` and I kept the genesis file in the same location. so the command means:
```
geth --datadir="your_data_directory" init genesis_file_location/genesis.json
```
<br>

To find the directory of any folder just navigate to the folder then open terminal there by ```right click``` and then ```Open in terminal``` then run the command ```pwd``` and it will return the directory of the folder you are in.<br><br>

Then run this command:
```
geth --datadir=/home/mohammadrokib/Codes/Private_BlockChain_2 --networkid=54321 --nodiscover console
```

Here,
```--networkid=54321``` is the network identifier for the private Ethereum network. This is a unique integer value which uniquely indicates to a specific network and avoids any conflict or confusion between two networks.
<br>

```--nodiscover``` this flag disables the peer discovery mechanisism in Geth. When geth is started with this flag, it will not try to discover other nodes on the network automatically.<br>

```console``` this flag starts the Geth console, which is an interactive command-line interface that allows to interact with the private Ethereum node that is created here.<br><br>


If all the above is done correctly then the terminal can be seen like this:
![Screenshot from 2023-03-10 08-41-01](https://user-images.githubusercontent.com/60141836/224209733-63a5467b-d096-4235-8977-0be89b3e545f.png)
<br>

Now, I can interact with the Blockchain that I just created. First I will create an account. To do that type the command: ```personal.newAccount("password")``` give any password you like in the place of password. The ouput will be:
```
INFO [03-10|08:59:40.112] Your new key was generated               address=0xe4E557bC95aD7Bc81C458746a67E019125C5AFb0
WARN [03-10|08:59:40.113] Please backup your key file!             path=/home/mohammadrokib/Codes/Private_Blockchain_2/keystore/UTC--2023-03-10T02-59-34.369104495Z--e4e557bc95ad7bc81c458746a67e019125c5afb0
WARN [03-10|08:59:40.113] Please remember your password! 
"0xe4e557bc95ad7bc81c458746a67e019125c5afb0"
```

Here ```0xe4e557bc95ad7bc81c458746a67e019125c5afb0``` is the public key of the account. And path of the key is given in the second line.<br><br>

The existence of the accounts can be verified by the command ```eth.accounts``` the public keys of the created accounts can be seen in the output.
```
["0xe4e557bc95ad7bc81c458746a67e019125c5afb0", "0xf3a082396bec4243f6cb8bac5c3ffedaf7466c04"]
```
I have created another account, that's why there are two accounts.<br><br>

Let's check the balance of the first account. To do that run this command with the public key of the account
```
eth.getBalance("0xe4e557bc95ad7bc81c458746a67e019125c5afb0")
```
It shows 0. Because the account is created just now so there is no balance. So how do we get some money? We will have to mine from that account to get money. And to mine the account have to be unlocked first.<br><br>


To unlock the first account type the command
```
personal.unlockAccount("0xe4e557bc95ad7bc81c458746a67e019125c5afb0", "password", 0)
```
Here,<br>
```0xe4e557bc95ad7bc81c458746a67e019125c5afb0``` is the public key of the first account.<br>
```password``` is the password of the first account assigned by me.<br>
```0``` idicates the number of seconds the account will remain unlocked. For zero its infinite.
<br><br>

Now, to start mining type the command
```
miner.start()
```
It will start the mining process from the first account since it is the only unlocked account. After mining for a bit type the below command to stop mining
```
miner.stop()
```

Now, lets check the balance of the first account with this command
```
eth.getBalance("0xe4e557bc95ad7bc81c458746a67e019125c5afb0")
```

It shows ```430000000000000000000``` for me. This is in **Wei**. It might show something else for you. It will depend on how long you have mined for. Ethereum has 3 units for their currency. Ether, Gwei and Wei.
```
1 Ether = 1000000000 Gwei = 1000000000000000000 Wei
1 Gwei = 1000000000 Wei
```
<br>

Now, what should I do if I want to mine with the second account. If there is only one account or if just the first account is being used for mining then the above mentioned process will do the job.<br>

But if I want to switch between accounts for mining first the account I want to mine from have to be unlocked with the ```personal.unlockAccount("public_key_of_the_account")``` command. Then to change the mining account type this command with the public key of the desired account
```
miner.setEtherbase("0xf3a082396bec4243f6cb8bac5c3ffedaf7466c04")
```