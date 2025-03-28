## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity中存储成本最高的变量类型是`storage`变量，其数据永久存储在区块链上。  
2. 使用`constant`关键字声明的常量可以节省Gas费，其值必须在编译时确定。  
4. 当合约收到不带任何数据的以太转账时，会自动触发`receive`函数。  

---

### 二、选择题

4. 函数选择器(selector)的计算方法是：  
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前4字节 ✓  
   **C)** 函数参数的ABI编码  
   **D)** 函数返回值的类型哈希  

5. 以下关于mapping的叙述错误的是：  
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套mapping  
   **C)** 可以通过`length`属性获取大小 ✓  
   **D)** 无法直接遍历所有键值对  

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和Gas退还角度）

`require`主要用于输入验证和外部条件检查，条件不满足时会退还剩余gas；`assert`用于检查内部不变量和不应该发生的情况，触发时会消耗所有gas；`revert`可以主动回滚交易并提供错误信息，同样会退还剩余gas。

7. 某合约同时继承A和B合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

在Solidity中，多重继承遵循C3线性化规则，合约声明时从右到左的顺序决定了继承顺序。在这个例子中，由于B合约在A合约的右边，所以B合约的foo()函数会被优先调用。这也是为什么在override时需要同时指定A和B，以明确处理所有被覆盖的函数。

8. 当使用`call`方法发送ETH时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

主要区别有三点：
1. Gas限制：transfer固定2300 gas，而call没有gas限制
2. 错误处理：transfer失败会自动revert交易，而call需要手动检查返回值
3. 安全性：transfer更安全但功能受限，call更灵活但需要注意重入攻击风险

