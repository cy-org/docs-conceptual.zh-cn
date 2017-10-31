---
title: "WS 可靠会话 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "可靠会话"
ms.assetid: 86e914f2-060b-432b-bd17-333695317745
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# WS 可靠会话
此示例演示可靠会话的用法。可靠会话为可靠消息传递和会话提供支持。可靠消息传递在失败时会重新尝试通信，并允许指定传递保证（如消息按顺序抵达）。会话在调用之间将保持客户端的状态。此示例实现了用来保持客户端状态的会话，并指定了按顺序传递保证。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\WS\wsReliableSession`  
  
 此示例基于实现计算器服务的[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。可靠会话功能是在客户端和服务的应用程序配置文件中启用和配置的。  
  
 在此示例中，服务由 Internet 信息服务 \(IIS\) 承载，客户端是一个控制台应用程序 \(.exe\)。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 此示例使用 `wsHttpBinding`。绑定是在客户端和服务的配置文件中指定的。绑定类型是在终结点元素的 `binding` 属性中指定的，如下面的示例配置中所示。  
  
```  
<endpoint address=""  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"   
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  
```  
  
 终结点包含一个 `bindingConfiguration` 属性，该属性引用一个名为“Binding1”的绑定配置。该绑定配置通过将 [\<reliableSession\>](../../../../docs/framework/configure-apps/file-schema/wcf/reliablesession.md)的 `enabled` 属性设置为 `true` 来启用可靠会话。有序会话的传递保证是通过将有序属性设置为 `true` 或 `false` 来控制的。默认值为 `true`。  
  
```  
<bindings>  
    <wsHttpBinding>  
        <binding name="Binding1">  
            <reliableSession enabled="true" />  
        </binding>  
    </wsHttpBinding>  
</bindings>  
  
```  
  
 服务实现类将实现 <xref:System.ServiceModel.InstanceContextMode> 实例化，以便针对每个客户端维护一个单独的类实例，如下面的示例代码中所示。  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)] public class CalculatorService : ICalculator  
{  
    ...  
}  
```  
  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。在客户端窗口中按 Enter 以关闭客户端。  
  
```  
  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### 设置、生成和运行示例  
  
1.  使用以下命令安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0。  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅