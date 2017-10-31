---
title: "CorFlags.exe（CorFlags 转换工具）"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CorFlags conversion tool
- CorFlags.exe
- portable executable files, CorFlags section
ms.assetid: ef900f8f-71ca-4dde-9b8c-95ddb0d7d89c
caps.latest.revision: 17
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 80fb48fc86d3010020a0a8a79bb2b4b7a6275368
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="corflagsexe-corflags-conversion-tool"></a>CorFlags.exe（CorFlags 转换工具）
利用 CorFlags 转换工具，你配置可移植可执行映像标头的 CorFlags 部分。  
  
 此工具会自动随 Visual Studio 一起安装。 若要运行此工具，请使用开发人员命令提示（或 Windows 7 中的 Visual Studio 命令提示）。 有关详细信息，请参阅[命令提示](../../../docs/framework/tools/developer-command-prompt-for-vs.md)。  
  
 在命令提示符处，键入以下内容：  
  
## <a name="syntax"></a>语法  
  
```  
CorFlags.exe assembly [options]  
```  
  
#### <a name="parameters"></a>参数  
  
|必选参数|描述|  
|------------------------|-----------------|  
|`assembly`|要为其配置 CorFlags 的程序集的名称。|  
  
|选项|描述|  
|------------|-----------------|  
|/32BIT[REQ]+|设置 32BITREQUIRED 标志。|  
|/32BIT[REQ]-|清除 32BITREQUIRED 标志。|  
|/32BITPREF+|设置 32BITPREFERRED 标志。 该应用程序甚至可以作为 32 位进程在 64 位平台上运行。 仅在 EXE 文件中设置此标志。 如果在 DLL 上设置此标志，则 DLL 将无法在 64 位进程中加载，并引发 <xref:System.BadImageFormatException> 异常。 具有此标志的 EXE 文件可以加载到 64 位进程中。<br /><br /> 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中是新增选项。|  
|/32BITPREF-|清除 32BITPREFERRED 标志。<br /><br /> 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中是新增选项。|  
|**/?**|显示该工具的命令语法和选项。|  
|/Force|强制执行更新，即使程序集具有强名称也是如此。 重要提示：如果更新使用强名称的程序集，则必须在执行其代码之前再次对其签名。|  
|**/help**|显示该工具的命令语法和选项。|  
|/ILONLY+|设置 ILONLY 标志。|  
|/ILONLY-|清除 ILONLY 标志。|  
|**/nologo**|取消显示 Microsoft 启动版权标志。|  
|/RevertCLRHeader|将 CLR 标头版本还原到 2.0。|  
|/UpgradeCLRHeader|将 CLR 标头版本升级到 2.5。 注意：程序集必须具有 2.5 版或更高版本的 CLR 标头才能在本机运行。|  
  
## <a name="remarks"></a>备注  
 如果未指定任何选项，则 CorFlags 转换工具将显示指定程序集的标志。  
  
## <a name="see-also"></a>另请参阅  
 [工具](../../../docs/framework/tools/index.md)   
 [64 位应用程序](../../../docs/framework/64-bit-apps.md)   
 [命令提示](../../../docs/framework/tools/developer-command-prompt-for-vs.md)

