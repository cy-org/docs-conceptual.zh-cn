---
title: "部署引用 PrintForm 组件 (Visual Basic 中) 的应用程序 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- PrintForm component [Visual Basic], deploying
ms.assetid: b595ea44-a712-4625-a761-190c64f59bbe
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 016643329d2ee66ca5a32f155cf91e0ee137f38f
ms.lasthandoff: 03/13/2017

---
# <a name="deploying-applications-that-reference-the-printform-component-visual-basic"></a>部署引用 PrintForm 组件 (Visual Basic 中) 的应用程序
如果你想要部署的应用程序引用<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件，必须在目标计算机上安装的组件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 Visual Studio 中不再包含 PowerPack 控件，但你可以从 [下载中心](http://www.microsoft.com/en-us/download/details.aspx?id=25169)下载它们。  
  
## <a name="installing-the-printform-as-a-prerequisite"></a>作为系统必备组件安装 PrintForm  
 若要成功部署应用程序，你还必须部署应用程序引用的所有组件。 安装必备项的过程称为 *引导*。  
  
 当<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>在开发计算机上安装组件，Microsoft Visual Basic Power Packs 引导程序包添加到[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]引导程序目录。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 当您按照添加对于任何系统必备组件的过程时，该包就可[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]或 Windows Installer 部署。  
  
 默认情况下，引导组件将从与安装包的相同的位置进行部署。 或者，你可以选择从 URL 或文件共享位置部署组件，用户可从这些位置按需进行下载。  
  
> [!NOTE]
>  若要安装引导组件，用户可能需要对计算机的管理员或类似用户权限。 有关[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]应用程序，这意味着，用户需要管理权限才能安装应用程序，而不考虑应用程序所指定的安全级别。 安装应用程序后，用户无需管理员权限即可运行该应用程序。  
  
 在安装期间，将提示用户安装<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>是否不存在于目标计算机上的组件。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 作为引导的替代方法，您可以预先部署<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>组件通过使用电子软件分发系统，如 Microsoft Systems Management Server。</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 与 ClickOnce 应用程序一起安装系统必备组件](http://msdn.microsoft.com/library/e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5)   
 [PrintForm 组件](../../../visual-basic/developing-apps/printing/printform-component.md)
