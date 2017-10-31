---
title: "WCF 数据服务的安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "应用程序安全 [WCF 数据服务]"
  - "WCF 数据服务, 安全性"
ms.assetid: 99fc2baa-a040-4549-bc4d-f683d60298af
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# WCF 数据服务的安全
本主题介绍开发、部署和运行访问支持 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 的服务的 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]和应用程序的特定安全注意事项。  除此之外，您还应遵循有关创建安全的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序的建议。  
  
 在计划如何保证基于 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务的安全时，必须同时解决身份验证和授权问题，前者是发现和验证主体身份的过程，后者是确定是否允许经过身份验证的主体访问所请求资源的过程。  还应当考虑是否使用 SSL 来加密消息。  
  
## 对客户端请求进行身份验证  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]本身不实现任何类型的身份验证，而是依赖数据服务宿主的身份验证设置。  这意味着服务将假定它接收到的任何请求已由网络主机进行了身份验证，并且该主机通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]提供的相应接口正确识别了请求的主体。  [OData 和身份验证系列文章](http://go.microsoft.com/fwlink/?LinkId=200381)对这些身份验证选项和方法进行了详细说明。  
  
### WCF 数据服务的身份验证选项  
 下表列出了一些可用来对发向 WCF 数据服务的请求进行身份验证的身份验证机制。  
  
|身份验证选项|说明|  
|------------|--------|  
|匿名身份验证|启用 HTTP 匿名身份验证时，任何主体都能连接到数据服务。  匿名访问无需凭据。  仅当希望允许任何人访问数据服务时，才使用此选项。|  
|基本和摘要式身份验证|需要由用户名和密码组成的凭据以进行身份验证。  支持非 Windows 客户端的身份验证。 **Security Note:**  基本身份验证凭据（用户名和密码）以明文形式发送，会被截取。  摘要式身份验证基于所提供的凭据发送一个哈希值，因而比基本身份验证更安全。  这两者都容易受到中间人攻击。  使用这些身份验证方法时，应考虑使用安全套接字层 \(SSL\) 加密客户端与数据服务之间的通信。 <br /><br /> Microsoft Internet Information Services \(IIS\) 为 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序中的 HTTP 请求提供了一种同时包含基本和摘要式身份验证的实现。  该 Windows 身份验证提供程序实现允许 .NET Framework 客户端应用程序在发给数据服务的请求的 HTTP 标头中提供凭据，以无缝协商 Windows 用户的身份验证。  有关更多信息，请参见[摘要式身份验证技术参考](http://go.microsoft.com/fwlink/?LinkId=200408)。<br /><br /> 如果希望使数据服务使用基于某种自定义身份验证服务的基本身份验证，而不是 Windows 凭据，则必须为身份验证实现一个自定义 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] HTTP 模块。<br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)]如何为 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]使用自定义基本身份验证方案的示例，请参见 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 和身份验证系列文章中的[自定义基本身份验证](http://go.microsoft.com/fwlink/?LinkID=200388)一文。|  
|Windows 身份验证|基于 Windows 的凭据使用 NTLM 或 Kerberos 进行交换。  该机制比基本或摘要式身份验证更安全，但它要求客户端是基于 Windows 的应用程序。  IIS 也为 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序中的 HTTP 请求提供了一种 Windows 身份验证的实现。  有关更多信息，请参见 [ASP.NET Forms Authentication Overview](../Topic/ASP.NET%20Forms%20Authentication%20Overview.md)。<br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)]如何为 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]使用 Windows 身份验证的示例，请参见 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 和身份验证系列文章中的 [Windows 身份验证](http://go.microsoft.com/fwlink/?LinkID=200384)一文。|  
|[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Forms 身份验证|Forms 身份验证使您可以使用自己的代码对用户进行身份验证，然后将身份验证标记保留在 Cookie 或页的 URL 中。  您使用自己创建的登录窗体对用户的用户名和密码进行验证。  未经过身份验证的请求被重定向到登录页，用户在该页上提供凭据和提交窗体。  如果应用程序对请求进行了验证，系统会颁发一个票证，该票证包含用于重建后续请求的标识的密钥。  有关更多信息，请参见 [Forms Authentication Provider](../Topic/Forms%20Authentication%20Provider.md)。 **Security Note:**  默认情况下，在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序中使用 Forms 身份验证时，包含 Forms 身份验证票证的 Cookie 并未进行安全保护。  应考虑要求使用 SSL 以保护身份验证票证和初始登录凭据。 <br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)]如何为 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]使用 Forms 身份验证的示例，请参见 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 和身份验证系列文章中的 [Forms 身份验证](http://go.microsoft.com/fwlink/?LinkID=200389)一文。|  
|基于声明的身份验证|在基于声明的身份验证中，数据服务依赖受信任的“第三方”标识提供程序服务对用户进行身份验证。  该标识提供程序对请求访问数据服务资源的用户进行肯定的身份验证并发出一个标记，授予对所请求资源的访问权限。  该标记随后提供给数据服务，后者基于与发出访问权限标记的标识服务的信任关系授予用户访问权限。<br /><br /> 使用基于声明的身份验证提供程序的优点是它们可用于跨越信任域对各种类型的客户端进行身份验证。  通过采用这样一种第三方提供程序，数据服务可以不必维护用户并对其进行身份验证，从而减轻了负担。  OAuth 2.0 是一个基于声明的身份验证协议，作为一项服务受到 Microsoft Azure AppFabric Access Control 的支持以进行联盟授权。  此协议支持基于 REST 的服务。  [!INCLUDE[crexample](../../../../includes/crexample-md.md)] 有关如何将 OAuth 2.0 用于 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]的示例，请参见 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 和身份验证系列中有关 [OData 和 OAuth](http://go.microsoft.com/fwlink/?LinkId=200514) 的博文。|  
  
<a name="clientAuthentication"></a>   
### 客户端库中的身份验证  
 默认情况下，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库在请求 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务时不提供凭据。  如果数据服务需要登录凭据以进行用户身份验证，可以在 <xref:System.Net.NetworkCredential>（可通过 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> 属性访问）中提供凭据，如下例所示：  
  
  
  
 有关更多信息，请参见[如何：为数据服务请求指定客户端凭据](../../../../docs/framework/data/wcf/specify-client-creds-for-a-data-service-request-wcf.md)。  
  
 如果数据服务需要的登录凭据不能通过使用 <xref:System.Net.NetworkCredential> 对象（如基于声明的标记或 Cookie）指定，则必须在 HTTP 请求中手动设置标头，通常是 `Authorization` 和 `Cookie` 标头。  有关这种身份验证方案的更多信息，请参见 [OData 和身份验证：客户端一侧的挂钩](http://go.microsoft.com/fwlink/?LinkID=200385)一文。  有关如何在请求消息中设置 HTTP 标头的示例，请参见[如何：设置客户端请求中的标头](../../../../docs/framework/data/wcf/how-to-set-headers-in-the-client-request-wcf-data-services.md)。  
  
## 模拟  
 通常，数据服务使用承载数据服务的工作进程的凭据访问所需资源，如服务器上的文件或数据库。  使用模拟时，[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序可以用发出请求的用户的 Windows 标识（用户帐户）执行。  模拟通常用在依赖 IIS 进行用户身份验证的应用程序中，并使用该主体的凭据访问所需资源。  有关更多信息，请参见 [ASP.NET Impersonation](../Topic/ASP.NET%20Impersonation.md)。  
  
## 配置数据服务授权  
 授权是基于之前的成功身份验证为所识别的主体或进程授予应用程序资源的访问权限。  作为一种通行做法，只应当为数据服务的用户授予刚好足够的权限以执行客户端应用程序所需的操作。  
  
### 限制对数据服务资源的访问  
 默认情况下，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]允许为能够访问数据服务的任何用户授予数据服务资源（实体集和服务操作）的常用读取和写入访问权限。  可以为数据服务公开的每个实体集分别定义用于定义读取和写入访问权限的规则。  我们建议将读取和写入访问权限仅限于客户端应用程序所需的资源。  有关更多信息，请参见[最低资源访问要求](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md#accessRequirements)。  
  
### 实现基于角色的侦听器  
 侦听器可用于在数据服务对数据服务资源采取操作之前截取对它们的请求。  有关更多信息，请参见[侦听器](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md)。  拦截器可让您基于发出请求的已进行身份验证的用户作出授权决策。  [!INCLUDE[crexample](../../../../includes/crexample-md.md)] 有关如何基于已进行身份验证的用户标识限制对数据服务资源访问的示例，请参见[如何：截获数据服务消息](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md)。  
  
### 限制对持久数据存储区和本地资源的访问  
 用于访问持久存储区的帐户应仅授予刚好足够的数据库或文件系统权限以支持数据服务的要求。  在使用匿名身份验证时，这是用于运行宿主应用程序的帐户。  有关更多信息，请参见[如何：开发在 IIS 上运行的 WCF 数据服务](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)。  使用模拟时，必须为经过身份验证的用户授予这些资源的访问权限，通常是作为 Windows 组的一部分。  
  
## 其他安全注意事项  
  
### 负载中的数据安全  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 以 HTTP 协议为基础。  在 HTTP 消息中，标头可能包含重要的用户凭据，具体取决于数据服务实现的身份验证。  消息正文还可能包含必须予以保护的重要客户数据。  在这两种情况下，我们建议使用 SSL 在网络上保护此信息。  
  
### 忽略的消息标头和 Cookie  
 除了声明内容类型和资源位置以外的 HTTP 请求标头将被忽略，数据服务永远不会设置它们。  
  
 Cookie 可用作身份验证方案的一部分，例如在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Forms 身份验证中。  但是，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]会忽略传入请求上设置的任何 HTTP Cookie。  数据服务的宿主可能会处理该 Cookie，但 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]运行时永远不会分析或返回 Cookie。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库也不会处理在响应中发送的 Cookie。  
  
### 自定义承载要求  
 默认情况下，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]将创建为一个承载于 IIS 中的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序。  这样数据服务便可以利用该平台的安全行为。  可以定义由自定义宿主承载的 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]。  有关更多信息，请参见[承载数据服务](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)。  承载数据服务的组件和平台还必须确保以下安全行为以防范对数据服务的攻击：  
  
-   限制针对所有可能操作的数据服务请求中接受的 URI 的长度。  
  
-   限制传入和传出 HTTP 消息的大小。  
  
-   限制任何给定时间点的未完成请求的总数。  
  
-   限制 HTTP 标头及其值的大小，并提供对数据标头的 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]访问。  
  
-   检测和计数已知攻击，如 TCP SYN 和消息重播攻击。  
  
### 值不进一步编码  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]运行时不对发送到数据服务的属性值进行进一步编码。  例如，当某个实体的字符串属性包含带格式的 HTML 内容时，数据服务不对标记进行 HTML 编码。  数据服务也不会在响应中对属性值进行进一步编码。  客户端库也不会执行任何其他编码。  
  
### 客户端应用程序的注意事项  
 以下安全注意事项适用于使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务的应用程序：  
  
-   客户端库假定用于访问数据服务的协议提供了适当安全级别。  
  
-   客户端库使用基础平台提供的传输堆栈的超时和分析选项的全部默认值。  
  
-   客户端库不从应用程序配置文件中读取任何设置。  
  
-   客户端库不实现任何跨域访问机制，  而是依赖于基础 HTTP 堆栈提供的机制。  
  
-   客户端库没有用户界面元素，并且它从不尝试显示或呈现它所接收或发送的数据。  
  
-   我们建议客户端应用程序始终对用户输入以及接受自非信任服务的数据进行验证。  
  
## 请参阅  
 [定义 WCF 数据服务](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)