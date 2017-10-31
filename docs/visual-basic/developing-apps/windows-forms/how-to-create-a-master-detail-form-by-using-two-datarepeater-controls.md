---
title: "如何︰ 使用两个 DataRepeater 控件 (Visual Studio) 创建母版-详细信息窗体 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, master/detail tables
ms.assetid: eec43ae3-05d8-45a1-8d41-3803c6359dbe
caps.latest.revision: 7
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 23789bb11cab17b50928651e1dc00d5d59640c0f
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-masterdetail-form-by-using-two-datarepeater-controls-visual-studio"></a>如何：使用两个 DataRepeater 控件创建主/详细信息窗体 (Visual Studio)
您可以使用两个或多个显示相关的数据<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件创建大纲/细节窗体。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 例如，您可能想要显示客户的列表中其中一个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>，并当用户选择某个客户，在第二个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>中显示该客户的订单列表</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
 可以通过将共享相同的主表节点从的明细项目显示相关的数据**数据源**窗口拖到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 例如，如果您有了 Customers 表和相关的 Orders 表的数据源，您看到这两个表为在树视图中的顶级节点**数据源**窗口。 展开客户节点，以便您可以看到的列。 请注意，在列表中的最后一列表示订单表的可展开节点。 此节点表示客户的相关的订单。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-display-related-data-in-two-datarepeater-controls"></a>若要在两个 DataRepeater 控件中显示相关的数据  
  
1.  将两个<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件从**Visual Basic PowerPacks**选项卡中**工具箱**到窗体或容器控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  拖动调整大小和位置的手柄以调整控件大小，并将其位置由并行。  
  
3.  在 **“数据”** 菜单上，单击 **“显示数据源”**。  
  
    > [!NOTE]
    >  如果**数据源**窗口为空，则向其添加数据源。 有关详细信息，请参阅[添加新数据源](https://docs.microsoft.com/visualstudio/data-tools/add-new-data-sources)。  
  
4.  在**数据源**窗口中，选择主表的顶级节点。  
  
5.  通过单击主表的拖放类型更改为详细信息**详细信息**表节点上的下拉列表中。  
  
6.  主表节点拖到第一个项模板区域<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
7.  展开主表节点并选择相关表的详细信息节点。  
  
8.  通过单击详细信息表的拖放类型更改为详细信息**详细信息**表节点上的下拉列表中。  
  
9. 选择此表节点，然后将其拖动到第二个项模板区域<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何︰ 在 DataRepeater 控件中显示绑定的数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何︰ 显示相关数据在 Windows 窗体应用程序](http://msdn.microsoft.com/library/60b1f1ec-6257-42ab-83f0-06d54ed364fd)   
 [如何︰ 更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
