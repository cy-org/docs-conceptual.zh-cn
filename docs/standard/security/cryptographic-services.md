---
title: "加密服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "密码系统 [.NET Framework]"
  - "派生类继承模式"
  - "数字签名"
  - "不对称加密算法"
  - "数字签名, 公钥系统"
  - "公钥"
  - "解密 [.NET Framework]"
  - "私钥"
  - "MAC 算法"
  - "加密算法"
  - "私钥, 概述"
  - "加密 [.NET Framework]"
  - "安全性 [.NET Framework], 加密"
  - "加密服务"
  - "对称加密算法"
  - "hash"
  - "消息验证代码"
  - "派生类继承"
  - "加密 [.NET Framework], 关于"
  - "随机数生成"
ms.assetid: f96284bc-7b73-44b5-ac59-fac613ad09f8
caps.latest.revision: 34
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 34
---
# 加密服务
<a name="top"></a> 公共网络（如 Internet）不提供实体之间安全通信的方式。 此类网络上的通信易被读取或甚至被未经授权的第三方修改。 加密有助于防止数据被查看，提供检测数据是否已修改的方法，并帮助提供一种跨不安全通道安全通信的方式。 例如，数据可通过使用加密算法进行加密、以加密状态进行传输并在稍后由预期方进行解密。 如果某个第三方截获了加密数据，将很难解密此数据。  
  
 在 .NET Framework 中，<xref:System.Security.Cryptography?displayProperty=fullName> 命名空间中的类将为你管理很多有关加密的详细信息。 一些类是非托管的 Microsoft 加密 API \(CryptoAPI\) 的包装，而其他类则是纯托管实现。 无需是加密方面的专家，即可使用这些类。 在创建其中一个加密算法类的新实例时，为易于使用，将自动生成密钥，并且默认属性将尽可能地安全可靠。  
  
 此概述提供了 .NET Framework 支持的加密方法和惯例的概要，包括 ClickOnce 清单、Suite B 和 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 中引入的下一代加密技术 \(CNG\) 支持。  
  
 本概述包含以下几节：  
  
-   [加密基元](#primitives)  
  
-   [私钥加密](#secret_key)  
  
-   [公钥加密](#public_key)  
  
-   [数字签名](#digital_signatures)  
  
-   [哈希值](#hash_values)  
  
-   [随机数生成](#random_numbers)  
  
-   [ClickOnce 清单](#clickonce)  
  
-   [Suite B 支持](#suite_b)  
  
-   [相关主题](#related_topics)  
  
 有关加密以及允许向应用程序添加加密安全的 Microsoft 服务、组件和工具的其他信息，请参阅本文档的“Win32 和 COM 开发、安全”部分。  
  
<a name="primitives"></a>   
## 加密基元  
 在使用加密的典型情况下，两方（Alice 和 Bob）均通过非安全通道进行通信。 Alice 和 Bob 想要确保其通信不可为任何可能正在侦听的人理解。 此外，由于 Alice 和 Bob 处于远程位置，所以 Alice 必须确保她从 Bob 处收到的信息在传输期间未被任何人修改。 此外，她必须确保此信息确实来自 Bob 本人，而不是模仿 Bob 的人。  
  
 加密用于实现以下目标：  
  
-   保密性：有助于防止用户的身份或数据被读取。  
  
-   数据完整性：有助于防止数据被更改。  
  
-   身份验证：确保数据来自于特定方。  
  
-   不可否认性：防止特定方否认其发送过消息。  
  
 若要实现这些目标，可以使用称为加密基元的算法和惯例的组合来创建加密方案。 下表列出了加密基元以及其用途。  
  
|加密基元|使用|  
|----------|--------|  
|私钥加密（对称加密）|在数据上执行转换，以防止其被第三方读取。 此类型的加密使用单个共享的密钥来加密和解密数据。|  
|公钥加密（非对称加密）|在数据上执行转换，以防止其被第三方读取。 此类型的加密使用公钥\/私钥对来加密和解密数据。|  
|加密签名|通过创建特定于参与方的数字签名，帮助验证数据是否来自此特定方。 此流程也使用哈希函数。|  
|加密哈希|将任意长度的数据映射到固定长度的字节序列。 哈希值在统计上是唯一的；不同的双字节序列不会有哈希处理为同一个值。|  
  
 [返回页首](#top)  
  
<a name="secret_key"></a>   
## 私钥加密  
 密钥加密算法使用单个密钥来加密和解密数据。 必须确保密钥不被未经授权的代理访问，因为具有此密钥的任意方均可使用此密钥解密你的数据或者加密自己的数据，而声称此数据来自于你。  
  
 密钥加密也称为对称加密，因为加密和解密所用的密码相同。 密钥加密算法非常迅速（相比于公钥算法），也非常适合在大型数据流上执行加密转换。 非对称加密算法（例如 RSA）从数学上来说在可加密的数据量方面存在限制。 对称加密算法通常没有这些问题。  
  
 一种名为分组加密的密钥算法用于一次加密一个数据块。 分组加密（例如数据加密标准 \(DES\)、TripleDES 和高级加密标准 \(AES\)）可将 *n* 字节的输入块通过加密转换为由加密字节构成的输出块。 如果想要加密或解密字节序列，则必须逐块执行。 由于 *n* 很小（DES 和 TripleDES 为 8 字节；AES 为 16 字节 \[默认值\]、24 字节或 32 字节），所以对于大于 *n* 的数据值，必须一次加密一个数据块。 小于 *n* 的数据值则必须扩展为 *n* 才能进行处理。  
  
 分组加密的一种简单形式被称为电子密码本 \(ECB\) 模式。 ECB 模式被视为不安全，因为它不使用初始化向量来初始化第一个纯文本块。 对于给定的密钥 *k*，不使用初始化向量的简单分组加密会将相同的纯文本输入块加密为相同的已加密文本的输出块。 因此，如果输入的纯文本流中存在重复的块，则输出密码文本流中也会有重复的块。 这些重复的输出块会警告未经授权的用户使用了可能被采用的算法访问不可靠的加密以及可能的攻击模式。 因此，ECB 密码模式非常易于分析，最终导致密钥易于被发现。  
  
 基类库中提供的分组加密类使用称为加密块链接 \(CBC\) 的默认链接模式，但可随意更改此默认设置。  
  
 通过使用初始化向量 \(IV\) 加密第一个纯文本块，CBC 密码克服了与 ECB 密码关联的问题。 每个后续纯文本块在加密之前，都将与之前的密码文本块进行位异或 \(`XOR`\) 运算。 因此，每个密码文本块均依赖于之前所有的块。 使用此系统时，可能已为未经授权的用户所知的常见消息头不可用来对密钥进行反向工程处理。  
  
 一种泄露以 CBC 密码加密的数据的方式是对每个可能的密钥执行详尽搜索。 具体取决于用来执行加密的密钥大小，这种搜索即使是使用最快的计算机也非常耗时，因此不可行。 密钥大小更大，解密更难。 虽然从理论上来说，加密并未使攻击者检索加密数据变得不可能，但它确实增加了执行此操作的成本。 如果花费三个月的时间执行详尽搜索来检索仅在几天之内有意义的数据，则详尽搜索方法不切实际。  
  
 密钥加密的缺点是它假定双方已商定密钥和 IV，并互相传达了密钥和 IV 的值。 IV 不被视为机密，并可以以纯文本的形式通过消息传输。 但是，密钥必须对未经授权的用户保密。 由于存在这些问题，密钥加密通常与公钥加密一起使用，以秘密地传达密钥和 IV 的值。  
  
 假定 Alice 和 Bob 是想通过非安全通道进行通信的双方，则他们可能按如下所示使用密钥加密：Alice 和 Bob 同意使用某种具有特定密钥和 IV 的特定算法（例如 AES）。 Alice 编写了一条消息，并创建了一个在其上发送消息的网络流（也许是已命名的管道或网络电子邮件）。 接下来，她使用密钥和 IV 对文本进行加密，然后通过 intranet 向 Bob 发送加密的消息和 IV。 Bob 收到加密文本并使用 IV 和之前商定的密钥对其进行解密。 如果传输遭到截获，侦听者无法恢复原始消息，因为他不知道密钥。 在此方案中，只有密钥必须保持机密。 在实际方案中，Alice 和 Bob 都可以生成密钥并使用公钥（非对称）加密将密钥（对称）传递给另一方。 有关公钥加密的详细信息，请参阅下一节。  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供以下实现密钥加密算法的类：  
  
-   <xref:System.Security.Cryptography.AesManaged>（在 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 引入）。  
  
-   <xref:System.Security.Cryptography.DESCryptoServiceProvider>。  
  
-   <xref:System.Security.Cryptography.HMACSHA1>（从技术上讲，这是一种密钥算法，因为它代表使用与密钥结合的加密哈希函数计算的消息验证代码。 请参阅本主题之后的[哈希值](#hash_values)。）  
  
-   <xref:System.Security.Cryptography.RC2CryptoServiceProvider>。  
  
-   <xref:System.Security.Cryptography.RijndaelManaged>。  
  
-   <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>。  
  
 [返回页首](#top)  
  
<a name="public_key"></a>   
## 公钥加密  
 公钥加密使用必须对从未经授权的用户保密的私钥和可以公开给任何人的公钥。 从数学上来讲，公钥和私钥是相互链接的；使用公钥加密的数据只能用私钥解密，而使用私钥签名的数据只能使用公钥进行验证。 公钥可供任何人使用；它用加密要发到送私钥所有者的数据。 公钥加密算法也称为非对称算法，因为加密数据需要一个密钥，而解密数据需要另一个密钥。 基本加密规则禁止密钥重复使用，并且每个通信会话的两个密钥应该是独有的。 但是，在实践中，非对称密钥的生存期通常很长。  
  
 双方（Alice 和 Bob）可能按如下所示使用公钥加密：首先，Alice 生成公钥\/私钥对。 如果 Bob 想要向 Alice 发送一条已加密的消息，他会向她索要公钥。 Alice 通过非安全网络向 Bob 发送她的公钥，然后 Bob 使用此密钥对消息进行加密。 Bob 将加密的消息发送给 Alice，然后她将使用自己的私钥对其进行解密。 如果 Bob 通过非安全通道收到 Alice 的密钥（例如，公用网络），则 Bob 容易受到中间人攻击。 因此，Bob 必须与 Alice 确认他具有其公钥的正确副本。  
  
 在 Alice 公钥的传输期间，未经授权的代理可能会截获此密钥。 此外，同一代理可能会截获来自 Bob 的加密消息。 不过，此代理不能使用公钥解密此消息。 该消息只能用 Alice 的私钥进行解密，而该私钥没有进行传输。 Alice 不使用她的私钥加密给 Bob 的回复消息，因为任何具有公钥的人都可以解密此消息。 如果 Alice 想要将消息回复给 Bob，她会向 Bob 索要他的公钥，并使用此公钥加密消息。 然后，Bob 将使用自己的关联私钥解密消息。  
  
 在此方案中，Alice 和 Bob 使用公钥（非对称）加密来传输密钥（对称）并使用密钥加密对双方会话的其余部分进行加密。  
  
 下表提供了公钥和密钥加密算法之间的比较：  
  
-   公钥加密算法使用固定的缓冲区大小，而密钥加密算法使用长度可变的缓冲区。  
  
-   公钥算法不能用于以密钥算法可用的方式将数据一起链接到流中，因为只可以加密少量数据。 因此，不对称操作不使用与对称操作相同的流式处理模型。  
  
-   相对于密钥加密，公钥加密具有大得多的密钥空间（密钥的可能值的范围）。 因此，公钥加密更不易遭受尝试每个可能的密钥的穷举攻击。  
  
-   公钥易于分发，因为它们不必要进行保护，前提是存在一些用来验证发件人身份的方式。  
  
-   一些公钥算法（例如 RSA 和 DSA，但不是 Diffie\-Hellman）可用于创建数字签名以验证数据发件人的身份。  
  
-   公钥算法与密钥算法相比非常慢，且其设计目的不是用于加密大量数据。 公钥算法仅对传输极少量的数据很有用。 通常情况下，公钥加密用于加密密钥算法要使用的密钥和 IV。 在密钥和 IV 传输完成后，密钥加密将用于对会话的其余部分加密。  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供以下实现公钥加密算法的类：  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellman>（基类）  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCng>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCngPublicKey>（基类）  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanKeyDerivationFunction>（基类）  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 RSA 允许加密和签名，但 DSA 仅可用于签名，而 Diffie\-Hellman 仅可用于生成密钥。 一般情况下，公钥算法的使用比私钥算法的更受限制。  
  
 [返回页首](#top)  
  
<a name="digital_signatures"></a>   
## 数字签名  
 公钥算法还可用于构成数字签名。 数字签名会验证发件人的身份（如果信任发件人的公钥），并有助于保护数据的完整性。 使用 Alice 生成的公钥，Alice 的数据的收件人可通过将数字签名与 Alice 的数据及其公钥进行比较来验证数据是否由 Alice 发送。  
  
 若要使用公钥加密以数字方式签署一条消息，Alice 首先要将哈希算法应用于此消息，以创建消息摘要。 消息摘要是数据紧凑且唯一的表示形式。 然后，Alice 使用她的私钥加密此消息摘要，以创建她的个人签名。 在收到消息和签名后，Bob 将使用 Alice 的公钥解密签名，以恢复此消息摘要，并且将使用 Alice 所使用的同一个哈希算法对消息进行哈希运算。 如果 Bob 计算的消息摘要与从 Alice 处收到的消息摘要完全匹配，Bob 就可以确定此消息来自私钥的持有人且数据不曾被修改。 如果 Bob 信任 Alice 就是私钥的持有人，他就会知道此消息来自 Alice。  
  
> [!NOTE]
>  任何人都可以验证签名，因为发件人的公钥众所周知，并且通常包含在数字签名格式中。 此方法不会保留消息的秘密性；对于机密消息，它也必须加密。  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供以下实现数字签名算法的类：  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDsa>（基类）  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 [返回页首](#top)  
  
<a name="hash_values"></a>   
## 哈希值  
 哈希算法将任意长度的二进制值映射到较小的固定长度的二进制值，称为哈希值。 哈希值是一段数据的数值表示形式。 如果对一段纯文本进行哈希处理，甚至只更改段落的一个字母，随后的哈希运算都将产生不同的值。 如果哈希是加密型强哈希，则其值将有明显的更改。 例如，如果更改了消息中的一个位，强哈希函数可能会生成相差 50% 的输出。 许多输入值可能哈希处理为相同的输出值。 但是，它无法以计算方式找到哈希处理为同一值的两个不同的输入。  
  
 双方（Alice 和 Bob）可以使用哈希函数来确保消息的完整性。 他们会选择要对其消息进行签名的哈希算法。 Alice 将编写一条消息，然后使用所选的算法为此消息创建一个哈希值。 然后，他们将按以下方法之一执行操作：  
  
-   Alice 向 Bob 发送纯文本消息和经过哈希处理的消息（数字签名）。 Bob 接收消息并进行哈希处理，然后将其哈希值与从 Alice 处接收到的哈希值进行比较。 如果哈希值相同，则消息未更改。 如果值不同，则消息在 Alice 编写后遭到更改。  
  
     遗憾的是，此方法不会确定发件人的真伪。 任何人都可以模仿 Alice 并向 Bob 发送消息。 他们可以使用相同的哈希算法来签署消息，而 Bob 可确定的只是消息与它的签名相匹配。 这是中间人攻击的一种形式。 有关详细信息，请参阅 [NIB：下一代加密技术 \(CNG\) 安全通信示例](http://msdn.microsoft.com/zh-cn/8048e94e-054a-417b-87c6-4f5e26710e6e)。  
  
-   Alice 通过非安全的公共通道向 Bob 发送纯文本消息。 Alice 通过安全的专用通道向 Bob 发送经过哈希处理的消息。 Bob 接收纯文本消息，对其进行哈希处理并将此哈希值与私下交换的哈希值进行比较。 如果哈希值匹配，则 Bob 知道两件事：  
  
    -   消息未被更改。  
  
    -   消息的发件人 \(Alice\) 是可信的。  
  
     为使此系统发挥作用，Alice 必须对 Bob 之外的所有方隐藏她的原始哈希值。  
  
-   Alice 通过非安全的公共通道向 Bob 发送纯文本消息，并将经过哈希处理的消息放置在其公开可见的网站上。  
  
     此方法可以通过防止任何人修改哈希值，从而防止消息遭到篡改。 尽管任何人都可读取此消息及其哈希值，但只有 Alice 可以更改哈希值。 想要模仿 Alice 的攻击者将需要访问 Alice 的网站。  
  
 之前的方法都无法防止他人读取 Alice 的消息，因为消息是以纯文本的形式传输的。 完整安全模式通常要求数字签名（消息签名）和加密。  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供以下实现哈希算法的类：  
  
-   <xref:System.Security.Cryptography.HMACSHA1>。  
  
-   <xref:System.Security.Cryptography.MACTripleDES>。  
  
-   <xref:System.Security.Cryptography.MD5CryptoServiceProvider>。  
  
-   <xref:System.Security.Cryptography.RIPEMD160>。  
  
-   <xref:System.Security.Cryptography.SHA1Managed>。  
  
-   <xref:System.Security.Cryptography.SHA256Managed>。  
  
-   <xref:System.Security.Cryptography.SHA384Managed>。  
  
-   <xref:System.Security.Cryptography.SHA512Managed>。  
  
-   所有安全哈希算法 \(SHA\)、消息摘要 5 \(MD5\) 和 ripemd\-160 算法的 HMAC 变体。  
  
-   所有 SHA 算法的 CryptoServiceProvider 实现（托管的代码包装）。  
  
-   所有 MD5 和 SHA 算法的下一代加密技术 \(CNG\) 实现。  
  
> [!NOTE]
>  MD5 的设计缺陷发现于 1996 年，并建议改用 SHA\-1。 在 2004 年，发现了其他缺陷，MD5 算法被认为不再安全。 Sha\-1 算法也发现不安全，现在建议改用 SHA\-2。  
  
 [返回页首](#top)  
  
<a name="random_numbers"></a>   
## 随机数生成  
 随机数生成是很多加密操作的必要组成部分。 例如，加密密钥需要尽可能的随机，以便使其很难再现。 加密随机数生成器必须生成在计算上预测的可能性不可大于 50% 的输出。 因此，预测下一个输出位的任何方法均不能比随机推测执行地更好。[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中的类使用随机数生成器来生成加密密钥。  
  
 <xref:System.Security.Cryptography.RNGCryptoServiceProvider> 类是随机数生成器算法的一个实现。  
  
 [返回页首](#top)  
  
<a name="clickonce"></a>   
## ClickOnce 清单  
 在 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 中，下列加密类使你可以获取并验证有关使用 [ClickOnce 技术](../Topic/ClickOnce%20Security%20and%20Deployment.md)部署的应用程序的清单签名的信息：  
  
-   当使用清单签名的 <xref:System.Security.Cryptography.ManifestSignatureInformation.VerifySignature%2A> 方法重载时，<xref:System.Security.Cryptography.ManifestSignatureInformation> 类将获取此清单签名的相关信息。  
  
-   可以使用 <xref:System.Security.ManifestKinds> 枚举来指定要验证的清单。 验证的结果是 <xref:System.Security.Cryptography.SignatureVerificationResult> 枚举值之一。  
  
-   <xref:System.Security.Cryptography.ManifestSignatureInformationCollection> 类提供已验证签名的 <xref:System.Security.Cryptography.ManifestSignatureInformation> 对象的只读集合。  
  
 此外，以下类提供特定的签名信息：  
  
-   <xref:System.Security.Cryptography.StrongNameSignatureInformation> 包含清单的强名称签名信息。  
  
-   <xref:System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation> 表示清单的验证码签名信息。  
  
-   <xref:System.Security.Cryptography.X509Certificates.TimestampInformation> 包含验证码签名上时间戳的相关信息。  
  
-   <xref:System.Security.Cryptography.X509Certificates.TrustStatus> 提供了一个检查验证码签名是否可信的简单方法。  
  
 [返回页首](#top)  
  
<a name="suite_b"></a>   
## Suite B 支持  
 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 支持美国国家安全局 \(NSA\) 发布的加密算法的 Suite B 集。 有关 Suite B 的详细信息，请参阅 [NSA Suite B 加密一览表](http://go.microsoft.com/fwlink/?LinkId=100111)。  
  
 包括以下算法：  
  
-   用于加密的密钥大小为 128、192 和 256 位的高级加密标准 \(AES\) 算法。  
  
-   用于哈希处理的安全哈希算法 SHA\-1、SHA\-256、SHA\-384 和 SHA\-512。 （最后三个通常分在一组，称为 SHA\-2。）  
  
-   使用 256 位、384 位和 521 位素数模数曲线进行签名的椭圆曲线数字签名算法 \(ECDSA\)。 NSA 文档具体定义了这些曲线并将其称为 P\-256、P\-384 和 P\-521。 此算法由 <xref:System.Security.Cryptography.ECDsaCng> 类提供。 它允许你使用私钥进行签名并使用的公钥对签名进行验证。  
  
-   使用 256 位、384 位和 521 位素数模数曲线进行密钥交换和机密协议的椭圆曲线 Diffie\-Hellman \(ECDH\) 算法。 此算法由 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 类提供。  
  
 美国联邦信息处理标准 \(FIPS\) 认证实现的 AES、SHA\-256、SHA\-384 和 SHA\-512 实现的托管代码包装在新的 <xref:System.Security.Cryptography.AesCryptoServiceProvider>、<xref:System.Security.Cryptography.SHA256CryptoServiceProvider>、<xref:System.Security.Cryptography.SHA384CryptoServiceProvider> 和 <xref:System.Security.Cryptography.SHA512CryptoServiceProvider> 类中可用。  
  
 [返回页首](#top)  
  
<a name="cng"></a>   
## 下一代加密技术 \(CNG\) 类  
 下一代加密技术 \(CNG\) 类提供了围绕本机 CNG 函数的托管包装。 （CNG 是 CryptoAPI 的替换。） 这些类的名称中包含“Cng”。 “中心到 CNG”包装类是 <xref:System.Security.Cryptography.CngKey> 密钥容器类，它将提取 CNG 密钥的存储和用法。 此类允许安全地存储密钥对或公钥并使用简单的字符串名称对其进行引用。 基于椭圆曲线的 <xref:System.Security.Cryptography.ECDsaCng> 签名类和 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 加密类可以使用 <xref:System.Security.Cryptography.CngKey> 对象。  
  
 <xref:System.Security.Cryptography.CngKey> 类用于各种其他操作，包括打开、创建、删除和导出密钥。 在直接调用本机函数时，它还提供对要使用的基础密钥句柄的访问。  
  
 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 还包括各种支持的 CNG 类，如下所示：  
  
-   <xref:System.Security.Cryptography.CngProvider> 维护密钥存储提供程序。  
  
-   <xref:System.Security.Cryptography.CngAlgorithm> 维护 CNG 算法。  
  
-   <xref:System.Security.Cryptography.CngProperty> 维护经常使用的密钥属性。  
  
 [返回页首](#top)  
  
<a name="related_topics"></a>   
## 相关主题  
  
|标题|描述|  
|--------|--------|  
|[加密模型](../../../docs/standard/security/cryptography-model.md)|介绍如何在基类库中实现加密。|  
|[演练：创建加密应用程序](../../../docs/standard/security/walkthrough-creating-a-cryptographic-application.md)|演示基本加密和解密任务。|  
|[配置加密类](../../../docs/framework/configure-apps/configure-cryptography-classes.md)|介绍如何将算法名称映射到加密类，以及如何将对象标识符映射到加密算法。|