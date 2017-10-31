---
title: "&lt;serviceHostingEnvironment&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 4f8a7c4f-e735-4987-979a-b74fcdae2652
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# &lt;serviceHostingEnvironment&gt;
此元素定义服务主机环境要为特定传输实例化的类型。  如果此元素为空，则使用默认类型。  此元素只能在应用程序或计算机级别的配置文件中使用。  
  
## 语法  
  
```  
  
<serviceHostingEnvironment  
     aspNetCompatibilityEnabled="Boolean"  
     minFreeMemoryPercentageToActivateService="Integer"  
     multipleSiteBindingsEnabled="Boolean">  
     <baseAddressPrefixFilters>  
        <add prefix="string"/>  
     </baseAddressPrefixFilters>  
      <serviceActivations>  
        <add factory="String" service="String"/>  
      </serviceActivations>  
     <transportConfigurationTypes>  
        <add name="String"   
             transportConfigurationType="String" />  
     </transportConfigurationTypes>  
</serviceHostingEnvironment>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|aspNetCompatibilityEnabled|一个布尔值，指示是否已为当前应用程序启用了 ASP.NET 兼容模式。  默认值为 `false`。<br /><br /> 当此属性设置为 `true` 时，对 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务的请求将流经 ASP.NET HTTP 管道，而通过非 HTTP 协议的通信将被禁止。  有关详细信息，请参阅[WCF 服务和 ASP.NET](../../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)。|  
|minFreeMemoryPercentageToActivateService|一个整数，指定在可以激活 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务之前，系统应该具有的最小可用内存量。 **Caution:**  若将此属性连同 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的 web.config 文件中的部分信任一起指定，会导致在该服务运行时发生 <xref:System.Security.SecurityException>。|  
|multipleSiteBindingsEnabled|一个布尔值，指定是否对每个站点启用多个 IIS 绑定。<br /><br /> IIS 由网站组成，这些网站是包含虚拟目录的虚拟应用程序的容器。  可通过一个或多个 IIS 绑定访问站点上的应用程序。  一个 IIS 绑定提供两条信息：绑定协议和绑定信息。  绑定协议定义进行通信所依据的方案，而绑定信息是用于访问站点的信息。  绑定协议的一个示例可以是 HTTP，而绑定信息可包含 IP 地址、端口、主机标头等。<br /><br /> IIS 支持一个站点指定多个 IIS 绑定，这会导致一个方案有多个基址。  但是，在一个站点下承载的 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务允许每个方案只绑定一个 BbaseAddress。<br /><br /> 若要为 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务对每个站点启用多个 IIS 绑定，请将此特性设置为 `true`。  请注意，仅对 HTTP 协议支持多个站点绑定。  配置文件中的终结点地址需要是一个完整的 URI。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<baseAddressPrefixFilters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md)|一个配置元素的集合，这些元素指定服务主机所使用的基址的前缀筛选器。|  
|[\<serviceActivations\>](../../../../../docs/framework/configure-apps/file-schema/wcf/serviceactivations.md)|一个描述激活设置的配置节。|  
|[\<transportConfigurationTypes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transportconfigurationtypes.md)|一个配置元素的集合，这些元素标识特定传输的类型。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|serviceModel|所有 Windows Communication Foundation \(WCF\) 配置元素的根元素。|  
  
## 备注  
 默认情况下，WCF 服务和 ASP.NET 一起在寄宿应用程序域 \(AppDomain\) 中并行运行。  即使 WCF 和 ASP.NET 可以在同一 AppDomain 中共存，但在默认情况下，ASP.NET HTTP 管道不会处理 WCF 请求。  因此，WCF 服务不能使用 ASP.NET 应用程序平台的一些元素，  其中包括  
  
-   ASP.NET File\/URL 授权  
  
-   ASP.NET 模拟  
  
-   基于 Cookie 的会话状态  
  
-   HttpContext.Current  
  
-   通过自定义 HttpModule 获得的管道扩展性  
  
 如果要使 WCF 服务在 ASP.NET 上下文中正常工作并仅通过 HTTP 进行通信，则可以使用 WCF 的 ASP.NET 兼容模式。  当 `aspNetCompatibilityEnabled` 属性在应用程序级别中设置为 `true` 时，此模式将启用。  服务实现必须使用 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 类来声明其可以在兼容模式中运行。  当启用此兼容模式时，  
  
-   ASP.NET File\/URL 授权将在 WCF 授权之前强制执行。  授权决定是基于请求的传输级标识的。  消息级别的标识将被忽略。  
  
-   WCF 服务操作开始是在 ASP.NET 模拟上下文中执行的。  如果为某个特定服务同时启用了 ASP.NET 模拟和 WCF 模拟，则将应用 WCF 模拟上下文。  
  
-   可以通过 WCF 服务代码使用 HttpContext.Current，并且阻止服务公开非 HTTP 终结点。  
  
-   WCF 请求由 ASP.NET 管道处理。  已配置为对传入请求执行操作的 HttpModule 也可以处理 WCF 请求。  这些 HttpModule 可包括 ASP.NET 平台组件（如 <xref:System.Web.SessionState.SessionStateModule>）以及自定义第三方模块。  
  
## 示例  
 下面的代码示例演示如何启用 ASP 兼容模式。  
  
## 代码  
  
```  
<serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>   
 [承载](../../../../../docs/framework/wcf/feature-details/hosting.md)   
 [WCF 服务和 ASP.NET](../../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)