---
title: "入门教程疑难解答 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 入门教程疑难解答
本主题列出使用“入门教程”时最常遇见的问题及其解决方法。  
  
1.  [无法在硬盘上找到项目文件。](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q1)  
  
2.  [尝试运行服务应用程序时出现以下错误：HTTP 无法注册 URL http://+:8000/ServiceModelSamples/Service/。进程不具有此命名空间的访问权限。](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q2)  
  
3.  [尝试使用 Svcutil.exe 工具时出现以下错误：“svcutil”不是内部或外部命令，也不是可操作的程序或批处理文件。](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q3)  
  
4.  [无法找到由 Svcutil.exe 生成的 App.config 文件。](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q4)  
  
5.  [编译客户端应用程序期间出现以下错误：“CalculatorClient”不包含“&lt;方法名称&gt;”的定义，并且找不到可接受类型为“CalculatorClient”的第一个参数的扩展方法“&lt;方法名称&gt;”(是否缺少 using 指令或程序集引用?)](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q5)  
  
6.  [编译客户端应用程序期间出现以下错误：找不到类型或命名空间名称“CalculatorClient”(是否缺少 using 指令或程序集引用?)](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q6)  
  
7.  [运行客户端期间出现以下错误：未处理的异常: System.ServiceModel.EndpointNotFoundException: 无法连接到 http://localhost:8000/ServiceModelSamples/Service/CalculatorService。TCP 错误代码 10061: 由于目标计算机主动拒绝，未能建立连接。](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q7)  
  
<a name="BKMK_q1"></a>   
## 无法在硬盘上找到项目文件。  
 在 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 中，将项目文件保存在 c:\\users\\\<用户名\\Documents\\\<Visual Studio version\>\\Projects [!INCLUDE[wv](../../../includes/wv-md.md)] 和  [!INCLUDE[win7_client_secondref](../../../includes/win7-client-secondref-md.md)] 下，对于 Windows 的早期版本，保存在 c:\\Documents and Settings\\\<用户名\>\\My Documents\\\<Visual Studio version\>\\Projects 下。  
  
<a name="BKMK_q2"></a>   
## 尝试运行服务应用程序时出现以下错误：HTTP 无法注册 URL http:\/\/\+:8000\/ServiceModelSamples\/Service\/。进程不具有此命名空间的访问权限。  
 必须使用管理特权来运行承载 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的进程。如果从 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 内运行服务，则必须以管理员身份运行 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]。为此，请单击**“开始”**，右击 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]，然后选择**“以管理员身份运行”**。如果从命令行提示符运行服务，则必须按类似方式以管理员身份启动命令行提示符。单击**“开始”**，右击**“命令提示符”**，然后选择**“以管理员身份运行”**。  
  
<a name="BKMK_q3"></a>   
## 尝试使用 Svcutil.exe 工具时出现以下错误：“svcutil”不是内部或外部命令，也不是可操作的程序或批处理文件。  
 Svcutil.exe 必须位于系统路径中。最简单的解决方案是使用命令提示符。单击**“开始”**，然后依次选择**“所有程序”**、[!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]、**“Visual Studio 工具”** 和 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]  **命令提示符**。对于 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 中附带的所有工具，此命令提示均能将系统路径设置为正确的位置。  
  
<a name="BKMK_q4"></a>   
## 无法找到由 Svcutil.exe 生成的 App.config 文件。  
 默认情况下，**“添加现有项”**对话框仅显示具有以下扩展名的文件：.cs、.resx、.settings、.xsd 和 .wsdl。通过在**“添加现有项”**对话框右下角的下拉列表框中选择**“所有文件\(\*.\*\)”**，可以指定您希望查看所有文件类型。  
  
<a name="BKMK_q5"></a>   
## 编译客户端应用程序期间出现以下错误：“CalculatorClient”不包含“\<方法名称\>”的定义，并且找不到可接受类型为“CalculatorClient”的第一个参数的扩展方法“\<方法名称\>”\(是否缺少 using 指令或程序集引用?\)  
 仅向外界公开标记有 `ServiceOperationAttribute` 的那些方法。如果在 `ICalculator` 接口的某个方法中省略了 `ServiceOperationAttribute` 特性，则当所编译的客户端应用程序调用缺少该特性的操作时，便会收到此错误消息。  
  
<a name="BKMK_q6"></a>   
## 编译客户端应用程序期间出现以下错误：找不到类型或命名空间名称“CalculatorClient”\(是否缺少 using 指令或程序集引用?\)  
 如果未将 Proxy.cs 或 Proxy.vb 文件添加到客户端项目，则会收到此错误。  
  
<a name="BKMK_q7"></a>   
## 运行客户端期间出现以下错误：未处理的异常: System.ServiceModel.EndpointNotFoundException: 无法连接到 http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService。TCP 错误代码 10061: 由于目标计算机主动拒绝，未能建立连接。  
 如果在未运行服务的情况下运行客户端应用程序，则会出现此错误。  
  
<a name="BKMK_q8"></a>   
## 未处理的异常: System.ServiceModel.Security.SecurityNegotiationException: 目标“http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService”与“http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService”的 SOAP 安全协商失败  
 此错误发生在已加入域但没有网络连接的计算机上。将计算机连接到网络，或者同时关闭客户端和服务的安全性。对于服务，将创建 WSHttpBinding 的代码修改为以下代码。  
  
```  
// Step 3 of the hosting procedure: Add a service endpoint  
selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
  
```  
  
 对于客户端，将 **\<binding\>** 元素下的 **\<security\>** 元素更改为以下内容：  
  
```  
<security mode="Node" />  
```  
  
## 请参阅  
 [入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [WCF 疑难解答快速入门](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md)   
 [安装问题疑难解答](../../../docs/framework/wcf/troubleshooting-setup-issues.md)