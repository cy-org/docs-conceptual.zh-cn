---
title: "安装问题疑难解答 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1644f885-c408-4d5f-a5c7-a1a907bc8acd
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 安装问题疑难解答
本主题说明如何排除 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 安装问题。  
  
## 有些 Windows Communication Foundation 注册表项无法通过在 .NET Framework 3.0 上执行 MSI 修复操作来修复  
 如果您删除下面的任何注册表项：  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelService 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelOperation 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelEndpoint 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\SMSvcHost 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\MSDTC Bridge 3.0.0.0  
  
 则在使用从**“控制面板”**中的**“添加\/删除程序”**小程序中启动的 .NET Framework 3.0 安装程序运行修复时，不会重新创建这些项。若要重新正确创建这些项，用户必须卸载并重新安装 .NET Framework 3.0。  
  
## 在安装 .NET Framework 3.0 软件包过程中 WMI Service Corruption 阻止 Windows Communication Foundation WMI 提供程序的安装  
 WMI Service Corruption 可能阻止 Windows Communication Foundation WMI 提供程序的安装。在安装过程中，Windows Communication Foundation 安装程序无法使用 mofcomp.exe 组件注册 WCF .mof 文件。下面列出了几个症状：  
  
1.  .NET Framework 3.0 安装成功完成，但未注册 WCF WMI 提供程序。  
  
2.  应用程序事件日志中显示一个错误事件，该事件指示在注册 WCF 的 WMI 提供程序或运行 mofcomp.exe 时出现问题。  
  
3.  用户的 %temp% 目录中名为 dd\_wcf\_retCA\* 的安装日志文件包含对注册 WCF WMI 提供程序失败的引用。  
  
4.  事件日志或安装跟踪日志文件中可能会列出以下异常之一：  
  
     ServiceModelReg \[11:09:59:046\]: System.ApplicationException: 使用“E:\\WINDOWS\\Microsoft.NET\\Framework\\v3.0\\Windows Communication Foundation\\ServiceModel.mof”执行 E:\\WINDOWS\\system32\\wbem\\mofcomp.exe 发生意外结果 3  
  
     或：  
  
     ServiceModelReg \[07:19:33:843\]: System.TypeInitializationException: “System.Management.ManagementPath”的类型初始值设定项引发异常。\-\-\-\> System.Runtime.InteropServices.COMException \(0x80040154\): 检索 COM 类工厂中 CLSID 为 {CF4CC405\-E2C5\-4DDD\-B3CE\-5E7582D8C9FA} 的组件时失败，原因是出现以下错误: 80040154。  
  
     或：  
  
     ServiceModelReg \[07:19:32:750\]: System.IO.FileNotFoundException: 无法加载文件或程序集“C:\\WINDOWS\\system32\\wbem\\mofcomp.exe”或其一个依赖项。系统找不到指定的文件。  
  
     文件名:“C:\\WINDOWS\\system32\\wbem\\mofcomp.exe”  
  
 若要解决前面说明的问题，必须按照以下步骤操作。  
  
1.  运行 [WMI Diagnosis Utility, version 2.0](http://go.microsoft.com/fwlink/?LinkId=94685)（WMI 诊断实用程序 2.0 版）以修复 WMI 服务。[!INCLUDE[crabout](../../../includes/crabout-md.md)]使用此工具的更多信息，请参见 [WMI Diagnosis Utility](http://go.microsoft.com/fwlink/?LinkId=94686)（WMI 诊断实用程序）主题。  
  
 使用**“控制面板”**中的**“添加\/删除程序”**小程序修复 .NET Framework 3.0 安装，或卸载\/重新安装 .NET Framework 3.0。  
  
## 在安装 .NET Framework 3.5 后修复 .NET Framework 3.0 会移除 .NET Framework 3.5 在 machine.config 中引入的配置元素  
 如果在安装 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 后修复 .NET Framework 3.0，则会从 machine.config 中移除由 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 引入的配置元素。但是，web.config 保持不变。解决方法是此后通过 ARP 修复 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]，或者将[工作流服务注册工具 \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 与 `/c` 开关结合使用。  
  
 [工作流服务注册工具 \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 可在 %windir%\\Microsoft.NET\\framework\\v3.5\\ 或 %windir%\\Microsoft.NET\\framework64\\v3.5\\ 中找到  
  
## 安装 .NET Framework 3.5 之后，为 WCF\/WF Webhost 正确配置 IIS  
 如果 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 安装无法配置与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 相关的其他 IIS 配置设置，将会在安装日志中记录错误，然后继续操作。对运行 WorkflowServices 应用程序的任何尝试都将失败，因为缺少必需的配置设置。例如，加载 xoml 或规则服务会失败。  
  
 若要解决此问题，请将[工作流服务注册工具 \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)与 `/c` 开关结合使用，以便在计算机上正确配置 IIS 脚本映射。[工作流服务注册工具 \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 可在 %windir%\\Microsoft.NET\\framework\\v3.5\\ 或 %windir%\\Microsoft.NET\\framework64\\v3.5\\ 中找到  
  
## 无法从程序集“System.ServiceModel, Version 3.0.0.0, Culture\=neutral, PublicKeyToken\=b77a5c561934e089”加载类型“System.ServiceModel.Activation.HttpModule”  
 如果安装了 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]，随后启用了 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)][!INCLUDE[indigo2](../../../includes/indigo2-md.md)] HTTP 激活，则会发生此错误。若要解决该问题，请在 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] 命令提示符下运行下面的命令行：  
  
```Output  
aspnet_regiis.exe -i -enable  
```  
  
## 请参阅  
 [设置说明](../../../docs/framework/wcf/samples/set-up-instructions.md)