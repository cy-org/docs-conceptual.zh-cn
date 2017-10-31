---
title: "工作流服务注册工具 (WFServicesReg.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e92c87b-99c5-4e8d-9d53-7944cc2b47d3
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 工作流服务注册工具 (WFServicesReg.exe)
工作流服务注册工具 \(WFServicesReg.exe\) 是一个独立的工具，可用于添加、移除或修复 Windows Workflow Foundation \(WF\) 服务的配置元素。  
  
## 语法  
  
```  
  
WFServicesReg.exe [-c | -r | -v | -m | -i]  
```  
  
## 备注  
 该工具可以在 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 安装位置（具体为 %windir%\\Microsoft.NET\\Framework\\v3.5）或 64 位计算机上的 %windir%\\Microsoft.NET\\Framework64\\v3.5 中找到。  
  
 下表说明了可用于工作流服务注册工具 \(WFServicesReg.exe\) 的选项。  
  
|选项|说明|  
|--------|--------|  
|`/c`|配置 Windows Workflow Services。在安装和修复方案中使用。|  
|`/r`|移除 Windows Workflow Services 配置。|  
|`/v`|打印详细信息（针对配置或移除）。|  
|`/m`|启用 MSI 日志记录格式。|  
|`/i`|应用程序运行时最小化窗口。|  
  
## 注册  
 该工具检查 Web.config 文件并注册以下内容：  
  
-   [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 引用程序集。  
  
-   用于 .xoml 文件的生成提供程序。  
  
-   用于 .xoml 和 .rules 文件的 HTTP 处理程序。  
  
 该工具检查 Machine.config 文件并注册以下扩展：  
  
-   behaviorExtensions  
  
-   bindingElementExtensions  
  
-   bindingExtensions  
  
 该工具还注册以下客户端元数据导入程序：  
  
-   policyImporters  
  
-   wsdlImporters  
  
 该工具还在 IIS 元数据库中注册 .xoml 和 .rules 脚本映射和处理程序。  
  
 在 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 计算机上（IIS 5.1 和 [!INCLUDE[iis601](../../../includes/iis601-md.md)]）注册一组 .xoml 和 .rules 脚本映射。  
  
 在 64 位计算机上，如果启用 `Enable32BitAppOnWin64` 开关，则该工具注册 WOW 模式脚本映射；如果禁用 `Enable32BitAppOnWin64` 开关，则该工具注册本机 64 位模式脚本映射。  
  
 在 [!INCLUDE[wv](../../../includes/wv-md.md)] 和 Windows Server 2008（IIS 7.0 及更高版本）计算机上，注册两组 .xoml 和 .rules 处理程序：一组用于集成模式，一组用于经典模式。  
  
 在 64 位计算机上，注册三组处理程序（无论 `Enable32BitAppOnWin64` 开关处于什么状态）：一组用于集成模式，一组用于 WOW 经典模式，一组用于本机 64 位经典模式。  
  
> [!NOTE]
>  与 ServiceModelreg.exe 不同，WFServicesReg.exe 不允许添加、移除和修复特定网站的脚本映射或处理程序。有关此问题的解决方法，请参见“修复脚本映射”一节。  
  
## 使用方案  
  
### 安装 .NET Framework 3.5 之后安装 IIS  
 在 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 计算机上，在安装 IIS 之前应安装 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]。由于 IIS 元数据库不可用，[!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 安装将在不安装 .xoml 和 .rules 脚本映射的情况下成功完成。  
  
 安装 IIS 后，可以使用具有 `/c` 开关的 WFServicesReg.exe 工具来安装这些特定的脚本映射。  
  
### 修复脚本映射  
  
#### 删除了网站节点下的脚本映射  
 在 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 计算机上，从网站节点中意外删除了 .xoml 或 .rules。通过运行具有 `/c` 开关的 WFServicesReg.exe 工具可以修复这个问题。  
  
#### 删除了特定网站下的脚本映射  
 在 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 计算机上，从特定网站（如默认网站）而不是网站节点中意外删除了 .xoml 或 .rules。  
  
 若要为特定网站修复已删除的处理程序，应当运行“WFServicesReg.exe \/r”以便从所有网站移除处理程序，然后运行“WFServicesReg.exe \/c”以便为所有网站创建相应的处理程序。  
  
### 切换 IIS 模式后配置处理程序  
 当 IIS 处于共享配置模式并且已安装 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 时，IIS 元数据库将配置在共享位置下。如果将 IIS 切换到非共享配置模式，则本地元数据库将不包含必需的处理程序。若要正确配置本地元数据库，可以将共享元数据库导入到本地，也可以运行“WFServicesReg.exe \/c”来配置本地元数据库。