## 第一章：走进 Web3 世界

1. 简单描述一下本地开发、部署合约的流程

   - 本地开发: 开发框架使用 Foundry 或 hardhat, 这里使用 Foundry 演示
     - Foundry 的默认合约目录是 `src/`, 测试文件目录是 `test/`, 部署脚本目录是 `script/`
     - 在 `src/` 目录下创建合约文件, 如 `MyContract.sol`
     - 通过 `forge install` 安装常用的依赖, 比如 `forge install OpenZeppelin/openzeppelin-contracts --no-commit`
     - 编写好合约后进行合约测试编写
     - 在 `test/` 目录下创建测试文件, 如 `MyContract.t.sol`, 并使用 `forge test` 运行测试
     - 使用 `forge coverage` 查看测试覆盖率
     - 通过 `forge snapshot` 查看合约的快照, 里面展示了 gas 使用情况
     - 为了保持部署的一致性, 通常会配合 `script/` 目录下的脚本文件一起使用
     - 在 `script/` 目录下创建脚本文件, 如 `MyContract.s.sol`
     - 测试文件的 setup 方法中, 会调用 `script/` 目录下的脚本文件进行部署, 这样就保证了部署的一致性
   - 部署合约:
     - 当然也可以先在本地部署调试, 部署之前要启动 Anvil 本地链
     - 正式部署前须要获取你要部署的链的 RPC URL, 如果要在部署后验证合约, 需要获取链的 ETHERSCAN_API_KEY
     - 使用 `forge script script/MyContract.s.sol:MyContractScript --rpc-url xxx --broadcast --verify -vvvv --etherscan-api-key xxx` 部署合约
     - 可以把这些运行的命令写到 Makefile 中, 方便后续使用
     - 当运行完部署命令后, 就可以在对应的链上看到合约了, 比如在 etherscan 上看查看合约

2. 简单描述一下用户在使用一个 DApp 时与合约交互的流程

   - 首先用户须要连接到 DApp 的网站, 比如通过钱包连接该网站
   - 然后用户须要在 DApp 的网站上进行操作, 比如点击按钮, 输入信息等
   - 当用户进行操作时, 会调用合约的函数, 这时会向链上发送交易
   - 此时钱包会弹出交易确认窗口, 用户须要确认交易
   - 确认之前要仔细检查交易信息, 比如交易金额, 交易地址等
   - 确认交易后, 钱包会向链上发送交易
   - 链上收到交易后, 会进行验证, 如果验证通过, 就会执行交易
   - 交易执行后, 会返回结果给用户
   - 用户可以在 DApp 的网站上看到交易结果

3. 通读[「区块链黑暗森林自救手册」](https://github.com/slowmist/Blockchain-dark-forest-selfguard-handbook/blob/main/README_CN.md)，列出你觉得最重要的三个安全技巧

   - 对任何事情都零信任和保持怀疑的对待
   - 私钥和助记词要妥善保管, 不要泄露给任何人
   - 使用钱包时, 要仔细检查交易信息, 比如交易金额, 交易地址等
