---
title: "如何：创建 Flowchart 工作流 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 185d7aea-68a6-4bd8-adde-45050f33170a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：创建 Flowchart 工作流
工作流可基于内置活动以及自定义活动来构造。本主题分步介绍如何创建使用内置活动（如 <xref:System.Activities.Statements.Flowchart> 活动）以及之前的[如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)主题中的自定义活动的工作流。该工作流模拟猜数游戏。  
  
> [!NOTE]
>  入门教程中的每个主题都依赖于前面的主题。若要完成本主题，必须先完成[如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)。  
  
> [!NOTE]
>  若要下载完整版教程，请参见 [Windows Workflow Foundation \(WF45\) \- 入门教程](http://go.microsoft.com/fwlink/?LinkID=248976)。  
  
### 创建工作流  
  
1.  在**解决方案资源管理器**中，右键单击**“NumberGuessWorkflowActivities”**，然后依次选择**“添加”**、**“新建项”**。  
  
2.  在**“已安装”**、**“常用项”**节点中，选择**“工作流”**。从**“工作流”**列表中选择**“活动”**。  
  
3.  在**“名称”**框中键入 `FlowchartNumberGuessWorkflow`，然后单击**“添加”**。  
  
4.  拖动**“工具箱”**的**“流程图”**部分中的**“Flowchart”**活动，然后将其放置在工作流设计图面上的**“在此处放置活动”**标签上。  
  
### 创建工作流变量和参数  
  
1.  在**解决方案资源管理器**中双击**“FlowchartNumberGuessWorkflow.xaml”**以在设计器中显示该工作流（如果尚未显示该工作流）。  
  
2.  单击工作流设计器左下方的**“参数”**，以显示**“参数”**窗格。  
  
3.  单击**“创建参数”**。  
  
4.  在**“名称”**框中键入 `MaxNumber`，从**“方向”**下拉列表中选择**“输入”**，再从**“参数类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该参数。  
  
5.  单击**“创建参数”**。  
  
6.  在新添加的 `MaxNumber` 参数下方的**“名称”**框中键入 `Turns`，从**“方向”**下拉列表中选择**“输出”**，再从**“参数类型”**下拉列表中选择**“Int32”**，然后按 Enter。  
  
7.  单击活动设计器左下方的**“参数”**，以关闭**“参数”**窗格。  
  
8.  单击工作流设计器左下方的**“变量”**，以显示**“变量”**窗格。  
  
9. 单击**“创建变量”**。  
  
    > [!TIP]
    >  如果未显示**“创建变量”**框，请单击工作流设计器图面上的 <xref:System.Activities.Statements.Flowchart> 活动以将其选中。  
  
10. 在**“名称”**框中键入 `Guess`，从**“变量类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该变量。  
  
11. 单击**“创建变量”**。  
  
12. 在**“名称”**框中键入 `Target`，从**“变量类型”**下拉列表中选择**“Int32”**，然后按 Enter 保存该变量。  
  
13. 单击活动设计器左下方的**“变量”**，以关闭**“变量”**窗格。  
  
### 添加工作流活动  
  
1.  拖动**“工具箱”**的**“基元”**部分中的**“Assign”**活动，并将其悬停在流程图顶部的**“开始”**节点上。当**“Assign”**活动位于**“开始”** 节点上时，在**“开始”**节点周围会出现三个三角形。将该**“Assign”**活动放置在直接位于**“开始”**节点下面的三角形上。此操作会将这两项链接在一起，并将该**“Assign”**活动指定为流程图中的第一个活动。  
  
    > [!NOTE]
    >  也还可以通过手动将活动链接到开始节点而将活动指示为流程图中的起始活动。为此，请将鼠标悬停在**“开始”** 节点上，单击鼠标悬停在**“开始”**节点上时出现的矩形之一，将连接线向下拖动至所需的活动，并将其放置在出现的一个矩形上。您还可以通过右键单击一个活动并选择**“设置为开始节点”**将该活动指定为起始活动。  
  
2.  在**“到”**框中键入 `Target`，并在**“输入 C\# 表达式”**或**“输入 VB 表达式”**框中键入以下表达式。  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    >  如果**“工具箱”**窗口未显示，请从**“视图”**菜单中选择**“工具箱”**。  
  
3.  拖动**“工具箱”**的**“NumberGuessWorkflowActivities”**部分中的一个**“Prompt”**活动，将其放置在上一步中的**“Assign”**活动下面，然后将该**“Prompt”**活动连接到该**“Assign”**活动。可通过三种方法来连接这两个活动。第一种方法是您在工作流活动上拖动**“Prompt”**活动时来连接它们。当您将**“Prompt”** 活动拖动到该工作流时，将其悬停在**“Assign”**活动上，然后将其放置在**“Prompt”**活动位于**“Assign”**活动上时出现的四个三角形之一上面。第二种方法是将**“Prompt”**活动拖动到所需位置处的工作流上。然后，将鼠标悬停在**“Assign”**活动上，并将出现的矩形之一向下拖动到**“Prompt”**活动。拖动鼠标，使连接线从**“Assign”**活动连接至**“Prompt”**活动的矩形之一，然后松开鼠标按钮。第三种方法与第一种方法十分类似，不同之处是，您不是从**“工具箱”**来拖动**“Prompt”**活动，而是从工作流设计图面上其所在的位置拖动该活动，将其悬停在**“Assign”**活动上，然后将其放置在出现的三角形之一上面。  
  
4.  在**“Prompt”**活动的**“属性窗口”**中的**“BookmarkName”**属性值框中键入 `"EnterGuess"`（包括引号）。在**“Result”**属性值框中键入 `Guess`，并在**“Text”**属性框中键入以下表达式。  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
    > [!TIP]
    >  如果**“属性窗口”**未显示，请从**“视图”**菜单选择**“属性窗口”**。  
  
5.  拖动**“工具箱”**的**“基元”**部分中的**“Assign”**活动，然后使用上一步中所描述的一种方法将其连接，使其位于**“Prompt”**活动下面。  
  
6.  在**“到”**框中键入 `Turns`，并在**“输入 C\# 表达式”**或**“输入 VB 表达式”**框中键入 `Turns + 1`。  
  
7.  拖动**“工具箱”**的**“流程图”**部分中的**“FlowDecision”**，然后在**“Assign”**活动下面将其连接。在**“属性窗口”**中，在**“Condition”**属性值框中键入以下表达式。  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
8.  将另一个**“FlowDecision”**活动从**“工具箱”**拖放到第一个活动下。通过从靠上**“FlowDecision”**活动中标记为**“False”**的矩形拖至第二个**“FlowDecision”**活动的顶部矩形，将这两个活动连接起来。  
  
    > [!TIP]
    >  如果在**“FlowDecision”**上看不到**“True”**和**“False”**标签，请将鼠标悬停在**“FlowDecision”**上。  
  
9. 单击第二个**“FlowDecision”**活动将其选中。在**“属性窗口”**中，在**“Condition”**属性值框中键入以下表达式。  
  
    ```vb-c#  
    Guess < Target  
    ```  
  
10. 将两个**“WriteLine”**活动从**“工具箱”**的**“基元”**部分并排拖放至两个**“FlowDecision”**活动下。将靠下**“FlowDecision”**活动的**“True”**操作连接到最左边的**“WriteLine”**活动，并将**“False”**操作连接到最右边的**“WriteLine”**活动。  
  
11. 单击最左边的**“WriteLine”**活动将其选中，然后在**“属性窗口”**的**“Text”**属性值框中键入以下表达式。  
  
    ```vb-c#  
    "Your guess is too low."  
    ```  
  
12. 将**“WriteLine”**连接到上方的**“Prompt”**活动的左侧。  
  
13. 单击最右边的**“WriteLine”**活动将其选中，然后在**“属性窗口”**的**“Text”**属性值框中键入以下表达式。  
  
    ```vb-c#  
    "Your guess is too high."  
    ```  
  
14. 将**“WriteLine”**活动连接到上方的**“Prompt”**活动的右侧。  
  
     下面的示例阐释已完成的工作流。  
  
     ![已完成的 Windows Workflow Foundation](../../../docs/framework/windows-workflow-foundation//media/gettingstartedtutorialcompletedflowchart.PNG "GettingStartedTutorialCompletedFlowchart")  
  
### 生成工作流  
  
1.  按 Ctrl\+Shift\+B 生成解决方案。  
  
     有关如何运行工作流的说明，请参见下一主题[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)。如果您已使用不同样式的工作流完成[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)步骤，并希望使用此步骤中的流程图工作流来运行该工作流，请跳到[如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)的[生成并运行应用程序](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md#BKMK_ToRunTheApplication)部分。  
  
## 请参阅  
 <xref:System.Activities.Statements.Flowchart>   
 <xref:System.Activities.Statements.FlowDecision>   
 [Windows Workflow Foundation 编程](../../../docs/framework/windows-workflow-foundation//programming.md)   
 [设计工作流](../../../docs/framework/windows-workflow-foundation//designing-workflows.md)   
 [入门教程](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)   
 [如何：创建活动](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)   
 [如何：运行工作流](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)