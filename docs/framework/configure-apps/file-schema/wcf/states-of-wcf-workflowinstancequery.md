---
title: "WCF 的 &lt;states&gt;，&lt;workflowInstanceQuery&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d17f7525-8035-4e9e-85a0-4cddae59f85d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# WCF 的 &lt;states&gt;，&lt;workflowInstanceQuery&gt;
表示创建跟踪记录时已跟踪工作流实例中已订阅状态的集合。  
  
 有关跟踪配置文件查询的更多信息，请参见[跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)。  
  
## 语法  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <workflowInstanceQueries>  
             <workflowInstanceQuery>  
                <states>  
                   <state name="Name"/>  
                </states>  
            </workflowInstanceQuery>  
         </workflowInstanceQueries>  
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
|[\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md)|创建跟踪记录时已跟踪工作流实例中的一个已订阅状态。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<workflowInstanceQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancequery.md)|一个查询，该查询跟踪工作流实例生命周期的更改，例如已开始或已完成的事件。|  
  
## 备注  
 返回的记录由此集合中的状态进行筛选。  
  
 下表中列出了可能的状态值。  
  
|状态|描述|  
|--------|--------|  
|Aborted|工作流实例已中止。|  
|已完成|工作流实例已完成。|  
|Deleted|工作流实例已删除。|  
|Idle|工作流实例处于空闲状态。|  
|Persisted|工作流实例已保留。|  
|Resumed|工作流实例已恢复。|  
|Started|工作流实例已启动。|  
|UnhandledException|工作流实例遇到了未经处理的异常。|  
|Unloaded|工作流实例已卸载。|  
|Canceled|工作流实例已取消。|  
|挂起|工作流实例处于挂起状态。|  
|Terminated|工作流实例已终止。|  
|Unsuspended|工作流实例已取消挂起。|  
  
## 示例  
 下面的配置使用此查询订阅 `Started` 实例状态的工作流实例级跟踪记录。  
  
```  
  
<workflowInstanceQueries>  
    <workflowInstanceQuery>  
      <states>  
        <state name="Started"/>  
      </states>  
    </workflowInstanceQuery>  
</workflowInstanceQueries>  
  
```  
  
## 请参阅  
 [System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.WorkflowInstanceQuery](assetId:///System.Activities.Tracking.WorkflowInstanceQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [工作流跟踪](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [跟踪配置文件](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)