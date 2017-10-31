---
title: "如何：创建顺序工作流 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5280e816-ae17-48c4-8de0-a1e6895dd8f0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：创建顺序工作流
工作流可基于内置活动以及自定义活动来构造。本主题分步介绍如何创建使用内置活动（如 <xref:System.Activities.Statements.Sequence> 活动）以及之前的[如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)主题中的自定义活动的工作流。该工作流模拟猜数游戏。  
  
> [!NOTE]
>  入门教程中的每个主题都依赖于前面的主题。若要完成本主题，必须先完成[如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)。  
  
> [!NOTE]
>  若要下载完整版教程，请参见 [Windows Workflow Foundation \(WF45\) \- 入门教程](http://go.microsoft.com/fwlink/?LinkID=248976)。  
  
### 创建工作流  
  
1.  在**解决方案资源管理器**中右键单击**“NumberGuessWorkflowActivities”**，并依次选择**“添加”**、**“新建项目”**。  
  
2.  在**“已安装”**、**“常用项”**节点中，选择**“工作流”**。从**“工作流”**列表中选择**“活动”**。  
  
3.  将 `SequentialNumberGuessWorkflow` 键入**“名称”**框中，然后单击**“添加”**。  
  
4.  从**“工具箱”**的**“控制流”**部分，将一个**“Sequence”**活动拖放到工作流设计图面上的**“在此处放置活动”**标签上。  
  
### 创建工作流变量和参数  
  
1.  如果设计器中尚未显示**“SequentialNumberGuessWorkflow.xaml”**工作流，请在**解决方案资源管理器**中双击该工作流，使其显示在设计器中。  
  
2.  单击工作流设计器左下方的**“参数”**，以显示**“参数”**窗格。  
  
3.  单击**“创建参数”**。  
  
4.  在**“名称”**框中键入 `MaxNumber`，从**“方向”**下拉列表中选择**“输入”**，再从**“参数类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该参数。  
  
5.  单击**“创建参数”**。  
  
6.  在新添加的 `MaxNumber` 参数下方的**“名称”**框中键入 `Turns`，从**“方向”**下拉列表中选择**“输出”**，再从**“参数类型”**下拉列表中选择**“Int32”**，然后按 Enter。  
  
7.  单击活动设计器左下方的**“参数”**，以关闭**“参数”**窗格。  
  
8.  单击工作流设计器左下方的**“变量”**，以显示**“变量”**窗格。  
  
9. 单击**“创建变量”**。  
  
    > [!TIP]
    >  如果未显示**“创建变量”**框，请单击工作流设计器图面上的**“Sequence”**活动以将其选中。  
  
10. 在**“名称”**框中键入 `Guess`，从**“变量类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该变量。  
  
11. 单击**“创建变量”**。  
  
12. 在**“名称”**框中键入 `Target`，从**“变量类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该变量。  
  
13. 单击活动设计器左下方的**“变量”**，以关闭**“变量”**窗格。  
  
### 添加工作流活动  
  
1.  从**“工具箱”**的**“基元”**部分，将一个**“Assign”**活动拖放到**“Sequence”**活动上。在**“To”**框中键入 `Target`，并将以下表达式键入**“输入 C\# 表达式”**或**“输入 VB 表达式”**框中。  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    >  如果**“工具箱”**窗口未显示，请从**“视图”**菜单中选择**“工具箱”**。  
  
2.  从**“工具箱”**的**“控制流”**部分，将一个**“DoWhile”**活动拖放至工作流中**“Assign”**活动之下。  
  
3.  在**“DoWhile”**活动的**“Condition”**属性值框中，键入以下表达式。  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
     <xref:System.Activities.Statements.DoWhile> 活动执行其子活动，然后计算其 <xref:System.Activities.Statements.DoWhile.Condition%2A>。如果 <xref:System.Activities.Statements.DoWhile.Condition%2A> 的计算结果为 `True`，则再次执行 <xref:System.Activities.Statements.DoWhile> 中的活动。在此示例中，将计算用户的猜测值，并且 <xref:System.Activities.Statements.DoWhile> 继续执行，直到猜测值正确。  
  
4.  从**“工具箱”**的**“NumberGuessWorkflowActivities”**部分，将一个**“Prompt”**活动拖放至上一步的**“DoWhile”**活动中。  
  
5.  在**“属性窗口”**中，将包括引号的 `"EnterGuess"` 键入**“Prompt”**活动的**“BookmarkName”**属性值框中。在**“Result”**属性值框中键入 `Guess`，并在**“Text”**属性框中键入以下表达式。  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
    > [!TIP]
    >  如果**“属性窗口”**未显示，请从**“视图”**菜单中选择**“属性窗口”**。  
  
6.  从**“工具箱”**的**“基元”**部分，将一个**“Assign”**活动拖放到**“DoWhile”**活动中，**“Prompt”**活动之后。  
  
    > [!NOTE]
    >  放下**“Assign”**活动时，注意观察工作流设计器如何自动添加**“Sequence”**活动，使之同时包含**“Prompt”**活动和新添加的**“Assign”**活动。  
  
7.  在**“To”**框中键入 `Turns`，并将 `Turns + 1` 键入**“输入 C\# 表达式”**或**“输入 VB 表达式”**框中。  
  
8.  从**“工具箱”**的**“控制流”**部分，将一个**“If”**活动拖放到**“Sequence”**活动中，新添加的**“Assign”**活动之后。  
  
9. 将以下表达式键入**“If”**活动的**“Condition”**属性值框。  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
10. 从**“工具箱”**的**“控制流”**部分，再将一个**“If”**活动拖放到第一个**“If”**活动的**“Then”**部分中。  
  
11. 将以下表达式键入新添加的**“If”**活动的**“Condition”**属性值框中。  
  
    ```vb-c#  
    Guess < Target  
    ```  
  
12. 从**“工具箱”**的**“基元”**部分拖放两个**“WriteLine”**活动，一个放在新添加**“If”**活动的**“Then”**部分，另一个放在**“Else”**部分。  
  
13. 单击**“Then”**部分中的**“WriteLine”**活动将其选中，然后将以下表达式键入**“Text”**属性值框中。  
  
    ```vb  
    "Your guess is too low."  
    ```  
  
14. 单击**“Else”**部分中的**“WriteLine”**活动将其选中，然后将以下表达式键入**“Text”**属性值框中。  
  
    ```vb  
    "Your guess is too high."  
    ```  
  
     下面的示例阐释已完成的工作流。  
  
     ![已完成的顺序工作流](../../../docs/framework/windows-workflow-foundation//media/wfsequentialgettingstartedtutorialcomplete.JPG "WFSequentialGettingStartedTutorialComplete")  
  
### 生成工作流  
  
1.  按 Ctrl\+Shift\+B 生成解决方案。  
  
     有关如何运行工作流的说明，请参见下一主题[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)。如果您已使用不同样式的工作流完成了[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)步骤，并希望使用此步骤中的顺序工作流运行它，请跳到[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)的[生成并运行应用程序](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md#BKMK_ToRunTheApplication)部分。  
  
## 请参阅  
 <xref:System.Activities.Statements.Flowchart>   
 <xref:System.Activities.Statements.FlowDecision>   
 [Windows Workflow Foundation 编程](../../../docs/framework/windows-workflow-foundation//programming.md)   
 [设计工作流](../../../docs/framework/windows-workflow-foundation//designing-workflows.md)   
 [入门教程](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)   
 [如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)   
 [如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)