# 📰Solidity初级：BidMaster盲拍系统

## **🎯 课题目标**

竞拍系统是指在一定时间内，由多个参与者对同一物品或服务进行竞价，最终以最高价者获得该物品或服务的一种交易方式。

在竞拍系统中，通常会设定一个起拍价和一个最低加价幅度，参与者需要在一定的时间内递交自己的出价，最终以出价最高者成交。竞拍系统通常由拍卖公司或拍卖机构管理，他们会负责组织竞拍、管理出价、确认竞拍结果等。

本门课程通过设计并实现一个拍卖系统，旨在介绍初级Solidity应用开发技能。ok, let's rock it~🚀

## **♨️ 传统竞拍系统痛点**

传统竞拍系统存在一些痛点，例如：

1. 中心化问题：传统的竞拍系统通常由中心化的拍卖机构或公司管理，参与者需要信任这些机构或公司，而这些机构或公司有时可能存在不公正的行为，例如操纵竞拍结果等。
2. 信息不对称问题：在传统的竞拍系统中，卖家拥有商品的信息优势，而买家则缺乏足够的信息，这可能导致买家出价过高或过低。
3. 高成本问题：传统的竞拍系统通常需要支付高额的手续费和服务费，这使得竞拍成本高昂，对小额商品的竞拍不太适合。
4. 时间限制问题：传统的竞拍通常需要在一定的时间内完成，这限制了参与者的灵活性，可能会错过竞拍机会。
5. 交易安全问题：在传统的竞拍系统中，交易过程中可能存在一些安全隐患，例如支付信息泄露、伪造竞拍记录等。
6. 一些竞拍通常需要参与者到现场进行竞拍，或通过电话或在线平台参与竞拍，存在空间上的限制。

这些问题影响了传统竞拍系统的公平性、透明度和效率。

## **🚦 竞拍系统 Web3 解决方案**

区块链上的竞拍系统是一种基于区块链技术的去中心化拍卖平台，具有以下优势：

1. 去中心化：区块链上的竞拍系统不依赖于中心化的拍卖机构，所有的交易都在区块链上完成，保证了交易的透明性和公正性。
2. 去信任：区块链上的竞拍系统采用智能合约进行交易，合约的执行是自动化的，不需要第三方的信任机构，降低了交易的成本和风险。
3. 数据不可篡改：区块链上的竞拍系统的交易记录被记录在区块链上，具有不可篡改性，保证了交易的真实性和可追溯性。
4. 低手续费：区块链上的竞拍系统的交易手续费相对较低，因为交易不需要中间人，而是由智能合约直接执行。

在区块链上的竞拍系统中，参与者可以使用加密货币（如以太坊、比特币等）进行竞拍，智能合约会自动管理竞拍过程，包括出价、竞拍时间、竞拍结果的确认等。竞拍结束后，合约会将竞拍成功者的数字货币转移给卖家，同时将竞拍失败者的数字货币返还给他们。

## **🎡 实践案例**

本次课题实践是做一版简化的区块链竞拍系统BidMaster，具体流程分为2部分：

- 第一部分：公开竞拍

  1. 用户竞拍，合约记录拍卖最高价与出价人
  2. 当有新的用户出价时，判断新出价是否大于当前最高出价，否则结束，是则进入下一步骤；
  3. 合约保存上一次最高出价用户地址和出价
  4. 拍卖结束，将所得转给受益人
  5. 让用户主动赎回未拍中的拍卖资金
- 第二部分：盲拍

在公开竞拍中，所有人的出价记录都会被上链公开，竞拍策略只要出价压过对手方即可。盲拍系统可以将竞拍者真实竞拍意图隐藏起来，增加了竞拍的玩法可能性。

盲拍特性是通过哈希不可逆特性做到的。目前几乎不可能找到哈希值（长度足够长）一样的两个字符串，因此投标人可通过该方式提交报价。在盲拍版本中，投标人只是发送一个出价金额+是否真实出价的标志位的哈希结果，在投标结束后，投标人需要明文传递出价金额+是否真实出价标志位公开盲拍信息，合约检查出价的哈希值是否与投标期间提供的相同。

为了防止投标者在赢得拍卖后不付款，系统要求竞拍者将资金连同出价一起发出。因此每次竞拍出价金额是公开的，但是实际竞拍信息是隐藏在哈希值中。同一个用户可以多次出价，但只在某一次出价中标明是真正的出价竞拍，投标人可以通过设置几个或高或低的无效出价来迷惑竞争对手。

盲拍版本主要步骤是对公开竞拍的版本进行优化：

1. 优化竞拍方法，保存盲拍信息哈希与出价
2. 用户披露盲拍信息，将非竞标资金返还用户
3. 拍卖结束，将所得转给受益人
4. 让用户主动赎回拍卖资金

![flowchart.png](https://ed3academy.xyz/github/courses/Bid_Master/flowchart.jpg)