---
title: "InvokeMethod | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04988eb3-65f8-456d-b1bd-509f5d05a57c
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# InvokeMethod
本示例演示使用 <xref:System.Activities.Statements.InvokeMethod> 活动调用类的方法的不同方式。  
  
 方法属于一个类，并表示所包含的操作集。<xref:System.Activities.Statements.InvokeMethod> 活动使您能够针对对象或类型调用方法，传入参数，并获取返回值。可以同步或异步调用方法。  
  
## 示例详细信息  
 本示例使用 <xref:System.Activities.Statements.InvokeMethod> 活动执行以下方案：  
  
1.  调用不含参数的实例方法。  
  
2.  调用含有两个参数（<xref:System.String> 和 <xref:System.Int32>）的实例方法。  
  
3.  调用含有两个参数（<xref:System.String> 和 <xref:System.Int32>）和一个 <xref:System.String>\[\] 类型的参数数组的实例方法。  
  
4.  调用含有 <xref:System.Int32> 类型的两个参数和一个 <xref:System.Int32> 类型的结果的实例方法。在本方案中，结果值绑定到一个变量，并在另一个活动中使用。使用 <xref:System.Activities.Statements.WriteLine> 活动在控制台中显示该结果值。  
  
5.  调用含有 <xref:System.String> 类型和 <xref:System.Int32> 类型的两个参数的静态方法。  
  
6.  调用含有一个 <xref:System.String> 类型的泛型参数的实例方法。  
  
7.  调用含有 <xref:System.String> 类型和 <xref:System.Int32> 类型的两个泛型参数的静态方法。  
  
8.  调用具有一个由 <xref:System.String> 类型的引用传递的参数的实例方法。在本方案中，引用参数绑定到一个变量 \(`outParam`\)，并在另一个活动中使用。使用 <xref:System.Activities.Statements.WriteLine> 活动在控制台上显示该引用参数。  
  
9. 调用异步的实例方法。  
  
10. 使用两个 <xref:System.Activities.Statements.InvokeMethod> 活动对一个对象的同一个实例调用两个不同的方法。  
  
11. 在对象的实例中存储一个值。  
  
12. 从对象的实例检索一个值。  
  
## 使用此示例  
 此示例分为两个版本。此示例的第一个版本通过 C\# 代码使用 [!INCLUDE[wf](../../../../includes/wf-md.md)] 编程模型演示 <xref:System.Activities.Statements.InvokeMethod> 的用法，它可以在 CodedWorkflow\\CS 文件夹下找到。此示例的第二个版本使用 XAML 演示 <xref:System.Activities.Statements.InvokeMethod> 的用法，它可以在 DesignerWorkflow\\CS 文件夹下找到。  
  
#### 运行编码的工作流示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CodedWorkflow\\CS 文件夹中的 InvokeMethodUsage.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
#### 运行设计器工作流示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 DesignerWorkflow\\CS 文件夹中的 InvokeMethodUsage.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Built-InActivities\InvokeMethod`  
  
## 请参阅