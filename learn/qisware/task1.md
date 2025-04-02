## 第一章：走进 Web3 世界

1. 简单描述一下本地开发、部署合约的流程      
初始化开发环境

安装 Node.js 和 Solidity 编译器；

安装开发工具（如 Hardhat、Foundry、Truffle 等）；

创建项目目录结构（如 contracts/, scripts/, tests/）。

编写智能合约

使用 Solidity 编写合约文件（.sol）；

常见编辑器：VS Code + Solidity 插件。

编译合约

使用框架提供的编译工具将 .sol 文件编译为 ABI 和 Bytecode；

编译结果用于部署和前端交互。

搭建本地测试网络

启动一个本地区块链节点（如 Hardhat Node、Ganache、Foundry Anvil）；

获得一组预置账户和测试 ETH，方便调试。

部署合约到本地链

编写部署脚本或使用命令行工具将合约部署到本地网络；

部署后获取合约地址用于后续交互。

测试与调试

编写自动化测试脚本（JavaScript、TypeScript、Rust、Solidity 等）；

也可以使用控制台与合约交互，模拟用户行为；

修复逻辑错误

2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程        
连接钱包：用户使用 MetaMask 等钱包连接 DApp；

发起操作：用户在前端界面点击按钮（如铸造 NFT、发起交易等）；

签名授权：钱包弹出签名窗口，用户确认操作；

交易广播：交易通过钱包发送到链上；

链上执行：智能合约在链上执行操作，返回结果；

前端反馈：DApp 前端监听交易状态并显示结果（成功/失败）                                        
 
3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧 
冷签名、不乱签、多钱包
使用硬件钱包（如 Ledger、Trezor）可以将签名操作在设备内部完成，确保私钥永远不会离开设备或触网
谨慎授权（Approve），控制合约授权权限
建立多钱包分层管理体系，降低损失范围