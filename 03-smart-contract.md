<h1 align="center">本体智能合约语法专辑（1）-合约简介</h1>

## 本体智能合约简介

本体智能合约是一个集多功能、轻量级、高可用、可并发、多语言、跨合约、跨虚拟机等于一体的完备体系。本体智能合约支持多种主流开发语言，如 C#, Python，开发者不需要学习新的语言即可很方便的开发本体智能合约，未来将支持更多主流开发语言，包括：Java, C++, Rust, Go, JavaScript 等。

本体智能合约具有确定性、高性能、扩展性的特性，包括两大模块：交互服务和虚拟机。交互服务提供了虚拟机和区块链账本之间的交互。虚拟机提供了智能合约的运行环境。交互服务包括原生服务和 NEO 虚拟机服务。原生服务提供了基础链上特殊智能合约的实现，这种合约能被快速方便地使用。NEO虚拟机服务提供了外部访问NEO 虚拟机的API, 它能增强智能合约的调用功能。

![ontology smart contract architecture.png](https://raw.githubusercontent.com/ontio/ontology-smartcontract/master/smart-contract-tutorial/images/smartcontract_architecture.png)

### 合约类型

本体智能合约有两种类型：Native合约和 NeoVm合约。Native合约是在本体底层直接编写的合约，不需要像部署普通合约那样编写合约代码，具有很高的执行效率，是对普通合约的极大优化，通用的服务包括：Oracle，DID 和权限管理，数据交易所都将采用 Native 合约实现。NeoVm合约是采用 NeoVm 虚拟机运行的合约，需要编写相应的合约代码，现支持的语言包含：C#，Python。 NeoVm 本身具有轻量级、可扩展、高性能的特性，通过结合 Interop Service 层能很好的打通虚拟机与账本层间的交互。

![ontology smart contract type.png](https://raw.githubusercontent.com/ontio/ontology-smartcontract/master/smart-contract-tutorial/images/smartcontract_type.png)

### 合约执行过程

本体智能合约运行需要传入合约运行所需要的脚本，以及运行合约的虚拟机类型，智能合约调度中心会更根据虚拟机类型，启动不同的虚拟机运行合约。当执行过程中，合约调用了 AppCall 指令(其中包含了运行合约的必要参数)，触发智能合约调度中心，调度中心将会根据传入的参数启动对应的虚拟机运行对应的脚本，直到合约运行完成为止。

![process](http://upload-images.jianshu.io/upload_images/150344-ac402b1c8eb3aa9a.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 合约费用模型

交易费用是 GAS limit 和 GAS price 的乘积。Gas limit 是在执行智能合约的 opcode 过程中计步时使用，理论上智能合约越复杂，需要的 GAS limit 数量越高，Ontology 交易设定最低的 GAS limit 数量是 20000。GAS price 是给执行 opcode 定价，GAS price 越高，共识节点会优先打包该笔交易。

## 总结

本体智能合约有着清晰的优势。第一，本体提供了非常高效的合约开发工具并支持主流开发语言Python，使开发者无需学习新的编程语言如solidity即可开发合约。第二，本体采用双通证模型，专门推出了ONG作为燃料（对标以太坊GAS），当使用Ontology的人多时，ONG费用高，人少时费用低。这种弹性成本符合开发者预期。另一方面，本体并不需要像EOS一样为使用CPU, 带宽资源抵押代币，为使用内存购买RAM。这也极大的方便了开发者。第三，本体具有极高的TPS，实现秒级出块时间，轻松保障用户使用体验，让开发者释放更多创意。

