---
title: "&lt;cancelRequestedQueries&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: eab5af7e-76fa-434d-9d36-873e995cee05
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;cancelRequestedQueries&gt;
表示一个查询集合，这些查询用于跟踪父活动取消子活动的请求。  跟踪参与者需要用此查询来订阅取消请求记录对象。  
  
 有关跟踪配置文件查询的更多信息，请参见[跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)  
  
## 语法  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <cancelRequestQueries>  
             <cancelRequestQuery activityName="String"  
                 childActivityName="String"/>  
          </cancelRequestQueries>  
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<cancelRequestedQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/cancelrequestedquery.md)|一个查询，用于跟踪父活动取消子活动的请求|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<workflow\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflow.md)|一个配置元素，包含 **activityDefinitionId** 属性所标识的特定工作流的所有查询。|  
  
## 请参阅  
 [System.ServiceModel.Activities.Tracking.Configuration.CancelRequestQueryElementCollection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.CancelRequestQueryElementCollection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.CancelRequestQuery](assetId:///System.Activities.Tracking.CancelRequestQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [工作流跟踪](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)