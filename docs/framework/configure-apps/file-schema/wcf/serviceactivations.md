---
title: "&lt;serviceActivations&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97e665b6-1c51-410b-928a-9bb42c954ddb
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;serviceActivations&gt;
一个配置元素，用于添加可定义虚拟服务激活设置（映射到 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务类型）的设置。  使用此配置元素可以在不使用 .svc 文件的情况下激活承载在 WAS\/IIS 中的服务。  
  
## 语法  
  
```  
  
<serviceHostingEnvironment>   
   <serviceActivations>  
      <add factory="String"  
           service="String"/>  
   </serviceActivations>  
</serviceHostingEnvironment>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-serviceactivations.md)|添加一个指定激活服务应用程序的配置元素。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|定义服务承载环境要为特定传输实例化的类型。|  
  
## 备注  
 下面的示例演示如何在 web.config 文件中配置激活设置。  
  
```  
<configuration>  
  <system.serviceModel>  
    <serviceHostingEnvironment>  
      <serviceActivations>  
        <add service="GreetingService"/>  
      </serviceActivations>  
    </serviceHostingEnvironment>  
  </system.serviceModel>  
</configuration>  
```  
  
 使用此配置，您可以在不使用 .svc 文件的情况下激活 GreetingService。  
  
 请注意，`<serviceHostingEnvironment>` 是应用程序级配置。  必须将包含此配置的 `web.config` 放置到虚拟应用程序的根目录下。  此外，`serviceHostingEnvironment` 是一个可继承的 machinetoApplication 节。  如果在计算机的根目录中注册了一个服务，应用程序中的每个服务都将继承此服务。  
  
 基于配置的激活支持通过 http 协议和非 http 协议进行激活。  它要求在 relatativeAddress 中使用扩展名，即  .svc、.xoml 或 .xamlx。  您可以将自己的扩展名映射到已知的 buildProviders，然后就可以通过任意扩展名激活服务。  如果发生冲突，`<serviceActivations>` 节将重写 .svc 注册。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ServiceActivationElementCollection>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>