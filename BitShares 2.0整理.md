# BitShares 2.0

>BitShares发布了全新的金融智能合约平台——BitShares 2.0。该平台允许任何资产在平台内进行
交易。BitShares 2.0实现了三个特性：
>
 - 市场锚锭资产 MPA
 - 用户发行资产 UIA
 - 去中心化的交易所 DEX
 - 动态用户权限系统


## 市场锚锭资产 MPA

- 加密货币的价格不稳定，所以难以成为交易媒介
- MPA让发行的加密货币价值稳定
- MPA也称为智能币(SmartCoins)，通过差价合约(CFD)的方式产生
- MPA合约的空头是抵押BTS，卖出MPA(比如BitUSD, BitCNY等)的一方
- MPA合约的多头是卖出BTS，买入MAP(比如BitUSD, BitCNY等)的一方
- MPA产生需要抵押三倍的资产，抵押物为BTS，空头抵押2倍BTS+多头卖出的1倍，抵押被系统冻结
- MPA发行价格需要101位证人喂价——根据多个不同的外盘价格，取中位数的方式
- 对于BitUSD来说，喂价的价格101个证人们根据外盘市场BTS/USD价格，给出BTS/BitUSD的价格
- MPA喂价是持续性的，最少每小时一次，这样始终锚锭外盘市场价格，目的是让MPA价格稳定
- 这样任何时候，空头都可以根据喂价卖空MPA，也可以买入MPA平仓
- 空头平仓时销毁相应的MPA，赎回BTS
- 用户可以创造他们自己的智能币

> 问题：证人是否会串通操纵喂价？==> 证人是否可信? ==> DPOS是否公平？

## 用户发行资产 UIA
- UIA是指注册在BitShares平台上的自定义的代币，可以持有或者交易
- 发行时设定规范：比如白名单用户才能持有和交易，手续费

支持如下资产：
- [存款收据 Deposit Receipts](#存款收据)
  - [1. 了解你的客户 Know Your Customer KYC](#了解你的客户)
  - [2. 资产绑定 Asset Seizing](#资产绑定)
  - [3. 市场约束 Market Restriction](#市场约束)
  - [4. 交易约束 Transfer Restrictions](#交易约束)
- [公司股份 Company Shares](#公司股份)
- [活动门票 Event Tickets](#活动门票)
- [奖励积分 Rewards Points](#奖励积分)
- [个人或公司债务 Individual or Corporate Debt](#个人或公司债务)
- [众筹 Crowd Funding](#众筹)
- [数字资产Digital Property](#数字资产)
- [私有化的智能货币 Privatized SmartCoins (稳定的加密货币Stable Cryptocurrencies)](#私有化的智能货币)
- [信息/预测市场 Information/Prediction Markets](#信息/预测市场)
- [如何通过发行资产盈利 How to Profit by Issuing an Asset](#如何通过发行资产盈利)
  - [收费池 Fee Pools](#收费池)

> 详细请参考 [用户发行资产 (User-Issued Assets)](http://www.bts.hk/bts2-0-user-issued-assets.html)

## 去中心化交易所 DEX

- 权力分割：订单写入区块链，使用MPA作为order book
- 全球统一的订单：消除高频交易和抢先交易(high-frequency trading and front running)
- 交易任何事物
- 取款不受限制
- 去中心化的：匿名交易，UIA需要受反洗钱法规限制，比如网关发行IOUs，但MPA不用。安全，签名权重
- 安全：>= 100% 准备金
- 快，但不够快：交易在几秒内完成，不存在优先交易，抢先交易或隐藏订单
- 隐私的去中心化：盲交易(blinded transactions)
- 订单匹配：价格优先，时间优先；收费标准
- 抵押的智能币：抵押低于某一点，强制清算
- 法币网关：费用和做空

## 动态用户权限系统

- 某一类交易设置一个阈值, 并未所有签名者设置权重
- 当多个签名者的权重大于阈值, 则交易通过
- 每个账号有owner和active两种权力(key): owner冷存储, 用于更改active; active用于平时签名(和ripple的冷暖钱包差不多的意思)
- 每个账号签名之后, 在权重到达阈值之前, 可以撤销签名
- 根据分配权重方式, 可以形成权限的层次结构, 对应现实世界的权力机构
- 每个交易需要如果超过两层, 就要新建一个交易(批准交易的交易)来批准, 新交易通过, 之前的交易也通过, 这样, 就可以无限层批准了


## BitShares 2.0实现
### 共识协议
  请参考我翻译的[委托股权证明](https://github.com/wchh/docs/blob/master/dposc.md)

### 源代码

- 源代码目录树第一层包含了program,libraries和test以及其他目录
- program包含了BitShares实现的几个程序，程序很简单，都是直接使用的libraries接口，几句代码实现。：
其中最主要的有4个程序：
  - cli-wallet：一个命令行钱包程序，实现了钱包所有的功能，安全应用或者用来测试等
  - witness-node：证人节点，打包区块和非打包区块
  - delayed-node：比证人的区块链少几次确认，防止区块链分叉
- 所有主要的代码和逻辑实现都在libraries中，主要目录结构如下：
  - App: 实现了应用程序的封装-->Application类; 以及证人节点的API; plugin插件系统
  - chain: 区块链协议的实现，分两层
    - protocol层：完整协议的定义
    - 封装层：对协议的封装，供其它程序使用
  - db: 自实现的数据库
  - fc: fast compile C++ 库，封装了boost库，支持异步事件，json封装，序列化等
  - net: 实现p2p 网络
  - p2p: 底层的低延迟网络，实现推送协议(push protocol)
  - plugin: 插件，比如证人，delayed-node等实现
  - wallet: 钱包API，cli-wallet直接调用此实现。封装了各种操作：比如资产发行，限价单等
