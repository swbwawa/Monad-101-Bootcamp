## 第一章：走进 Web3 世界

1. 简单描述一下本地开发、部署合约的流程
   * 安装forge、cast、anvil等工具
   * 编写solidity合约代码，使用forge编译
   * 使用anvil启动本地节点
   * 使用cast发送交易，部署合约
   * 使用forge测试合约
   * 使用forge部署合约到目标链

2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程
   * 在DApp中连接钱包
   * 用户通过和前端界面交互，调用合约的abi接口
   * 钱包签名并广播
   * 交互成功后，DApp读取链上信息，更新界面
 
3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧 
   * 使用多签，尽量降低单点风险
   * 签名所见即所签，看到的内容就是预期要签名的内容
   * 零信任+持续验证，注意网页、钱包、合约存在潜在的后门风险