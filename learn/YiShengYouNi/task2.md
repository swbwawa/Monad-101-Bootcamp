## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity中存储成本最高的变量类型是`storage`变量，其数据永久存储在区块链上。  
2. 使用`constant`关键字声明的常量可以节省Gas费，其值必须在编译时确定。  
3. 当合约收到不带任何数据的以太转账时，会自动触发`receive`函数。  
   - receive()函数必须是 external、payable，不能有参数或返回值。
   - 仅在合约接收到 ETH 且 没有附加数据 时触发。

---

### 二、选择题

4. 函数选择器(selector)的计算方法是：  
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前4字节  ✅
   **C)** 函数参数的ABI编码  
   **D)** 函数返回值的类型哈希  

5. 以下关于mapping的叙述错误的是：  
   **A)** 键类型可以是任意基本类型  ✅
   **B)** 值类型支持嵌套mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对  

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和Gas退还角度）

|关键点| require| assert| revert|
|---|---|---|---|
|触发条件|条件不满足（业务逻辑检查）|逻辑错误（不应发生的情况）|主动回滚|
|常用于| 输入验证、权限控制 |内部一致性检查 |自定义错误处理|
|失败信息|支持错误消息| Solidity 0.8+ 自动提供 Panic 错误 |可自定义错误消息|
|Gas 退还| 消耗的 Gas 退还| 所有 Gas 消耗 |消耗的 Gas 退还|

🚀 最佳实践：

- 能用 require 就不用 revert，因为 require 更直观。
- 能用 error 就不用字符串错误消息，减少 Gas。
- assert 仅用于检查不应该发生的情况，失败会消耗所有 Gas

7. 某合约同时继承A和B合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

答： 先B后A。  B 在继承列表中比 A 优先级更高，所以会调用 B 的 foo() 函数。

如果交换继承顺序 is B, A，则先A后B.

8. 当使用`call`方法发送ETH时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

|对比项 |call{value: 1 ether}("")| transfer(1 ether) |
| ---|---|--- |
| Gas 限制| 不限制 Gas，默认 2300 Gas，但可手动调整 | 固定 2300 Gas |
|失败时行为| 失败时返回 false，需手动检查 |失败会自动 revert |
| 安全性 |易受重入攻击，需额外防范 | 较安全，无法执行复杂逻辑 |
| 推荐使用场景| 低级调用、可控错误处理、非信任环境| 简单转账，适用于不执行复杂回调的场景|

官方推荐： ✅ 使用 call{value: amount}("") 并手动检查返回值。
❌ 避免使用 transfer()，以防 Gas 限制导致不可预见的失败
