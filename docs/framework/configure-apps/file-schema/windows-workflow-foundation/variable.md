---
title: "&lt;variable&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 46cc8cbc-10ec-4625-8813-3f5cd6c6afde
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;variable&gt;
表示与此活动查询关联的变量的集合。  
  
 有关跟踪配置文件查询的更多信息，请参见[跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
## 语法  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <activityStateQueries>  
             <activityStateQuery activityName="String" />  
                <variables>  
                   <variable name="String"/>  
                </variables>  
          </activityStateQueries>  
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|name|一个字符串，指定变量的名称。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<variable\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/variable.md)|与活动状态查询相关联的变量。|  
  
## 备注  
 ActivityStateQuery 的一项独特功能是能够在跟踪工作流的执行时提取数据。  这在访问跟踪记录后续执行时可提供其他上下文。  可以使用 [\<arguments\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/arguments.md)、[\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md) 和 [\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md) 元素从工作流中的任何活动提取任何变量或参数。下面的示例演示在发出活动的 `Closed` 跟踪记录时提取变量和参数的活动状态查询。  变量和参数只能使用 ActivityStateRecord 来提取，因此使用 [\<activityStateQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activitystatequery.md) 在跟踪配置文件内进行订阅。  
  
```  
  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
  
```  
  
## 请参阅  
 [System.ServiceModel.Activities.Tracking.Configuration.VariableElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.VariableElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.ActivityStateQuery](assetId:///System.Activities.Tracking.ActivityStateQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [工作流跟踪](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)