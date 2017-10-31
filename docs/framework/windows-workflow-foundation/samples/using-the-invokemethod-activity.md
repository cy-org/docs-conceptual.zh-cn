---
title: "使用 InvokeMethod 活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6643550-d043-4ac7-8069-9c55ebbb4233
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 使用 InvokeMethod 活动
此示例演示如何使用 <xref:System.Activities.Statements.InvokeMethod%601> 活动调用公共类中的公共方法。<xref:System.Activities.Statements.InvokeMethod%601> 活动允许工作流针对对象调用方法、传入参数、获取返回值、指定泛型方法的类型以及指定方法是同步的还是异步的。  
  
 示例中有一个非泛型版本的 <xref:System.Activities.Statements.InvokeMethod> 活动（其中的返回值设置为 <xref:System.Activities.Statements.InvokeMethod.Result%2A> 属性）和一个泛型版本的 <xref:System.Activities.Statements.InvokeMethod%601> 活动（其中的返回值通过 `TResult` 类型的 <xref:System.Activities.Statements.InvokeMethod.Result%601.Result%2A> 属性返回）。  
  
 此示例演示如何调用各种不同的方法类型。下面的列表详细介绍了此示例中演示的方法类型：  
  
-   调用不含参数的实例方法。  
  
-   调用含有两个参数（System.String 和 System.Int32）的实例方法。  
  
-   调用含有两个参数（System.String 和 System.Int32）和一个 System.String\[\] 类型的参数数组的实例方法。  
  
-   调用含有两个参数（两个 System.Int32 数）和一个 System.Int32 类型的结果的实例方法。  
  
     使用 <xref:System.Activities.Statements.WriteLine> 活动将返回值绑定到一个变量，并输出到控制台。  
  
-   调用含有两个参数（System.String 和 System.Int32）的静态方法。  
  
-   调用含有一个泛型参数 \(System.String\) 的实例方法。  
  
-   调用含有两个泛型参数（System.String 和 System.Int32）的静态方法。  
  
-   调用包含一个按引用传递的参数的 \(System.String\) 实例方法。  
  
     使用 <xref:System.Activities.Statements.WriteLine> 活动将引用的参数绑定到一个变量，并输出到控制台。  
  
-   调用异步的实例方法。  
  
## 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 InvokeMethodUsage.sln 解决方案文件。  
  
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