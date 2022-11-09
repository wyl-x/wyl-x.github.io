---
title: web3开发相关
date: 2022/4/21 20:11:39
tags: web3
categories: JavaScript
---

最近做一个web3 的 NFT 项目， 对这方面比较陌生，记录下开发中学到的相关知识

## 区块链
区块链(1.0)是一个基于密码学安全的分布式账本，是一个方便验证，不可篡改的账本。
通常认为与智能合约相结合的区块链为区块链2.0, 如以太坊是典型的区块链2.0

## 智能合约
以太坊与比特币很大的不同是以太坊拥有智能合约的概念。 比特币是数字货币-价值存储。 而以太坊不单单是数字货币，它们是可以区块链上运行代码。

首先要了解的是**智能合约是以太坊网络上的一种特殊帐户**。 我们有用户帐户，还可以拥有智能合约帐户。

<!-- more -->

用户帐户有:

- 地址（有点像我们的银行帐号 - 比特币也有同样的概念）
- 余额（我有多少钱: 以太）


智能合约账户有：
- 地址
- 余额（有多少钱: 以太）
- 状态
- 代码
地址是帐户的唯一标识符，与常规用户帐户一样。

余额也与常规用户帐户相同。 不同的是，智能合约的余额意味着代码可以拥有资金，它可以管理资金。因此如果代码不正确，它可能会错误处理这笔资金。

智能合约帐户的状态是智能合约中声明的所有变量和变量的当前状态。 它的工作方式与大多数编程语言中的类中的变量变量相同。 实际上，最简单方法去理解智能合约可以类比为一个类实例化对象，唯一的区别是这个对象永远存在区块链网络中（除非程序进行自毁）。

智能合约的代码是编译后可以在以太坊客户端和节点可以运行的字节码。 它是在创建智能合约时执行的代码，它包含我们可以调用的函数。 就像面向对象编程语言中的对象一样。


## 前端相关/ DApp
Web3.js 和 ethers.js 都是 JavaScript 库，其作用是使开发者可以与以太坊区块链交互。  

## web3.js
Web3.js 有一个主类，称为 web3。在该类中可以找到该库的大多数功能。组成 web3js 的另外 5 个模块分别是：

1. web3-eth
2. web3-shh
3. web3-bzz
4. web3-net
5. web3-utils


### web3-eth
web3-eth 模块中包含函数，其作用是使 web3.js 的用户可以与以太坊区块链进行交互。具体来说，这些函数能够与智能合约、归外部所有的账户、节点、挖出的区块以及交易进行交互。下面是三个说明示例：

web3.eth.getBalance 的作用是获得指定区块的某个地址的以太坊余额
web3.eth.signTransaction 的作用是对交易签名
web3.eth.sendSignedTransaction 的作用是将签名的交易发送到以太坊区块链。

### web3-shh
web3-shh 模块的作用是使你可以与 Whisper 协议进行交互。Whisper 是一个消息传输协议，其目的是轻松广播消息以及进行低层异步通信。下面显示了两个说明性示例：

web3.shh.post 将 whisper 消息发布到网络
web3.shh.subscribe 创建传入的 whisper 消息订阅


### web3-bzz
web3-bzz 模块的作用是使你可以与 Swarm 交互。Swarm 是一个去中心化存储平台和内容分发服务，它可以用来为去中心化应用存储图片或视频等文件。下面显示了两个说明性示例：

web3.bzz.upload 的作用是使你可以将文件和文件夹上传到 Swarm
Web3.bzz.download 的作用是使你可以从 Swarm 下载文件和文件夹

### web3-net
web3-net 模块的作用是使你可以与以太坊节点的网络属性进行交互。通过 web3-net，你可以采用你需要获得的信息所关联的协议后加 .net（在这里使用 * 指定，表示选择 web.eth.net、web3.shh.net 或 web3.bzz.net）来查找该节点的相关信息。下面显示了两个说明性示例：

web3.*.net.getID 返回网络 ID
web3.*.net.getPeerCount 返回连接到节点的对等点数


### web3-utils
web3-utils 模块为你提供实用程序函数，这些函数可在以太坊去中心化应用以及其他 web3.js 模块中使用。实用程序函数可以重复使用，使代码编写更轻松，在 JavaScript 和其他编程语言中很常见。Web3-utils 包含实用程序函数，这些函数用于转换数字、验证值是否满足特定条件以及搜索数据集。下面显示了三个说明性示例：

web3.utils.toWei 将以太转换为 Wei
web3.utils.hexToNumberString 将十六进制值转换为字符串
web3.utils.isAddress，校验特定字符串是否为有效的以太坊地址。


## ethers.js
与 web3.js 相似，ethers.js 有四个模块，构成应用程序编程界面 (API)。

1. Ethers.provider
2. Ethers.contract
3. Ethers.utils
4. Ethers.wallets


### ethers.provider
Ethers.provider 的作用是封装与以太坊区块链的连接。它可以用于签发查询和发送已签名的交易，这将改变区块链的状态。下面显示了三个说明性示例：

ethers.providers.InfuraProvider 的作用是使你可以与 Infura 托管的以太坊节点网络建立连接
ethers.provider.getBalance 将为你获取区块链中某个地址或区块的以太坊余额
ethers.provider.resolve 将解析传递到以太坊地址的以太坊名称服务 (ENS) 名称

### ethers.contract
Ethers.contract 的作用是部署智能合约并与它交互。具体来说，该模块中的函数用于侦听从智能合约发射的事件、调用智能合约提供的函数、获取有关智能合约的信息，以及部署智能合约。下面显示了两个说明性示例：

ethers.ContractFactory.fromSolidity 从 Solidity 编译器的编译器输出或从 Truffle 生成的 JSON 文件创建一个用于部署智能合约的“工厂”。ethers.Contract 使你可以与已部署的智能合约进行交互。


### ethers.utils
Ethers.utils 提供用于格式化数据和处理用户输入的实用程序函数。Ethers.utils 的作用方式与 web3-utils 相似，能够简化去中心化应用的构建流程。下面提供了三个示例：

ethers.utils.getContractAddress 从用于部署智能合约的交易中提取智能合约地址
ethers.utils.computeAddress 通过传递与地址相关的公钥或私钥的函数来计算地址 ethers.utils.formatEther 将所传递的 Wei 金额转换为 Ether 十进制字符串格式

### ethers.wallet
Ethers.wallet 提供的功能与我们目前讨论过的其他模块截然不同。Ethers.wallet 的作用是使你可以与现有钱包（以太坊地址）建立连接、创建新钱包以及对交易签名。下面提供了三个示例：

ethers.wallet.createRandom 将创建随机新账户。
ethers.wallet.sign 将对交易签名并将已签名的交易返回为十六进制字符串的形式（通过“承诺”— 如果你刚接触 JavaScript，我们建议你阅读有关承诺的更多内容，它们的作用是在未来某个时间点对它们进行计算时可以返回数据）。
ethers.wallet.getBalance 将为我们提供钱包地址的以太坊余额。
Web3.js 在 web3.eth 模块中有一个类似的包，称为 web3.eth.accounts。但是，在该包的文档中有如下说明：“该包未经审核，可能不安全。在用于生产环境之前，请注意妥善清除内存，安全存储私钥，并适当测试交易接收和发送功能！”

## 参考文档
- [web3.js 文档](https://learnblockchain.cn/docs/web3.js/)
- [ethers.js 文档](https://learnblockchain.cn/docs/ethers.js/)
- [Hardhat 开发环境](https://learnblockchain.cn/docs/hardhat/getting-started/#%E6%A6%82%E8%BF%B0)
- [Solidity 文档](https://learnblockchain.cn/docs/solidity/)

