---
title: "HTTP 传输安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3439262-c58e-4d30-9f2b-a160170582bb
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# HTTP 传输安全
如果使用 HTTP 作为传输，则由安全套接字层 \(SSL\) 实现提供安全。  SSL 广泛用于 Internet 中，以便向客户端证明服务的身份，并且随后向通道提供保密性（加密）。  本主题说明 SSL 的工作方式以及 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中是如何实现它的。  
  
## 基本 SSL  
 SSL 的工作方式可以通过一个典型方案得到最好的说明，在本示例中，该方案为银行的网站。  该网站允许客户使用用户名和密码登录。  在经过身份验证之后，用户可以执行事务，例如查看帐户余额、支付帐单以及将钱从一个帐户转到其他帐户。  
  
 当用户第一次访问该网站时，SSL 机制启动一系列与用户客户端（在此情况下为 Internet Explorer）的协商，称为“握手”。  SSL 首先向客户证明银行网站的身份。  这一步骤是必需的，因为客户首先必须知道他们正在与真实网站进行通信，而不是与一个试图引诱他们键入自己的用户名和密码的诈骗网站进行通信。  SSL 通过使用由受信任的颁发机构（例如 VeriSign）提供的 SSL 证书来执行此身份验证。  其逻辑如下：VeriSign 担保该银行网站的身份是真实的。  由于 Internet Explorer 信任 VeriSign，因此也信任该网站。  如果您希望向 VeriSign 进行核实，可以通过单击 VeriSign 徽标执行此操作。  这将显示一份含有到期日期以及接受方（银行网站）的真实性声明。  
  
 若要启动一个安全会话，客户端向服务器发送一个等效于“你好”的项，连同一个它可以用来签名、生成哈希以及进行加密和解密的加密算法列表。  作为响应，该网站发送回一个确认以及它对算法组之一的选择。  在该初次握手期间，双方都发送和接收 Nonce。  “Nonce”是一段随机生成的数据，该数据与网站的公钥一起使用以创建哈希。  “哈希”是使用某种标准算法（例如 SHA1）从两个数得到的一个新数。  （客户端和网站还交换消息以协商要使用的哈希算法。）哈希是唯一的，并且仅在客户端和网站之间的会话中使用以便对消息进行加密和解密。  客户端和服务都具有原始 Nonce 和证书的公钥，所以通信两端可以生成同一个哈希。  因此，客户端可以通过以下方式验证服务所发送的哈希：\(a\) 使用商定的算法根据数据计算哈希；并 \(b\) 将计算出的哈希与服务所发送的哈希进行比较。如果二者匹配，则客户端可以确信该哈希未遭篡改。  客户端随后可以将此哈希用作密钥，以便对同时包含另一个新哈希的消息进行加密。  服务可以使用此哈希对消息进行解密，并重新获得倒数第二个哈希。  这样，通信双方就都获知累积的信息（Nonce、公钥和其他数据），并且可以创建最后一个哈希（也称主密钥）。  这个最终的密钥使用倒数第二个哈希加密后发送。  然后，使用主密钥对用来重置会话的消息进行加密和解密。  由于客户端和服务都使用同一密钥，因此该密钥又称为“会话密钥”。  
  
 会话密钥还被描述为对称密钥，或“共享秘密”。具有对称密钥很重要，因为它减少了事务双方所需执行的计算量。  如果每个消息都要求对 Nonce 和哈希进行新的交换，那么性能将会下降。  因此，SSL 的最终目标是使用允许消息在通信双方之间自由流动的对称密钥，同时具有更高程度的安全和效率。  
  
 因为协议可能因网站而异，所以前面的描述只是所发生过程的简化版本。  还有一种可能，就是客户端和网站都在握手期间生成在算法上相结合的 Nonce，以增加数据交换过程的复杂性，从而为该过程提供更多的保护。  
  
### 证书和公钥基础结构  
 在握手期间，服务还将其 SSL 证书发送到客户端。  该证书包含一些信息，例如证书的到期日期、颁发机构以及网站的统一资源标识符 \(URI\)。  客户端将该 URI 与它原来联系的 URI 进行比较，以确保二者匹配，并且对日期和颁发机构进行检查。  
  
 每个证书都具有两个密钥：一个私钥和一个公钥，并且这两个密钥称为一个“交换密钥对”。  简言之，只有证书的所有者知道私钥，而公钥则可以从证书中读取。  这两个密钥都可用来加密和解密摘要、哈希或其他密钥，但它们只能用于相反的操作。  例如，如果客户端使用公钥加密，则只有网站可以使用私钥对消息进行解密。  同样，如果网站使用私钥加密，则客户端可以使用公钥解密。  这可以使客户端确信只与私钥的拥有者交换消息，因为只有使用私钥加密的消息才可以使用公钥进行解密。  而网站可以确信它正在与已经使用公钥加密的客户端交换消息。  然而，这种交换仅对初次握手是安全的，因此在创建实际的对称密钥时要复杂得多。  尽管如此，所有通信都依赖于服务具有有效的 SSL 证书。  
  
## 使用 WCF 实现 SSL  
 HTTP 传输安全（或 SSL）是在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 外部提供的。  可以使用两种方式之一来实现 SSL；决定因素是承载应用程序的方式：  
  
-   如果要使用 Internet 信息服务 \(IIS\) 作为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 宿主，请使用 IIS 基础结构来设置 SSL 服务。  
  
-   如果要创建自承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序，则可以使用 HttpCfg.exe 工具将 SSL 证书绑定到相应的地址。  
  
### 使用 IIS 实现传输安全  
  
#### IIS 7.0  
 若要将 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 设置为安全宿主（使用 SSL），请参见 [IIS 7.0 测试版：在 IIS 7.0 中配置安全套接字层](http://go.microsoft.com/fwlink/?LinkId=88600)（可能为英文网页）。  
  
 若要配置证书以便与 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 一起使用，请参见 [IIS 7.0 测试版：在 IIS 7.0 中配置服务器证书](http://go.microsoft.com/fwlink/?LinkID=88595)（可能为英文网页）。  
  
#### IIS 6.0  
 若要将 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 设置为安全宿主（使用 SSL），请参见[配置安全套接字层](http://go.microsoft.com/fwlink/?LinkId=88601)（可能为英文网页）。  
  
 若要配置证书以便与 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 一起使用，请参见 [Certificates\_IIS\_SP1\_Ops](http://go.microsoft.com/fwlink/?LinkId=88602)。  
  
### 将 HttpCfg 用于 SSL  
 如果要创建自承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序，请从 [Windows XP Service Pack 2 支持工具网站](http://go.microsoft.com/fwlink/?LinkId=29002)（可能为英文网页）下载 HttpCfg.exe 工具。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]通过 HttpCfg.exe 使用 X.509 证书设置端口的更多信息，请参见[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
## 请参阅  
 [传输安全](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [消息安全](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)