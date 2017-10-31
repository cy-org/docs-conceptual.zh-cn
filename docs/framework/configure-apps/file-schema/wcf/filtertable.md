---
title: "&lt;filterTable&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e9f05441-3ad1-49b9-a267-71724aa094b4
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;filterTable&gt;
表示一个路由表，此表包含计算消息所依据的筛选器的列表，以及当筛选器的计算结果为 true 时消息要路由到的客户端终结点。  
  
## 语法  
  
```vb  
  
<routing>  
      <filterTables>  
        <filterTable name="String">  
          <entries>  
            <add backupList=”String”  
                 endpointName="String"   
                 filterName="String"   
                 priority="Integer" />  
          </entries>  
        </table>  
      </routingTables>  
</routing>  
  
```  
  
```csharp  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|元素|描述|  
|--------|--------|  
|name|一个字符串，包含此配置元素的唯一名称。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<筛选器\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filters-of-routing.md)|路由筛选器与在筛选器匹配时消息要发送到的目标终结点之间的映射。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|一个包含路由表的配置节。|  
  
## 请参阅  
 [System.ServiceModel.Routing.Configuration.RoutingSection](assetId:///System.ServiceModel.Routing.Configuration.RoutingSection?qualifyHint=False&amp;autoUpgrade=True)