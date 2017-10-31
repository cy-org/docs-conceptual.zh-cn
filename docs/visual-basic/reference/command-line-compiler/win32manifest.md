---
title: "/win32manifest (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- /win32manifest compiler option [Visual Basic]
- win32manifest compiler option [Visual Basic]
- -win32manifest compiler option [Visual Basic]
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b07d5816e5bb80a95e608fa7214a2db48ebac0dc
ms.lasthandoff: 03/13/2017

---
# <a name="win32manifest-visual-basic"></a>/win32manifest (Visual Basic)
标识用户定义的 Win32 应用程序清单文件要嵌入到项目的可移植可执行 (PE) 文件。  
  
## <a name="syntax"></a>语法  
  
```  
/win32manifest: fileName  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`fileName`|自定义清单文件的路径。|  
  
## <a name="remarks"></a>备注  
 默认情况下，Visual Basic 编译器将嵌入到指定 asInvoker 请求的执行级别的应用程序清单。 它在其中可执行文件生成，通常为 bin\Debug 或 bin\Release 文件夹时使用 Visual Studio 的相同文件夹中创建清单。 如果您想要提供自定义清单，例如，若要指定请求的执行级别的 highestAvailable 或 requireAdministrator，使用此选项以指定文件的名称。  
  
> [!NOTE]
>  此选项与[/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)是互相排斥的选项。 如果您尝试在同一命令行中使用这两个选项，则会生成错误。  
  
 没有应用程序清单，应用程序指定的请求的执行级别都将遵循在 Windows Vista 中的用户帐户控制功能下的文件/注册表虚拟化。 有关虚拟化的详细信息，请参阅[Windows Vista 上的 ClickOnce 部署](https://docs.microsoft.com/visualstudio/deployment/clickonce-deployment-on-windows-vista)。  
  
 如果任意下列条件为真，您的应用程序将遵循虚拟化︰  
  
1.  您使用`/nowin32manifest`选项，你不提供清单在更高版本的生成步骤或 Windows 资源 (.res) 文件的一部分使用`/win32resource`选项。  
  
2.  提供一个自定义清单，不指定请求的执行级别。  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]创建一个默认.manifest 文件并将其存储在可执行文件旁的调试和发布目录。 您可以查看或编辑默认应用程序清单文件，方法是单击**视图 UAC 设置**上**应用程序**项目设计器中的选项卡。 有关详细信息，请参阅[应用程序页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)。  
  
 您可以通过使用提供的应用程序清单作为自定义后期生成步骤或作为 Win32 资源文件的一部分`/nowin32manifest`选项。 如果您希望应用程序会受到在 Windows Vista 上的文件或注册表虚拟化，使用该相同的选项。 这将使编译器创建和嵌入在 PE 文件中的默认清单。  
  
## <a name="example"></a>示例  
 下面的示例演示了 Visual Basic 编译器将插入 PE 默认清单。  
  
> [!NOTE]
>  编译器将插入清单 XML 的标准应用程序名称 MyApplication.app。 这是一种解决方法，使应用程序可以在 Windows Server 2003 Service Pack 3 上运行。  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/nowin32manifest (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)
