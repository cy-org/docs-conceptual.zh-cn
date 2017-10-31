---
title: "DynamicActivity 创建 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d8ebe82f-98c8-4452-aed7-2c60a512b097
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# DynamicActivity 创建
此示例演示在运行时使用 <xref:System.Activities.DynamicActivity> 活动来创建活动的两种不同方式。  
  
 在此示例中，在运行时使用包含 <xref:System.Activities.Statements.Sequence> 活动（该活动包含 <xref:System.Activities.Statements.ForEach%601> 和 <xref:System.Activities.Statements.Assign%601> 活动）的主体创建一个活动。将一个整数输入列表传递到该活动中，并将其设置为一个属性。然后 <xref:System.Activities.Statements.ForEach%601> 活动循环访问值列表并累积值。在 <xref:System.Activities.Statements.Assign%601> 活动中，通过将累积值除以列表中的元素数量来计算平均值，并将此值赋给平均值变量。  
  
 此示例演示如何使用 <xref:System.Activities.DynamicActivity> 活动，该活动流入变量作为输入参数，并流入返回值作为输出参数。该活动具有一个名为 `Numbers` 的输入参数，该参数是一个整数列表。<xref:System.Activities.Statements.ForEach%601> 活动循环访问值列表并累积值。在 <xref:System.Activities.Statements.Assign%601> 活动中，通过累积值除以列表中的元素数量来计算平均值，并将此值赋给平均值变量。平均值作为一个名为 `Average` 的输出参数返回。  
  
 通过编程方式创建动态活动时，按下面的代码示例中所示声明输入和输出。  
  
```csharp  
DynamicActivity act = new DynamicActivity()  
{  
    DisplayName = "Find average",  
    Properties =   
    {  
        // Input argument  
        new DynamicActivityProperty  
        {  
            Name = "Numbers",  
            Type = typeof(InArgument<List<int>>),  
            Value = numbers  
        },  
        // Output argument  
        new DynamicActivityProperty  
        {  
            Name = "Average",  
            Type = typeof(OutArgument<double>),  
            Value = average  
        }  
    },  
};  
  
```  
  
 下面的代码示例演示用于计算列表中值的平均值的 `DynamicActivity` 的完整定义。  
  
```  
DynamicActivity act = new DynamicActivity()  
{  
    DisplayName = "Find average",  
    Properties =   
    {  
        // Input argument  
        new DynamicActivityProperty  
        {  
            Name = "Numbers",  
            Type = typeof(InArgument<List<int>>),  
            Value = numbers  
        },  
        // Output argument  
        new DynamicActivityProperty  
        {  
            Name = "Average",  
            Type = typeof(OutArgument<double>),  
            Value = average  
        }  
    },  
    Implementation = () =>  
        new Sequence  
        {  
            Variables = { result, accumulator },  
            Activities =  
            {  
                new ForEach<int>  
                {  
                    Values =  new ArgumentValue<IEnumerable<int>> { ArgumentName = "Numbers" },                                  
                    Body = new ActivityAction<int>  
                    {  
                        Argument = iterationVariable,  
                        Handler = new Assign<int>  
                        {  
                            To = accumulator,  
                            Value = new InArgument<int>(env => iterationVariable.Get(env) +  accumulator.Get(env))  
                        }  
                    }  
                },  
  
                // Calculate the average and assign to the output argument.  
                new Assign<double>  
                {  
                    To = new ArgumentReference<double> { ArgumentName = "Average" },  
                    Value = new InArgument<double>(env => accumulator.Get(env) / numbers.Get(env).Count<int>())  
                },  
            }  
        }  
};  
```  
  
 通过 XAML 创建动态活动时，按下面的代码示例中所示声明输入和输出。  
  
```  
<Activity x:Class="Microsoft.Samples.DynamicActivityCreation.FindAverage"  
          xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
          xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <x:Members>  
    <x:Property Name="Numbers" Type="InArgument(scg:List(x:Int32))" />  
    <x:Property Name="Average" Type="OutArgument(x:Double)" />  
  </x:Members>  
    ...  
    ...  
</Activity>  
```  
  
 可使用 [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)] 以可视化方式创建 XAML。如果它包含在 Visual Studio 项目中，请确保将其“生成操作”设置为“无”，以防止对它进行编译。然后可以使用以下调用动态加载 XAML。  
  
```  
Activity act2 = ActivityXamlServices.Load(@"FindAverage.xaml");  
  
```  
  
 可按照下面的代码示例中所示，可以使用通过编程方式或通过加载 XAML 工作流创建的 <xref:System.Activities.DynamicActivity> 实例。请注意，传递给 `WorkflowInvoker.Invoke` 的“act”是在第一个代码示例中定义的“act”<xref:System.Activities.Activity>。  
  
```  
IDictionary<string, object> results = WorkflowInvoker.Invoke(act, new Dictionary<string, object> { { "Numbers", numbers } });  
  
Console.WriteLine("The average calculated using the code activity is = " + results["Average"]);  
  
```  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 DynamicActivityCreation.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
## 命令行参数  
 此示例接受命令行参数。用户可以为活动提供一个数字列表来计算其平均值。要使用的数字列表以由空格分隔的数字列表的形式进行传递。例如，若要计算 5、10 和 32 的平均值，请使用下面的命令行调用此示例。  
  
 **DynamicActivityCreation 5 10 32**   
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Built-InActivities\DynamicActivity\DynamicActivityCreation`  
  
## 请参阅