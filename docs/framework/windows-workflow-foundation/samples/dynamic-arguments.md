---
title: "动态参数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 122ad479-d306-4602-a943-5aefe711329d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 动态参数
此示例演示如何实现由活动使用方而不是活动作者为其定义参数的活动。此示例是通过重写运行时构造活动元数据的方式来做到这一点的。  
  
## 示例详细信息  
 在执行之前，运行时通过以下方法生成活动的描述：检查活动类型的公共成员，并自动声明参数、变量、子级活动和活动委托作为活动元数据一部分。这样做可确保构造正确的工作流，以及管理运行时关系和生存期规则。通常，活动作者通过指定派生自 <xref:System.Activities.Argument> 的活动类型的公共成员，定义活动的参数。对于每个派生自 <xref:System.Activities.Argument> 的公共成员，运行时创建一个 <xref:System.Activities.RuntimeArgument>，并将其绑定到该成员上用户提供的参数集。但是，在某些情况下，活动的使用方会提供一些可确定参数集的配置。活动作者重写 <xref:System.Activities.Activity.CacheMetadata%2A> 以自定义生成活动元数据的方式，其中包括与活动相关的参数集。  
  
 此示例演示如何为一个可调用方法的活动动态生成参数列表。活动使用方指定需要调用的类型和方法名称以及要传递到该方法的参数集合。  
  
> [!NOTE]
>  此示例的目的是演示如何重写 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 以及如何使用 <xref:System.Activities.RuntimeArgument>。关于此活动可以调用的方法的种类有一些要注意的事项。例如，它不能使用泛型数组或参数数组。.NET Framework 中随附的 <xref:System.Activities.Statements.InvokeMethod> 活动可处理这些情况以及其他情况。  
  
 `MethodInvoke` 活动重写 <xref:System.Activities.CodeActivity.CacheMetadata%2A>，并首先创建 <xref:System.Activities.RuntimeArgument> 以处理方法调用的任何结果。它将此 <xref:System.Activities.RuntimeArgument> 绑定到名为 `Result` 的公共的、可设置的 <xref:System.Activities.OutArgument>。如果 `MethodInvoke.Result` 为 `null`，则运行时会自动使用一个 <xref:System.Activities.OutArgument>（配置为对其类型使用默认表达式）填充它。此行为意味着，活动作者从来不必检查参数属性是否为 `null`。  
  
 接下来，<xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写从用户提供的 `MethodName` 和 `TargetType` 中确定它用于调用的 `MethodInfo`。`DetermineMethodInfo` 方法采用传递到 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 重写的 <xref:System.Activities.CodeActivityMetadata> 参数，以便可以将任何配置错误报告为验证错误。可以通过调用 `metadata.AddValidationError` 来完成此操作。  
  
 在设置 `MethodInfo` 之后，此示例将循环访问 `MethodInfo` 参数。对于每个参数，它将创建一个 <xref:System.Activities.RuntimeArgument>，并将其从 `Parameters` 属性绑定到用户提供的集合中的对应参数。最后，通过调用 `metadata.SetArgumentsCollection`，将 <xref:System.Activities.RuntimeArgument> 的集合与该活动关联。  
  
 请注意，可以使用 <xref:System.Activities.RuntimeArgument> 进行参数解析，就如同处理 `resultArgument` 或用户提供的参数以及 `Parameters` 集合一样。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 DynamicArguments.sln 文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\DynamicArguments`  
  
## 请参阅