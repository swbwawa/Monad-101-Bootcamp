## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity 中存储成本最高的变量类型是`storage`变量，其数据永久存储在区块链上。
2. 使用`constant`关键字声明的常量可以节省 Gas 费，其值必须在编译时确定。
3. 当合约收到不带任何数据的以太转账时，会自动触发`fallback`函数。

---

### 二、选择题

4. 函数选择器(selector)的计算方法是： B
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前 4 字节  
   **C)** 函数参数的 ABI 编码  
   **D)** 函数返回值的类型哈希

5. 以下关于 mapping 的叙述错误的是： C
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套 mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和 Gas 退还角度）

- revert：revert(error)终止运行并撤销更改的状态, 会退还 gas。
- require：require(msg.sender == owner, 'not owner') 需要调用者是 owner，如果失败退还 gas
- assert：不会退还 gas

require 不推荐使用，msg 很长的话会消耗 gas

7. 某合约同时继承 A 和 B 合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

B 的 foo() 先执行
在 C 里面，使用 override(A, B) 指定覆盖/重写 foo()，但 C 并没有实现自己的 foo() 逻辑，而是沿着继承链向上查找。因此，按照继承线性化规则，B 先于 A，所以 B 的 foo() 会被调用。

8. 当使用`call`方法发送 ETH 时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

**call**

- call()没有 gas 限制，可以支持对方合约 fallback()或 receive()函数实现复杂逻辑。
- call()如果转账失败，不会 revert。
- call()的返回值是(bool, bytes)，其中 bool 代表着转账成功或失败，需要额外代码处理一下。

**transfer**

- transfer()的 gas 限制是 2300，足够用于转账，但对方合约的 fallback()或 receive()函数不能实现太复杂的逻辑。
- transfer()如果转账失败，会自动 revert（回滚交易）。
