---
title: "使用文本文件跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56a82682-73c2-4b91-a206-4d8bb12c561b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 使用文本文件跟踪
此示例演示如何通过创建自定义跟踪参与者来扩展 [!INCLUDE[wf](../../../../includes/wf-md.md)] 中的跟踪。跟踪参与者是一些 .NET Framework 类，这些类将接收从运行时发出的跟踪记录。可以创建一个跟踪参与者以将跟踪事件传输给方案所需的任何目标。例如，ETW（Windows 事件跟踪）跟踪参与者将作为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的一部分提供。此示例中的跟踪参与者以 XML 格式将记录写入文本文件。  
  
## 示例详细信息  
 若要优化跟踪参与者的有用性和可靠性，则必须完成一些附加步骤以将跟踪参与者连接到运行时。下表描述此示例中用于创建遵循最佳实践的跟踪参与者的类。  
  
|类|说明|  
|-------|--------|  
|`TextFileTrackingExtensionElement`|<xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 用于定义用来配置文本文件跟踪参与者的配置节。这将允许用户使用标准 .NET Framework 配置文件来指定日志文件的目标。|  
|`TextFileTrackingBehavior`|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的行为允许用户将扩展注入运行时。当服务启动时，此行为会将跟踪参与者添加到服务中。|  
|`TextFileTrackingParticipant`|一个跟踪参与者，它在运行时接收跟踪参与者并以 XML 的形式将这些参与者存储在日志文件中。|  
  
## 行为扩展元素配置  
 若要利用先前使用 .NET Framework 配置文件描述的行为扩展元素，需要再执行一个步骤。必须将下面的配置置于要使用扩展的配置文件中。  
  
```  
<system.serviceModel>  
    <extensions>  
      <behaviorExtensions>  
        <add name="textFileTracking" type="Microsoft.Samples.TextFileTracking.TextFileTrackingExtensionElement, WFStockPriceApplication, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </behaviorExtensions>  
    </extensions>  
…  
  </system.serviceModel>  
  
```  
  
> [!NOTE]
>  有关行为扩展元素配置的完整示例用法，请参见示例中的 Web.config 文件。  
  
## 自定义跟踪记录  
 GetStockPrices.cs 文件演示如何从 <xref:System.Activities.CodeActivity> 中创建自定义跟踪记录。在运行示例时，请查找该记录。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 WFStockPriceApplication.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
     浏览器窗口打开和显示侦听应用程序的目录。  
  
4.  在浏览器中，单击 StockPriceService.xamlx。  
  
5.  浏览器将显示**“StockPriceService”**页，其中包含本地服务 wsdl 地址。复制此地址。  
  
     本地服务 wsdl 地址的示例为 http:\/\/localhost:53797\/StockPriceService.xamlx?wsdl。  
  
6.  通过使用 [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)]，转到 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 文件夹（默认安装文件夹为 %SystemDrive%\\Program Files\\Microsoft Visual Studio 10.0）。然后找到 Common7\\IDE\\ 子文件夹。  
  
7.  双击 WcfTestClient.exe 文件以启动 WCF 测试客户端。  
  
8.  在 WCF 测试客户端中，从**“文件”**菜单中选择**“添加服务…”**。  
  
9. 将刚刚复制的 URL 粘贴到文本框中。  
  
10. 单击**“确定”**关闭对话框。  
  
11. 使用 WCF 测试客户端来测试服务。  
  
    1.  在 WCF 测试客户端中，双击**“IStockPriceService”**节点下的**“GetStockPrice\(\)”**。  
  
         **“GetStockPrice\(\)”**方法将显示在右窗格中（带有一个参数）。  
  
    2.  键入 Contoso 作为该参数的值。  
  
    3.  单击**“调用”**。  
  
12. 查看位于 %APPDATA%\\trackingRecords.log 处的应用程序数据目录中的日志文件中的跟踪事件。  
  
    > [!NOTE]
    >  %APPDATA% 是一个环境变量，它在 [!INCLUDE[wv](../../../../includes/wv-md.md)]、[!INCLUDE[lserver](../../../../includes/lserver-md.md)] 或 Windows Server 2008 中解析为 %SystemDrive%\\Users\\\<username\>\\AppData\\Roaming。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Tracking\TextFileTracking`  
  
## 请参阅  
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)