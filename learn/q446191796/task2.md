## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity中存储成本最高的变量类型是`storage`变量，其数据永久存储在区块链上。  
2. 使用`constant 或 immutable`关键字声明的常量可以节省Gas费，其值必须在编译时确定。  
4. 当合约收到不带任何数据的以太转账时，会自动触发`receive`函数。  

---

### 二、选择题

4. 函数选择器(selector)的计算方法是：A B  
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前4字节  
   **C)** 函数参数的ABI编码  
   **D)** 函数返回值的类型哈希  

5. 以下关于mapping的叙述错误的是：C  
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对  

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和Gas退还角度）

触发条件：require 用于检查用户输入或外部条件（如余额不足），assert 用于检查内部不变性（如数学计算结果），revert 用于手动回滚交易。

Gas 退还：三者条件检查的 Gas 不退还；require 和 revert 适合外部错误，assert 用于内部错误，assert 失败通常表示代码有 bug。



7. 某合约同时继承A和B合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

实际执行的是 B 合约的 foo() 函数。
原因：Solidity 继承遵循 从右到左 的线性化顺序（C → B → A），override(A,B) 表示优先覆盖 B 的版本

8. 当使用`call`方法发送ETH时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```
(1) addr.call{value: 1 ether}("")：
底层调用，不自动处理异常（需手动检查返回值）。
支持发送 ETH 并调用任意函数（通过 data 字段）。
Gas 限制可自定义（默认传递所有剩余 Gas）。
(2) addr.transfer(1 ether)：
封装了 call，失败时 自动回滚（等价于 require(addr.call{value: 1 ether}(""))）。
固定 Gas 限制（2300 Gas），防止重入攻击但可能因 Gas 不足失败
