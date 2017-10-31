---
title: "如何：在 DataRepeater 控件中显示未绑定的控件 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater"
  - "DataRepeater, 添加未绑定控件"
  - "显示未绑定数据"
ms.assetid: f234fa40-5a13-4209-930e-7c5f81e86e66
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 如何：在 DataRepeater 控件中显示未绑定的控件 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

除了绑定控件外，您可能还希望向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 中添加其他控件，例如，在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的每个项上重复显示的静态标签或图像。  
  
> [!NOTE]
>  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 上还必须至少有一个绑定控件，否则在运行时将不会显示任何内容。  
  
### 向 DataRepeater 中添加未绑定控件  
  
1.  从**“工具箱”**的**“Visual Basic PowerPacks”**选项卡中将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到窗体或容器控件中。  
  
2.  拖动大小调整控点和定位控点来调整该控件的大小以及定位该控件。  
  
     您还可以通过在“属性”窗口中更改**“大小”**和**“位置”**属性来调整该控件的大小以及定位该控件。  
  
3.  向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中添加至少一个数据绑定控件。  有关更多信息，请参见 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)。  
  
4.  从**“工具箱”**中将一个控件拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域。  
  
     请注意，该控件有两个矩形区域。  内部区域是项模板；运行时将在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的每个项中重复添加到该模板中的控件。  外部区域是视区，项将显示在该区域中；运行时将不显示添加到该区域中的控件。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：使用两个 DataRepeater 控件创建主\/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)