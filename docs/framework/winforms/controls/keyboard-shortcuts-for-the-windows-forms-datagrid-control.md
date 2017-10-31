---
title: "Windows 窗体 DataGrid 控件的键盘快捷键 | Microsoft Docs"
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
  - "DataGrid 控件 [Windows 窗体], 导航键"
  - "键盘快捷键, DataGrid 控件"
ms.assetid: a01780f9-20d5-4f5f-808f-c790c9a007a5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Windows 窗体 DataGrid 控件的键盘快捷键
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 下表列出了可用于在 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件中导航的键盘快捷键：  
  
|操作|快捷方式|  
|--------|----------|  
|完成单元格输入并向下移动到下一个单元格。<br /><br /> 如果焦点在子表链接上，则导航至该表。|Enter|  
|如果处于单元格编辑模式，则取消单元格编辑。<br /><br /> 如果处于字幕选择模式，则取消在行上的编辑。|Esc|  
|当编辑单元格时，删除插入点前的字符。|Backspace|  
|当编辑单元格时，删除插入点后的字符。|Delete|  
|移动到当前行的第一个单元格。|Home|  
|移动到当前行的最后一个单元格。|End|  
|突出显示当前单元格中的字符并将插入点置于该行的末尾。  与双击单元格的行为相同。|F2|  
|如果焦点在单元格上，则移动到该行中的下一个单元格。<br /><br /> 如果焦点在某行中最后一个单元格上，则移动到该行的第一个子表链接并将其展开。<br /><br /> 如果焦点在子链接上，则移动到下一个子链接。<br /><br /> 如果焦点在最后一个子链接上，则移动到下一行的第一个单元格。|TAB|  
|如果焦点在单元格上，则移动到该行中的上一个单元格。<br /><br /> 如果焦点在某行中第一个单元格上，则移动到上一行中最后一个展开的子表链接，或移动到上一行中最后一个单元格。<br /><br /> 如果焦点在子链接上，则移动到上一个子链接。<br /><br /> 如果焦点在第一个子链接上，则移动到上一行的最后一个单元格。|Shift\+Tab|  
|按 Tab 键顺序移动到下一个控件。|Ctrl\+Tab|  
|按 Tab 键顺序移动到上一个控件。|Ctrl\+Shift\+Tab|  
|如果在子表中，则向上移动到父表。  与单击“后退”按钮的行为相同。|Alt\+向左键|  
|展开子表链接。  Alt\+向下键展开所有链接，而不仅仅是选定的链接。|Alt\+向下键或 Ctrl\+加号键|  
|折叠子表链接。  Alt\+向上键折叠所有链接，而不仅仅是选定的链接。|Alt\+向上键或 Ctrl\+减号键|  
|按箭头的方向移动到最远的一个非空单元格。|Ctrl\+方向键|  
|按箭头的方向将所选内容扩展一行（不包括子表链接）。|Shift\+向上\/向下键|  
|按箭头的方向将所选内容扩展到最远的一个非空行（不包括子表链接）。|Ctrl\+Shift\+向上\/向下键|  
|移动到左上角的单元格。|Ctrl\+Home|  
|移动到右下角的单元格。|Ctrl\+End|  
|将所选内容扩展到顶端行。|Ctrl\+Shift\+Home|  
|将所选内容扩展到底端行。|Ctrl\+Shift\+End|  
|选择当前行（不包括子表链接）。|Shift\+空格键|  
|选择整个网格（不包括子表链接）。|Ctrl\+A|  
|当在子表中时，显示父行。|Ctrl\+Page Down|  
|当在子表中时，隐藏父行。|Ctrl\+Page Up|  
|将所选内容向下扩展一个屏幕（不包括子表链接）。|Shift\+Page Down|  
|将所选内容向上扩展一个屏幕（不包括子表链接）。|Shift\+Page Up|  
|为当前行调用 <xref:System.Windows.Forms.DataGrid.EndEdit%2A> 方法。|Ctrl\+Enter|  
|当处于编辑模式时，向单元格输入 <xref:System.DBNull.Value?displayProperty=fullName> 值。|CTRL\+0|  
  
## 请参阅  
 [DataGrid 控件概述](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)