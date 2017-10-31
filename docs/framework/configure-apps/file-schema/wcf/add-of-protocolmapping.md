---
title: "&lt;protocolMapping&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 08e62249-1641-41d1-91b1-66d7b46244e4
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;protocolMapping&gt; 的 &lt;add&gt;
表示传输协议方案（如 http、net.tcp、net.pipe 等）和 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 绑定之间的默认协议映射。  当在运行时创建默认终结点时，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 将查看已配置的映射，并确定要用于基于特定内容的地址的绑定。  
  
## 语法  
  
```vb  
  
<protocolMapping>  
    <add binding="String”  
         bindingConfiguration="String”  
         scheme="http/net.msmq/net.pipe/net.tcp"/>  
</protocolMapping>  
  
```  
  
```csharp  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|元素|描述|  
|--------|--------|  
|绑定|一个字符串，指定在创建默认终结点时要用于终结点的绑定类型。|  
|bindingConfiguration|一个字符串，指定要引用的绑定配置节的名称。|  
|scheme|要用于默认终结点的传输协议方案。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<protocolMapping\>](../../../../../docs/framework/configure-apps/file-schema/wcf/protocolmapping.md)|表示一个配置节，用于定义传输协议方案（如 http、net.tcp、net.pipe 等）和 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 绑定之间的默认协议映射。|  
  
## 示例  
 下面的配置示例演示 machine.config 文件中的默认协议映射。  您可以通过修改 machine.config 文件在计算机级别重写此默认映射。  或者，如果您只希望在应用程序范围内重写此映射，则可以在应用程序配置文件中重写此节，并为单独的协议方案更改映射。  
  
```  
  
<protocolMapping>  
        <add scheme="http" binding="basicHttpBinding"/>  
        <add scheme="net.tcp" binding="netTcpBinding"/>  
        <add scheme="net.pipe" binding="netNamedPipeBinding"/>  
        <add scheme="net.msmq" binding="netMsmqBinding"/>  
</protocolMapping>  
  
```  
  
## 请参阅  
 [System.ServiceModel.Configuration.ProtocolMappingSection](assetId:///System.ServiceModel.Configuration.ProtocolMappingSection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.ServiceModel.Configuration.ProtocolMappingElement](assetId:///System.ServiceModel.Configuration.ProtocolMappingElement?qualifyHint=False&amp;autoUpgrade=True)