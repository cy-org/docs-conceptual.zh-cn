---
title: "多个协定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2bef319b-fe9c-4d49-ac6c-dfb23eb35099
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 多个协定
“多个协定”示例演示如何在一个服务上实现多个协定，以及如何配置终结点以便与实现的每个协定进行通信。此示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。该服务已进行修改以定义两个协定：`ICalculator` 协定和 `ICalculatorSession` 协定。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 服务类同时实现了 `ICalculator` 和 `ICalculatorSession` 协定。因为其中一个协定需要一个会话，所以该服务使用 <xref:System.ServiceModel.InstanceContextMode> 实例模式在会话生存期内维护状态。  
  
 服务配置已进行修改，定义了两个终结点，以公开每个协定。`ICalculator` 终结点是使用 `basicHttpBinding` 在基地址上公开的。`ICalculatorSession` 终结点是使用 `wsHttpBinding`（其 `bindingConfiguration` 属性设置为 `BindingWithSession`）在基地址\/会话上公开的，如下面的示例配置中所示。  
  
```  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <!-- ICalculator endpoint is exposed using BasicBinding at the base  
       address provided by host:   
       http://localhost/servicemodelsamples/service.svc  -->  
  <endpoint address=""  
            binding="basicHttpBinding"  
            contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  <!-- ICalculatorSession endpoint is exposed using BindingWithSession  
       at {baseaddress}/session:  
       http://localhost/servicemodelsamples/service.svc/session -->  
  <endpoint address="session"  
            binding="wsHttpBinding"  
            bindingConfiguration="BindingWithSession"   
           contract="Microsoft.ServiceModel.Samples.ICalculatorSession" />  
  ...  
</service>  
  
```  
  
 生成的客户端代码现在包含同时适用于原始 `ICalculator` 协定和新 `ICalculatorSession` 协定的客户端类。客户端配置和代码已进行修改，可以与相应服务终结点上的每个协定进行通信。  
  
 客户端是一个控制台窗口应用程序 \(.exe\)。服务是由 Internet 信息服务 \(IIS\) 承载的。  
  
 客户端控制台窗口显示发送给每个终结点的操作，首先是基本终结点，然后是安全终结点。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Services\MultipleContracts`  
  
## 请参阅