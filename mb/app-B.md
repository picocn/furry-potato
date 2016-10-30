比特币改进建议
====


比特币改进建议（Bitcoin improvement proposals， BIP）是一种向比特币社区提供信息，描述比特币及其处理过程及外部环境新特性的设计文档。

基于BIP0001 *BIP目的和指南*，BIP可以分为三种类型：

*标准BIP（Standard BIP）*

    描述影响大多数或全部比特币实现的改变，比如网络协议的改变，区块或交易验证规则的改变，或者任何影响比特币应用互操作性的变化或补充。

*说明性BIP（Informational BIP）*

    说明性BIP不提出新的特性，仅描述比特币设计问题，向比特币社区提供通用指南或信息。说明性BIP不需要征得比特币社区的同意或推荐，所以用户或开发者可以忽略说明性BIP，也可以选择接受建议。

*过程BIP(Process BIP)*

    描述比特币的处理过程，或者提议对过程进行改进或添加新的事件。过程BIP与标准BIP类似，但适用领域不包括比特币协议本身。它们可能提出一种实现方案，但不会针对比特币代码库；过程BIP一般都要求社区达成共识；不像说明性BIP，过程BIP是强制的，用户不能选择忽略。过程BIP的示例包括决策过程的规程、指南及变化，比特币开发中工具或环境的变化等。任何元BIP（meta-BIP）也被视为过程BIP。


比特币改进建议记录于Github版本库中。**表B-1**显示了截至2014年秋天的所有BIP的一个快照。要了解已有BIP及其内容的最新消息，可以访问官方文档库。

*表B-1 BIP快照*

|BIP序号|链接 |标题| 作者 |类型 |状态|
|----|-------|-----|------|------|------|
|1| https://github.com/bitcoin/bips/blob/master/bip-0001.mediawiki |BIP目标与指南| Amir Taaki |标准|活跃|
|10| https://github.com/bitcoin/bips/blob/master/bip-0010.mediawiki |多重签名交易分布|Alan Reiner| 说明性|草案|
|11| https://github.com/bitcoin/bips/blob/master/bip-0011.mediawiki |M-N标准交易|Gavin Andresen |标准|采纳|
|12| https://github.com/bitcoin/bips/blob/master/bip-0012.mediawiki |OP_EVAL |Gavin Andresen |标准 |撤销|
|13| https://github.com/bitcoin/bips/blob/master/bip-0013.mediawiki |支付到脚本哈希地址格式|Gavin Andresen|标准|终稿|
|14| https://github.com/bitcoin/bips/blob/master/bip-0014.mediawiki |协议版本与用户代理| Amir Taaki,Patrick Strateman|标准 |采纳|
|15 | https://github.com/bitcoin/bips/blob/master/bip-0015.mediawiki |别名|Amir Taaki |标准| 撤销|
|16| https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki |支付到脚本哈希|Gavin Andresen|标准 |采纳|
|17| https://github.com/bitcoin/bips/blob/master/bip-0017.mediawiki |OP_CHECKHASHVERIFY(CHV)|Luke Dashjr |撤销|草案|
|18| https://github.com/bitcoin/bips/blob/master/bip-0018.mediawiki |哈希脚本校验|Luke Dashjr |标准| 草案|
|19| https://github.com/bitcoin/bips/blob/master/bip-0019.mediawiki |M-N标准交易(Low SigOp)|Luke Dashjr| 标准|草案|
|20| https://github.com/bitcoin/bips/blob/master/bip-0020.mediawiki |URI方案 |Luke Dashjr |标准|被替代|
|21| https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki |URI方案| Nils Schneider,Matt Corallo|标准 |采纳|
|22| https://github.com/bitcoin/bips/blob/master/bip-0022.mediawiki |getblocktemplate - 基础|Luke Dashjr |标准| 采纳|
|23| https://github.com/bitcoin/bips/blob/master/bip-0023.mediawiki |getblocktemplate - 矿池挖矿|Luke Dashjr |标准| 采纳|
|30| https://github.com/bitcoin/bips/blob/master/bip-0030.mediawiki |重复交易| Pieter Wuille |标准 |采纳|
|31| https://github.com/bitcoin/bips/blob/master/bip-0031.mediawiki |应答消息| Mike Hearn |标准 |采纳|
|32| https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki |层次化确定性钱包| Pieter Wuille |说明性|采纳|
|33| https://github.com/bitcoin/bips/blob/master/bip-0033.mediawiki |分层节点| Amir Taaki| 标准 |草案|
|34|	https://github.com/bitcoin/bips/blob/master/bip-0034.mediawiki	|区块版本2，币基中的高度|Gavin Andresen|标准|采纳|
|35|	https://github.com/bitcoin/bips/blob/master/bip-0035.mediawiki	|内存池消息|Jeff Garzik|标准|采纳|
|36|	https://github.com/bitcoin/bips/blob/master/bip-0036.mediawiki	|用户服务|Stefan Thomas|标准|草案|
|37|	https://github.com/bitcoin/bips/blob/master/bip-0037.mediawiki	|布隆过滤器|Mike Hearn and Matt Corallo|	标准|采纳|
|38|	https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki	|密码保护的私钥|Mike Caldwell|标准|草案|
|39|	https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki	|用于创建确定性密钥的助记码|Slush|标准|草案|
|40|	-	|Stratum连线协议|Slush|标准|BIP编号已分配|
|41|	-	|Stratum挖矿协议|Slush|标准|BIP编号已分配|
|42|	https://github.com/bitcoin/bips/blob/master/bip-0042.mediawiki |比特币的有限货币供应|	Pieter Wuille|标准|草案|
|43|	https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki |确定性钱包的目标域|	Slush|标准|草案|
|44|	https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki	|确定性钱包的多账户层次|Slush|标准|草案|
|50|	https://github.com/bitcoin/bips/blob/master/bip-0050.mediawiki	|2013年3月链分叉事后研究|Gavin Andresen|说明性|草案|
|60|	https://github.com/bitcoin/bips/blob/master/bip-0060.mediawiki	|固定长度“版本”消息（交易中继字段）|Amir Taaki|标准|草案|
|61|	https://github.com/bitcoin/bips/blob/master/bip-0061.mediawiki	|“拒绝”P2P消息|Gavin Andresen|标准|草案|
|62|	https://github.com/bitcoin/bips/blob/master/bip-0062.mediawiki	|处理延展性|	Pieter Wuille |标准|草案|
|63|	-	|隐形地址|Peter Todd |标准|BIP编号已分配|
|64|	https://github.com/bitcoin/bips/blob/master/bip-0064.mediawiki	|获取utxo消息|	Mike Hearn |标准|草案|
|70|	https://github.com/bitcoin/bips/blob/master/bip-0070.mediawiki	|支付协议|Gavin Andresen |标准|草案|
|71|	https://github.com/bitcoin/bips/blob/master/bip-0071.mediawiki	|支付协议MIME类型|Gavin Andresen|标准|草案|
|72|	https://github.com/bitcoin/bips/blob/master/bip-0072.mediawiki	|支付协议的URI|Gavin Andresen |标准|草案|
|73|	https://github.com/bitcoin/bips/blob/master/bip-0073.mediawiki |在支付请求URL中使用“accept”报文头|Stephen Pair|标准|草案|