---
title: "&lt;baseAddressPrefixFilter&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b226bede-8459-4de9-b2ac-3d39604ce2bc
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;baseAddressPrefixFilter&gt; 的 &lt;add&gt;
表示一个指定传递筛选器的配置元素。传递筛选器提供了一种机制，使得在 IIS 中承载 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 应用程序时可选取适当的 Internet 信息服务 \(IIS\) 绑定。  
  
## 语法  
  
```  
  
<serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="string"/>  
     </baseAddressPrefixFilters>  
</serviceHostingEnvironment>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|prefix|用于与基址的一部分进行匹配的 URI。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<baseAddressPrefixFilters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md)|一个指定传递筛选器的配置元素的集合。传递筛选器提供了一种机制，使得在 IIS 中承载 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 应用程序时可选取适当的 IIS 绑定。|  
  
## 备注  
 前缀筛选器为共享的宿主提供程序提供一种指定服务要使用的 URI 的方法。  它使得共享主机可以在同一站点上通过同一方案的不同基址承载多个应用程序。  
  
 IIS 网站是包含虚拟目录的虚拟应用程序的容器。  可通过一个或多个 IIS 绑定访问站点上的应用程序。  IIS 绑定提供两条信息：绑定协议和绑定信息。  绑定协议（例如 HTTP）定义发生通信所基于的方案，而绑定信息（例如 IP 地址、端口、主机头）包含用于访问站点的数据。  
  
 IIS 支持为每个站点指定多个 IIS 绑定，这会导致每个方案有多个基址。  因为一个站点承载的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务只允许绑定到每个方案的一个基址，所以您可以使用前缀筛选器功能选取所需的承载服务的基址。  根据可选前缀列表筛选器筛选 IIS 提供的传入基址。  
  
 例如，您的站点可包含以下基址。  
  
```  
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 可以使用下面的配置文件在 appdomain 级指定前缀筛选器。  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix=”net.tcp://test1.fabrikam.com:8000”/>  
        <add prefix=”http://test2.fabrikam.com:9000”/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 在此示例中，`net.tcp://test1.fabrikam.com:8000` 和 `http://test2.fabrikam.com:9000` 是允许传递的各自方案的唯一基址。  
  
 默认情况下，未指定前缀时，将传递所有地址。  而指定前缀后，将只允许传递该方案的匹配基址。  
  
> [!NOTE]
>  筛选器不支持任何通配符。  此外，IIS 提供的基址可能有绑定到在 `baseAddressPrefixFilters` 列表中未列出的其他方案的地址。  不会筛选出这些地址。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElement>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>   
 [承载](../../../../../docs/framework/wcf/feature-details/hosting.md)