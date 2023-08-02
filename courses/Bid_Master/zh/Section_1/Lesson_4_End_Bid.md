# 📊撤回出价过高的竞标

## **🚧 教学目标**

1. 了解和掌握全局变量_ 时间戳
2. 了解和掌握构造函数
3. 了解和掌握修饰器
 

## **💚 任务描述**

为保证竞拍的公平性、提高竞拍的参与度和积极性，在竞拍系统中为竞拍设置了时间限制，限定参与者只有在竞拍允许时长内才可竞拍否则提示“不在竞拍时间段内”。同理，系统触发竞拍结束也有时间限制，必须在竞拍截止后才可以结束竞拍并且将竞拍所得款转给受益人。具体业务逻辑如下：      
假设投标受益人为B，投标时长60s   
1. 用户A在拍卖截止时间前投标10 Wei，交易成功；
2. 用户A在拍卖截止时间前结束拍卖，抛出异常，中断结束拍卖；   
3. 拍卖截止用户A投标10 Wei，交易回滚；
4. 拍卖截止用户A结束拍卖，交易成功，收益人B余额增加10 Wei

本次任务的目标
1. 完成合约的初始化设置（设置投标受益人、投标时长）
2. 竞拍出价的时间限制检测
3. 为合约添加竞拍结束方法，并未该方法添加时间限制检测

## **⚡ 相关知识**
知识点简述，（后续会替换AI课件，可以先参看AI脚本：）  
[AI课件](https://docs.qq.com/sheet/DSmdHWWNoT25LTENl?tab=zlpfgb)  
   

## **✨ 任务关键步骤分析**
1. 声明两个公共状态变量，用于存储合约的受益人及合约的结束时间
2. 编写一个构造函数，初始化合约受益人及合约的结束时间
3. 编写一个竞拍时间检测修饰器，限定参与者只能在竞拍截止前竞拍
4. 编写一个竞拍时间检测修饰器，限定只能在竞拍截止后才能结束竞拍
5. 编写一个竞拍时间检测修饰器，限定只能在竞拍截止后才能结束竞拍
6. 编写一个竞拍结束方法，标记竞拍结束，将竞拍所得款转给受益人  

## **✨ 任务疑难点分析**
1. 在构造函数中如何计算合约的结束时间？
解析：为构造函数添加两个参数，一个是接收指定的受益人，一个是接收竞拍时长，合约的结束时间为初始化合约的当前时间+竞拍时长即为合约的结束时间。

2. 限定出价在竞拍截止之前才可以，如何为合约添加一个判断是否在截止日期之前的修饰器。
解析：限制合约出价的修饰器业务逻辑提示，定义一个修饰器，添加一个函数参数，用于接收合约结束时间，在修饰器函数体中，判断当前块的时间戳是否大于截止日期时间戳，如果是，抛出异常回滚交易。同理，限制竞拍结束方法在竞拍截止之后才可执行的修饰器业务逻辑也是类似的。
```Solidity
    modifier onlyBefore(函数参数接收截止竞拍时间) {
        //如果当前时间戳是否大于截止时间，抛出异常，回滚交易
        _;
    }
```   
## **✨ 任务实现**
1. **完善合约**  
    根据步骤提示，完善右侧合约文件中begin...end之间的代码。

3. **合约测试**  
   a. 编译和部署合约   

   b. 设定投标受益人，投标时长为60s

   c. 用户A在拍卖截止时间前投标10 Wei，交易成功，查看相应的状态变量，最高竞拍者信息记录为用户A，竞拍价为10

   d. 用户A在拍卖截止时间前结束拍卖，抛出异常，中断结束拍卖； 

   e. 拍卖截止用户A投标10 Wei，抛出异常，交易回滚； 

   f. 拍卖截止用户A结束拍卖，交易成功，收益人B余额增加10 Wei，查看受益人B的账户是否有10 Wei

   

至此，完成了任务43合约的调试，部署和测试。
## **🌸 知识测试**  