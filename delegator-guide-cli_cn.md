# 委托人指南 (CLI)

This document contains all the necessary information for delegators to interact with the Cosmos Hub through the Command-Line Interface (CLI).
本文介绍了如果使用Cosmos Hub的命令行交互（CLI）程序实现通证委托的相关知识和操作步骤。 

It also contains instructions on how to manage accounts, restore accounts from the fundraiser and use a ledger nano device.
同时，本文也包括了如何管理账户，如何从筹款人那里回复账户，以及如何使用一个硬件钱包的相关知识。 

::: danger 危险警告
**Very Important**: Please assure that you follow the steps described hereinafter
carefully, as negligence in this significant process could lead to an indefinite
loss of your Atoms. Therefore, read through the following instructions in their 
entirety prior to proceeding and reach out to us in case you need support.
**重要提示**：请务必按照下面的操作步骤谨慎操作，过程中的任何错误都有可能导致您永远失去所拥有的通证。因此，请再开始操作之前先仔细阅读全文，如果有任何问题可以联系我们获得支持。 

Please also note that you are about to interact with the Cosmos Hub, a
blockchain technology containing highly experimental software. While the
blockchain has been developed in accordance to the state of the art and audited
with utmost care, we can nevertheless expect to have issues, updates and bugs.
Furthermore, interaction with blockchain technology requires
advanced technical skills and always entails risks that are outside our control.
By using the software, you confirm that you understand the inherent risks
associated with cryptographic software (see also risk section of the 
[Interchain Cosmos Contribution terms](https://github.com/cosmos/cosmos/blob/master/fundraiser/Interchain%20Cosmos%20Contribution%20Terms%20-%20FINAL.pdf)) and that the Interchain Foundation and/or 
the Tendermint Team may not be held liable for potential damages arising out of the use of the
software. Any use of this open source software released under the Apache 2.0 license is
done at your own risk and on a "AS IS" basis, without warranties or conditions
of any kind.

另请注意，您即将要与Cosmos Hub发生进行互动，Cosmos Hub是仍然是一个包含高度实验性的区块链技术软件。虽然
Cosmos Hub区块链是应用现有最新技术开发并经过审核的，但我们仍然可能会在运行时遇到问题，仍然需要不断更新和修复漏洞。此外，使用区块链技术仍然要求有很高的技术能力，并且有可能遇到我们无法预知和控制的风险。使用Cosmos Hub前，您需要充分了解可能发生的与加密软件相关联的风险（请参考[Cosmos跨链贡献条款](https://github.com/cosmos/cosmos/blob/master/fundraiser/Interchain%20Cosmos%20Contribution%20Terms%20-%20FINAL.pdf)中关于风险的部分条款），并且我们跨链基金会和(或)Tendermint团队对于因为使用本产品而可能产生的损失不承担任何责任。使用Cosmos Hub需要遵守Apache 2.0开源软件授权条款，在此授权下，使用者需要自己承担所有责任，所使用的软件按“现状”提供且不提供任何形式的保障或条件。 
:::

Please exercise extreme caution!
请务必谨慎行事！

## Table of contents

- [委托人指南 (CLI)](#%E5%A7%94%E6%89%98%E4%BA%BA%E6%8C%87%E5%8D%97-cli)
  - [Table of contents](#table-of-contents)
  - [安装 `gaiacli`](#%E5%AE%89%E8%A3%85-gaiacli)
  - [Cosmos Accounts Cosmos账户](#cosmos-accounts-cosmos%E8%B4%A6%E6%88%B7)
    - [Restoring an account from the fundraiser 通过募资人恢复一个账户](#restoring-an-account-from-the-fundraiser-%E9%80%9A%E8%BF%87%E5%8B%9F%E8%B5%84%E4%BA%BA%E6%81%A2%E5%A4%8D%E4%B8%80%E4%B8%AA%E8%B4%A6%E6%88%B7)
      - [On a ledger device 恢复到一个数字钱包设备](#on-a-ledger-device-%E6%81%A2%E5%A4%8D%E5%88%B0%E4%B8%80%E4%B8%AA%E6%95%B0%E5%AD%97%E9%92%B1%E5%8C%85%E8%AE%BE%E5%A4%87)
      - [On a computer 在计算机上](#on-a-computer-%E5%9C%A8%E8%AE%A1%E7%AE%97%E6%9C%BA%E4%B8%8A)
    - [Creating an account 创建一个账户](#creating-an-account-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E8%B4%A6%E6%88%B7)
      - [Using a ledger device 使用数字钱包设备](#using-a-ledger-device%08-%E4%BD%BF%E7%94%A8%E6%95%B0%E5%AD%97%E9%92%B1%E5%8C%85%E8%AE%BE%E5%A4%87)
      - [Using a computer 用一台电脑](#using-a-computer-%E7%94%A8%E4%B8%80%E5%8F%B0%E7%94%B5%E8%84%91)
  - [Accessing the Cosmos Hub network 访问Cosmos Hub网络](#accessing-the-cosmos-hub-network-%08%E8%AE%BF%E9%97%AEcosmos-hub%E7%BD%91%E7%BB%9C)
    - [Running your own full-node 运行您自己的全功能节点](#running-your-own-full-node-%E8%BF%90%E8%A1%8C%E6%82%A8%E8%87%AA%E5%B7%B1%E7%9A%84%E5%85%A8%E5%8A%9F%E8%83%BD%E8%8A%82%E7%82%B9)
    - [Connecting to a remote full-node 连接到一个远端全功能节点](#connecting-to-a-remote-full-node-%08%E8%BF%9E%E6%8E%A5%E5%88%B0%E4%B8%80%E4%B8%AA%E8%BF%9C%E7%AB%AF%E5%85%A8%E5%8A%9F%E8%83%BD%E8%8A%82%E7%82%B9)
  - [Setting up `gaiacli` 设置 `gaiacli`](#setting-up-gaiacli-%08%E8%AE%BE%E7%BD%AE-gaiacli)
  - [Querying the state 状态查询](#querying-the-state-%E7%8A%B6%E6%80%81%E6%9F%A5%E8%AF%A2)
  - [Sending Transactions 发起交易](#sending-transactions-%E5%8F%91%E8%B5%B7%E4%BA%A4%E6%98%93)
    - [A note on gas and fees 关于gas 和 fee](#a-note-on-gas-and-fees-%08%E5%85%B3%E4%BA%8Egas-%E5%92%8C-fee)
    - [Bonding Atoms and Withdrawing rewards 抵押Atom通证和提取奖励](#bonding-atoms-and-withdrawing-rewards-%E6%8A%B5%E6%8A%BCatom%E9%80%9A%E8%AF%81%E5%92%8C%E6%8F%90%E5%8F%96%E5%A5%96%E5%8A%B1)
  - [Participating in governance 参与链上治理](#participating-in-governance-%E5%8F%82%E4%B8%8E%E9%93%BE%E4%B8%8A%E6%B2%BB%E7%90%86)
      - [Primer on governance 链上治理入门](#primer-on-governance-%E9%93%BE%E4%B8%8A%E6%B2%BB%E7%90%86%E5%85%A5%E9%97%A8)
      - [In practice 实践练习](#in-practice-%E5%AE%9E%E8%B7%B5%E7%BB%83%E4%B9%A0)
    - [Signing transactions from an offline computer 从一台离线电脑上签署交易](#signing-transactions-from-an-offline-computer-%08%E4%BB%8E%E4%B8%80%E5%8F%B0%E7%A6%BB%E7%BA%BF%E7%94%B5%E8%84%91%E4%B8%8A%E7%AD%BE%E7%BD%B2%E4%BA%A4%E6%98%93)

## 安装 `gaiacli` 

`gaiacli`: This is the command-line interface to interact with a `gaiad` full-node. 
`gaiacli`: 与`gaiad`全节点交互的命令行用户界面。 

::: warning 警告
**Please check that you download the latest stable release of `gaiacli` that is available**
**请检查并且确认你下载的`gaiacli`是可获得的最新稳定版本**
:::

[**Download the binaries**]
**下载已编译代码**
Not available yet. 
暂不提供

[**Install from source**]
[**通过源代码安装**](https://cosmos.network/docs/gaia/installation.html)

::: tip 提示 
`gaiacli` is used from a terminal. To open the terminal, follow these steps:
`gaiacli` 需要通过操作系统的终端窗口使用，打开操作系统终端窗口的步骤如下所示： 
- **Windows**: `开始` > `所有程序` > `附件` > `终端`
- **MacOS**: `访达` > `应用程序` > `实用工具` > `终端`
- **Linux**: `Ctrl` + `Alt` + `T`
:::

## Cosmos Accounts Cosmos账户

At the core of every Cosmos account, there is a seed, which takes the form of a 12 or 24-words mnemonic. From this mnemonic, it is possible to create any number of Cosmos accounts, i.e. pairs of private key/public key. This is called an HD wallet (see [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) for more information on the HD wallet specification).
每个Cosmos账户的核心基础是一个包含12或24个词的助记词组种子（seed），通过这个助记词可以生成任意数量的Cosmos账户，例如，一组私钥/公钥对。这被称为一个硬件钱包（跟多硬件钱包相关说明请参见[BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)）  

```
        账户 0                            账户 1                              账户 2

+------------------+              +------------------+               +------------------+
|                  |              |                  |               |                  |
|       地址 0      |              |      地址 1      |               |       地址 2      |
|        ^         |              |        ^         |               |        ^         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        +         |              |        +         |               |        +         |
|       公钥 0      |              |      公钥 1      |               |       公钥 2      |
|        ^         |              |        ^         |               |        ^         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        +         |              |        +         |               |        +         |
|       私钥 0      |              |      私钥 1      |               |       私钥 2      |
|        ^         |              |        ^         |               |        ^         |
+------------------+              +------------------+               +------------------+
         |                                 |                                  |
         |                                 |                                  |
         |                                 |                                  |
         +--------------------------------------------------------------------+
                                           |
                                           |
                                 +---------+---------+
                                 |                   |
                                 |  助记词 (Seed)     |
                                 |                   |
                                 +-------------------+
```

The funds stored in an account are controlled by the private key. This private key is generated using a one-way function from the mnemonic. If you lose the private key, you can retrieve it using the mnemonic. However, if you lose the mnemonic, you will lose access to all the derived private keys. Likewise, if someone gains access to your mnemonic, they gain access to all the associated accounts. 
私钥是控制一个账户中所存资产的钥匙。私钥是通过助记词单向产生的。如果您不小心丢失了私钥，你可以通过助记词恢复。 然而，如果你丢失了助记词，那么你就有可能失去对由这个助记词产生的所有私钥的控制。同样，如果有人获得了你的助记词，他们就可以操作所有相关联的账户。  

::: danger 警告
**Do not lose or share your 12 words with anyone. To prevent theft or loss of funds, it is best to ensure that you keep multiple copies of your mnemonic, and store it in a safe, secure place and that only you know how to access. If someone is able to gain access to your mnemonic, they will be able to gain access to your private keys and control the accounts associated with them.**
**千万不要丢失或者告诉其他人你的12个词的助记词组。 为了防止资产被盗或者丢失，您最好多备份几份助记词， 并且把它们存放在只有您知道的安全地方， 这样做将有助于保障您的私钥以及相关账户的安全。**
:::

The address is a public string with a human-readable prefix (e.g. `cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg`) that identifies your account. When someone wants to send you funds, they send it to your address. It is computationally infeasible to find the private key associated with a given address. 

Cosmos地址是一个以可读词开头的字符串(比如`cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg`) 

### Restoring an account from the fundraiser 通过募资人恢复一个账户

::: tip 提示
*NOTE: This section only concerns fundraiser participants*
*注：这部分内容仅适用于众筹活动参与者*
:::

If you participated in the fundraiser, you should be in possession of a 12-words mnemonic. Newly generated mnemonics use 24 words, but 12-word mnemonics are also compatible with all the Cosmos tools. 
如果您是众筹的参与者，你应该有一个12个词的助记词组。新产生的助记词用24个词，但是12个词的助记词组也兼容所有Cosmos工具。 

#### On a ledger device 恢复到一个数字钱包设备

At the core of a ledger device, there is a mnemonic used to generate accounts on multiple blockchains (including the Cosmos Hub). Usually, you will create a new mnemonic when you initialize your ledger device. However, it is possible to tell the ledger device to use a mnemonic provided by the user instead. Let us go ahead and see how you can input the mnemonic you obtained during the fundraiser as the seed of your ledger device. 
一个数字钱包设备的核心是采用一个主机词在多个区块链上创建账户（包括Cosmos hub）。 通常，您会在初始化您的数字钱包设备时创建一个新的助记词。 然而，您也可以告诉钱包设备用您提供的一个助记词来替代创建一个新助记词。 让我们一起来看如何将您在参与众筹时获得的助记词设定为一个数字钱包设备的种子

::: warning 警告
*NOTE: To do this, **it is preferable to use a brand new ledger device.**. Indeed, there can be only one mnemonic per ledger device. If, however, you want to use a ledger that is already initialized with a seed, you can reset it by going in `Settings`>`Device`>`Reset All`. **Please note that this will wipe out the seed currently stored on the device. If you have not properly secured the associated mnemonic, you could lose your funds!!!***

*注意：**最好使用一个新的钱包设备**来恢复您的Cosmos账户。确实，每个数字钱包设备只能有一个助记词。 当然，您可以通过 `设置`>`设备`>`重置所有` 将一个已经有助记词（用过的）数字钱包重新初始化。**但请注意，这样会清空您设备中现有的助记词，如果您没有做好备份的话，有可能会丢失您的资产***
:::

The following steps need to be performed on an un-initialized ledger device:
对于一个没有初始化的数字钱包设备，您需要做如下操作。 

1. Connect your ledger device to the computer via USB
2. Press both buttons
3. Do **NOT** choose the "Config as a new device" option. Instead, choose "Restore Configuration"
4. Choose a PIN
5. Choose the 12 words option
6. Input each of the words you got during the fundraiser, in the correct order. 

1. 将您的数字钱包设备通过USB与电脑链接
2. 同时按下两个按钮
3. **不要**选择“配置一个新设备”选项，而是选择“恢复配置”
4. 选择一个PIN
5. 选择12个词选项
6. 逐个按顺序输入您在众筹时获得的12个助记词 

Your ledger is now correctly set up with your fundraiser mnemonic! Do not lose this mnemonic! If your ledger is compromised, you can always restore a new device again using the same mnemonic.
现在，您的钱包已经正确的设置好您在众筹时获得的助记词！千万不要丢失您的助记词！任何时候您的钱包设备出现问题，您都可以通过助记词在一个新的钱包设备上恢复所有账户。 

Next, click [here](#using-a-ledger-device) to learn how to generate an account. 
接下来，请点击[这里](#using-a-ledger-device)来学习如何产生一个账户。

#### On a computer 在计算机上

::: warning 警告
**NOTE: It is more secure to perform this action on an offline computer**
**注意： 在一台没有联网的计算机上执行以下操作会更加安全**
::: 

To restore an account using a fundraiser mnemonic and store the associated encrypted private key on a computer, use the following command:
如果您希望同过众筹时获得的助记词恢复账户并保存相关联的私钥，请按以下步骤操作： 

```bash
gaiacli keys add <yourKeyName> --recover
```

You will be prompted to input a passphrase that is used to encrypt the private key of account `0` on disk. Each time you want to send a transaction, this password will be required. If you lose the password, you can always recover the private key with the mnemonic. 
首先，您需要输入一个密码来对您硬盘上账户`0`的私钥进行加密。 每次您发出一笔交易时都将需要输入这个密码。 如果您丢失了密码，您可以通过助记词来恢复您的私钥。 

- `<yourKeyName>` is the name of the account. It is a reference to the account number used to derive the key pair from the mnemonic. You will use this name to identify your account when you want to send a transaction.
- `<yourKeyName>` 是账户名称，用来指代用助记词生成私钥/公钥对的Cosmos账户。在您发起交易时，这个账户名称被用来识别您的账户。 
  
- You can add the optional `--account` flag to specify the path (`0`, `1`, `2`, ...) you want to use to generate your account. By default, account `0` is generated. 
- 您可以通过增加 `--account` 标志来指定您账户生成的路径 (`0`, `1`, `2`, ...)， `0` 是缺省值。 


### Creating an account 创建一个账户

To create an account, you just need to have `gaiacli` installed. Before creating it, you need to know where you intend to store and interract with your private keys. The best options are to store them in an offline dedicated computer or a ledger device. Storing them on your regular online computer involves more risk, since anyone who infiltrates your computer through the internet could exfiltrate your private keys and steal your funds.
创建账户前，您需要先安装`gaiacli`，同时，您需要知道你希望在哪里保存和使用您的私钥。 最好的办法是把他们保持在一台没有上网的电脑或者一个硬件钱包设备里面。 将私钥保持在一台上网的电脑里面时比较危险的，任何人通过网络攻击都有可能获取您的私钥，进而盗取您的资产。 

#### Using a ledger device 使用数字钱包设备

::: warning 警告
**Only use Ledger devices that you bought factory new or trust fully**
**建议仅使用您新买的钱包设备或者时您足够信任的设备**
:::

When you initialize your ledger, a 24-word mnemonic is generated and stored in the device. This mnemonic is compatible with Cosmos and Cosmos accounts can be derived from it. Therefore, all you have to do is make your ledger compatible with `gaiacli`. To do so, you need to go through the following steps:
当您初始化您的钱包设备时，设备会产生一个24个词的助记词组。这个助记词组和Cosmos是兼容的，我们可以通过这个主机词组创建Cosmos账户。 所以， 您需要做的是确认您的钱包设备兼容`gaiacli`，通过下面的步骤可以帮助您确认您的设备是否兼容：

1. Download the Ledger Live app [here](https://www.ledger.com/pages/ledger-live). 
2. Connect your ledger via USB and update to the latest firmware
3. Go to the ledger live app store, and download the "Cosmos" application (this can take a while). **Note: You may have to enable `Dev Mode` in the `Settings` of Ledger Live to be able to download the "Cosmos" application**. 
4. Navigate to the Cosmos app on your ledger device
   
5. 下载[Ledger Live应用](https://www.ledger.com/pages/ledger-live). 
6. 通过USB将钱包与计算机连接，并且将钱包固件升级到最新版本。 
7. 到Ledger Live钱包的应用商店下载”Cosmos“应用（这可能需要花些时间）。**下载”Cosmos“应用程序需要在Ledger Live钱包`seeting`选项中激活`Dev Mode`**

Then, to create an account, use the following command:
然后，通过以下命令创建账户：

```bash
gaiacli keys add <yourAccountName> --ledger 
```

- `<yourKeyName>` is the name of the account. It is a reference to the account number used to derive the key pair from the mnemonic. You will use this name to identify your account when you want to send a transaction.
- `<yourKeyName>` 是账户名称，用来指代用助记词生成私钥/公钥对的Cosmos账户。在您发起交易时，这个账户名称被用来识别您的账户。 
  
- You can add the optional `--account` flag to specify the path (`0`, `1`, `2`, ...) you want to use to generate your account. By default, account `0` is generated. 
- 您可以通过增加 `--account` 标志来指定您账户生成的路径 (`0`, `1`, `2`, ...)， `0` 是缺省值。

#### Using a computer 用一台电脑

::: warning 警告
**NOTE: It is more secure to perform this action on an offline computer**
**注意：在一台没有上网的电脑上操作会更加安全**
:::

To generate an account, just use the following command:
然后，通过以下命令创建账户：

```bash
gaiacli keys add <yourKeyName>
```

The command will generate a 24-words mnemonic and save the private and public keys for account `0` at the same time. You will be prompted to input a passphrase that is used to encrypt the private key of account `0` on disk. Each time you want to send a transaction, this password will be required. If you lose the password, you can always recover the private key with the mnemonic. 
这个命令会产生一个24个词的助记词组，并且同时保存账户 `0` 的私钥和公钥。 另外，您还需要输入一个密码来对您硬盘上账户`0`的私钥进行加密。 每次您发出一笔交易时都将需要输入这个密码。 如果您丢失了密码，您可以通过助记词来恢复您的私钥。 

::: danger 危险提示
**Do not lose or share your 12 words with anyone. To prevent theft or loss of funds, it is best to ensure that you keep multiple copies of your mnemonic, and store it in a safe, secure place and that only you know how to access. If someone is able to gain access to your mnemonic, they will be able to gain access to your private keys and control the accounts associated with them.**
**千万不要丢失或者告诉其他人你的12个词的助记词组。 为了防止资产被盗或者丢失，您最好多备份几份助记词， 并且把它们存放在只有您知道的安全地方，如果有人取得您的助记词，那么他也就取得了您的私钥并且可以控制相关联的账户。**
::: 

::: warning 警告
After you have secured your mnemonic (triple check!), you can delete bash history to ensure no one can retrieve it:
在确认已经安全保存好您的助记词以后（至少3编！），你可以用如下命令清楚终端窗口中的命令历史记录，以防有人通过历史记录获得您的助记词。 

```bash
history -c
rm ~/.bash_history
```
:::

You can generate more accounts from the same mnemonic using the following command:
你可以用以下命令使用助记词生成多个账户： 

```bash
gaiacli keys add <yourKeyName> --recover --account 1
```

- `<yourKeyName>` is the name of the account. It is a reference to the account number used to derive the key pair from the mnemonic. You will use this name to identify your account when you want to send a transaction.
- - `<yourKeyName>` 是账户名称，用来指代用助记词生成私钥/公钥对的Cosmos账户。在您发起交易时，这个账户名称被用来识别您的账户。 
  
- You can add the optional `--account` flag to specify the path (`0`, `1`, `2`, ...) you want to use to generate your account. By default, account `0` is generated. 
- 您可以通过增加 `--account` 标志来指定您账户生成的路径 (`0`, `1`, `2`, ...)， `0` 是缺省值。

This command will prompt you to input a passphrase as well as your mnemonic. Change the account number to generate a different account.
这条命令需要您输入一个密码。改变账号就代表生成了一个新的账户。  

## Accessing the Cosmos Hub network 访问Cosmos Hub网络

In order to query the state and send transactions, you need a way to access the network. To do so, you can either run your own full-node, or connect to someone else's.
为了查询网络状态和发起交易，你需要通过自建一个全功能节点，或者连接到其他人的全功能节点访问Cosmos Hub网络

::: danger 警告
**NOTE: Do not share your mnemonic (12 or 24 words) with anyone. The only person who should ever need to know it is you. This is especially important if you are ever approached via email or direct message by someone requesting that you share your mnemonic for any kind of blockchain services or support. No one from Cosmos, the Tendermint team or the Interchain Foundation will ever send an email that asks for you to share any kind of account credentials or your mnemonic."**.
**注意： 请不要与任何人分享您的助记词，您是唯一需要知道这些助记词的人。如果任何人通过邮件或者其他社交媒体向您要求您提供您的助记词，那就需要警惕了。 请记住，Cosmos和Tendermint团队，或者跨链基金会都永远不会通过邮件要求您提供您的账户密码或者助记词。**
::: 

### Running your own full-node 运行您自己的全功能节点

This is the most secure option, but comes with relatively high resource requirements. In order to run your own full-node, you need good bandwidth and at least 1TB of disk space. 
这是最安全的途径，但需要相当多的资源。您需要有较大的带宽和至少1TB的磁盘容量来运行一个全功能节点。  

You will find the tutorial on how to install `gaiad` [here](https://cosmos.network/docs/gaia/installation.html), and the guide to run a full-node [here](https://cosmos.network/docs/gaia/join-testnet.html).
 `gaiad`的安装教程在[这里](https://cosmos.network/docs/gaia/installation.html)， 而如何运行一个全节点指导在[这里](https://cosmos.network/docs/gaia/join-testnet.html)

### Connecting to a remote full-node 连接到一个远端全功能节点

If you do not want or cannot run your own node, you can connect to someone else's full-node. You should pick an operator you trust, because a malicious operator could return  incorrect query results or censor your transactions. However, they will never be able to steal your funds, as your private keys are stored locally on your computer or ledger device. Possible options of full-node operators include validators, wallet providers or exchanges. 
如果您不想或者没有能力运行一个全功能节点，您也可以连接到其他人的全功能节点。您需要谨慎的选择一个可信的运营商，因为恶意的运营商往往会向您反馈错误的查询结果，或者对您的交易进行监控。 然而，他们永远也无法盗取您的资产，因为您的私钥仅保持在您的本地计算机或者钱包设备中。 可能提供全节点的运营商包括验证人，钱包供应商或者交易所。 

In order to connect to the full-node, you will need an address of the following form: `https://77.87.106.33:26657` (*Note: This is a placeholder*). This address has to be communicated by the full-node operator you choose to trust. You will use this address in the [following section](#setting-up-gaiacli).
连接到其他人提供的全节点，你需要一个全节点地址，如`https://77.87.106.33:26657`。 这个地址是您的供应商提供的一个可信的接入地址。你会在下一节中用到这个地址。 

## Setting up `gaiacli` 设置 `gaiacli`

::: tip 提示
**Before setting up `gaiacli`, make sure you have set up a way to [access the Cosmos Hub network](#accessing-the-cosmos-hub-network)**
**在开始设置 `gaiacli`前，请确认你已经可以[访问Cosmos Hub网络](#accessing-the-cosmos-hub-network)**
:::

::: warning 警告
**Please check that you are always using the latest stable release of `gaiacli`**
**请确认您使用的`gaiacli`是最新的稳定版本**
:::

`gaiacli` is the tool that enables you to interact with the node that runs on the Cosmos Hub network, whether you run it yourself or not. Let us set it up properly.
`gaiacli` 是实现与Cosmos Hub网络上您自己运行的节点或者其他人运行的节点交互的工具，让我们来完成对它的配置。 

In order to set up `gaiacli`, use the following command:
您需要用下面的命令行完成对`gaiacli`的配置：

```bash
gaiacli config <flag> <value>
```

It allows you to set a default value for each given flag. 
此命名允许您为每个参数设置缺省值。 

First, set up the address of the full-node you want to connect to:
首先，设置你想要访问的全功能节点的地址：

```bash
gaiacli config node <host>:<port

// 样例: gaiacli config node https://77.87.106.33:26657
```

If you run your own full-node, just use `tcp://localhost:26657` as the address. 
如果你是运行你自己的全功能节点，可以使用 `tcp://localhost:26657` 作为地址。 

Then, let us set the default value of the `--trust-node` flag: 
然后，让我们设置 `--trust-node` 指标的缺省值。 

```bash
gaiacli config trust-node false

// Set to true if you run a light-client node, false otherwise
```

Finally, let us set the `chain-id` of the blockchain we want to interact with:
最后，让我们设置我们需要访问的区块链的 `chain-id` 

```bash
gaiacli config chain-id gos-6
```

## Querying the state 状态查询

::: tip 提示
**Before you can bond atoms and withdraw rewards, you need to [set up `gaiacli`](#setting-up-gaiacli)**
** 你在准备抵押ATOM通证和取回奖励前，需要先完成 [`gaiacli` 配置](#setting-up-gaiacli)**
:::

`gaiacli` lets you query all relevant information from the blockchain, like account balances, amount of bonded tokens, outstanding rewards, governance proposals and more. Next is a list of the most useful commands for delegator. 
`gaiacli` 可以帮助您获得所有区块链的相关信息， 比如账户余额，抵押通证数量，奖励，治理提案，以及其他信息。 下面是一组用于委托操作的命令

```bash
// query account balances and other account-related information
// 查询账户余额或者其他账户相关信息
gaiacli query account

// query the list of validators
// 查询验证人列表
gaiacli query staking validators

// query the information of a validator given their address 
// 查询指定地址的验证人的信息(e.g. cosmosvaloper1n5pepvmgsfd3p2tqqgvt505jvymmstf6s9gw27)
gaiacli query staking validator <validatorAddress>

// query all delegations made from a delegator given their address (e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg)
// 查询指定地址的验证人相关的所有委托信息 (e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg)
gaiacli query staking delegations <delegatorAddress>

// query a specific delegation made from a delegator (e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg) to a validator (e.g. cosmosvaloper1n5pepvmgsfd3p2tqqgvt505jvymmstf6s9gw27) given their addresses
// 查询从一个指定地址的委托人(e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg)和一个指定地址的验证人(e.g. cosmosvaloper1n5pepvmgsfd3p2tqqgvt505jvymmstf6s9gw27) 之间的委托交易
gaiacli query staking delegation <delegatorAddress> <validatorAddress>

// query the rewards of a delegator given a delegator address (e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg)
// 查询一个指定地址的委托人(e.g. cosmos10snjt8dmpr5my0h76xj48ty80uzwhraqalu4eg)所能获得的奖励情况
gaiacli query distr rewards <delegatorAddress> 

// query all proposals currently open for depositing
// 查询所有现在正等待抵押的提案
gaiacli query gov proposals --status deposit_period

// query all proposals currently open for voting
//查询所有现在正等待投票的填
gaiacli query gov proposals --status voting_period

// query a proposal given its proposalID
// 查询一个指定propsalID的提案信息
gaiacli query gov proposal <proposalID>
```

For more commands, just type:
需要了解跟多的命令，只需要用：

```bash
gaiacli query
```

For each command, you can use the `-h` or `--help` flag to get more information.
对于每条命令，您都可以使用`-h` 或 `--help` 参数来获得更多的信息。 

## Sending Transactions 发起交易

### A note on gas and fees 关于gas 和 fee

Transactions on the Cosmos Hub network need to include a transaction fee in order to be processed. This fee pays for the gas required to run the transaction. The formula is the following:
Cosmos Hub网络上的交易在被执行时需要支付 fee。 这个fee是用于支付执行交易所需的gas。 计算公式如下： 
```
fees = gas * gasPrices
```

The `gas` is dependent on the transaction. Different transaction require different amount of `gas`. The `gas` amount for a transaction is calculated as it is being processed, but there is a way to estimate it beforehand by using the `auto` value for the `gas` flag. Of course, this only gives an estimate. You can adjust this estimate with the flag `--gas-adjustment` (default `1.0`) if you want to be sure you provide enough `gas` for the transaction. 
 `gas` 的多少取决于交易类型，不同的交易类型会被收取不同的 `gas` 。每个交易的 `gas` 费是在实际执行过程中计算的，但我们可以通过设置 `gas` 参数中的 `auto` 值实现在交易前对 `gas` 费的估算，但这只是一个粗略的估计，你可以通过 `--gas-adjustment` (缺省值 `1.0`) 对预估的`gas` 值进行调节，以确保为交易支付足够的`gas` 。 

The `gasPrice` is the price of each unit of `gas`. Each validator sets a `min-gas-price` value, and will only include transactions that have a `gasPrice` greater than their `min-gas-price`. 
`gasPrice` 用于设置单位 `gas` 的价格. 每个验证人会设置一个最低 gas 价格`min-gas-price`, 并且只会将`gasPrice`大于`min-gas-price`的交易打包。 

The transaction `fees` are the product of `gas` and `gasPrice`. As a user, you have to input 2 out of 3. The higher the `gasPrice`/`fees`, the higher the chance that your transaction will get included in a block. 
交易的`fees` 是`gas` 和 `gasPrice`的乘积。作为一个用户，你需要输入3个参数中至少2个， `gasPrice`/`fees`的值越大，您的交易就越有机会被打包执行。 

### Bonding Atoms and Withdrawing rewards 抵押Atom通证和提取奖励

::: tip 提示
**Before you can bond atoms and withdraw rewards, you need to [set up `gaiacli`](#setting-up-gaiacli) and [create an account](#creating-an-account)**
**在您执行通证抵押或取回奖励之前，您需要完成[`gaiacli` 设置](#setting-up-gaiacli) 和 [创建账户](#creating-an-account)**
:::

::: warning 警告
**Before bonding Atoms, please read the [delegator faq](https://cosmos.network/resources/delegators) to understand the risk and responsabilities involved with delegating**
**在抵押通证前，请仔细阅读[委托者常见问题](https://cosmos.network/resources/delegators) 并且理解其中的风险和责任**
:::

::: warning 警告
**Note: These commands need to be run on an online computer. It is more secure to perform them commands using a ledger device. For the offline procedure, click [here](#signing-transactions-from-an-offline-computer).**
**注意：执行以下命令需要在一台与网络连接的计算机。用一个钱包设备执行这些命令会更安全。关于离线交易过程请看[这里](#signing-transactions-from-an-offline-computer).**
::: 

```bash
// Bond a certain amount of Atoms to a given validator
// 向指定验证人绑定一定数量的Atom通证
// 参数设定样例: <validatorAddress>=cosmosvaloper18thamkhnj9wz8pa4nhnp9rldprgant57pk2m8s, <amountToBound>=10000stake, <gasPrice>=0.001stake

gaiacli tx staking delegate <validatorAddress> <amountToBond> --from <delegatorKeyName> --gas auto --gas-prices <gasPrice>


// 提取所有的奖励
// 参数设定样例: <gasPrice>=0.001stake 

gaiacli tx distr withdraw-all-rewards --from <delegatorKeyName> --gas auto --gas-prices <gasPrice>


// Unbond a certain amount of Atoms from a given validator 
// 向指定验证人申请解绑一定数量的Atom通证
// You will have to wait 3 weeks before your Atoms are fully unbonded and transferrable 
// 解绑的通证需要3周后才能完全解锁并可以交易，
// 参数设定样例: <validatorAddress>=cosmosvaloper18thamkhnj9wz8pa4nhnp9rldprgant57pk2m8s, <amountToUnbound>=10000stake, <gasPrice>=0.001stake

gaiacli tx staking unbond <validatorAddress> <amountToUnbond> --from <delegatorKeyName> --gas auto --gas-prices <gasPrice>
```

::: 提示
If you use a connected Ledger, you will be asked to confirm the transaction on the device before it is signed and broadcast to the network
::: 
如果您是使用一个联网的钱包设备，在交易被广播到网络前您需要在设备上确认交易。 

To confirm that your transaction went through, you can use the following queries:
确认您的要以已经发出，可以用以下查询：

```bash
// your balance should change after you bond Atoms or withdraw rewards
// 您的账户余额在您抵押Atom通证或者取回奖励后会发生变化
gaiacli query account

// 您在抵押后应该能查到委托交易
gaiacli query staking delegations <delegatorAddress>

// this returns your tx if it has been included
// 如果交易已经被打包，将会返回交易记录（tx）
// use the tx hash that was displayed when you created the tx
// 在以下查询命令中可以使用显示的交易哈希值作为参数
gaiacli query tx <txHash>

```

Double check with a block explorer if you interact with the network through a trusted full-node. 
如果您是连接到一个可信全功能节点的话，您可以通过一个区块链浏览器做检查。 

## Participating in governance 参与链上治理

#### Primer on governance 链上治理入门

The Cosmos Hub has a built-in governance system that lets bonded Atom holders vote on proposals. There are three types of proposal:
Cosmos Hub有一个内建的治理系统，该系统允许抵押通证的持有人参与提案投票。系统现在支持3种提案类型：

- `Text Proposals`: These are the most basic type of proposals. They can be used to get the opinion of the network on a given topic. 
- `Text Proposals`: 这是最基本的一种提案类型，通常用于获得大家对某个网络治理意见的观点。 
- `Parameter Proposals`: These are used to update the value of an existing parameter.
- `Parameter Proposals`: 这种提案通常用于改变网络参数的设定。 
- `Software Upgrade Proposal`: These are used to propose an upgrade of the Hub's software.
- `Software Upgrade Proposal`: 这个提案用于升级Hub的软件。 

Any Atom holder can submit a proposal. In order for the proposal to be open for voting, it needs to come with a `deposit` that is greater than a parameter called `minDeposit`. The `deposit` need not be provided in its entirety by the submitter. If the initial proposer's `deposit` is not sufficient, the proposal enters the `deposit_period` status. Then, any Atom holder can increase the deposit by sending a `depositTx`. 
任何Atom通证的持有人都能够提交一个提案。 为了让一个提案获准公开投票，提议人必须要抵押一定量的通证 `deposit`，且抵押值必须大于 `minDeposit` 参数设定值. 提案的抵押不需要提案人一次全部交付。如果早期提案人交付的 `deposit` 不足，那么提案进入 `deposit_period` 状态。 此后，任何通证持有人可以通过 `depositTx` 交易增加对提案的抵押。 

Once the `deposit` reaches `minDeposit`, the proposal enters the `voting_period`, which lasts 2 weeks. Any **bonded** Atom holder can then cast a vote on this proposal. The options are `Yes`, `No`, `NoWithVeto` and `Abstain`. The weight of the vote is based on the amount of bonded Atoms of the sender. If they don't vote, delegator inherit the vote of their validator. However, delegators can override their validator's vote by sending a vote themselves. 
当`deposit` 达到 `minDeposit`，提案进入2周的 `voting_period` 。 任何**抵押了通证**的持有人都可以参与对这个提案的投票。投票的选项有`Yes`, `No`, `NoWithVeto` 和 `Abstain`. 投票的权重取决于投票人所抵押的通证数量。如果通证持有人不投票，那么委托人将被任务与他们委托的验证人投了相同的票。 当然，委托人也可以自己投出与所委托验证人不同的票。  

At the end of the voting period, the proposal is accepted if there are more than 50% `Yes` votes (excluding `Abstain ` votes) and less than 33.33% of `NoWithVeto` votes (excluding `Abstain` votes).
当投票期结束后，获得50%（不包括投`Abstain `票）以上 `Yes` 投票权重且少于33.33% 的`NoWithVeto`（不包括投`Abstain `票）提案将被接受， 

#### In practice 实践练习

::: tip 提示
**Before you can bond atoms and withdraw rewards, you need to [bond Atoms](#bonding-atoms-and-withdrawing-rewards)**
**在您能够抵押通证或者提取奖励以前，您需要了解[通证抵押](#bonding-atoms-and-withdrawing-rewards)**
:::

::: warning 警告
**Note: These commands need to be run on an online computer. It is more secure to perform them commands using a ledger device. For the offline procedure, click [here](#signing-transactions-from-an-offline-computer).**

**注意：执行以下命令需要在一台与网络连接的计算机。用一个钱包设备执行这些命令会更安全。关于离线交易过程请看[这里](#signing-transactions-from-an-offline-computer).**
::: 

```bash
// 提交一个提案
// <type>=text/parameter_change/software_upgrade
// ex value for flag: <gasPrice>=0.0001stake

gaiacli tx gov submit-proposal --title "Test Proposal" --description "My awesome proposal" --type <type> --deposit=10stake --gas auto --gas-prices <gasPrice> --from <delegatorKeyName>

// 增加对提案的抵押
// Retrieve proposalID from $gaiacli query gov proposals --status deposit_period
// 通过 $gaiacli query gov proposals --status deposit_period 命令获得 `proposalID` 
// 参数设定样例: <deposit>=1stake

gaiacli tx gov deposit <proposalID> <deposit> --gas auto --gas-prices <gasPrice> --from <delegatorKeyName>

// Vote on a proposal
// 对一个提案投票
// Retrieve proposalID from $gaiacli query gov proposals --status voting_period 
通过 $gaiacli query gov proposals --status deposit_period 命令获得 `proposalID` 
// <option>=yes/no/no_with_veto/abstain

gaiacli tx gov vote <proposalID> <option> --gas auto --gas-prices <gasPrice> --from <delegatorKeyName>
```

### Signing transactions from an offline computer 从一台离线电脑上签署交易


If you do not have a ledger device and want to interact with your private key on an offline computer, you can use the following procedure. First, generate an unsigned transaction on an **online computer** with the following command (example with a bonding transaction):
如果你没有数字钱包设备，而且希望和一台存有私钥的没有联网的电脑进行交互， 你可以使用如下过程。 首先，在**联网的电脑上**生成一个没有签名的交易，然后通过下列命令操作（下面以抵押交易为例）：

```bash
// 抵押Atom通证
// 参数设定样例: <amountToBound>=10000stake, <bech32AddressOfValidator>=cosmosvaloper18thamkhnj9wz8pa4nhnp9rldprgant57pk2m8s, <gasPrice>=0.001stake

gaiacli tx staking delegate <validatorAddress> <amountToBond> --from <delegatorKeyName> --gas auto --gas-prices <gasPrice> --generate-only > unsignedTX.json
```

Then, copy `unsignedTx.json` and transfer it (e.g. via USB) to the offline computer. If it is not done already, [create an account on the offline computer](#using-a-computer). For additional security, you can double check the parameters of your transaction before signing it using the following command:
然后，复制 `unsignedTx.json` 并且帮它转移到没有联网的电脑上（比如通过U盘）。如果还没有在没联网的电脑上建立账户，可先[在没有联网的电脑上建立账户](#using-a-computer)。为了进一步保障安全，你可以在签署交易前用以下命令对参数进行检查。 

```bash
cat unsignedTx.json
```

Now, sign the transaction using the following command:
现在，通过以下命令对交易签名：

```bash
gaiacli tx sign unsignedTx.json --from <delegatorKeyName> > signedTx.json
```

Copy `signedTx.json` and transfer it back to the online computer. Finally, use the following command to broadcast the transaction:
复制 `signedTx.json` 并把转移回联网的那台电脑。最后，用以下命令向网络广播交易。 

```bash
gaiacli tx broadcast signedTx.json
```
