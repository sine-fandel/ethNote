# ethNote
a note web app built on ethereum

## API book

Contract Methods: isExistUsername, createUser, getUserCount, setNote, getNote

GET / static RETURN{front-page}

POST /signup {username: string} RETURN{label: bool, msg: string}

POST /signin {username: string} RETURN{label: bool, msg: string}

GET /getNote/{username} RETURN{label: bool, msg: string, note: string}

POST /updateNote/{username} {note: string} RETURN{label: bool, msg: string}

GET /getUserCount RETURN{userCount: int}


## 2018-12-24

在remix网页上部署合约运行没有问题，但是一到本地部署就出问题。开始我以为是用truffle部署的问题，就改成用remix部署，nodejs调用web3，发现还是不行，然后写了一个非常非常简单的test的读写函数，没有问题；这时知道是代码问题，我就在创建user的函数里一句一句调试，最后发现nodejs的web3脾气是这样的：**不能在一个函数中调用两次数组push，也不能调用两次mapping，也不能在mapping中包含结构体**，最后为了能在node上调用web3合约函数，老子把合约改成了**只有一个username的数组，一个username到单个string的映射作为笔记内容**，把address完全从合约中删掉了，笔记内容也只能一个username一条，一个字符串。

开始的设计本身为了简单就很少逻辑了，结果node的web3又这样，现在的项目简直和一个helloworld一样，但是花的时间都够在普通数据库上写一个大博客了，可能这就是block chain吧。


### 运行

* 私链geth：

```
geth --networkid 999 --datadir "E:\Course\BlockChain\Eth-Private\privateData"  --rpc --rpcaddr 0.0.0.0 --rpcport 10070 --rpcapi "personal,db,eth,net,web3,admin,debug,miner,shh,txpool" --port 10071 --rpccorsdomain "*" --nodiscover console
```
```
personal.unlockAccount(eth.accounts[0], "123456")
```
```
miner.start()
```

* 部署合约：已经部署好了，abi和address已经放到app.js中了，不要再改了。

* 前后端：
```
node app.js
```
