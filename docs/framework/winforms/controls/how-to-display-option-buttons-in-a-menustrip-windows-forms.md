---
title: "如何：在 MenuStrip 中显示选项按钮（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "显示选项按扭, MenuStrip [Windows 窗体]"
  - "MenuStrip [Windows 窗体], 显示选项按扭"
  - "选项按钮 [Windows 窗体], 在 MenuStrip 中显示"
ms.assetid: 8b596af2-9ff8-4f7b-93d7-cba830e167f4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 MenuStrip 中显示选项按钮（Windows 窗体）
选项按钮也称作单选按钮，它与复选框很相似，但用户一次只能选中一个。  尽管在默认情况下 <xref:System.Windows.Forms.ToolStripMenuItem> 类不提供选项按钮行为，但该类提供复选框行为供自定义，以便为 <xref:System.Windows.Forms.MenuStrip> 控件中的菜单项实现选项按钮行为。  
  
 当菜单项的 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> 属性为 `true` 时，用户可以单击该项以切换选中标记的显示。  <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 属性指示项的当前状态。  要实现基本选项按钮行为，必须确保在选中一个项时，将以前选中项的 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 属性设置为 `false`。  
  
 下面的过程描述如何在继承 <xref:System.Windows.Forms.ToolStripMenuItem> 类的类中实现此功能及附加功能。  `ToolStripRadioButtonMenuItem` 类重写诸如 <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A> 和 <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> 等成员，以提供选项按钮的选择行为和外观。  此外，此类重写 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性，这样，除非选中父项，否则将禁用子菜单上的选项。  
  
### 实现选项按钮选择行为  
  
1.  将 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> 属性初始化为 `true` 以启用项的选择。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#110)]
     [!code-vb[ToolStripRadioButtonMenuItem#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#110)]  
  
2.  选定新项后，重写 <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A> 方法以清除以前选定项的选择。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#120)]
     [!code-vb[ToolStripRadioButtonMenuItem#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#120)]  
  
3.  重写 <xref:System.Windows.Forms.ToolStripMenuItem.OnClick%2A> 方法，以确保单击已选定的项时不会将选择清除。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#130)]
     [!code-vb[ToolStripRadioButtonMenuItem#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#130)]  
  
### 修改选项按钮项的外观  
  
1.  重写 <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> 方法，以使用 <xref:System.Windows.Forms.RadioButtonRenderer> 类通过选项按钮来替换默认选中标记。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#140)]
     [!code-vb[ToolStripRadioButtonMenuItem#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#140)]  
  
2.  重写 <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseEnter%2A>、<xref:System.Windows.Forms.ToolStripMenuItem.OnMouseLeave%2A>、<xref:System.Windows.Forms.ToolStripMenuItem.OnMouseDown%2A> 和 <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseUp%2A> 方法，以跟踪鼠标状态并确保 <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> 方法绘制正确的选项按钮状态。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#150)]
     [!code-vb[ToolStripRadioButtonMenuItem#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#150)]  
  
### 在未选中父项时禁用子菜单上的选项  
  
1.  重写 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 属性，以便当项具有 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> 值为 `true` 且 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 值为 `false` 的父项时禁用该项。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#160)]
     [!code-vb[ToolStripRadioButtonMenuItem#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#160)]  
  
2.  重写 <xref:System.Windows.Forms.ToolStripMenuItem.OnOwnerChanged%2A> 方法，以订阅父项的 <xref:System.Windows.Forms.ToolStripMenuItem.CheckedChanged> 事件。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#170)]
     [!code-vb[ToolStripRadioButtonMenuItem#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#170)]  
  
3.  在父项 <xref:System.Windows.Forms.ToolStripMenuItem.CheckedChanged> 事件的处理程序中，使项无效以通过新启用的状态更新显示。  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#180)]
     [!code-vb[ToolStripRadioButtonMenuItem#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#180)]  
  
## 示例  
 下面的代码示例提供完整的 `ToolStripRadioButtonMenuItem` 类以及一个 <xref:System.Windows.Forms.Form> 类和 `Program` 类以演示选项按钮行为。  
  
 [!code-csharp[ToolStripRadioButtonMenuItem#000](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#000)]
 [!code-vb[ToolStripRadioButtonMenuItem#000](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#000)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RadioButtonRenderer>   
 [MenuStrip 控件](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [如何：实现自定义 ToolStripRenderer](../../../../docs/framework/winforms/controls/how-to-implement-a-custom-toolstriprenderer.md)