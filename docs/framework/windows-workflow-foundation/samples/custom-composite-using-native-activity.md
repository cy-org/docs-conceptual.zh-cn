---
title: "使用本机活动的自定义复合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef9e739c-8a8a-4d11-9e25-cb42c62e3c76
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 使用本机活动的自定义复合
此示例演示如何编写一个 <xref:System.Activities.NativeActivity>，该活动安排其他 <xref:System.Activities.Activity> 对象以控制工作流的执行流。此示例使用两个通用的控制流（Sequence 和 While）来演示如何做到这一点。  
  
## 示例详细信息  
 从开始 `MySequence`，注意到的第一件事就是从  <xref:System.Activities.NativeActivity> 派生。<xref:System.Activities.NativeActivity> 是  <xref:System.Activities.Activity> 对象公开的工作流运行时通过完整的广度的 <xref:System.Activities.NativeActivityContext> 传递给 `Execute` 方法。  
  
 `MySequence` 公开 <xref:System.Activities.Activity> 对象的一个公共集合，此对象集合由工作流作者填充。在执行工作流之前，工作流运行时会对工作流中的每个活动调用 <xref:System.Activities.Activity.CacheMetadata%2A> 方法。在此过程中，运行时将建立用于数据范围限定和生存期管理的父子关系。<xref:System.Activities.Activity.CacheMetadata%2A> 方法的默认实现使用 `MySequence` 活动的 <xref:System.ComponentModel.TypeDescriptor> 实例类来添加 <xref:System.Activities.Activity> 或 <xref:System.Collections.IEnumerable>\<<xref:System.Activities.Activity>\> 类型的任何公共属性作为 `MySequence` 活动的子级。  
  
 当一个活动公开子级活动的公共集合时，这些子级活动可能会共享状态。对于父级（在此例中为 `MySequence`）而言，最佳做法是也公开一个变量集合，以便子级活动能够通过这些变量来完成上述任务。与子级活动类似，<xref:System.Activities.Activity.CacheMetadata%2A> 方法将添加 <xref:System.Activities.Variable> 或 <xref:System.Collections.IEnumerable>\<<xref:System.Activities.Variable>\> 类型的公共属性作为与 `MySequence` 活动关联的变量。  
  
 除了由 `MySequence` 的子级操作的公共变量之外，`MySequence` 还必须跟踪它在执行其子级时的位置。为了完成此任务，它使用一个私有变量 `currentIndex`。通过在 `MySequence` 活动的 <xref:System.Activities.Activity.CacheMetadata%2A> 方法内添加对 <xref:System.Activities.NativeActivityMetadata.AddImplementationVariable%2A> 方法的调用，将此变量作为 `MySequence` 环境的一部分进行注册。添加到 `MySequence` `Activities` 集合的 <xref:System.Activities.Activity> 对象无法访问通过这种方式添加的变量。  
  
 当运行时执行 `MySequence` 时，运行时将调试其 <xref:System.Activities.NativeActivity.Execute%2A> 方法，并传入一个 <xref:System.Activities.NativeActivityContext>。<xref:System.Activities.NativeActivityContext> 是该活动的代理运行时取消引用参数和变量，以及其他调度的回 <xref:System.Activities.Activity> 对象，或  `ActivityDelegates`。`MySequence` 使用 `InternalExecute` 方法封装在单一方法中计划第一个子级和所有后续子级的逻辑。它首先取消引用 `currentIndex`。如果它等于 `Activities` 集合中的计数，则完成序列，该活动将返回而不计划任何工作，并且运行时将它移动到 <xref:System.Activities.ActivityInstanceState> 状态。如果 `currentIndex` 小于活动的计数，则从 `Activities` 集合获取下一个子级，然后 `MySequence` 调用 <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>，并传入要计划的子级和一个指向 `InternalExecute` 方法的 <xref:System.Activities.CompletionCallback>。最后，递增 `currentIndex`，并将控制权交回给运行时。只要 `MySequence` 的实例已计划一个 <xref:System.Activities.Activity> 对象，运行时就会认为它处于“正在执行”状态。  
  
 当子级活动完成时，将执行 <xref:System.Activities.CompletionCallback>。循环将从顶部继续。与 `Execute` 类似，<xref:System.Activities.CompletionCallback> 采用一个 <xref:System.Activities.NativeActivityContext>，以便实现者能够访问运行时。  
  
 `MyWhile` 与 `MySequence` 的不同之处在于，它会重复计划一个 <xref:System.Activities.Activity> 对象，并使用一个名为 `Condition` 的 <xref:System.Activities.Activity%601>\<bool\> 来确定此计划是否应发生。与 `MySequence` 类似，`MyWhile` 使用 `InternalExecute` 方法来集中其计划逻辑。它通过使用一个名为 `OnEvaluationCompleted` 的 <xref:System.Activities.CompletionCallback%601>\<bool\> 来计划 `Condition`<xref:System.Activities.Activity>\<bool\>。执行完 `Condition` 之后，可以通过此 <xref:System.Activities.CompletionCallback> 在一个名为 `result` 的强类型参数中获得执行结果。如果结果为 `true`，`MyWhile` 将调用 <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>，并传入 `Body`<xref:System.Activities.Activity> 对象和 `InternalExecute` 作为 <xref:System.Activities.CompletionCallback>。执行完 `Body` 之后，在 `InternalExecute` 中又会再次计划 `Condition`，开始再次循环。如果 `Condition` 返回 `false`，则 `MyWhile` 的实例会将控制权交回给运行时而不计划 `Body`，运行时会将其移动到 <xref:System.Activities.ActivityInstanceState> 状态。  
  
#### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 Composite.sln 示例解决方案。  
  
2.  生成和运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\CustomCompositeNativeActivity`  
  
## 请参阅