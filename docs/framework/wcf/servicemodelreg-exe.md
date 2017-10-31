---
title: "ServiceModel 注册工具 (ServiceModelReg.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 396ec5ae-e34f-4c64-a164-fcf50e86b6ac
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# ServiceModel 注册工具 (ServiceModelReg.exe)
利用此命令行工具可以管理 WCF 和 WF 组件在单一计算机上的注册。在正常情况下，不应使用此工具，因为 WCF 和WF 组件在安装时配置。但如果您遇到服务激活方面问题，可以尝试使用此工具注册组件。  
  
## 语法  
  
```  
  
ServiceModelReg.exe[(-ia|-ua|-r)|((-i|-u) -c:<command>)] [-v|-q] [-nologo] [-?]  
```  
  
## 备注  
 可在以下位置中找到此工具：  
  
 %SystemRoot%\\Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\  
  
> [!NOTE]
>  在 [!INCLUDE[wv](../../../includes/wv-md.md)] 上运行 ServiceModel 注册工具时，**“Windows 功能”**对话框可能不会反映出已打开**“Microsoft .NET Framework 3.0”**之下的**“Windows Communication Foundation HTTP 激活”**选项。可通过以下方法访问**“Windows 功能”**对话框：依次单击**“开始”**、**“运行”**，然后键入**“OptionalFeatures”**。  
  
 下表介绍可用于 ServiceModelReg.exe 的选项。  
  
|选项|说明|  
|--------|--------|  
|`-ia`|安装所有 WCF 和 WF 组件。|  
|`-ua`|卸载所有 WCF 和 WF 组件。|  
|`-r`|修复所有 WCF 和 WF 组件。|  
|`-i`|安装使用 –c 指定的 WCF 和 WF 组件。|  
|`-u`|卸载使用 –c 指定的 WCF 和 WF 组件。|  
|`-c`|安装或卸载组件：<br /><br /> -   httpnamespace \- HTTP 命名空间保留项<br />-   tcpportsharing \- TCP 端口共享服务<br />-   tcpactivation \- TCP 激活服务（.NET 4 客户端配置文件中不支持）<br />-   namedpipeactivation \- 命名管道激活服务（.NET 4 客户端配置文件中不支持<br />-   msmqactivation \- MSMQ 激活服务（.NET 4 客户端配置文件中不支持<br />-   etw \- ETW 事件跟踪清单（Windows Vista 或更高版本）|  
|`-q`|安静模式（仅显示错误日志记录）|  
|`-v`|详细模式。|  
|`-nologo`|取消版权和标题消息。|  
|`-?`|显示帮助文本|  
  
## 修复 FileLoadException 错误  
 如果计算机上安装了以前版本的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]，当您运行 ServiceModelReg 工具注册新安装时，可能会收到 `FileLoadFoundException` 错误。即使从以前的安装中手动移除了文件（但保留 machine.config 设置不变），也可能发生这种情况。  
  
 错误消息类似于以下内容。  
  
```  
Error: System.IO.FileLoadException: Could not load file or assembly 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)  
File name: 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  
```  
  
 从错误消息中，您应注意到早期的客户技术预览 \(CTP\) 版本安装了 System.ServiceModel 2.0.0.0 版程序集。而已发布 System.ServiceModel 程序集的当前版本为 3.0.0.0。因此，当您想要在安装过 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 早期 CTP 版本（但未完全卸载）的计算机上安装 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 的正式版本时，会遇到此问题。  
  
 ServiceModelReg.exe 无法清除以前的版本项，也无法注册新的版本项。唯一的解决方法是手动编辑 machine.config。可在以下位置找到此文件。  
  
```  
%windir%\Microsoft.NET\Framework\v2.0.50727\config\machine.config   
```  
  
 如果在 64 位计算机上运行 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]，您还应编辑位于此位置的相同文件。  
  
```  
%windir%\Microsoft.NET\Framework64\v2.0.50727\config\machine.config   
```  
  
 在此文件中找到引用“System.ServiceModel, Version\=2.0.0.0”的任何 XML 节点，并删除这些节点及任何子节点。保存文件并重新运行 ServiceModelReg.exe 可解决此问题。  
  
## 示例  
 下面的示例演示如何使用 ServiceModelReg.exe 工具最常用的选项。  
  
```  
ServiceModelReg.exe -ia  
  Installs all components  
ServiceModelReg.exe -i -c:httpnamespace -c:etw  
  Installs HTTP namespace reservation and ETW manifests  
ServiceModelReg.exe -u -c:etw  
  Uninstalls ETW manifests  
ServiceModelReg.exe -r  
  Repairs an extended install  
```