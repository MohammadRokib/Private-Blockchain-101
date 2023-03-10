Assalamu Alaikum Wa Rahmatullah

Today, we will see how to make a private Blockchain using geth. Geth is a go implementation of Ethereum. Geth can be downloaded from this link: [GNS3](https://www.gns3.com/software/download/). If you are following this tutorial then I would recommend downloading version 1.10.26. Otherwise some of the commands I am going to use here will not work.

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
This json file defines our genesis block which is the first block of our Blockchain. This part of the **genesis.json** file can be changed.<br>

Here, inside "alloc" ```0x0000000000000000000000000000000000000001``` is an account which will probably work as the coinbase. And ```"balance": "1000000000000000000"``` is the balance of the coinbase. You can change the values inside "alloc" as you like. But don't change the other values.<br><br>

After doing that open terminal and run the following commands:
```
geth --datadir=/home/mohammadrokib/Codes/Private_BlockChain_2 init /home/mohammadrokib/Codes/Private_BlockChain_2/genesis.json
```

With this command I am initializing the blockchain with the genesis file inside a folder which is the datadir. My datadir is /home/mohammadrokib/Codes/Private_BlockChain_2 and I kept the genesis file in the same location. Thus location of the genesis file is the same.<br>
To find the directory just navigate to the folder then open terminal there and run the command **pwd** and it will return the folder you are in.<br><br>

Then run this command:
```
geth --datadir=/home/mohammadrokib/Codes/Private_BlockChain_2 --networkid=54321 --nodiscover console
```

This command will start the blockchain from the datadir and a JavaScript console will comeup. We can interact with the blockchain from the console.
