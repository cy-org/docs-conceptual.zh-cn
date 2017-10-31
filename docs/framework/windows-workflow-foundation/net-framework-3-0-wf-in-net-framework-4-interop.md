---
title: "在 .NET Framework 4 中将 .NET Framework 3.0 WF 活动与 Interop 活动一起使用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 71f112ba-abb0-46f7-b05f-a5d2eb9d0c5c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 在 .NET Framework 4 中将 .NET Framework 3.0 WF 活动与 Interop 活动一起使用
 <xref:System.Activities.Statements.Interop> 活动是 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] (WF 4.5) 活动包装 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 内的 (WF 3.5) 活动 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流。 WF 3 活动可以是单叶活动，也可以是整个活动树。 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 活动的执行（包括取消和异常处理）和持久化在执行的 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流实例的上下文中进行。  
  
> [!NOTE]
>   <xref:System.Activities.Statements.Interop> 活动不会不会显示在工作流设计器工具箱除非工作流的项目都有其 **目标框架** 设置设为 **.NET Framework 4.5**。  
  
## <a name="criteria-for-using-a-wf-3-activity-with-an-interop-activity"></a>将 WF 3 活动与 Interop 活动一起使用的条件  
 若要成功执行在使 WF 3 活动 <xref:System.Activities.Statements.Interop> 活动，必须满足以下条件︰  
  
-   WF 3 活动必须派生自 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName>。  
  
-   必须将 WF 3 活动声明为 `public`，不能为 `abstract`。  
  
-   WF 3 活动必须具有一个公共的默认构造函数。  
  
-   由于在界面中的限制类型 <xref:System.Activities.Statements.Interop> 活动可以支持， <xref:System.Workflow.Activities.HandleExternalEventActivity> 和 <xref:System.Workflow.Activities.CallExternalMethodActivity> 不能为使用直接，但是的派生活动创建工作流通信活动工具 (WCA.exe) 可以使用。 请参阅 [Windows Workflow Foundation 工具](http://go.microsoft.com/fwlink/?LinkId=178889) 有关的详细信息。  
  
## <a name="configuring-a-wf-3-activity-within-an-interop-activity"></a>在 Interop 活动中配置 WF 3 活动  
 若要配置和跨互操作边界将数据传入和传出 WF 3 活动，WF 3 活动的元数据属性公开的属性和 <xref:System.Activities.Statements.Interop> 活动。 WF 3 活动的元数据属性 (如 <xref:System.Workflow.ComponentModel.Activity.Name%2A>) 通过公开 <xref:System.Activities.Statements.Interop.ActivityMetaProperties%2A> 集合。 这是一个名称/值对的集合，用于为 WF 3 活动的元数据属性定义值。 元数据属性是为其支持依赖项属性的属性 <xref:System.Workflow.ComponentModel.DependencyPropertyOptions> 设置标志。  
  
 通过公开 WF 3 活动属性 <xref:System.Activities.Statements.Interop.ActivityProperties%2A> 集合。 这是一组名称 / 值对，其中每个值 <xref:System.Activities.Argument> 对象，用于为 WF 3 活动的属性定义参数。 由于无法推断 WF 3 活动属性的方向，每个属性呈现为 <xref:System.Activities.InArgument>/<xref:System.Activities.OutArgument> 对。 根据活动的使用情况的属性，您可能想要提供 <xref:System.Activities.InArgument> 条目， <xref:System.Activities.OutArgument> 条目，或两者。 所需的名称 <xref:System.Activities.InArgument> 对集合中的项的 WF 3 活动上定义为属性的名称。 所需的名称 <xref:System.Activities.OutArgument> 集合中的条目将是属性的名称和字符串"Out"的串联。  
  
## <a name="limitations-of-using-a-wf-3-activity-within-an-interop-activity"></a>在 Interop 活动中使用 WF 3 活动的限制  
 WF 3 系统提供的活动不能直接包装在 <xref:System.Activities.Statements.Interop> 活动。 对于某些 WF 3 活动，如 <xref:System.Workflow.Activities.DelayActivity>, ，这是因为存在类似的 WF 4.5 活动。 对于其他活动，这是因为不支持活动的这个功能。 许多 WF 3 系统提供的活动可以在通过包装的工作流使用 <xref:System.Activities.Statements.Interop> 活动，但受到以下限制︰  
  
1.  <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.Receive> 中不能使用 <xref:System.Activities.Statements.Interop> 活动。  
  
2.  <xref:System.Workflow.Activities.WebServiceInputActivity>, ，<xref:System.Workflow.Activities.WebServiceOutputActivity>, ，和 <xref:System.Workflow.Activities.WebServiceFaultActivity> 中不能使用 <xref:System.Activities.Statements.Interop> 活动。  
  
3.  <xref:System.Workflow.Activities.InvokeWorkflowActivity> 中不能使用 <xref:System.Activities.Statements.Interop> 活动。  
  
4.  <xref:System.Workflow.ComponentModel.SuspendActivity> 中不能使用 <xref:System.Activities.Statements.Interop> 活动。  
  
5.  中不能使用与补偿相关的活动 <xref:System.Activities.Statements.Interop> 活动。  
  
 另外，还有一些行为具体信息可了解有关使用 WF 3 活动内 <xref:System.Activities.Statements.Interop> 活动︰  
  
1.  WF 3 中包含的活动 <xref:System.Activities.Statements.Interop> 活动初始化时 <xref:System.Activities.Statements.Interop> 执行活动。 在 WF 4.5 中，执行之前工作流实例没有初始化阶段。  
  
2.  WF 4.5 运行时事务开始后，无论事务开始的位置没有检查点工作流实例状态 (内部还是外部 <xref:System.Activities.Statements.Interop> 活动)。  
  
3.  中活动的 WF 3 跟踪记录 <xref:System.Activities.Statements.Interop> 活动提供给 WF 4.5 跟踪参与者为 <xref:System.Activities.Tracking.InteropTrackingRecord> 对象。 <xref:System.Activities.Tracking.InteropTrackingRecord> 派生 <xref:System.Activities.Tracking.CustomTrackingRecord>。  
  
4.  WF 3 自定义活动可以在互操作环境中使用工作流队列访问数据，其访问方式与在 WF 3 工作流运行时中完全相同。 不需要更改任何自定义活动代码。 在主机上，数据排入 WF 3 工作流队列是通过恢复 <xref:System.Activities.Bookmark>。 书签的名称是字符串形式的 <xref:System.IComparable> 工作流队列名称。  
  
## <a name="see-also"></a>另请参阅  
 [在.NET Framework 4.5 工作流中使用.NET Framework 3.0 或.NET Framework 3.5 活动](../../../docs/framework/windows-workflow-foundation/samples/using-a-net-3-0-or-net-3-5-activity-in-a-net-4-5-workflow.md)