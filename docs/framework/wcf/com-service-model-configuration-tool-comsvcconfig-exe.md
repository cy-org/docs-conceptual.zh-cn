---
title: "COM+ 服务模块配置工具 (ComSvcConfig.exe) | Microsoft Docs"
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
helpviewer_keywords: 
  - "WCF, COM+ 集成"
  - "Windows Communication Foundation, COM+ 集成"
ms.assetid: 7717c6c2-85fc-418b-a8ed-bad8e61cec5c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# COM+ 服务模块配置工具 (ComSvcConfig.exe)
利用 COM\+ 服务模块配置命令行工具 \(ComSvcConfig.exe\)，您可以配置要作为 Web 服务公开的 COM\+ 接口。  
  
## 语法  
  
```  
  
ComSvcConfig.exe /install | /uninstall | /list [/application:<ApplicationID | ApplicationName>] [/contract:<ClassID | ProgID | *,InterfaceID | InterfaceName | *>] [/hosting:<complus | was>] [/webSite:<WebsiteName>] [/webDirectory:<WebDirectoryName>] [/mex] [/id] [/nologo] [/verbose] [/help] [/partial]  
```  
  
## 备注  
  
> [!NOTE]
>  您必须是本地计算机上的管理员才能使用 ComSvcConfig.exe。  
  
 可在以下位置中找到此工具  
  
 %SystemRoot%\\Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\  
  
 有关 ComSvcConfig.exe 的更多信息，请参见[如何：使用 COM\+ 服务模型配置工具](../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md)。  
  
 下表介绍可用于 ComSvcConfig.exe 的模式。  
  
|选项|说明|  
|--------|--------|  
|`install`|为服务模块集成安装 COM\+ 接口配置。<br /><br /> 缩写形式：`/i`。|  
|`uninstall`|从服务模块集成中卸载 COM\+ 接口配置。<br /><br /> 缩写形式：`/u`。|  
|`list`|列出有关 COM\+ 应用程序和组件的信息，这些应用程序和组件具有为服务模块集成配置的接口。<br /><br /> 缩写形式：`/l`。|  
  
 下表介绍可用于 ComSvcConfig.exe 的标志。  
  
|选项|说明|  
|--------|--------|  
|`/application:<` *ApplicationID*  `&#124;`  *ApplicationName* `>`|指定要配置的 COM\+ 应用程序。<br /><br /> 缩写形式：`/a`。|  
|`/contract:<` *ClassID*  `&#124;`  *ProgID*  `&#124; *,` *InterfaceID*  `&#124;`  *InterfaceName*  `&#124; *` `>`|指定将作为服务协定配置的 COM\+ 组件和接口。<br /><br /> 缩写形式：`/c`。<br /><br /> 尽管在指定组件和接口名称时可以使用通配符 \(\*\)，但我们建议您不要使用通配符，因为这样可能会公开您不打算公开的接口。|  
|`/hosting:<` *complus*  `&#124;`  *was* `>`|指定是使用 COM\+ 宿主模式还是 Web 宿主模式。<br /><br /> 缩写形式：`/h`。<br /><br /> 如果使用 COM\+ 宿主模式，将需要显式激活 COM\+ 应用程序。如果使用 Web 宿主模式，将能够按照需要自动激活 COM\+ 应用程序。如果 COM\+ 应用程序是库应用程序，它将在 Internet 信息服务 \(IIS\) 进程中运行。如果 COM\+ 应用程序是服务器应用程序，它将在 Dllhost.exe 进程中运行。|  
|`/webSite:<` *WebsiteName* `>`|指定使用 Web 宿主模式时（请参见 `/hosting` 标志）用于宿主的网站。<br /><br /> 缩写形式：`/w`。<br /><br /> 如果未指定网站，则使用默认网站。|  
|`/webDirectory:<` *WebDirectoryName* `>`|指定在使用 Web 宿主时（请参见 `/hosting` 标志）用于宿主的虚拟目录。<br /><br /> 缩写形式：`/d`。|  
|`/mex`|将元数据交换 \(MEX\) 服务终结点添加到默认服务配置，以支持要从服务中检索协定定义的客户端。<br /><br /> 缩写形式：`/x`。|  
|`/id`|以 ID 的形式显示应用程序、组件和接口信息。<br /><br /> 缩写形式：`/k`。|  
|`/nologo`|防止 ComSvcConfig.exe 显示其徽标。<br /><br /> 缩写形式：`/n`。|  
|`/verbose`|除遇到的任何错误之外还输出所有警告或信息性文本。<br /><br /> 缩写形式：`/v`。|  
|`/help`|显示用法消息。<br /><br /> 缩写形式：`/?`。|  
|`/partial`|在指定的接口包含一个或多个可公开的方法签名时生成一个服务配置。在服务初始化时，兼容的方法显示为服务协定上的操作，而非兼容方法将被忽略且不显示在服务协定中。<br /><br /> 如果缺少此标志，工具将不会在指定接口包含一个或多个不兼容方法时生成服务配置。|  
  
## 示例  
  
### 说明  
 下面的示例使用 COM\+ 宿主模式将 `ItemOrders.IFinancial` 组件（来自 OnlineStore COM\+ 应用程序）的 `IFinances` 接口添加到作为 Web 服务公开的接口集中。除遇到的任何错误外还将输出所有警告。  
  
### 代码  
  
```  
ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
```  
  
### 说明  
 下面的示例使用 Web 宿主模式将 `ItemInventory.Warehouse` 组件（来自 OnlineWarehouse COM\+ 应用程序）的 `IStockLevels` 接口添加到作为 Web 服务公开的接口集中。Web 服务是宿主在 IIS 的 OnlineWarehouse 虚拟目录中的网站。  
  
### 代码  
  
```  
ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse  
```  
  
### 说明  
 下面的示例从作为 Web 服务公开的接口集中移除 `ItemOrders.Financial` 组件（来自 OnlineStore COM\+ 应用程序）的 `IFinances` 接口。  
  
### 代码  
  
```  
ComSvcConfig.exe /uninstall /application:OnlineStore /interface:ItemOrders.Financial,IFinances /hosting:complus  
```  
  
### 说明  
 下面的示例为本地计算机上的 OnlineStore COM\+ 应用程序列出当前公开的 COM\+ 宿主接口，以及相应的地址和绑定详细信息。  
  
### 代码  
  
```  
ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
```  
  
## 请参阅  
 [如何：使用 COM\+ 服务模型配置工具](../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md)