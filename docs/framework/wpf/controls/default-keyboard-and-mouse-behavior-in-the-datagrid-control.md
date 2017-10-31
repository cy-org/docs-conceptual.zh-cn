---
title: "DataGrid 控件中的默认键盘和鼠标行为 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DataGrid [WPF], 键盘行为"
  - "DataGrid [WPF], 鼠标行为"
  - "键盘行为 [WPF], DataGrid"
  - "鼠标行为 [WPF], DataGrid"
ms.assetid: 563b8854-ca39-4d97-8235-17eaa0f93c8d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# DataGrid 控件中的默认键盘和鼠标行为
本主题描述用户如何通过使用键盘和鼠标与 <xref:System.Windows.Controls.DataGrid> 控件进行交互。  
  
 与 <xref:System.Windows.Controls.DataGrid> 的典型交互包括导航、选择和编辑。  <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 和 <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> 属性共同影响选择行为。  引起本主题中所述行为导致的默认值是 <xref:System.Windows.Controls.DataGridSelectionMode?displayProperty=fullName> 和 <xref:System.Windows.Controls.DataGridSelectionUnit?displayProperty=fullName>。  更改这些值可能会导致与所述行为不同的行为。  单元格何时才处于编辑模式，编辑控件可能重写 <xref:System.Windows.Controls.DataGrid> 的标准键盘行为。  
  
## 默认键盘行为  
 下表列出了 <xref:System.Windows.Controls.DataGrid> 的默认键盘行为。  
  
|键或组合键|说明|  
|-----------|--------|  
|向下键|将焦点移到在当前单元格正下方的单元格。  如果焦点位于最后一行中，则按向下键不执行任何操作。|  
|向上键|将焦点移到在当前单元格正上方的单元格。  如果焦点位于第一行中，则按向上键不执行任何操作。|  
|向左键|将焦点移到行中的前一个单元格。  如果焦点位于该行中的第一个单元格，则按向左键不执行任何操作。|  
|向右键|将焦点移到行中的下一个单元格。  如果焦点位于该行中的最后一个单元格，则按向右键不执行任何操作。|  
|Home|将焦点移到当前行的第一个单元格。|  
|End|将焦点移到当前行的最后一个单元格。|  
|Page Down|如果行不是分组的，按照完全显示的行数向下滚动控件。  将焦点移到完全显示的最后一行，但不改变列。<br /><br /> 如果行是分组的，将焦点移到 <xref:System.Windows.Controls.DataGrid> 中的最后一行，同时不更改列。|  
|向上翻页|如果行不是分组的，按照完全显示的行数向上滚动控件。  将焦点移到显示的第一行，但不改变列。<br /><br /> 如果行是分组的，将焦点移到 <xref:System.Windows.Controls.DataGrid> 中的第一行，同时不更改列。|  
|TAB|将焦点移到当前行的下一个单元格。  如果焦点经位于此行的最后一个单元格，则将焦点移到下一行的第一个单元格。  如果焦点位于控件的最后一个单元格，则将焦点按父容器的 Tab 键顺序移到下一个控件。<br /><br /> 如果当前单元格处于编辑模式，按 tab 键引起焦点从当前行移开，则对行做的任何更改都会在焦点改变前进行提交。|  
|Shift\+Tab|将焦点移到当前行的上一个单元格。  如果焦点已经位于此行中的第一个单元格，则将焦点移到前一行的最后一个单元格。  如果焦点位于控件的第一个单元格，则将焦点按父容器的 Tab 键顺序移到前一个控件。<br /><br /> 如果当前单元格处于编辑模式，按 tab 键引起焦点从当前行移开，则对行做的任何更改都会在焦点改变前进行提交。|  
|Ctrl\+向下键|将焦点移到当前列的最后一个单元格。|  
|Ctrl\+向上键|将焦点移到当前列的第一个单元格。|  
|Ctrl\+向右键|将焦点移到当前行的最后一个单元格。|  
|Ctrl\+向左键|将焦点移到当前行的第一个单元格。|  
|Ctrl\+Home|将焦点移到控件的第一个单元格。|  
|Ctrl\+End|将焦点移到控件的最后一个单元格。|  
|Ctrl\+Page Down|与 Page Down 相同。|  
|Ctrl\+Page Up|与 Page Up 相同。|  
|F2|如果对于当前列 <xref:System.Windows.Controls.DataGrid.IsReadOnly%2A?displayProperty=fullName> 属性是 `false`，并且 <xref:System.Windows.Controls.DataGridColumn.IsReadOnly%2A?displayProperty=fullName> 属性是 `false`，则使当前单元格进入单元格编辑模式。|  
|Enter|提交对当前单元格和行的所有更改，并将焦点移到在当前单元格正下方的单元格。  如果焦点位于最后一行，则提交所有更改，而不移动焦点。|  
|Esc|如果控件处于编辑模式，则取消编辑并恢复已在控件中进行的任何更改。  如果基础数据源实现 <xref:System.ComponentModel.IEditableObject>，则第二次按 Esc 将取消整个行的编辑模式。|  
|Backspace|当编辑单元格时，删除光标前的字符。|  
|Delete|当编辑单元格时，删除光标后的字符。|  
|Ctrl\+Enter|提交对当前单元格的所有更改，而不移动焦点。|  
|Ctrl\+A|如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，选择  <xref:System.Windows.Controls.DataGrid> 中的所有行。|  
  
## 选择键  
 如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 属性设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，则导航行为不会改变，但是在按 Shift 键（包括 Ctrl\+Shift 键）的同时使用键盘导航将修改多行选择。  导航开始前，控件将当前行标记为定位行。  在按 Shift 键的同时进行定位时，所选内容包括定位行和当前行之间的所有行。  
  
 以下选择键将修改多行选择。  
  
-   Shift\+向下键  
  
-   Shift\+向上键  
  
-   Shift\+Page Down  
  
-   Shift\+Page Up  
  
-   Ctrl\+Shift\+向下键  
  
-   Ctrl\+Shift\+向上键  
  
-   Ctrl\+Shift\+Home  
  
-   Ctrl\+Shift\+End  
  
## 默认鼠标行为  
 下表列出了 <xref:System.Windows.Controls.DataGrid> 的默认鼠标行为。  
  
|鼠标操作|说明|  
|----------|--------|  
|单击某一未选择行|使已单击的行成为当前行，已单击的单元格成为当前单元格。|  
|单击当前单元格|将当前的单元格置于编辑模式下。|  
|拖动某一列标头单元格|如果对于当前列 <xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A?displayProperty=fullName> 属性是 `true`，并且 <xref:System.Windows.Controls.DataGridColumn.CanUserReorder%2A?displayProperty=fullName> 属性是 `true`，则移动该列将其放入新的位置。|  
|拖动某一列标头分隔符|如果对于当前列 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> 属性是 `true`，并且 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> 属性是 `true`，则调整该列的大小。|  
|双击列标题分隔符|如果当前列的 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> 属性为 `true`，并且 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> 属性为 `true`，则使用 <xref:System.Windows.Controls.DataGridLength.Auto%2A> 调整大小模式自动调整该列的大小。|  
|单击某一列标头单元格|如果对于当前列 <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A?displayProperty=fullName> 属性是 `true`，并且 <xref:System.Windows.Controls.DataGridColumn.CanUserSort%2A?displayProperty=fullName> 属性是 `true`，则对该列排序。<br /><br /> 单击已排序的某一列的标头将颠倒该列的排序方向。<br /><br /> 单击多列标头的同时按 Shift 键将以单击的顺序按多列排序。|  
|Ctrl\+单击某一行|如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，则修改非连续多行选择。<br /><br /> 如果该行已被选择，则取消选择该行。|  
|Shift\+单击某一行|如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，则修改连续多行选择。|  
|单击行组标题|展开或折叠组。|  
|单击 <xref:System.Windows.Controls.DataGrid> 左上角的“全选”按钮|如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，选择  <xref:System.Windows.Controls.DataGrid> 中的所有行。|  
  
## 鼠标选择  
 如果 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 属性设置为 <xref:System.Windows.Controls.DataGridSelectionMode>，在按 Ctrl 或 Shift 的同时单击某一行将修改多行选择。  
  
 按 Ctrl 键的同时单击某一行时，该行会更改其选择状态，而其他所有行均保持其当前选择状态。  请操作以选择不相邻行的范围。  
  
 按 Shift 的同时单击某一行时，所选内容包括当前行与单击之前处于当前行位置的定位行之间的所有行。  随后按 Shift 键的同时单击会更改当前行，而不是定位行。  请操作以选择相邻行的范围。  
  
 CTRL \+ SHIFT 可以组合以选择相邻的行的不相邻范围。  要做到这一点，请按前面部分所述在单击时按 Shift 选择第一个范围。  选择第一个范围的行之后，在按住 Ctrl 的同时单击可选择下一个范围中的第一行，然后在按住 Ctrl\+Shift 的同时单击下一个范围中的最后一行。  
  
## 请参阅  
 <xref:System.Windows.Controls.DataGrid>   
 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A>