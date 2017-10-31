---
title: "For 活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2ea751b4-36f0-48aa-a115-70a2ab89f6d8
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# For 活动
For 示例演示如何生成一个继承自 <xref:System.Activities.NativeActivity> 的自定义活动，以及如何在工作流中使用此活动来执行实际示例。该示例中包含的自定义活动的功能与 C\# `for` 语句的功能类似。  
  
 `For` 自定义活动具有名为 `InitAction`、`IterationAction`、`Condition` 和 `Body` 的属性，这些属性分别对应于标准 C\# `For` 语句中包含的初始化语句、交互式语句、继续条件和正文语句。  
  
 下表说明示例中的主要文件。  
  
|文件|说明|  
|--------|--------|  
|For.cs|`For` 自定义活动的类定义，它扩展 <xref:System.Activities.NativeActivity> 类以提供 C\# `For` 语句的功能。|  
|Program.cs|一个客户端应用程序，它使用自定义 `For` 活动对集合执行基本交互式工作。|  
  
> [!NOTE]
>  在使用 `For` 自定义活动时，请确保设置了 `Condition` 属性；否则，将出现无限循环。  
  
## 演示  
 创建从 <xref:System.Activities.NativeActivity> 继承的自定义活动。  
  
## 讨论  
 下表介绍了此示例中包含的活动的属性。  
  
 InitAction  
 初始化语句  
  
 IterationAction  
 交互式语句  
  
 Condition  
 继续语句  
  
 Body  
 正文语句  
  
 此活动从 <xref:System.Activities.NativeActivity> 继承，以通过使用 <xref:System.Activities.NativeActivityContext> 的 `ScheduleActivity` 方法之一来获取对运行时功能（如计划要运行的其他活动）的访问权。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]，打开 For.sln 解决方案文件。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 F5 运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\For`  
  
## 请参阅