---
title: "如何：使用 LineShape 控件绘制直线 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "文本行, 绘图"
  - "LineShape 控件"
ms.assetid: 83e71b4e-aa76-4f9b-b547-8704309fd1e5
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：使用 LineShape 控件绘制直线 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

您可以使用 <xref:Microsoft.VisualBasic.PowerPacks.LineShape> 控件在设计时和运行时在窗体或容器上绘制水平线、垂直线或对角线。  
  
 **说明** 在下面的说明中，您的计算机可能会对 Visual Studio 的某些用户界面元素显示不同的名称或位置。  您安装的 Visual Studio 版本以及使用的设置决定了这些元素。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时绘制直线  
  
1.  从**“工具箱”**的**“Visual Basic PowerPacks”**选项卡中将 <xref:Microsoft.VisualBasic.PowerPacks.LineShape> 控件拖到窗体或容器控件中。  
  
2.  拖动大小调整控点和移动控点来调整直线的大小以及定位直线。  
  
     还可以通过在**“属性”**窗口中更改 `X1`、`X2`、`Y1` 和 `Y2` 属性来调整直线的大小以及定位直线。  
  
3.  还可以选择在**“属性”**窗口中设置其他属性（如 `BorderStyle` 或 `BorderColor`）来更改直线的外观。  
  
### 在运行时绘制直线  
  
1.  在**“项目”**菜单上，单击**“添加引用”**。  
  
2.  在**“添加引用”**对话框中选择**“Microsoft.VisualBasic.PowerPacks.VS”**，然后单击**“确定”**。  
  
3.  在**“代码编辑器”**中，将 `Imports` 或 `using` 语句添加到模块的顶部：  
  
    ```vb#  
    Imports Microsoft.VisualBasic.PowerPacks  
    ```  
  
    ```c#  
    using Microsoft.VisualBasic.PowerPacks;  
    ```  
  
4.  将下面的代码添加到 `Event` 过程中：  
  
     [!code-cs[VbPowerPacksLine#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-draw-lines-with-the-lineshape-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksLine#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-draw-lines-with-the-lineshape-control-visual-studio_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.LineShape>   
 [Line 和 Shape 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-line-and-shape-controls-visual-studio.md)   
 [如何：使用 OvalShape 和 RectangleShape 控件绘制形状](../../../visual-basic/developing-apps/windows-forms/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls.md)