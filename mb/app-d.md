sx工具集可用命令
==============

sx命令包括：

**已过时的**：

Electrum风格的确定性密钥和地址

    genaddr 从钱包种子或主公钥中确定性的生成一个比特币地址
    genpriv 从种子中确定性的生成一个私钥
    genpub 从钱包种子或主公钥中确定性的生成一个公钥
    mpk 从确定性钱包种子中解开一个主公钥
    newseed 生成一个确定性钱包种子

**实验性的**：

应用

    wallet 实验性命令行钱包

**离线区块链**

区块头

    showblkhead 显示区块头详细信息

**离线密钥和地址**

基本

    addr 查看一个公钥或私钥的比特币地址
    embed-addr 生成一个嵌入区块链的比特币地址
    get-pubkey 如果地址存在取其公钥
    newkey 创建一个新私钥
    pubkey 查看私钥的公共部分
    validaddr 验证一个地址

头脑存储

    brainwallet 从任意口令生成一个256位的比特币私钥
    mnemonic 从128位electrum 或bip32种子中生成12个助记单词

HD / BIP32

    hd-priv 从另一个HD私钥生成一个新的HD（层次化确定性）私钥
    hd-pub 从另一个HD私钥或公钥生成一个HD公钥
    hd-seed 生成一个新的随机HD密钥
    hd-to-address 将HD公钥或私钥转换为一个比特币地址
    hd-to-wif 将HD私钥转换为WIF格式私钥

多重签名地址

    scripthash 从原始脚本的十六进制数据创建BIP16脚本哈希地址

隐形

    stealth-addr 从给定输入查看一个隐形地址
    stealth-initiate 初始化一个新的隐形支付
    stealth-newkey 生成新的隐形密钥和地址
    stealth-show-addr 显示一个隐形地址的详细信息
    stealth-uncover 披露一个隐形地址
    stealth-uncover-secret 披露一个隐形秘密

离线交易

脚本处理

    mktx 创建一个未签名交易
    rawscript 从一个脚本创建原始十六进制表示
    set-input 设置交易输入
    showscript 显示一个原始脚本的详情
    showtx 显示交易详情
    sign-input 对一个交易输入进行签名
    unwrap 从十六进制字符串中验证校验码并恢复版本字节和原始数据
    validsig 验证交易输入的签名
    wrap 添加版本字节和校验码到十六进制字符串中

在线（比特币P2P）

区块链更新

    sendtx-node 将交易发送到一个节点上
    sendtx-p2p 将交易发送到比特币网络上

在线（BLOCKCHAIN.INFO）

区块链查询 （BLOCKCHAIN.INFO）

    bci-fetch-last-height 使用blockchain.info获取最小区块高度
    bci-history 从blockchain.info获取输出点，价值以及其支出的列表

区块链更新

    sendtx-bci 发送交易到blockchain.info/pushtx.

在线（BLOCKEXPLORER.COM）

区块链查询（blockexplorer.com）

    blke-fetch-transaction 从blockexplorer.com获取一个交易

在线（OBELISK）

区块链查询

    balance 以聪为单位显示一个地址的余额
    fetch-block-header 获取元素区块头
    fetch-last-height 获取最小区块高度
    fetch-stealth 使用网络连接向obelisk负载均衡器后台发送请求以获取隐藏信息
    fetch-transaction 使用网络连接向obelisk负载均衡器后台发送请求以获取原始交易信息
    fetch-transaction-index 获取交易所在区块的高度及交易位置索引号
    get-utxo 从给定的地址集中获取足够的未花费输出以支付一定金额的比特币
    history 获取特定地址的输出点，价值及其支出的列表，使用grep过滤出未花费的输出，其结果可以被mktx命令调用
    validtx 验证一个交易

区块链更新

    sendtx-obelisk 发送交易到obelisk服务器

区块链观察

    monitor 监控一个地址Monitor an address.
    watchtx 通过在网络中对一个特定哈希的搜索来观察交易

OBELISK管理

    initchain 初始化一个区块链

**实用工具**

椭圆曲线计算

    ec-add-modp 计算整数+整数的结果
    ec-multiply 整数与点的乘积
    ec-tweak-add 计算点+整数*生成点

格式（BASE 58）

    base58-decode 将base58转换为十六进制
    base58-encode 将十六进制转换为base58

格式（BASE58CHECK）
    base58check-decode 将base58check转换为十六进制
    base58check-encode 将十六进制转换为base58check
    decode-addr 将地址从base58check转换为内部RIPEMD表示
    encode-addr 将地址从内部RIPEMD表示转换为base58格式

格式（WIF）

    secret-to-wif 将秘密指数值转换为WIF格式
    wif-to-secret 将WIF格式转换为秘密指数值

哈希

    ripemd-hash 从标准输入数据通过RIPEMD转换为哈希
    sha256 采用SHA256算法对数据做哈希计算

杂项

    qrcode 离线生成比特币的二维码

“聪”的换算

    btc 将“聪”换算为比特币
    satoshi 将比特币换算成“聪”

通过'sx help COMMAND'可以查看单个命令的详细说明

----------------

接下来，我们将通过一些例子来尝试对密钥和地址进行操作。
采用newkey命令，利用操作系统的随机数生成器生成一个新的私钥。我们将标准输出保存到文件private_key:

    $ sx newkey > private_key
    $ cat private_key
    5Jgx3UAaXw8AcCQCi1j7uaTaqpz2fqNR9K3r4apxdYn6rTzR1PL

现在，使用pubkey命令从刚才生成的私钥生成公钥。将私钥文件通过重定向命令输出到标准输入，将标准输出重定向到一个新文件public_key：

    $ sx pubkey < private_key > public_key
    $ cat public_key
    02fca46a6006a62dfdd2dbb2149359d0d97a04f430f12a7626dd409256c12be500

我们可以使用addr命令将公钥转换为地址。将公钥文件通过重定向输出到标准输入：

    $ sx addr < public_key
    17re1S4Q8ZHyCP8Kw7xQad1Lr6XUzWUnkG

生成的密钥称为type-0非确定性密钥。意思是每个密钥均从随机数生成器生成。sx工具集也支持type-2确定性密钥，“主”密钥生成后，可以由它衍生出一个子密钥链或子密钥树。

首先，我们创建一个“种子”，它将成为衍生密钥链的基础，与Electrum钱包或其他类似的钱包兼容。我们使用newseed命令来生成种子：

    $ sx newseed > seed
    $ cat seed
    eb68ee9f3df6bd4441a9feadec179ff1

种子的值也可以导出成容易阅读的助记码，这种形式比十六进制字符串更加容易保存和输入，使用的命令为mnemonic：

    $ sx mnemonic < seed > words
    $ cat words
    adore repeat vision worst especially veil inch woman cast recall dwell appreciate

助记词可以用于重新生成种子，使用的命令仍然是mnemonic:

    $ sx mnemonic < words
    eb68ee9f3df6bd4441a9feadec179ff1

    
With the seed, we can now generate a sequence of private and public keys, a key chain.
We use the genpriv command to generate a sequence of private keys from a seed and
the addr command to generate the corresponding public key:
    $ sx genpriv 0 < seed
    5JzY2cPZGViPGgXZ4Syb9Y4eUGjJpVt6sR8noxrpEcqgyj7LK7i
    $ sx genpriv 0 < seed | sx addr
    1esVQV2vR9JZPhFeRaeWkAhzmWq7Fi7t7
    $ sx genpriv 1 < seed
    5JdtL7ckAn3iFBFyVG1Bs3A5TqziFTaB9f8NeyNo8crnE2Sw5Mz
    $ sx genpriv 1 < seed | sx addr
    1G1oTeXitk76c2fvQWny4pryTdH1RTqSPW
With deterministic keys we can generate and regenerate thousands of keys, all derived
from a single seed in a deterministic chain. This technique is used in many wallet ap‐
plications to generate keys that can be backed up and restored with a simple multiword
mnemonic. This is easier than having to back up the wallet with all its randomly gen‐
erated keys every time a new key is created.
