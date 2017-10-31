---
title: "如何：创建活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c09b1e99-21b5-4d96-9c04-ec31db3f4436
caps.latest.revision: 39
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# 如何：创建活动
活动是 [!INCLUDE[wf1](../../../includes/wf1-md.md)] 中的核心行为单元。活动的执行逻辑可以使用托管代码实现，也可以使用其他活动实现。本主题演示如何创建两个活动。第一个活动是简单活动，它使用代码来实现其执行逻辑。第二个活动的实现是用其他活动定义的。后续教程步骤会使用这些活动。  
  
> [!NOTE]
>  若要下载完整版教程，请参见 [Windows Workflow Foundation \(WF45\) — 入门教程](http://go.microsoft.com/fwlink/?LinkID=248976)。  
  
### 创建活动库项目  
  
1.  打开 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]，然后从**“文件”**菜单中依次选择**“新建”**和**“项目”**。  
  
2.  在**“已安装”**、**“模板”**列表中，展开**“其他项目类型”**节点，然后选择**“Visual Studio 解决方案”**。  
  
3.  从**“Visual Studio 解决方案”**列表中选择**“空白解决方案”**。请确保在 .NET Framework 版本下拉列表中选择**“.NET Framework 4.5”**。在**“名称”**框中键入 `WF45GettingStartedTutorial`，然后单击**“确定”**。  
  
4.  在**解决方案资源管理器**中右键单击**“WF45GettingStartedTutorial”**，然后依次选择**“添加”**和**“新建项目”**。  
  
    > [!TIP]
    >  如果未显示**解决方案资源管理器**窗口，请从**“视图”**菜单选择**“解决方案资源管理器**。  
  
5.  在**“已安装”**节点中，选择**“Visual C\#”**、**“工作流”**（或**“Visual Basic”**、**“工作流”**）。请确保在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 版本下拉列表中选择**“.NET Framework 4.5”**。从**“工作流”**列表中选择**“活动库”**。在**“名称”**框中，键入 `NumberGuessWorkflowActivities`，然后单击**“确定”**。  
  
    > [!NOTE]
    >  根据在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中配置为主要语言的编程语言，**“Visual C\#”**或**“Visual Basic”**节点可能位于**“已安装”**节点下的**“其他语言”**节点中。  
  
6.  在**解决方案资源管理器**中右键单击**“Activity1.xaml”**，然后选择**“删除”**。单击**“确定”**以确认。  
  
### 创建 ReadInt 活动  
  
1.  从**“项目”**菜单中选择**“添加新项”**。  
  
2.  在**“已安装”**、**“常用项”**节点中，选择**“工作流”**。从**“工作流”**列表中选择**“代码活动”**。  
  
3.  在**“名称”**框中键入 `ReadInt`，然后单击**“添加”**。  
  
4.  将现有的 `ReadInt` 定义替换为下面的定义。  
  
     [!code-csharp[CFX_WF_GettingStarted#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/readint.cs#1)]
     [!code-vb[CFX_WF_GettingStarted#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/readint.vb#1)]  
  
    > [!NOTE]
    >  `ReadInt` 活动派生自 <xref:System.Activities.NativeActivity%601> 而不是 <xref:System.Activities.CodeActivity>，这是默认的代码活动模板。如果活动提供单个结果，可以使用 <xref:System.Activities.CodeActivity%601>，它是通过 <xref:System.Activities.Activity%601.Result%2A> 参数公开的，但是 <xref:System.Activities.CodeActivity%601> 不支持使用书签，因此使用 <xref:System.Activities.NativeActivity%601>。  
  
### 创建 Prompt 活动  
  
1.  按 Ctrl\+Shift\+B 生成项目。通过生成项目，可以使用此项目中的 `ReadInt` 活动生成此步骤中的自定义活动。  
  
2.  从**“项目”**菜单中选择**“添加新项”**。  
  
3.  在**“已安装”**、**“常用项”**节点中，选择**“工作流”**。从**“工作流”**列表中选择**“活动”**。  
  
4.  在**“名称”**框中键入 `Prompt`，然后单击**“添加”**。  
  
5.  如果设计器中尚未显示**“Prompt.xaml”**工作流，请在**解决方案资源管理器**中双击该工作流，使其显示在设计器中。  
  
6.  单击活动设计器左下方的**“参数”**按钮，以显示**“参数”**窗格。  
  
7.  单击**“创建参数”**。  
  
8.  在**“名称”**框中键入 `BookmarkName`，从**“方向”**下拉列表中选择**“输入”**，再从**“参数类型”**下拉列表中选择**“String”**，然后按 Enter 保存该参数。  
  
9. 单击**“创建参数”**。  
  
10. 在新添加的 `BookmarkName` 参数下方的**“名称”**框中键入 `Result`，从**“方向”**下拉列表中选择**“输出”**，再从**“参数类型”**下拉列表中选择**“Int32”**，然后按 Enter。  
  
11. 单击**“创建参数”**。  
  
12. 在**“名称”**框中键入 `Text`，从**“方向”**下拉列表中选择**“输入”**，再从**“参数类型”**下拉列表中选择**“String”**，然后按 Enter 保存该参数。  
  
     在以下步骤中，这三个参数将绑定到添加到 `Prompt` 活动中的 <xref:System.Activities.Statements.WriteLine> 和 `ReadInt` 活动的相应参数。  
  
13. 单击活动设计器左下方的**“参数”**，以关闭**“参数”**窗格。  
  
14. 从**“工具箱”**的**“控制流”**部分中，将 **Sequence** 活动拖到 **Prompt** 活动设计器的**“在此处放置活动”**标签上。  
  
    > [!TIP]
    >  如果**“工具箱”**窗口未显示，请从**“视图”**菜单中选择**“工具箱”**。  
  
15. 从**“工具箱”**的**“基元”**部分中，将 **WriteLine** 活动拖到 **Sequence** 活动设计器的**“在此处放置活动”**标签上。  
  
16. 将 **WriteLine** 活动的 **Text** 参数绑定到 **Prompt** 活动的 **Text** 参数，方法是在**“属性”**窗口中的**“输入 C\# 表达式”**框或者**“输入 VB 表达式”**框中键入 `Text`，然后按 Tab 键两次。这会关闭 IntelliSense 列表成员窗口，并通过将选择范围移离属性保存属性值。通过在活动本身的**“输入 C\# 表达式”**或**“输入 VB 表达式”**框中键入 `Text`，也可以设置此属性。  
  
    > [!TIP]
    >  如果**“属性窗口”**未显示，请从**“视图”**菜单中选择**“属性窗口”**。  
  
17. 将 **ReadInt** 活动从**“工具箱”**的 **NumberGuessWorkflowActivities** 部分拖到 **Sequence** 活动中，以便它位于 **WriteLine** 活动之后。  
  
18. 将**“ReadInt”**活动的**“BookmarkName”**参数绑定到**“Prompt”**活动的**“BookmarkName”**参数，方法是在**“属性窗口”**中**“BookmarkName”**参数右侧的**“输入 VB 表达式”**框中键入 `BookmarkName`，然后按 Tab 键两次以关闭 IntelliSense“列出成员”窗口并保存该属性。  
  
19. 将**“ReadInt”**活动的**“Result”**参数绑定到**“Prompt”**活动的**“Result”**参数，方法是在**“属性窗口”**中**“Result”**参数右侧的**“输入 VB 表达式”**框中键入 `Result`，然后按 Tab 键两次。  
  
20. 按 Ctrl\+Shift\+B 生成解决方案。  
  
     有关如何使用这些活动创建工作流的说明，请参见教程的下一步骤[如何：创建工作流](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)。  
  
## 请参阅  
 <xref:System.Activities.CodeActivity>   
 <xref:System.Activities.NativeActivity%601>   
 [设计和实现自定义活动](../../../docs/framework/windows-workflow-foundation//designing-and-implementing-custom-activities.md)   
 [入门教程](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)   
 [如何：创建工作流](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)   
 [在自定义设计器中使用 ExpressionTextBox](../../../docs/framework/windows-workflow-foundation/samples/using-the-expressiontextbox-in-a-custom-activity-designer.md)