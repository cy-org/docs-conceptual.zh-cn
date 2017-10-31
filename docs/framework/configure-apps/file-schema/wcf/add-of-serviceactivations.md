---
title: "&lt;serviceActivations&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5b01fc8-ee84-48b7-95fd-95ab54fa871f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;serviceActivations&gt; 的 &lt;add&gt;
一个配置元素，用于定义虚拟服务激活设置（映射到 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务类型）的设置。  使用此配置元素可以在不使用 .svc 文件的情况下激活承载在 WAS\/IIS 中的服务。  
  
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
  
|特性|描述|  
|--------|--------|  
|factory|一个字符串，指定生成服务激活元素的工厂的 CLR 类型名称。|  
|service|实现服务的 ServiceType（完全限定的 Typename 或短的 Typename（将它置于 App\_Code 文件夹中时））。|  
|relativeAddress|当前 IIS 应用程序内的相对地址，例如“Service.svc”。  在 WCF4.0 中，此相对地址必须包含其中一个已知文件扩展名（.svc、.xamlx、...）之一。  relativeUrl 不存在于任何物理文件中|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|一个描述激活设置的配置节。|  
  
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
 <xref:System.ServiceModel.Configuration.ServiceActivationElement>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>