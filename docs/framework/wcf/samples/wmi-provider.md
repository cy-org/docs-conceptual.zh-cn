---
title: "WMI 提供程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# WMI 提供程序
此示例演示如何在运行时使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中内置的 Windows Management Instrumentation \(WMI\) 提供程序从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务中收集数据。  另外，此示例还演示如何向服务添加用户定义的 WMI 对象。  该示例激活[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)的 WMI 提供程序，并演示如何在运行时从 `ICalculator` 服务收集数据。  
  
 WMI 是 Microsoft 基于 Web 的企业管理 \(WBEM\) 标准的实现。  有关 WMI SDK 的更多信息，请参阅 MSDN Library  \(http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/wmisdk\/wmi\/wmi\_start\_page.asp\)。  WBEM 是有关应用程序如何向外部管理工具公开管理规范的行业标准。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 WMI 提供程序，该提供程序是一个在运行时通过 WBEM 兼容接口公开规范的组件。  管理工具可以在运行时通过接口连接至服务。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 公开服务的特性，如地址、绑定、行为和侦听器。  
  
 在应用程序的配置文件中激活内置 WMI 提供程序。  这可以通过 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 一节中的 [\<诊断\>](../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md)的 `wmiProviderEnabled` 特性完成，如以下配置示例所示：  
  
```  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
  
```  
  
 此配置项公开 WMI 接口。  现在，您可以通过此接口连接管理应用程序并访问应用程序的管理规范。  
  
## 自定义 WMI 对象  
 将 WMI 对象添加到服务，可以显示用户定义的信息以及内置的 WMI 提供程序信息。  这可以通过使用 Installutil.exe 应用程序将服务方案发布到 WMI 来实现。  本主题末尾的安装说明介绍了如何实现上述操作的说明以及更详细的信息。  
  
## 访问 WMI 信息  
 可以采用多种不同方式访问 WMI 数据。  Microsoft 提供脚本、[!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 应用程序、C\+\+ 应用程序和 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的 WMI API \(http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/wmisdk\/wmi\/using\_wmi.asp\)。  
  
 此示例使用两个 Java 脚本：一个脚本用于枚举在计算机上运行的服务及其某些属性，另一个脚本用于查看用户定义的 WMI 数据。  该脚本打开与 WMI 提供程序的连接、分析数据并显示所收集的数据。  
  
 启动该示例可以创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的一个运行中实例。  在该服务运行的同时，在命令提示符处使用以下命令运行每个 Java 脚本：  
  
```  
cscript EnumerateServices.js  
  
```  
  
 该脚本访问服务中包含的规范，并生成下面的输出：  
  
```  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 接下来，运行第二个 Java 脚本可以显示用户定义的 WMI 数据：  
  
```  
cscript EnumerateCustomObjects.js  
```  
  
 该脚本访问服务中包含的用户定义的规范，并生成下面的输出：  
  
```  
  
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
  
```  
  
 该输出显示计算机上正在运行一个单一服务。  该服务公开一个实现 `ICalculator` 协定的终结点。  该终结点实现的行为和绑定的设置列作消息堆栈的各个元素的总和。  
  
 WMI 不仅限于公开 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构的管理规范。  该应用程序可以通过相同机制公开它自己的特定域数据项。  WMI 是用于检查和控制 Web 服务的统一机制。  
  
#### 设置、生成和运行示例  
  
1.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成解决方案的 C\# 或 Visual Basic .NET 版本，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  通过在宿主目录中的 service.dll 文件上运行 InstallUtil.exe（InstallUtil.exe 的默认位置是“%WINDIR%\\Microsoft.NET\\Framework\\v4.0.30319”），可以将服务方案发布到 WMI。  只有在对 service.dll 文件进行了更改的情况下才需要执行此步骤。  有关详细信息，请参阅“如何：将方案发布到已检测的应用程序的 WMI”一节中位于 http:\/\/msdn2.microsoft.com\/library\/ms186147.aspx 的“通过检测应用程序提供管理信息”。  
  
4.  若要在单机配置或跨计算机配置上运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
    > [!NOTE]
    >  如果您在安装 ASP.NET 之后安装了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，则可能需要运行 "%WINDIR%\\ Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\servicemodelreg.exe " \-r \-x 以便为 ASPNET 帐户授予发布 WMI 对象的权限。  
  
5.  使用下面的命令可以查看通过 WMI 显示的示例：`cscript EnumerateServices.js` 或 `cscript EnumerateCustomObjects.js`。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## 请参阅  
 [AppFabric 监视示例 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=193959)