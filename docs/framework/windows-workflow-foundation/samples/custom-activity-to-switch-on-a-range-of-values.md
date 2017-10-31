---
title: "要基于一系列值进行切换的自定义活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 441e0a17-421f-430c-ba97-59e4cc6c88e3
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 要基于一系列值进行切换的自定义活动
此示例演示如何创建扩展对 <xref:System.Activities.Statements.Switch%601> 的使用的自定义活动。常规的 <xref:System.Activities.Statements.Switch%601> 语句允许基于单个值进行切换。但在一些业务方案中，活动必须基于一系列值进行切换。例如，活动可能在基于 1 和 5 之间切换值时执行一个操作，在基于 6 和 10 之间切换值时执行另一个操作，并为所有其他值执行默认操作。此自定义活动完全支持上述方案。  
  
## SwitchRange 活动  
 `SwitchRange` 活动将在其表达式的结果值包含在其某个 `Cases` 的范围内时计划一个子活动。  
  
 下面的代码示例是一个基于一系列值进行切换的自定义活动。  
  
```csharp  
  
public sealed class SwitchRange<T> : NativeActivity where T : IComparable  
{  
   [RequiredArgument]  
   [DefaultValue(null)]  
   public InArgument<T> Expression { get; set; }  
  
   public IList<CaseRange<T>> Cases  
  
   [DefaultValue(null)]  
   public Activity Default { get; set; }}  
}  
```  
  
|||  
|-|-|  
|属性|说明|  
|表达式|这是要计算并与 Cases 列表中的范围进行比较的表达式。该表达式的结果的类型为 T。|  
|Cases|每个示例包含一个范围（From 和 To）和一个活动 \(Body\)。计算表达式并将其与范围进行比较。如果表达式的结果位于某个示例的范围内，则执行对应的活动。|  
|Default|没有匹配的示例时所执行的活动。在设置为 `null` 时，不采用任何操作。|  
  
## CaseRange 类  
 `CaseRange` 类表示 `SwitchRange` 活动中的范围。`CaseRange` 的每个实例均包含一个范围（由 `From` 和 `To` 构成）和一个 `Body` 活动，如果在范围内计算 `SwitchRange` 中的表达式，则将计划该活动。  
  
 下面的代码示例是 `CaseRange` 类的定义。  
  
```  
  
public class CaseRange<T> where T : IComparable  
{  
    public T From { get; set; }  
  
    public T To { get; set; }  
  
    public Activity Action { get; set; }  
}  
```  
  
> [!NOTE]
>  示例中定义的 `SwitchRange` 和 `CaseRange` 类都是可使用实现 `IComparable` 的任何类型的泛型类（如 <xref:System.Activities.Statements.Switch%601> 类）。  
  
## 示例用法  
 下面的代码示例演示如何使用 `SwitchRange` 活动。  
  
```csharp  
  
Activity SwitchRange = new SwitchRange<int>  
{  
    Expression = new InArgument<int>(value),  
    Cases =   
    {  
        new CaseRange<int>                      
        {  
            From = 1,  
            To = 5,  
            Action = new WriteLine  
            {  
                Text = "Case 1-5 selected",  
            }  
        },  
        new CaseRange<int>  
        {  
            From = 6,  
            To = 10,  
            Action = new WriteLine  
            {  
                Text = "Case 6-10 selected",  
            }  
        }  
    },  
    Default = new WriteLine { Text = "Default Case selected" }  
};  
```  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 SwitchRange.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SwitchRange`  
  
## 请参阅