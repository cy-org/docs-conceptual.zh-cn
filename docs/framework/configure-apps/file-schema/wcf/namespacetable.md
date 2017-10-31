---
title: "&lt;namespaceTable&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 64801766-01b7-4c65-9ce6-70ad5af67689
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;namespaceTable&gt;
表示用于定义一组元素的配置节，这些元素包含随后可在 XPath 筛选器中用于路由的前缀映射的命名空间。  
  
## 语法  
  
```vb  
  
<routing>  
   <namespaceTable>  
     <add namespace="String" prefix="String" />   
   </namespaceTable>  
</routing>  
  
```  
  
```csharp  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<筛选器\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filter.md)|定义用于 XPath 表达式的命名空间前缀映射。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|表示用于定义一组路由筛选器的配置节，这些筛选器确定计算传入消息时使用的 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] <xref:System.ServiceModel.Dispatcher.MessageFilter> 的类型，以及用于定义在筛选器匹配时消息发送到的目标终结点的路由表。|  
  
## 请参阅  
 [System.ServiceModel.Routing.Configuration.NamespaceElementCollection](assetId:///System.ServiceModel.Routing.Configuration.NamespaceElementCollection?qualifyHint=False&amp;autoUpgrade=True)