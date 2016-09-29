	$ ./configure --help
	
	`configure' configures Bitcoin Core 0.9.0 to adapt to many kinds of systems.
	
	Usage: ./configure [OPTION]... [VAR=VALUE]...
	
	To assign environment variables (e.g., CC, CFLAGS...), specify them as
	VAR=VALUE.  See below for descriptions of some of the useful variables.
	
	Defaults for the options are specified in brackets.
	
	Configuration:
	  -h, --help              display this help and exit
	      --help=short        display options specific to this package
	      --help=recursive    display the short help of all the included packages
	  -V, --version           display version information and exit
	
	[... many more options and variables are displayed below ...]
	
	Optional Features:
	  --disable-option-checking  ignore unrecognized --enable/--with options
	  --disable-FEATURE       do not include FEATURE (same as --enable-FEATURE=no)
	  --enable-FEATURE[=ARG]  include FEATURE [ARG=yes]
	
	[... more options ...]
	
	Use these variables to override the choices made by `configure' or to help
	it to find libraries and programs with nonstandard names/locations.
	
	Report bugs to <info@bitcoin.org>.
	
	$

configure脚本允许你通过使用--enable-FEATURE或--disable-FEATURE标志，来启用或禁用bitcoind某些功能。其中的FEATURE由具体功能名称代替，功能名称在以上帮助的输出信息中列出。在本章中，我们将构建的bitcoind客户端打开所有默认功能。我们将不使用配置标志，但你最好审阅并了解客户端包含哪些可选功能。接下来，运行configure脚本来自动发现所有必要的库，并为系统创建一个定制的构建脚本：

	$ ./configure
	checking build system type... x86_64-unknown-linux-gnu
	checking host system type... x86_64-unknown-linux-gnu
	checking for a BSD-compatible install... /usr/bin/install -c
	checking whether build environment is sane... yes
	checking for a thread-safe mkdir -p... /bin/mkdir -p
	checking for gawk... no
	checking for mawk... mawk
	checking whether make sets $(MAKE)... yes
	[... many more system features are tested ...]
	configure: creating ./config.status
	config.status: creating Makefile
	config.status: creating src/Makefile
	config.status: creating src/test/Makefile
	config.status: creating src/qt/Makefile
	config.status: creating src/qt/test/Makefile
	config.status: creating share/setup.nsi
	config.status: creating share/qt/Info.plist
	config.status: creating qa/pull-tester/run-bitcoind-for-test.sh
	config.status: creating qa/pull-tester/build-tests.sh
	config.status: creating src/bitcoin-config.h
	config.status: executing depfiles commands
	$

如果一切顺利，configure命令将成功完成定制化构建脚本的创建，这个脚本允许我们编译bitcoind。如果有缺失的库或者其他错误，configure命令将终止创建构建脚本，并输出错误。如果发生错误，很可能是因为缺失库或者库不兼容。再次查阅构建文档，确认已安装了所有先决要求。然后重新运行configure看看是否已修复了错误。接下来，你将编译源代码，这个过程可能会持续一个钟头。在编译的过程中，你每几秒或者每几分钟就会看到一些输出信息，如果有什么问题，错误信息也会显示出来。编译过程如果被中断，你也可以随时恢复编译过程。键入*make*开始编译吧：

	$ make
	Making all in src
	make[1]: Entering directory `/home/ubuntu/bitcoin/src'
	make all-recursive
	make[2]: Entering directory `/home/ubuntu/bitcoin/src'
	Making all in .
	make[3]: Entering directory `/home/ubuntu/bitcoin/src'
		CXX addrman.o
		CXX alert.o
		CXX rpcserver.o
		CXX bloom.o
		CXX chainparams.o
	[... many more compilation messages follow ...]
		CXX test_bitcoin-wallet_tests.o
		CXX test_bitcoin-rpc_wallet_tests.o
		CXXLD test_bitcoin
	make[4]: Leaving directory `/home/ubuntu/bitcoin/src/test'
	make[3]: Leaving directory `/home/ubuntu/bitcoin/src/test'
	make[2]: Leaving directory `/home/ubuntu/bitcoin/src'
	make[1]: Leaving directory `/home/ubuntu/bitcoin/src'
	make[1]: Entering directory `/home/ubuntu/bitcoin'
	make[1]: Nothing to be done for `all-am'.
	make[1]: Leaving directory `/home/ubuntu/bitcoin'
	$

如果一切顺利，bitcoind就编译好了。最后的步骤是将bitcoind安装到系统路径中，仍然使用*make*命令：

	$ sudo make install
	Making install in src
	Making install in .
	 /bin/mkdir -p '/usr/local/bin'
	  /usr/bin/install -c bitcoind bitcoin-cli '/usr/local/bin'
	Making install in test
	make  install-am
	 /bin/mkdir -p '/usr/local/bin'
	  /usr/bin/install -c test_bitcoin '/usr/local/bin'
	$

你可以通过查看系统中以下两个可执行程序的位置来确认bitcoind是否已经正确安装：

	$ which bitcoind
	/usr/local/bin/bitcoind

	$ which bitcoin-cli
	/usr/local/bin/bitcoin-cli

默认安装下，bitcoind安装于*/usr/local/bin*目录下。当你第一次运行bitcoind时，它会提醒你创建一个配置文件，这个配置文件包含访问JSON-RPC接口的高强度密码。键入*bitcoind*在终端上运行bitcoind：

	$ bitcoind
	Error: To use the "-server" option, you must set a rpcpassword in the configuration file:
	/home/ubuntu/.bitcoin/bitcoin.conf
	It is recommended you use the following random password:
	rpcuser=bitcoinrpc
	rpcpassword=2XA4DuKNCbtZXsBQRRNDEwEY2nM6M4H9Tx5dFjoAVVbK
	(you do not need to remember this password)
	The username and password MUST NOT be the same.
	If the file does not exist, create it with owner-readable-only file permissions.
	It is also recommended to set alertnotify so you are notified of problems;
	for example: alertnotify=echo %s | mail -s "Bitcoin Alert" admin@foo.com

在你喜欢的编辑器中编辑配置文件，设置参数，将密码替换为一个bitcoind建议的高强度密码。不要使用范例中使用的密码。在*.bitcoin*目录下创建一个命名为*./bitcoind/bitcoin.conf*的配置文件，输入用户名和密码：

	rpcuser=bitcoinrpc
	rpcpassword=2XA4DuKNCbtZXsBQRRNDEwEY2nM6M4H9Tx5dFjoAVVbK

当你编辑这个配置文件时，你可能还希望设置几个其他选项，比如*txindex*（参见第47页《交易数据库索引和txindex选项）。若需要查看所有可用选项，请键入*bitcoind --help*。

现在，运行比特币核心客户端。第一次运行时，它会通过下载所有区块来重建比特币区块链。这是一个好几个G的大文件，平均需要花费两天才能全量下载。你可以利用BitTorrent客户端从SourceForge下载部分区块链副本来缩短区块链初始化时间。

通过*-daemon*选项可以在后台运行bitcoind:

	$ bitcoind -daemon
	Bitcoin version v0.9.0rc1-beta (2014-01-31 09:30:15 +0100)
	Using OpenSSL version OpenSSL 1.0.1c 10 May 2012
	Default data directory /home/bitcoin/.bitcoin
	Using data directory /bitcoin/
	Using at most 4 connections (1024 file descriptors available)
	init message: Verifying wallet...
	dbenv.open LogDir=/bitcoin/database ErrorFile=/bitcoin/db.log
	Bound to [::]:8333
	Bound to 0.0.0.0:8333
	init message: Loading block index...
	Opening LevelDB in /bitcoin/blocks/index
	Opened LevelDB successfully
	Opening LevelDB in /bitcoin/chainstate
	Opened LevelDB successfully
	[... more startup messages ...]

#通过命令行调用比特币核心的JSON-RPC接口

比特币核心客户端实现了一个可供命令行助手*bitcoin-cli*调用的JSON-RPC接口。这使我们得以实验性的访问那些通常由程序通过API调用的功能。开始前，我们先调用help命令来看一下全部可用的RPC命令列表：

	$ bitcoin-cli help
	addmultisigaddress nrequired ["key",...] ( "account" )
	addnode "node" "add|remove|onetry"
	backupwallet "destination"
	createmultisig nrequired ["key",...]
	createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
	decoderawtransaction "hexstring"
	decodescript "hex"
	dumpprivkey "bitcoinaddress"
	dumpwallet "filename"
	getaccount "bitcoinaddress"
	getaccountaddress "account"
	getaddednodeinfo dns ( "node" )
	getaddressesbyaccount "account"
	getbalance ( "account" minconf )
	getbestblockhash
	getblock "hash" ( verbose )
	getblockchaininfo
	getblockcount
	getblockhash index
	getblocktemplate ( "jsonrequestobject" )
	getconnectioncount
	getdifficulty
	getgenerate
	gethashespersec
	getinfo
	getmininginfo
	getnettotals
	getnetworkhashps ( blocks height )
	getnetworkinfo
	getnewaddress ( "account" )
	getpeerinfo
	getrawchangeaddress
	getrawmempool ( verbose )
	getrawtransaction "txid" ( verbose )
	getreceivedbyaccount "account" ( minconf )
	getreceivedbyaddress "bitcoinaddress" ( minconf )
	gettransaction "txid"
	gettxout "txid" n ( includemempool )
	gettxoutsetinfo
	getunconfirmedbalance
	getwalletinfo
	getwork ( "data" )
	help ( "command" )
	importprivkey "bitcoinprivkey" ( "label" rescan )
	importwallet "filename"
	keypoolrefill ( newsize )
	listaccounts ( minconf )
	listaddressgroupings
	listlockunspent
	listreceivedbyaccount ( minconf includeempty )
	listreceivedbyaddress ( minconf includeempty )
	listsinceblock ( "blockhash" target-confirmations )
	listtransactions ( "account" count from )
	listunspent ( minconf maxconf ["address",...] )
	lockunspent unlock [{"txid":"txid","vout":n},...]
	move "fromaccount" "toaccount" amount ( minconf "comment" )
	Using Bitcoin Core’s
	ping
	sendfrom "fromaccount" "tobitcoinaddress" amount ( minconf "comment" "commentto" )
	sendmany "fromaccount" {"address":amount,...} ( minconf "comment" )
	sendrawtransaction "hexstring" ( allowhighfees )
	sendtoaddress "bitcoinaddress" amount ( "comment" "comment-to" )
	setaccount "bitcoinaddress" "account"
	setgenerate generate ( genproclimit )
	settxfee amount
	signmessage "bitcoinaddress" "message"
	signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )
	stop
	submitblock "hexdata" ( "jsonparametersobject" )
	validateaddress "bitcoinaddress"
	verifychain ( checklevel numblocks )
	verifymessage "bitcoinaddress" "signature" "message"
	walletlock
	walletpassphrase "passphrase" timeout
	walletpassphrasechange "oldpassphrase" "newpassphrase"

##从比特币核心客户端的状态中获取消息

命令：*getinfo*

比特币的*getinfo* RPC命令显示比特币网络节点、钱包、区块链数据库状态的基础信息，使用*bitcoin-cli来运行：

	$ bitcoin-cli getinfo
	{
		"version" : 90000,
		"protocolversion" : 70002,
		"walletversion" : 60000,
		"balance" : 0.00000000,
		"blocks" : 286216,
		"timeoffset" : -72,
		"connections" : 4,
		"proxy" : "",
		"difficulty" : 2621404453.06461525,
		"testnet" : false,
		"keypoololdest" : 1374553827,
		"keypoolsize" : 101,
		"paytxfee" : 0.00000000,
		"errors" : ""
	}

数据以JavaScript对象符号（JSON）格式返回，这种格式不仅可以轻易被编程语言“消费”，对人来说，也是易于阅读的。在数据中，我们可以看到比特币软件客户端的版本号（90000），协议版本号（70002），钱包版本（60000）。我们也可以看到钱包的余额，当前为0。还能看到区块高度，告诉我们客户端总共看到了多少区块（286216）。我们也看到各种有关比特币网络和当前客户端相关设置的统计信息。我们将在本章剩余部分更详细的了解这些设置。

![notes](notes.png)这将需要一些时间，也许超过一天，等待bitcoind客户端从其他比特币客户端下载区块，以“追赶上”当前的区块链高度。你可以通过getinfo查看已知的区块来检查进度。

##钱包设置和加密

命令：*encryptwallet, walletpassphrase*

在开始创建密钥和其他命令前，你需要首先利用密码来给钱包加密。在这个例子中，我们使用*encryptwallet*命令和密码“foo”，显然用更加强壮和复杂的密码替代“foo”是必须的！

	$ bitcoin-cli encryptwallet foo
	wallet encrypted; Bitcoin server stopping, restart to run with encrypted wallet. The keypool has been flushed, you need to make a new backup.
	$

你可以重新运行*getinfo*来检查钱包是否已经加密。这次，你会注意到有个新的条目叫*unlocked_until*。这是一个计数器，显示钱包解密密码在内存中存储，保持钱包解锁状态的时间。首先，这个会被设为0，代表钱包是被锁定的：

	$ bitcoin-cli getinfo
	{
		"version" : 90000,
	#[... other information...]
		"unlocked_until" : 0,
		"errors" : ""
	}
	$

为了解锁钱包，发出*walletpassphrase*命令，它包含两个参数--密码、直到钱包重新锁定的超时秒数（时间计数器）：

	$ bitcoin-cli walletpassphrase foo 360
	$

你可以重新运行*getinfo*确认钱包是否已解锁以及超时时间：

	$ bitcoin-cli getinfo
	{
		"version" : 90000,
	#[... other information ...]
		"unlocked_until" : 1392580909,
		"errors" : ""
	}

##钱包备份，明文导出，恢复
命令：*backupwallet, importwallet, dumpwallet*

接下来，我们练习创建钱包备份文件，然后从备份文件中恢复钱包。使用*backupwallet*命令来备份，提供文件名作为命令参数。这里，我们将钱包备份到文件*wallet.backup*中：

	$ bitcoin-cli backupwallet wallet.backup
	$

现在，利用*importwallet*来从备份文件中恢复钱包。如果钱包是锁定状态的，你需要先进行解锁（在接下来的章节中查看*walletpassphrase*）。

	$ bitcoin-cli importwallet wallet.backup
	$

*dumpwallet*命令可用于将钱包导出到人眼可读的文本文件：

	$ bitcoin-cli dumpwallet wallet.txt
	$ more wallet.txt
	# Wallet dump created by Bitcoin v0.9.0rc1-beta (2014-01-31 09:30:15 +0100)
	# * Created on 2014-02- 8dT20:34:55Z
	# * Best block at time of backup was 286234 (0000000000000000f74f0bc9d3c186267bc45c7b91c49a0386538ac24c0d3a44),
	#   mined on 2014-02- 8dT20:24:01Z
	
	KzTg2wn6Z8s7ai5NA9MVX4vstHRsqP26QKJCzLg4JvFrp6mMaGB9 2013-07- 4dT04:30:27Z change=1 # addr=16pJ6XkwSQv5ma5FSXMRPaXEYrENCEg47F
	Kz3dVz7R6mUpXzdZy4gJEVZxXJwA15f198eVui4CUivXotzLBDKY 2013-07- 4dT04:30:27Z change=1 # addr=17oJds8kaN8LP8kuAkWTco6ZM7BGXFC3gk
	[... many more keys ...]
	
	$

##钱包地址和接收交易

命令：*getnewaddress, getreceivedbyaddress, listtransactions, getaddressesbyaccount, getbalance*

比特币参考客户端维护着一个地址池，这个大小在命令*getinfo*的输出项*keypoolsize*中展示。这些地址是自动生成，可用于公共接收地址或者零钱地址。为取得一个这种地址，使用*getnewaddress*命令：

	$ bitcoin-cli getnewaddress
	1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL

现在，我们可以从外部钱包（假设你在交易所，网络钱包或者在其他地方运行的bitcoind钱包中已经拥有一些比特币），通过地址发送一笔小额的比特币到我们的bitcoind钱包。在这个例子中，我们将发送50毫比特（0.050比特币）到之前这个地址。

我们现在可以询问bitcoind客户端通过这个地址接收到比特币金额，指定需要多少次确认，一笔资金才计入余额中，我们将指定0确认。从另一个钱包发送比特币几秒后，我们将看到它在钱包中反映出来。我们使用*getreceivedbyaddress*命令并结合地址以及0确认次数来查看：

	$ bitcoin-cli getreceivedbyaddress 1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL 0
	0.050000

如果省略掉命令最后一个0，我们将只能看到经过至少*minconf*次确认的金额，*minconf*是最少确认次数的设置值，未达到这个确认次数，交易不会计入余额。*minconf*设置值是在bitcoind配置文件中设置的。因为发送这个比特币的交易仅仅发生在几秒前，它尚未被确认，所以我们看到它只列出了一个0余额：

	$ bitcoin-cli getreceivedbyaddress 1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL
	0.00000000

钱包接收到的所有交易也可以利用*listtransactions*命令列出来：

	$ bitcoin-cli listtransactions
	[
	    {
	        "account" : "",
	        "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
	        "category" : "receive",
	        "amount" : 0.05000000,
	        "confirmations" : 0,
	        "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
	        "time" : 1392660908,
	        "timereceived" : 1392660908
	    }
	]

我们还可以利用*getaddressesbyaccount*命令列出钱包中的所有地址：

	$ bitcoin-cli getaddressesbyaccount ""
	[
	    "1LQoTPYy1TyERbNV4zZbhEmgyfAipC6eqL",
	    "17vrg8uwMQUibkvS2ECRX4zpcVJ78iFaZS",
	    "1FvRHWhHBBZA8cGRRsGiAeqEzUmjJkJQWR",
	    "1NVJK3JsL41BF1KyxrUyJW5XHjunjfp2jz",
	    "14MZqqzCxjc99M5ipsQSRfieT7qPZcM7Df",
	    "1BhrGvtKFjTAhGdPGbrEwP3xvFjkJBuFCa",
	    "15nem8CX91XtQE8B1Hdv97jE8X44H3DQMT",
	    "1Q3q6taTsUiv3mMemEuQQJ9sGLEGaSjo81",
	    "1HoSiTg8sb16oE6SrmazQEwcGEv8obv9ns",
	    "13fE8BGhBvnoy68yZKuWJ2hheYKovSDjqM",
	    "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
	    "1KHUmVfCJteJ21LmRXHSpPoe23rXKifAb2",
	    "1LqJZz1D9yHxG4cLkdujnqG5jNNGmPeAMD"
	]

最后，命令*getbalance*可以显示钱包的全部余额，它将合并所有经过至少*minconf*次确认的交易的金额。

	$ bitcoin-cli getbalance
	0.05000000

现在，我们来看看前面利用*gettransaction*命令列出的传入交易。我们可以通过交易哈希值提取到一笔交易，在*gettransaction*命令中，它是*txid*的值。

	$ bitcoin-cli gettransaction 9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3
	{
	    "amount" : 0.05000000,
	    "confirmations" : 0,
	    "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
	    "time" : 1392660908,
	    "timereceived" : 1392660908,
	    "details" : [
	        {
	            "account" : "",
	            "address" : "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL",
	            "category" : "receive",
	            "amount" : 0.05000000
	        }
	    ]
	}

![notes](notes.png)在未确认前交易ID不具有权威性。区块链中交易哈希值缺失不意味着交易未被执行。这被称之为“交易可塑性性”，因为交易哈希可以在区块确认前被修改。一旦确认，*txid*就是不变的，权威的。

通过命令*gettransaction*显示的交易形式是一种简化的形式。为了获取完整交易代码并解码它，我们需要利用两个命令：*getrawtransaction*和*decoderawtransaction*。首先，*getrawtransaction*取交易哈希（*txid*）作为参数，并返回一个“原始”的十六进制字符串，就像它在比特币网络上的样子。

	$ bitcoin-cli getrawtransaction 9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66
	c309acbae2c14ae3
	
	0100000001d717279515f88e2f56ce4e8a31e2ae3e9f00ba1d0add648e80c480ea22e0c7d3000000
	008b483045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b3
	02203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba2014104793ac8
	a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b884ac5b5b6dede05ba84727e34
	c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5ceaffffffff02404b4c00000000001976a91407bd
	b518fa2e6089fd810235cf1100c9c13d1fd288ac1f312906000000001976a914107b7086b3151893
	5c8d28703d66d09b3623134388ac00000000

为了解码这些十六进制字符串，需要使用*decoderawtransaction*命令。拷贝粘贴这些十六进制作为*decoderawtransaction*的第一个参数，获取完整的以JSON数据结构解析的内容。（出于格式化需要，十六进制字符串在以下例子中被截短了）：

	$ bitcoin-cli decoderawtransaction 0100000001d717279515f88e2f56ce4e8a31e2ae3e9f00
	ba1d0add648e80c480ea22e0c7d3000000008b483045022100a4ebbeec83225dedead659bbde7da3d
	026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d3
	4c5b9b2ac1bd193dfba2014104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65
	e4c4b884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5ceaffffffff
	02404b4c00000000001976a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac1f312906000
	000001976a914107b7086b31518935c8d28703d66d09b3623134388ac00000000

	{
	    "txid" : "9ca8f969bd3ef5ec2a8685660fdbf7a8bd365524c2e1fc66c309acbae2c14ae3",
	    "version" : 1,
	    "locktime" : 0,
	    "vin" : [
	        {
	            "txid" : "d3c7e022ea80c4808e64dd0a1dba009f3eaee2318a4ece562f8ef815952717d7",
	            "vout" : 0,
	            "scriptSig" : {
	                "asm" : "3045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba20104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5cea",
	                "hex": "483045022100a4ebbeec83225dedead659bbde7da3d026c8b8e12e61a2df0dd0758e227383b302203301768ef878007e9ef7c304f70ffaf1f2c975b192d34c5b9b2ac1bd193dfba2014104793ac8a58ea751f9710e39aad2e296cc14daa44fa59248be58ede65e4c4b884ac5b5b6dede05ba84727e34c8fd3ee1d6929d7a44b6e111d41cc79e05dbfe5cea"
	            },
	            "sequence" : 4294967295
	        }
	    ],
	    "vout" : [
	        {
	            "value" : 0.05000000,
	            "n" : 0,
	            "scriptPubKey" : {
	                "asm" : "OP_DUP OP_HASH160 07bdb518fa2e6089fd810235cf1100c9c13d1fd2 OP_EQUALVERIFY OP_CHECKSIG",
	                "hex" : "76a91407bdb518fa2e6089fd810235cf1100c9c13d1fd288ac",
	                "reqSigs" : 1,
	                "type" : "pubkeyhash",
	                "addresses" : [
	                    "1hvzSofGwT8cjb8JU7nBsCSfEVQX5u9CL"
	                ]
	            }
	        },
	        {
	            "value" : 1.03362847,
	            "n" : 1,
	            "scriptPubKey" : {
	                "asm" : "OP_DUP OP_HASH160 107b7086b31518935c8d28703d66d09b36231343 OP_EQUALVERIFY OP_CHECKSIG",
	                "hex" : "76a914107b7086b31518935c8d28703d66d09b3623134388ac",
	                "reqSigs" : 1,
	                "type" : "pubkeyhash",
	                "addresses" : [
	                    "12W9goQ3P7Waw5JH8fRVs1e2rVAKoGnvoy"
	                ]
	            }
	        }
	    ]
	}

这里的交易解码显示了一个交易的所有组成元素，包括交易输入和输出。在这个例子中，我们看到交易往我们的新地址记录50毫比特，使用了一个输入生成了两个输出。这个交易的输入是从上一笔已确认交易的输出（显示为*vin*下*d3c7*开始的*txid*）。两个输出一个是50毫比特的入账，另一笔是交易找零。
