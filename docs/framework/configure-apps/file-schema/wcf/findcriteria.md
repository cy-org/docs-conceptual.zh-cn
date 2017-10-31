---
title: "&lt;findCriteria&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5454cd19-6bf5-4ba8-94d1-f58d10dc1917
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;findCriteria&gt;
一个配置元素，提供客户端应用程序用于搜索发现服务的一组条件。  可将这些条件划分为搜索条件（指定要查找的服务）和查找终止条件（搜索应持续的时长）。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <dynamicEndpoint>   
          <standardEndpoint>  
             <discoveryClientSettings discoveryEndpoint=”String” >  
               <findCriteria duration=”TimeSpan”  
                  maxResults=”Integer”   
                  scopeMatchBy=”Uri” >  
                  <contractTypeNames>  
                     <add name="String" namespace="String" />  
                  <contractTypeNames>  
                  <extensions />  
                  <scopes>  
                    <add scope="URI"/>  
                  </scopes>  
               </findCriteria>  
             </discoveryClientSettings>  
          <standardEndpoint>  
       </dynamicEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|duration|一个 Timespan 值，指定等待网络上的服务所发送的答复的最长时间。  默认持续时间为 20 秒。|  
|maxResults|一个整数，指定等待网络或 Internet 上的服务所发送的最大答复数。  如果在经过 `duration` 特性指定的值之前收到的答复达到了最大数目，则查找操作将结束。|  
|scopeMatchBy|一个 URI，指定当对 Probe 消息中的范围和终结点中的范围进行匹配时采用的匹配算法。<br /><br /> 支持五种范围匹配规则。  如果未指定范围匹配规则，则使用 `ScopeMatchByPrefix`。  有关这方面的更多信息，请参见 <xref:System.ServiceModel.Discovery.FindCriteria>。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<contractTypeNames\>](../../../../../docs/framework/configure-apps/file-schema/wcf/contracttypenames.md)|一个配置元素集合，这些元素包含工作流服务协定类型的名称。|  
|\<findCriteria\> 的 \<extensions\>|一个 XML 元素对象集合，这些对象提供扩展。|  
|[\<scopes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopes.md)|一个对象集合，这些对象包含在查找操作过程中用于查找一个或多个特定服务的绝对 URI。<br /><br /> 如果找到特定服务，则表示已在服务 URI 和范围 URI 之间进行了成功的匹配，此匹配操作有时是借助处理匹配复杂性的范围规则完成的。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|包含应用程序以客户端形式参与服务发现过程所需的设置。|  
  
## 请参阅  
 <xref:System.ServiceModel.Discovery.FindCriteria>   
 <xref:System.ServiceModel.Discovery.Configuration.FindCriteriaElement>