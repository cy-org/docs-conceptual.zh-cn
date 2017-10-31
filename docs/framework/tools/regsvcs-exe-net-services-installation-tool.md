---
title: "Regsvcs.exe（.NET 服务安装工具）"
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
- Regsvcs.exe
- .NET Services Installation tool
- loading assemblies
- assemblies [.NET Framework], registering
- type libraries
- registering assemblies
ms.assetid: 5220fe58-5aaf-4e8e-8bc3-b78c63025804
caps.latest.revision: 21
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 931fc9ee10762485f8fc4da906109023f15e09f8
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="regsvcsexe-net-services-installation-tool"></a>Regsvcs.exe（.NET 服务安装工具）
.NET 服务安装工具执行下列操作：  
  
-   加载并注册程序集。  
  
-   生成、注册类型库并将其安装到指定的 COM+ 应用程序中。  
  
-   配置以编程方式添加到类的服务。  
  
 若要运行此工具，请使用开发人员命令提示（或 Windows 7 中的 Visual Studio 命令提示）。 有关详细信息，请参阅[命令提示](../../../docs/framework/tools/developer-command-prompt-for-vs.md)。  
  
 在命令提示符处，键入以下内容：  
  
## <a name="syntax"></a>语法  
  
```  
      regsvcs [/c | /fc | /u] [/tlb:typeLibraryFile] [/extlb]  
[/reconfig] [/componly] [/appname:applicationName]  
[/nologo] [/quiet]assemblyFile.dll   
```  
  
#### <a name="parameters"></a>参数  
  
|参数|描述|  
|--------------|-----------------|  
|assemblyFile.dll|源程序集文件。 此程序集必须用强名称进行签名。 有关详细信息，请参阅[使用强名称为程序集签名](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)。|  
  
|选项|描述|  
|------------|-----------------|  
|/appdir: path|指定应用程序的根目录。|  
|/appname: applicationName|指定要查找或创建的 COM+ 应用程序的名称。|  
|**/c**|创建目标应用程序。|  
|/componly|只配置组件；忽略方法和接口。|  
|/exapp|指定此工具需要现有应用程序。|  
|/extlb|使用现有类型库。|  
|/fc|查找或创建目标应用程序。|  
|**/help**|显示该工具的命令语法和选项。|  
|/noreconfig|不重新配置现有的目标应用程序。|  
|**/nologo**|取消显示 Microsoft 启动版权标志。|  
|/parname: name|指定要查找或创建的 COM+ 应用程序的名称或 ID。|  
|/reconfig|重新配置现有目标应用程序。 这是默认设置。|  
|/tlb: typelibraryfile|指定要安装的类型库文件。|  
|/u|卸载目标应用程序。|  
|**/quiet**|指定安静模式；取消显示登录和成功消息。|  
|**/?**|显示该工具的命令语法和选项。|  
  
## <a name="remarks"></a>备注  
 Regsvcs.exe 需要由 assemblyFile.dll 指定的源程序集文件。 此程序集必须用强名称进行签名。 有关强名称签名的更多信息，请参阅[使用强名称为程序集签名](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)。 目标应用程序的名称和类型库文件的名称都是可选的。 如果 applicationName 参数尚不存在，则该参数可从源程序集文件生成并且将由 Regsvcs.exe 创建。 typelibraryfile 参数可以指定类型库名称。 如果未指定类型库名称，默认情况下，Regsvcs.exe 将使用程序集名称。  
  
 当 Regsvcs.exe 注册组件的方法时，它需要遵从那些方法的[要求](http://msdn.microsoft.com/en-us/e5283e28-2366-4519-b27d-ef5c1ddc1f48)和[链接要求](../../../docs/framework/misc/link-demands.md)。 因为该工具在完全受信任的环境中执行，所以大多数权限要求都会成功。 但是，如果组件中的方法受 <xref:System.Security.Permissions.StrongNameIdentityPermission> 或 <xref:System.Security.Permissions.PublisherIdentityPermission> 的要求或链接要求保护，则 Regsvcs.exe 无法注册这些组件。  
  
 你必须在本地计算机上具有管理特权才能使用 Regsvcs.exe。  
  
 如果 Regsvcs.exe 在执行上述任何操作时失败，它将显示相应的错误信息。  
  
## <a name="examples"></a>示例  
 下面的命令将 `myTest.dll` 中包含的所有公共类添加到 `myTargetApp`（一个现有的 COM+ 应用程序）中，同时生成 `myTest.tlb` 类型库。  
  
```  
regsvcs /appname:myTargetApp myTest.dll  
```  
  
 下面的命令将 `myTest.dll` 中包含的所有公共类添加到 `myTargetApp`（一个现有的 COM+ 应用程序）中，同时生成 `newTest.tlb` 类型库。  
  
```  
regsvcs /appname:myTargetApp /tlb:newTest.tlb myTest.dll  
```  
  
## <a name="see-also"></a>另请参阅  
 [工具](../../../docs/framework/tools/index.md)   
 [如何：使用强名称为程序集签名](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)   
 [命令提示](../../../docs/framework/tools/developer-command-prompt-for-vs.md)

