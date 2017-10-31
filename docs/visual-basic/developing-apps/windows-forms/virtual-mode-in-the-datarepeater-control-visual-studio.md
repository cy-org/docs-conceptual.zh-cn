---
title: "DataRepeater 控件 (Visual Studio) 中的虚拟模式 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- virtual data binding
- DataRepeater
- DataRepeater, virtual mode
ms.assetid: 5fb805dc-2d8b-4139-b1e3-86e4c2667221
caps.latest.revision: 13
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
ms.openlocfilehash: 85f7e250c57a507e891eb30756c0550098cce9e0
ms.lasthandoff: 03/13/2017

---
# <a name="virtual-mode-in-the-datarepeater-control-visual-studio"></a>DataRepeater 控件中的虚拟模式 (Visual Studio)
如果想要显示的表格数据的大量<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件，可以通过设置提高性能<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>属性设置为`True`和显式管理对其数据源的控件的交互。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件提供了几个事件，您可以处理与数据源进行交互并根据需要在运行时显示的数据。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="how-virtual-mode-works"></a>虚拟模式的工作原理  
 有关最常见的方案<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件将绑定的子控件<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>到数据源在设计时，并允许<xref:System.Windows.Forms.BindingSource>传递来回根据需要的数据。</xref:System.Windows.Forms.BindingSource> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 当您使用的虚拟模式时，这些控件将不绑定到数据源和数据在运行时对基础数据源来回传递。  
  
 当<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>属性设置为`True`，通过添加从控件创建的用户界面**工具箱**而不是添加绑定的控件从**数据源**窗口。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>  
  
 根据控件的控件引发事件，并且必须添加代码来处理数据的显示。 当新<xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>滚动进行查看，<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>事件引发的每个控件一次并且必须提供的值中每个控件<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>事件处理程序。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>  
  
 如果其中一个控件中的数据更改，用户<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>引发事件，您必须验证数据并将其保存到您的数据源。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>  
  
 如果用户添加新项时，<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>引发事件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> 使用此事件处理程序在您的数据源中创建一条新记录。 若要防止意外的更改，您必须监视<xref:System.Windows.Forms.Control.KeyDown>事件对于每个控件和调用<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A>如果用户按 ESC 键。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> </xref:System.Windows.Forms.Control.KeyDown>  
  
 如果您的数据源发生更改，则可以刷新<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件通过调用<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A>和<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A>方法。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 必须按顺序调用这两种方法。  
  
 最后，您必须实现的事件处理程序<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>事件都发生在删除某项后，还可以选择实现<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems>和<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems>事件，当用户通过按 DELETE 键删除某个项时发生。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>  
  
## <a name="implementing-virtual-mode"></a>实现虚拟模式  
 以下是实现虚拟模式下所需的步骤。  
  
#### <a name="to-implement-virtual-mode"></a>实现虚拟模式  
  
1.  拖动<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件从**Visual Basic PowerPacks**选项卡中**工具箱**到窗体或容器控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 设置<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>属性设置为`True`。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>  
  
2.  将控件从**工具箱**拖动的项模板区域 （上部区域） 到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 对于您想要显示的数据源中的每个字段，将需要一个控件。  
  
3.  实现的处理程序<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>事件，以便为每个控件提供值。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> 当新时，将引发此事件<xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>滚动到视图。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 该代码将类似以下示例中，这是一个名为的数据源`Employees`。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_1.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_1.cs)]  
  
4.  实现的处理程序<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>事件来存储数据。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> 当用户将更改提交给<xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>的子控件时，将引发此事件 该代码将类似以下示例中，这是一个名为的数据源`Employees`。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_2.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_2.cs)]  
  
5.  实现一个处理程序的每个子控件<xref:System.Windows.Forms.Control.KeyDown>事件和监视器 ESC 键。</xref:System.Windows.Forms.Control.KeyDown> 调用<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A>方法，以阻止<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>因而引发的事件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> 该代码将类似下面的示例。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_3.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_3.cs)]  
  
6.  实现的处理程序<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>事件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> 当用户添加到一个新项时，将引发此事件<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 该代码将类似以下示例中，这是一个名为的数据源`Employees`。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_4.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_4.cs)]  
  
7.  实现的处理程序<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>事件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved> 当用户删除现有项，将发生此事件。 该代码将类似以下示例中，这是一个名为的数据源`Employees`。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_5.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_5.cs)]  
  
8.  对于控制级别验证，可以选择实现的处理程序<xref:System.Windows.Forms.Control.Validating>的子控件的事件。</xref:System.Windows.Forms.Control.Validating> 该代码将类似下面的示例。  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&#6;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_6.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode&#6;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_6.cs)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)
