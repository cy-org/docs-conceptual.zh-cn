---
title: "变量和参数跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f3d9d30-d899-49aa-b7ce-a8d0d32c4ff0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 变量和参数跟踪
当跟踪工作流的执行时，提取数据往往很有用。这在访问跟踪记录后续执行时可提供其他上下文。在 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中，您可以使用跟踪在工作流的任意活动范围内提取所有可见变量或参数。跟踪配置文件简化了对数据的提取。  
  
## 变量和参数  
 变量和参数在活动发出 ActivityStateRecord 时提取。仅当变量位于活动范围中时，才能提取该变量。按如下方式指定将在活动中提取的变量：  
  
-   如果变量用变量名称指定，跟踪则在正跟踪的当前活动和父活动中查找变量。系统将在当前活动范围和父范围中搜索变量。  
  
-   如果要提取的变量使用 name\="\*" 指定，则提取正跟踪的当前活动中的所有变量。此种情况下，将不会提取范围中在父活动中定义的变量。  
  
 当提取参数时，提取的参数依赖于活动状态。当活动状态为 Executing 时，只能提取 `InArguments`。对于任何其他活动状态（Closed、Faulted、Canceled），则可以提取所有参数，即 InArguments 和 OutArguments。  
  
 下面的示例演示用于在发出活动的 `Closed` 跟踪记录时提取变量和参数的活动状态查询。变量和参数只能使用 <xref:System.Activities.Tracking.ActivityStateRecord> 来提取，因此使用 <xref:System.Activities.Tracking.ActivityStateQuery> 在跟踪配置文件内进行订阅。  
  
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
  
## 保护存储在变量和参数中的信息  
 默认情况下，跟踪变量或参数对 WF 运行时可见。工作流开发人员可以采取以下步骤，阻止访问这些变量或参数：  
  
1.  对变量的值进行加密。  
  
2.  控制跟踪配置文件的创作，以阻止提取变量或参数。  
  
3.  对于自定义跟踪参与者，请确保 WF 代码不会泄露存储在变量或参数中的敏感信息。  
  
## 请参阅  
 [Windows Server App Fabric 监视](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [使用 App Fabric 监视应用程序](http://go.microsoft.com/fwlink/?LinkId=201275)