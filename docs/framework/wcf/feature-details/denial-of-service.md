---
title: "拒绝服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "拒绝服务 [WCF]"
ms.assetid: dfb150f3-d598-4697-a5e6-6779e4f9b600
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 拒绝服务
当系统处于过载状态而无法处理消息或者处理速度极慢时，会出现拒绝服务的情况。  
  
## 过量占用内存  
 如果读取的 XML 文档具有大量唯一的本地名称、命名空间或前缀，则可能会出现问题。  如果使用的是从 <xref:System.Xml.XmlReader> 派生的类，并针对每一项调用了 <xref:System.Xml.XmlReader.LocalName%2A>、<xref:System.Xml.XmlReader.Prefix%2A> 或 <xref:System.Xml.XmlReader.NamespaceUri%2A> 属性，则返回的字符串将添加到 <xref:System.Xml.NameTable> 中。  <xref:System.Xml.NameTable> 包含的集合的大小绝不会减小，它会创建字符串句柄的虚拟“内存泄漏”。  
  
 缓解措施包括：  
  
-   从 <xref:System.Xml.NameTable> 类派生并实施最大大小配额。  （当 <xref:System.Xml.NameTable> 已满时，将无法阻止使用或切换 <xref:System.Xml.NameTable>。）  
  
-   避免使用所提到的这些属性，而是尽可能将 <xref:System.Xml.XmlReader.MoveToAttribute%2A> 方法与 <xref:System.Xml.XmlReader.IsStartElement%2A> 方法结合使用；这些方法不返回字符串，从而可以避免过度填充 <xref:System.Xml.NameTable> 集合的问题。  
  
## 恶意客户端向服务发送过多的许可证请求  
 如果恶意客户端通过过多的许可证请求来攻击某个服务，则可能会致使服务器占用过量的内存。  
  
 缓解操作：使用 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 类的下列属性：  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxCachedCookies%2A>：控制在 `SPNego` 或 `SSL` 协商之后服务器所缓存的有时限的 `SecurityContextToken` 的最大数目。  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.IssuedCookieLifetime%2A>：控制在 `SPNego` 或 `SSL` 协商之后服务器所颁发的 `SecurityContextTokens` 的生存期。  在此时间期限内，服务器将缓存 `SecurityContextToken`。  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxPendingSessions%2A>：控制在服务器上建立但尚未针为其处理任何应用程序消息的安全对话的最大数目。  此配额可防止客户端在服务上建立安全对话从而致使服务维护每个客户端的状态，但是从不使用这些状态。  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.InactivityTimeout%2A>：控制服务使安全对话保持活动状态（而不接收来自对话客户端的应用程序消息）的最长时间。  此配额可防止客户端在服务上建立安全对话从而致使服务维护每个客户端的状态，但是从不使用这些状态。  
  
## WSDualHttpBinding 或双向自定义绑定要求客户端身份验证  
 默认情况下，<xref:System.ServiceModel.WSDualHttpBinding> 会启用安全性。  但是，如果通过将 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 属性设置为 <xref:System.ServiceModel.MessageCredentialType> 而禁用客户端身份验证，则恶意用户可能会致使针对第三个服务进行拒绝服务攻击。  发生此问题的原因在于，恶意客户端可能会指示服务向第三个服务发送消息流。  
  
 为了缓解此问题，请不要将该属性设置为 `None`。  另请注意，在创建具有双向消息模式的自定义绑定时也可能出现此问题。  
  
## 可以填充审核事件日志  
 如果恶意用户了解到审核功能处于启用状态，则该攻击者可能会发送导致写入审核项的无效消息。  如果以这种方式填充审核日志，则审核系统会出现故障。  
  
 为了缓解此问题，请将 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 属性设置为 `true`，然后使用事件查看器的属性来控制审核行为。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用事件查看器查看和管理事件日志的更多信息，请参见[事件查看器](http://go.microsoft.com/fwlink/?LinkId=186123)（可能为英文网页）。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [审核](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
## 无效的 IAuthorizationPolicy 实现可能会致使服务挂起  
 如果在有错误的 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 接口实现上调用 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> 方法，则可能会致使服务挂起。  
  
 缓解操作：仅使用受信任的代码。  即，仅使用在编写后经过测试的代码或者来自受信任提供者的代码。  未经深思熟虑，请勿允许在代码中插入对 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 的不受信任的扩展。  这适用于服务实现中所使用的全部扩展。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不在应用程序代码与使用扩展点插入的外部代码之间进行任何区分。  
  
## 可能需要调整最大 Kerberos 令牌大小  
 如果客户端属于许多组（大约 900 个，尽管实际数字因组的数目而异），则可能会在消息头的块超过 64 KB 时出现问题。  在这种情况下，可以按照 Microsoft 支持文章 [Internet Explorer Kerberos 身份验证因连接到 IIS 的缓冲区不足而无法进行](http://go.microsoft.com/fwlink/?LinkId=89176)（可能为英文网页）中的说明来增加最大 Kerberos 令牌大小。您还可能需要增加最大 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息大小来容纳较大的 Kerberos 令牌。  
  
## 自动注册功能会为计算机生成多个具有相同主题名称的证书  
 “自动注册”是 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 的一个功能，它自动为用户和计算机注册证书。  如果计算机处于启用了该功能的域中，那么，每当有新计算机加入网络中时，都会自动创建一个既定目的为客户端身份验证的 X.509 证书，并将其插入本地计算机的“个人”证书存储区。  但是，自动注册功能对它在缓存中创建的所有证书使用同一主题名称。  
  
 其影响是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可能无法在具有自动注册功能的域中打开。  出现此问题的原因在于，有多个证书具有计算机的完全限定域名系统 \(DNS\) 名称，从而使得默认的服务 X.509 凭据搜索条件可能会不明确。  一个证书源于自动注册功能；而另一个可能是自行颁发的证书。  
  
 为了缓解此问题，请通过对 [\<serviceCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)使用更精确的搜索条件来引用要使用的确切证书。  例如，使用 <xref:System.Security.Cryptography.X509Certificates.X509FindType> 选项并按照证书的唯一指纹（哈希）来指定证书。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]自动注册功能的更多信息，请参见 [Windows Server 2003 中的证书自动注册功能](http://go.microsoft.com/fwlink/?LinkId=95166)（可能为英文网页）。  
  
## 用于授权的多个备选主题名称中的最后一个  
 在极少数情况下，如果 X.509 证书包含多个备选主题名称，并且您使用备选主题名称进行授权，则授权可能会失败。  
  
## 使用 ACL 保护配置文件  
 您可以在代码和配置文件中为 [!INCLUDE[infocard](../../../../includes/infocard-md.md)] 所颁发的令牌指定必需的和可选的声明。  这会导致在发送到安全令牌服务的 `RequestSecurityToken` 消息中发出相应的元素。  攻击者可能会通过修改代码或配置来移除必需的或可选的声明，从而可能会让安全令牌服务颁发不允许访问目标服务的令牌。  
  
 缓解措施：要求具有访问计算机的权限才能修改配置文件。  使用文件访问控制列表 \(ACL\) 来保护配置文件。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 只允许从配置中加载位于应用程序目录或全局程序集缓存中的代码。  使用目录 ACL 可以保护目录。  
  
## 达到了服务安全会话的最大数目  
 当客户端由某个服务成功进行身份验证，而且与此服务建立了安全会话时，此服务会记住该会话，直到该会话被客户端取消或者过期。  对于建立的每个会话都将进行计数，直到达到与该服务的同时活动会话的最大数目限制。  达到该限制时，尝试与该服务创建新会话的客户端将被拒绝，直到一个或多个活动会话过期或者被客户端取消。  一个客户端可以与某个服务建立多个会话，对于每个会话都将计数，直到达到相应的限制。  
  
> [!NOTE]
>  在使用有状态会话时，上述内容并不适用。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]有状态会话的更多信息，请参见[如何：为安全会话创建安全上下文令牌](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
 若要缓解此问题，请通过设置 <xref:System.ServiceModel.Channels.SecurityBindingElement> 类的 <xref:System.ServiceModel.Channels.SecurityBindingElement> 属性来设置活动会话的最大数目限制以及会话的最长生存期限制。  
  
## 请参阅  
 [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [信息泄露](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [特权提升](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denial of Service](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [重播攻击](../../../../docs/framework/wcf/feature-details/replay-attacks.md)   
 [篡改](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [不支持的方案](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)