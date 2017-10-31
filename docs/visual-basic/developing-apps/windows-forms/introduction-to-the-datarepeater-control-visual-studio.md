---
title: "介绍 DataRepeater 控件 (Visual Studio) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- repeating data
- DataRepeater, overview
- DataRepeater
ms.assetid: 78a52a1d-65f0-4ecb-97ff-53bc114300c5
caps.latest.revision: 8
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
ms.openlocfilehash: 86078426494caabefc6bbfb036037007e830e1cb
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-the-datarepeater-control-visual-studio"></a>DataRepeater 控件简介 (Visual Studio)
Visual Basic Power Packs<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件是可滚动容器，用于显示控件重复数据，例如，行在数据库表中。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 可用作一种替代方法<xref:System.Windows.Forms.DataGridView>控制何时需要更好地控制数据的布局。</xref:System.Windows.Forms.DataGridView> <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>"重复"相关的控件的一组通过在滚动视图中创建多个实例。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 这使用户能够同时查看多条记录。  
  
## <a name="overview"></a>概述  
 在设计时<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控制由两个部分组成。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 外部部分是*视区*、 滚动数据在运行时的显示。 内部 （顶级） 部分，称为*项模板*，放置，将重复在运行时，通常一个控件对应的数据源中的每个字段的控件。 属性和项模板中的控件封装在<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>属性。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>  
  
 在运行时，<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>复制到一个虚拟<xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>用于在每个记录滚动到视图时显示数据的对象。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 您可以自定义的显示中的单个记录<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>事件，例如，突出显示根据它所包含的值的字段。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 有关详细信息，请参阅[如何︰ 更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)。  
  
 最常见的用途<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件将显示数据库表或其他绑定的数据源中的数据。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 除了[!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)]数据对象<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件可以绑定到的任何类都实现<xref:System.Collections.IList>（包括数组） 的接口，而实现的任何类<xref:System.ComponentModel.IListSource>接口的任何类都实现<xref:System.ComponentModel.IBindingList>接口或任何实现类都<xref:System.ComponentModel.IBindingListView>接口。</xref:System.ComponentModel.IBindingListView> </xref:System.ComponentModel.IBindingList> </xref:System.ComponentModel.IListSource> </xref:System.Collections.IList> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
### <a name="data-binding"></a>数据绑定  
 通常情况下，通过拖动字段来完成数据绑定**数据源**窗口拖到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 有关详细信息，请参阅[如何︰ 在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)。  
  
 当处理大量数据，您可以设置<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>属性设置为`True`来显示可用数据的子集。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 虚拟模式下都需要的数据缓存从其实现<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>将被填充，并且您必须在运行时控制与数据缓存的所有交互。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 有关详细信息，请参阅[DataRepeater 控件中的虚拟模式](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md)。  
  
 您还可以通过以下方式显示未绑定的控件上<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 例如，您可以在每个项上显示图像，它将重复。 有关详细信息，请参阅[如何︰ 在 DataRepeater 控件中显示未绑定控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)。  
  
### <a name="events"></a>事件  
 最重要的事件<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控制是<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>事件，当新项目滚动到视图，与<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>事件，选择一项时，将引发该事件。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 您可以使用<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>事件以更改项的外观。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 例如，可以突出显示负值。 使用<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>事件，以在选择了某项时访问控件的值。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件都公开所有标准的控件事件在代码编辑器中。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 但是，一些事件应不使用。 键盘和鼠标事件，如`KeyDown`， `Click`，和`MouseDown`将不会引发运行时由于<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件本身永远不会具有焦点。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>不在设计时公开事件，因为它仅在运行时创建。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 如果您希望处理键盘和鼠标事件，您可以添加<xref:System.Windows.Forms.Panel>控制转移到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>在设计时，然后处理事件的<xref:System.Windows.Forms.Panel>。</xref:System.Windows.Forms.Panel> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:System.Windows.Forms.Panel> 有关详细信息，请参阅[DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)。  
  
### <a name="customizations"></a>自定义  
 有多种方法自定义外观和行为的<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控制，请在运行时和设计时。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 属性可以设置要更改颜色、 隐藏或修改项的标头，将方向从垂直改为水平，以及更多。 有关详细信息，请参阅[如何︰ 更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)，[如何︰ 在 DataRepeater 控件中显示项标头](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)，和[如何︰ 更改 DataRepeater 控件的布局](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)。  
  
 请注意，某些属性应用到<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>控件自身，而其他用户仅适用于<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>。</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 请确保您具有正确设置属性之前所选控件的节。 有关详细信息，请参阅[如何︰ 更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)。  
  
 其他自定义包括控制能够添加或删除记录、 添加搜索功能和母版和详细信息的格式显示相关的数据。 有关详细信息，请参阅[如何︰ 禁用添加和删除 DataRepeater 项](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)，[如何︰ 在 DataRepeater 控件中搜索数据](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)，和[如何︰ 创建母版/详细信息窗体使用两个 DataRepeater 控件 (Visual Studio)](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)。  
  
## <a name="see-also"></a>另请参阅  
 [DataRepeater 控件](../../../visual-basic/developing-apps/windows-forms/datarepeater-control-visual-studio.md)   
 [演练︰ 在 DataRepeater 控件中显示数据](../../../visual-basic/developing-apps/windows-forms/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
