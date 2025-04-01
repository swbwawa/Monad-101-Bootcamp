
# 第一章：走进 Web3 世界

## 1. 简单描述一下本地开发、部署合约的流程

1. 安装开发环境

在本地开发 Solidity 智能合约，推荐使用以下工具：

- Node.js （管理依赖）
- Hardhat 或 Foundry（智能合约开发框架）
- Metamask 或私钥管理工具（部署合约时使用）

```sh
# 安装 Hardhat（推荐）
npm install -g hardhat

# 安装 Foundry（可选）
curl -L <https://foundry.paradigm.xyz> | bash
foundryup

```

2. 创建项目

```sh
# 使用 Hardhat 初始化一个 Solidity 项目
mkdir my-contract && cd my-contract
npx hardhat init

# 使用 Foundry 初始化：
forge init my-contract
cd my-contract

```

3. 编写 Solidity 智能合约(如：MyContract.sol)

```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MyContract {
    uint256 public value;

    function setValue(uint256 _value) public {
        value = _value;
    }
}
```

4. 编译合约

```sh
# Hardhat 编译
npx hardhat compile

Foundry 编译
forge build
```

5. 部署智能合约

5.1. Hardhat 部署

```javascript
// 部署脚本：scripts/deploy.js：
const hre = require("hardhat");

async function main() {
    const MyContract = await hre.ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy();
    await myContract.deployed();

    console.log("MyContract deployed to:", myContract.address);
}

main().catch((error) => {
    console.error(error);
    process.exit(1);
});
```

```sh
# 执行部署
npx hardhat run scripts/deploy.js --network localhost
```

5.2. Foundry 部署

```solidity
// 部署脚本 script/Deploy.s.sol

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "forge-std/Script.sol";
import "../contracts/MyContract.sol";

contract Deploy is Script {
    function run() external {
        vm.startBroadcast();
        new MyContract();
        vm.stopBroadcast();
    }
}
```

```sh
# 执行部署
forge script script/Deploy.s.sol --fork-url <http://localhost:8545> --broadcast
```

6. 交互 & 测试

6.1 本地测试

```sh
# Hardhat 测试
npx hardhat test

# Foundry 测试
forge test
```

7. 部署到测试网

- 如果要部署到测试网（如 Sepolia），需要：

- 获取测试 ETH（Faucet 领测试币）

- 配置 hardhat.config.js

- 设置私钥或使用 Hardhat 的账户管理

- 执行部署脚本

```sh

npx hardhat run scripts/deploy.js --network sepolia

```

## 2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程

1. 用户访问 DApp

   - 通过 Web 浏览器打开 DApp（通常是一个前端 Web 应用）。
   - 连接钱包（如 MetaMask）。

2. 用户触发操作

   - 在 DApp 前端点击按钮（如“存入”、“转账”）。
   - 前端调用智能合约方法，并准备交易数据。

3. 前端发送交易请求

   - DApp 通过 Web3.js / ethers.js 与智能合约交互。
   - 调用智能合约的 call（读取数据）或 send（执行交易）。

4. 钱包确认交易

   - 用户在钱包（如 MetaMask）中看到交易详情，并手动确认。
   - 钱包将交易签名，并提交到区块链网络。

5. 交易广播 & 矿工验证

   - 交易被广播到区块链网络。
   - 矿工/验证者将交易打包进区块，并执行合约逻辑。

6. 交易成功 & 事件通知

   - 交易成功后，链上状态更新。
   - 智能合约可能触发事件，前端监听事件更新 UI。
   - DApp 通过轮询或 WebSocket 获取最新状态，并反馈给用户。

## 3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧

1. 零信任：除了自己，谁都不要轻易相信。
2. 鸡蛋不要放在一个篮子里：分散资产，降低风险。
3. 不要随意点击链接：保持警惕，避免钓鱼攻击。
