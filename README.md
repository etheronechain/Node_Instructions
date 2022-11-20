# Ether One Node_Instructions

Basic Instructions to start a new node on Ubuntu Distro. Based on your OS and environment, you may need to make changes.

On Ubuntu 18,20,22

## User Creation 
-----------------
Create a user ubuntu and provide sudo permission

Try not to use root to install. Use ubuntu user to continue with steps below.

## Default Ports
--------------
Open ports 30303, 8545 

## Pre-Requisites
-----------------

##Install Go Lang: 
----------------

```bash
cd ..
wget https://storage.googleapis.com/golang/go1.19.linux-amd64.tar.gz
tar -xvf go1.19.linux-amd64.tar.gz
sudo rm -fr /usr/local/go
sudo mv go /usr/local
export GOROOT=/usr/local/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

Installing Ether One Node 
---------------------------
Clone Repo
-----------------
git clone https://github.com/etheronechain/go-ethereum.git
ls -la
cd go-ethereum/
sudo apt-get update && sudo apt-get dist-upgrade -y
sudo apt-get install build-essential make git screen unzip curl nginx pkg-config nmap xterm screen tcl -y
make geth

Genesis Block
--------------

// Download Genesis block and init blockchain

git clone https://github.com/etheronechain/Genesis.git  

// If go-ethereum is in /home/ubuntu/node/go-ethereum/

// run this command

./build/bin/geth init /home/ubuntu/node/go-ethereum/Genesis/genesis.json

Start Geth and Node Sync
----------------- 
// Start geth to sync to nodes/blockchain in the folder /home/ubuntu/node/go-ethereum/

./build/bin/geth --networkid 4949 --port 30303 --http --http.port 8545 --http.addr <Host IP Address> --http.api personal,eth,net --http.corsdomain '*' --allow-insecure-unlock  --syncmode full

// You can connect to geth to check the sync progress and create new coinbase account in another terminal

./build/bin/geth attach /home/ubuntu/.ethereum/geth.ipc

// for example use the commands below 

// use this to connect to seed node in console of geth

admin.addPeer("enode://a6ee2eaca69b93e630e9067b142fc7a803cf6361fd7de03b5071243a69b71b6878a9786b873658eb13345a2e92c62e0ce62e90f8e68bbccd84814fe0b3e90274@165.227.42.184:30303")

eth.syncing : see sync stats. Displays false when sync is complete

eth.syncing.highestBlock - eth.syncing.currentBlock : see how many blocks your node is behind. Displays NaN when current

eth.syncing.knownStates - eth.syncing.pullStates : see how many states your node is behind. Displays NaN when current

web3.net.peerCount : see how may peers you are connected to

// run this command to get you enode. Send us this to whitelist
admin.nodeInfo
