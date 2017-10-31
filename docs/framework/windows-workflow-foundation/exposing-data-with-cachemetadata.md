---
title: "使用 CacheMetadata 公开数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 使用 CacheMetadata 公开数据
在执行某活动之前，工作流运行时会获取所需的所有活动信息以保持活动的执行。工作流运行时在 <xref:System.Activities.Activity.CacheMetadata%2A> 方法执行期间获取这些信息。在执行此方法的时候，此方法的默认实现为运行时提供活动公开的所有公共参数、变量和子活动；如果活动需要向运行时提供比这更多的信息（如私有成员或将由该活动安排的活动），可以重写此方法以进行提供。  
  
## 默认 CacheMetadata 行为  
 <xref:System.Activities.NativeActivity> 所派生活动的 <xref:System.Activities.NativeActivity.CacheMetadata%2A> 的默认实现将通过以下方式来处理以下方法类型：  
  
-   <xref:System.Activities.InArgument%601>、<xref:System.Activities.OutArgument%601> 或 <xref:System.Activities.InOutArgument%601>（泛型参数）：这些参数作为参数公开给运行时，具有与公开的属性名称和类型相等的名称和类型、相应的参数方向和某些验证数据。  
  
-   <xref:System.Activities.Variable> 或其中的任何子类：这些成员作为公共变量公开给运行时。  
  
-   <xref:System.Activities.Activity> 或其中的任何子类：这些成员作为公共子活动公开给运行时。可以通过调用 <xref:System.Activities.ActivityMetadata.AddImportedChild%2A>、传入子活动来显式实现默认行为。  
  
-   <xref:System.Activities.ActivityDelegate> 或其中的任何子类：这些成员作为公共委托公开给运行时。  
  
-   <xref:System.Activities.Variable> 类型的 <xref:System.Collections.ICollection>：集合中的所有元素都作为公共变量公开给运行时。  
  
-   <xref:System.Activities.Activity> 类型的 <xref:System.Collections.ICollection>：集合中的所有元素都作为公共子活动公开给运行时。  
  
-   <xref:System.Activities.ActivityDelegate> 类型的 <xref:System.Collections.ICollection>：集合中的所有元素都作为公共委托公开给运行时。  
  
 从 <xref:System.Activities.Activity>、<xref:System.Workflow.Activities.CodeActivity> 和 <xref:System.Activities.AsyncCodeActivity> 派生的活动 <xref:System.Activities.Activity.CacheMetadata%2A> 也能起到以上的作用，但有以下差异：  
  
-   从 <xref:System.Activities.Activity> 派生的类不能安排子活动或委托，所以此类成员作为导入的子活动或委托公开。  
  
-   从 <xref:System.Activities.CodeActivity> 和 <xref:System.Activities.AsyncCodeActivity> 派生的类不支持变量、子活动或委托，所以将只公开参数。  
  
## 重写 CacheMetadata 以向运行时提供信息  
 以下代码段演示如何在 <xref:System.Activities.Activity.CacheMetadata%2A> 方法执行期间向活动的元数据添加有关成员的信息。注意，调用了该方法的基类以缓存有关活动的所有公共数据。  
  
```  
protected override void CacheMetadata(NativeActivityMetadata metadata)  
{      
    base.CacheMetadata(metadata);  
    metadata.AddImplementationChild(this._writeLine);  
    metadata.AddVariable(this._myVariable);  
    metadata.AddImplementationVariable(this._myImplementationVariable);  
  
    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));  
    metadata.Bind(argument, this.SomeName);  
    metadata.AddArgument(argument);  
}  
  
```  
  
## 使用 CacheMetadata 公开实现子活动  
 为了使用变量将数据传递给将由活动安排的子活动，有必要将变量添加为实现变量；不能用这种方式设置公共变量的值。原因在于，活动将更有可能作为功能的实现（有参数）执行，而不是作为封装类（有属性）执行。但是，在有些情况下，必须显式设置参数，如使用 <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A> 时，因为安排的活动不能像子活动那样访问父活动的参数。  
  
 下面的代码段演示如何使用 <xref:System.Activities.Activity.CacheMetadata%2A> 将参数从本机活动传入一个安排的活动。  
  
```  
public sealed class ChildActivity : NativeActivity  
{  
    public WriteLine _writeLine;  
    public InArgument<string> Message { get; set; }  
    private Variable<string> MessageVariable { get; set; }  
    public ChildActivity()  
    {  
        MessageVariable = new Variable<string>();  
        _writeLine = new WriteLine  
        {  
            Text = new InArgument<string>(MessageVariable),  
        };  
    }  
    protected override void CacheMetadata(NativeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        metadata.AddImplementationVariable(this.MessageVariable);  
        metadata.AddImplementationChild(this._writeLine);  
    }  
    protected override void Execute(NativeActivityContext context)  
    {  
        string configuredMessage = context.GetValue(Message);  
        context.SetValue(MessageVariable, configuredMessage);  
        context.ScheduleActivity(this._writeLine);  
    }  
}  
  
```