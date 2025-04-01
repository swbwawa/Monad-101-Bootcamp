## 第一章：走进 Web3 世界

1. 简单描述一下本地开发、部署合约的流程
	1)设置开发环境，通常包括:
		node.js和npm
		truffle和hardhat
	2)编写智能合约
		使用solidity编写智能合约，可以使用remix或者vscode都行
	3)编译合约
	4)配置开发网络
	5)部署合约

2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程   	
	1)用户访问 DApp，连接钱包（如 MetaMask）。
	2)用户发起交易，例如调用智能合约函数。
	3)钱包签署交易，用户确认交易。
	4)交易上链，智能合约状态更新。
	5)DApp 等待交易确认，并根据结果更新前端。
	6)用户收到反馈，例如操作成功或失败提示。                                             
3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧 
	1)备份钱包，助记词手抄
	2)签名需谨慎，不认识的app不要乱连
	3)定时取消授权