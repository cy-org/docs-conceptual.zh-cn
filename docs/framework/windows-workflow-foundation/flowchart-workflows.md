---
title: "流程图工作流 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0a3475c-d22f-49eb-8912-973c960aebf5
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# 流程图工作流
流程图是用于设计程序的已知范例。Flowchart 活动通常用于实现非顺序工作流，但如果未使用 `FlowDecision` 节点，则也可以用于顺序工作流。  
  
## 流程图工作流结构  
 Flowchart 活动是一种活动，该活动包含要执行的活动集合。流程图还包含流控件元素，如 <xref:System.Activities.Statements.FlowDecision> 和 <xref:System.Activities.Statements.FlowSwitch>，该元素根据变量的值指导所包含活动间的执行。  
  
## 流节点的类型  
 根据执行元素时所需的流控制类型，使用不同的元素类型。流程图元素的类型包括：  
  
-   `FlowStep` \- 在流程图中对执行步骤进行建模。  
  
-   `FlowDecision` \- 基于布尔条件建立执行分支，类似于 <xref:System.Activities.Statements.If>。  
  
-   `FlowSwitch` – 基于独占 Switch 分支执行，类似于 <xref:System.Activities.Statements.Switch%601>。  
  
 每个链接都具有一个 `Action` 属性，该属性定义可用于执行子活动，和定义要执行哪一个或哪几个元素的 `Next` 属性的 <xref:System.Activities.ActivityAction>（当前元素完成执行时）。  
  
### 使用 FlowStep 节点创建一个基本的活动顺序  
 若要建立一个基本的顺序模型，在该模型中依次执行两个活动，请使用 `FlowStep` 元素。在下面的示例中，使用了两个 `FlowStep` 元素按顺序执行两个活动。  
  
```  
<Flowchart>  
  <FlowStep>      
  <Assign DisplayName="Get Name">  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:String">[result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:String">["User"]</InArgument>  
    </Assign.Value>  
  </Assign>  
    <FlowStep.Next>  
      <FlowStep>  
        <WriteLine Text="["Hello, " & result]"/>  
</FlowStep>  
    </FlowStep.Next>  
  </FlowStep>  
</Flowchart>  
  
```  
  
### 使用 FlowDecision 节点创建条件流程图  
 若要在流程图工作流中建立条件流节点的模型（即，创建一个充当传统流程图的决策符号的链接），请使用 <xref:System.Activities.Statements.FlowDecision> 节点。该节点的 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 属性设置为定义条件的表达式，并且，如果表达式的计算结果为 `true` 或 `false`，则 <xref:System.Activities.Statements.FlowDecision.True%2A> 和 <xref:System.Activities.Statements.FlowDecision.False%2A> 属性设置为要执行的 <xref:System.Activities.Statements.FlowNode> 实例。下面的示例演示如何定义使用 <xref:System.Activities.Statements.FlowDecision> 节点的工作流。  
  
```  
<Flowchart>  
  <FlowStep>  
    <Read Result="[s]"/>  
    <FlowStep.Next>  
      <FlowDecision>  
        <IsEmpty Input="[s]" />  
        <FlowDecision.True>  
    <FlowStep>  
            <Write Text="Empty"/>  
    </FlowStep>  
        </FlowDecision.True>  
        <FlowDecision.False>  
    <FlowStep>  
            <Write Text="Non-Empty"/>  
          </FlowStep>  
        </FlowDecision.False>  
      </FlowDecision>  
    </FlowStep.Next>  
  </FlowStep>  
</Flowchart>  
  
```  
  
### 使用 FlowSwitch 节点创建独占 Switch  
 若要建立某个流程图的模型，在该流程图中基于匹配的值选择了一个独占路径，请使用 <xref:System.Activities.Statements.FlowSwitch%601> 节点。<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 属性设置为具有 <xref:System.Object> 的类型参数的 <xref:System.Activities.Activity%601>，该属性定义要针对其匹配选项的值。<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 属性定义键词典和 <xref:System.Activities.Statements.FlowNode> 对象，以匹配条件表达式和 <xref:System.Activities.Statements.FlowNode> 对象的集，这些对象定义在给定情况与条件表达式匹配时的执行流方式。<xref:System.Activities.Statements.FlowSwitch%601> 还定义一个 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> 属性，该属性定义没有情况与条件表达式匹配时的执行流方式。下面的示例演示如何定义使用 <xref:System.Activities.Statements.FlowSwitch%601> 元素的工作流。  
  
```  
<Flowchart>  
    <FlowSwitch>  
      <FlowStep x:Key="Red">  
        <WriteRed/>  
      </FlowStep>  
      <FlowStep x:Key="Blue">  
        <WriteBlue/>  
      </FlowStep>  
      <FlowStep x:Key="Green">  
        <WriteGreen/>  
      </FlowStep>  
    </FlowSwitch>  
</Flowchart>  
  
```