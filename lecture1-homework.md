# 第 1 课 练习
## ZKP 三色演示
**练习 1**： 证明仍然是零知识的，因为验证者依然不知道两个节点之外的任何知识。但是证明者的虚假声明有可能被通过。

答：不是零知识。对于任意一个图，假设我们现在是Verifier方，通过每次选择图中任意的两个节点，询问Prover它们的颜色，不断重复，如果能得到Prover对这个图的三色方案，这样就证明了这一过程不是零知识。首先我们确定我们要图色的三个颜色{a,b,c}，下图示例选择a=红色，b=蓝色，c=黄色。任意选择图中的一条边，涂上两个不同的颜色a与b，红色与蓝色。

**练习 2**：
1. 因为需要证明我是群组里的一员，这个秘密值则是我拥有的群组私钥哈希。用于标识我唯一的身份。
2. ZK 证明我在ZKmessage上发布的消息是属于某一个组的，我的身份也是某一个组成员，证明密钥被用来生成组签名。
3. 为了实现匿名性，防止身份信息的泄露。

答：
“秘密值”其实就是私钥。作用有：

（a）用于证明是消息是小组中的一个成员发出的。实现匿名发送消息的目的。

匿名留言板和课程中讲的匿名投票过程类似。

zkmessage中代码：

myHash := mimc(secret)
(myHash - hash1)(myHash - hash2)(myHash - hash3)... == 0
msgAttestation := mimc(msg, secret)
我们能用私钥计算出公钥，并证明是Group的一个成员。每次发消息都会选择一个group，达到匿名的作用。

(b)私钥可以用于我们对消息签名。

msgAttestation := mimc(msg, secret)
(c)私钥能用来揭露消息发送者。作为小组的一个成员，能证明某个消息是我发送的，可用自己的私钥进行验证。

**Inputs:**
- myHash - MiMC hash of user's secret key (public)
- msg - the unsigned message to be validated (public)
- msgAttestation - the signed message to be validated (public)
- secret - User's secret key (private)

**Outputs:**
(none)
(d)拒绝签名。作为小组的一个成员，证明自己不是消息的发送者。

- msgAttestation != MiMC(msg, secret)
- myHash == MiMC(secret)
用白话写出 ZK 中正在证明的陈述。

ZK中想要证明的是一个消息是由一个Group中的一个成员发出的。

从不同的浏览器或计算机登录到相同的 zkmessage 帐户。 解释为什么 zkmessage 不能像大多数社交应用程序一样，只使用简单的“用户名/密码” 。

如果是简单的“用户/密码”而非“公钥/私钥”，那么zkmessage中的消息并不能确保是一个Group中的一个成员中发出的，无法对此进行证明。有以下情况可能发生：

(a)恶意的攻击者可以发送任何消息，然后随意指定一个Group，假定是小组中的一个成员发送的。如果是中心化的后端，可以直接在后台发送消息和指定小组成员，但是不能证明该消息是小组中的成员发送的。

(b)小组中的一个成员也无法拒签一个消息，或者证明自己是该消息的发送者。

(c)简单的“用户名/密码”无法实现对用户特性筛选的功能。比如有以太坊公钥的用户才能加入某个小组。

简单的“用户名/密码”失去了密码学中群签名以及ZK中证明的功能。

