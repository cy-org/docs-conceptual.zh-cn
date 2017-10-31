---
title: "如何：将程序集安装到全局程序集缓存"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- strong-named assemblies, global assembly cache
- global assembly cache, installing assemblies
- Global Assembly Cache tool
ms.assetid: a7e6f091-d02c-49ba-b736-7295cb0eb743
caps.latest.revision: 24
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c1a0eb5034c10b84b02f493cd21bccd121c8315c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-install-an-assembly-into-the-global-assembly-cache"></a>如何：将程序集安装到全局程序集缓存
可通过两种方法将强名称程序集安装到全局程序集缓存 (GAC) 中：  
  
> [!IMPORTANT]
>  仅强名称程序集可安装到 GAC 中。 若要了解如何创建强名称程序集，请参阅[如何：使用强名称为程序集签名](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)。  
  
-   使用 [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx)。  
  
     通过创建 InstallShield Limited Edition 项目可在 Visual Studio 2012 和 Visual Studio 2013 中执行此操作。  
  
     这是将程序集添加到全局程序集缓存的最常用方法，建议采用。 此安装程序可提供全局程序集缓存中程序集的引用计数，还具有其他优点。  
  
-   使用[全局程序集缓存工具 (Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)。  
  
     你可以使用 Gacutil.exe 将强名称程序集添加到全局程序集缓存，并查看全局程序集缓存的内容。  
  
    > [!NOTE]
    >  Gacutil.exe 只用于开发，不应用于将产品程序集安装到全局程序集缓存中。  
  
> [!NOTE]
>  在 .NET Framework 的早期版本中，可以使用 Shfusion.dll Windows 外壳扩展通过将程序集拖到文件资源管理器中来安装这些程序集。 从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]开始，Shfusion.dll 已过时。  
  
### <a name="to-use-the-global-assembly-cache-tool-gacutilexe"></a>使用全局程序集缓存工具 (Gacutil.exe)  
  
1.  在命令提示符处，键入下列命令：  
  
     gacutil -i \<assembly name>  
  
     在此命令中，“assembly name”是要在全局程序集缓存中安装的程序集的名称。  
  
 下面的示例将文件名为 `hello.dll` 的程序集安装到全局程序集缓存。  
  
```  
gacutil -i hello.dll  
```  
  
 有关详细信息，请参阅[全局程序集缓存工具 (Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)。  
  
### <a name="to-use-an-installshield-limited-edition-project"></a>使用 InstallShield Limited Edition 项目  
  
1.  通过以下方式将安装程序和部署包添加到解决方案：打开解决方案的快捷菜单，然后选择“添加”、“新建项目”。  
  
2.  在“添加新项目”对话框的“已安装”文件夹中，选择“其他项目类型”、“安装和部署”和“InstallShield Limited Edition”，并为项目指定名称。 （如果出现提示，下载、安装并激活 InstallShield。）  
  
3.  通过使用“解决方案资源管理器”中的“项目助手”或通过选择“解决方案资源管理器”中已编号步骤的子步骤，执行安装和部署项目的常规配置。如果未将程序集添加到 GAC，则按需配置设置。  
  
4.  若要开始将程序集添加到 GAC 的过程，请选择“文件”（位于“解决方案资源管理器”中“指定应用程序数据”步骤的下方）。  
  
5.  在“目标计算机的文件夹”窗格中，打开“目标计算机”的快捷菜单，再选择“显示预定义的文件夹”、“[GlobalAssemblyCache]”。  
  
6.  对于包含要安装到全局程序集缓存中的程序集的解决方案中的每个项目：  
  
    1.  在“源计算机的文件夹”窗格中，选择此项目。  
  
    2.  在“目标计算机的文件夹”窗格中，选择“[GlobalAssemblyCache]”。  
  
    3.  在“源计算机的文件”窗格中，选择“主输出来源”<project_name>。  
  
    4.  将步骤 c 中的文件拖动到“目标计算机的文件”窗格（或使用文件快捷菜单上的“复制”和“粘贴”命令）。  
  
## <a name="see-also"></a>另请参阅  
 [使用程序集和全局程序集缓存](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [如何：从全局程序集缓存中删除程序集](../../../docs/framework/app-domains/how-to-remove-an-assembly-from-the-gac.md)   
 [Gacutil.exe（全局程序集缓存工具）](../../../docs/framework/tools/gacutil-exe-gac-tool.md)   
 [如何：使用强名称为程序集签名](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)   
 [Windows Installer 部署](http://msdn.microsoft.com/en-us/121be21b-b916-43e2-8f10-8b080516d2a0)

