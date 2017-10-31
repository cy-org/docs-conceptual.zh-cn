---
title: "等待输入活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d58c344e-9ee8-4ce2-b199-75b3fe45237f
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 等待输入活动
此示例演示如何在工作流中创建命名书签。[!INCLUDE[wf](../../../../includes/wf-md.md)] 不提供声明性书签创建的活动。因此，当您需要在工作流中创建书签时，必须编写一个创建书签的自定义活动。此示例中定义的 `WaitForInput` 活动提供了此项功能，以便用户可以通过声明方式在工作流内创建书签。  
  
## 此示例中的项目  
  
||||  
|-|-|-|  
|**项目名称**|**说明**|**主要文件**|  
|WaitForInput|包含 `WaitForInput` 活动及其设计器|WaitForInput.cs<br /><br /> `WaitForInput` 活动定义。|  
|||WaitForInputDesigner.xaml<br /><br /> `WaitForInput` 活动的自定义设计器。|  
|||TypeToFirstGenericArgumentConverter.cs<br /><br /> 用于更新设计器中活动的泛型类型的 WPF 类型转换器。|  
|WaitForInputTestClient|示例客户端应用程序，它可通过工作流设计器使用一些 WaitForInput 活动来配置和运行工作流。|Sequence1.xaml<br /><br /> 使用 `WaitForInput` 活动的顺序工作流。|  
|||Program.cs<br /><br /> 运行在 Sequence1.xaml 中定义的工作流的实例。|  
  
## WaitForInput 活动  
 `WaitForInput` 活动在工作流中创建一个命名书签。该书签等待一个信号，然后接收它的所配置的类型的数据。当书签恢复之后，将可以通过 `Result` 属性使用传入到工作流中的数据。  
  
 `WaitForInput` 活动派生自 <xref:System.Activities.NativeActivity> 类，因为它必须创建只能通过 <xref:System.Activities.NativeActivityContext> 类访问的书签。  
  
 该活动应用了三个特性，分别用于绑定设计器、添加可更新的泛型参数功能以及将默认泛型类型设置为 string。该活动还具有下表中列出的参数。  
  
||||  
|-|-|-|  
|**名称**|**类型**|**说明**|  
|TResult|泛型参数 \(TResult\)|书签的类型。这是在书签恢复时要传给书签的数据的类型。|  
|BookmarkName|InArgument\<string\>|书签的名称。|  
|Result|InArgument\<TResult\>|书签恢复时要传递到活动的数据。|  
  
## WaitForInput 活动设计器  
 `WaitForInput` 活动设计器在 WaitForInputDesigner.xaml 文件中实现。`WaitForInput` 活动及其设计器包含在同一个程序集中。下图显示了工具箱中与程序集具有相同名称的类别中的 `WaitForInput` 活动。  
  
 ![WaitForInput 工具箱屏幕快照](../../../../docs/framework/windows-workflow-foundation/samples/media/waitforinputtoolbox.jpg "WaitForInputToolbox")  
  
 下图显示了 `WaitForInput` 设计器。因为 `WaitForInput` 活动是最基本的，所以设计器允许在设计器图面上直接设置它的所有参数。  
  
 ![WaitForInput 活动设计器](../../../../docs/framework/windows-workflow-foundation/samples/media/waitforinputdesigner.jpg "WaitForInputDesigner")  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 WaitForInput.sln 文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要启用示例而不进行调试，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\WaitForInput`  
  
## 请参阅