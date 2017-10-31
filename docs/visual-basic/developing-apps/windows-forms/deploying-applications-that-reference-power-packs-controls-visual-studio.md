---
title: "部署引用 Power Pack 控件 (Visual Studio) 的应用程序 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Power Packs, deploying
ms.assetid: f2230f53-a745-4731-89e6-033943faa209
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
ms.openlocfilehash: 4d342e655dcfe18ed3b5fc1d2710571ed8e3369e
ms.lasthandoff: 03/13/2017

---
# <a name="deploying-applications-that-reference-power-packs-controls-visual-studio"></a>部署引用 Power Pack 控件 (Visual Studio) 的应用程序
如果想要部署引用 Power Pack 控件的应用程序 (<xref:Microsoft.VisualBasic.PowerPacks.LineShape>， <xref:Microsoft.VisualBasic.PowerPacks.OvalShape>， <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape>，或<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>)，必须在目标计算机上安装控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> </xref:Microsoft.VisualBasic.PowerPacks.OvalShape> </xref:Microsoft.VisualBasic.PowerPacks.LineShape>  
  
## <a name="installing-the-power-packs-controls-as-a-prerequisite"></a>作为系统必备组件安装 Power Pack 控件  
 若要成功部署应用程序，你还必须部署应用程序引用的所有组件。 安装必备项的过程称为 *引导*。  
  
 当[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]安装到开发计算机上，引导程序包添加到一个 Power Pack[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]引导程序目录。 当您按照添加对于任何系统必备组件的过程时，该包就可[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]或 Windows Installer 部署。  
  
 默认情况下，引导组件将从与安装包的相同的位置进行部署。 或者，你可以选择从 URL 或文件共享位置部署组件，用户可从这些位置按需进行下载。  
  
> [!NOTE]
>  若要安装引导组件，用户可能需要对计算机的管理员或类似用户权限。 有关[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]应用程序，这意味着，用户需要管理权限才能安装应用程序，而不考虑应用程序所指定的安全级别。 安装应用程序后，用户无需管理员权限即可运行该应用程序。  
  
 在安装期间，将提示用户如果不存在于目标计算机上安装 Power Pack 控件。  
  
 作为引导的替代方法，你可以预先部署 Power Pack 控件，通过使用诸如 Microsoft Systems Management Server 的电子软件分发系统。  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 与 ClickOnce 应用程序一起安装系统必备组件](http://msdn.microsoft.com/library/e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5)   
 [Visual Basic Power Pack 控件](../../../visual-basic/developing-apps/windows-forms/power-packs-controls.md)
