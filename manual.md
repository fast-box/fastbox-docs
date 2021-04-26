# Manual of FastBox TestNet

## 1. Environment configuration
### 1.1 Update apt get source
```
$ sudo apt-get update
```
### 1.2 Install Git
```
$ sudo apt-get install git
```
### 1.3 Prepare go installation package
```
$ wget -c https://storage.googleapis.com/golang/go1.12.1.linux-amd64.tar.gz
```
### 1.4 Select the installation path
```
$ tar -C /usr/local -xzf go1.12.1.linux-amd64.tar.gz
```
### 1.5 Add path environment variable
```
$ vim /etc/profile
```

### 1.6 Add the following
```
export GOPATH=/home/gopath
export GOROOT=/usr/local/go
PATH=$GOROOT/bin:$GOPATH/bin:$PATH
```
### 1.7 Make profile file effective
```
$ source /etc/profile
```
### 1.8 Check go environment
```
$ go env
```
### 1.9 Check go version
```
$ go version
```

## 2. Fastbox program download
### 2.1 Determine program execution path
Enter `sudo mkdir /home/fbox-bin` to create the program execution path, where `/home/fbox-bin` can be changed to the specified path.
```
$ sudo mkdir /home/fbox-bin
```
### 2.2 Select download path
Input `cd /home/`, where `/home/` can be changed to the specified path;
```
$ cd /home/
```
### 2.3 Download fastbox source code
Enter `git clone https://github.com/fast-box/fastbox.git`.

When the progress becomes 100%, the "checking availability Done", the download is successful,
continue to the next step;
```
$ git clone https://github.com/fast-box/fastbox.git
```
### 2.4 Compile fastbox
Enter `cd fastbox/`, continue to input `make all` to compile fastbox;
```
$ cd fastbox/
$ make all
```

### 2.5 Copy program to execution path
input `cp build/bin/* /home/fbox-bin/`
```
$ cp build/bin/* /home/fbox-bin/
```

According to the above example, copy the program to other nodes /home/fbox-bin/ in turn.

### 2.6 Configure genesis block

- Enter /home/fbox-bin 
- Input vim fbox.json 
- Enter the following in the open JSON file and save to exit

```json
{
"config": {
"chainId": 1000,
"prometheus": {
"period": 10,
"epoch": 200
}
},
"timestamp": "0x5b7eba85",
"extraData":
"0x687062000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
00000000000000000000000000000000000000000000000000000000000000000000",
"difficulty": "0x1",
"coinbase": "0x0000000000000000000000000000000000000000",
"number": "0x0",
"parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
```
## 3. Connect to test network
### 3.1 initialize the node
```
$ ./fbox --datadir node/data init fbox.json
```
### 3.2 create a new account
```
$ ./fbox --datadir node/data account new
04cbf60fdcc485a76b0b8a389da7bd87da180edd
```
### 3.3 background start node
Input command background start node
```
$ nohup ./fbox --datadir node/data --unlock 0x04cbf60fdcc485a76b0b8a389da7bd87da180edd --password[password] --networkid 1000 --port
27000 --rpcaddr 0.0.0.0 --rpcport 8600 --verbosity 3 --rpc --rpcapi shx,miner,web3,admin,txpool,debug,personal,net &
```
### 3.4 start mining
Input `./fbox attach http://127.0.0.1:8600` open the console and then enter `miner.start()` start mining.
```
$ ./fbox attach http://127.0.0.1:8600
miner.start()
```
