---
title: "Windows 窗体 DataGridView 控件中的默认键盘和鼠标处理 | Microsoft Docs"
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
  - "数据网格, 鼠标处理"
  - "DataGridView 控件 [Windows 窗体], 键盘处理"
  - "DataGridView 控件 [Windows 窗体], 鼠标处理"
  - "DataGridView 控件 [Windows 窗体], 导航键"
  - "键盘, DataGridView 控件中的默认处理"
  - "鼠标, DataGridView 控件中的默认处理"
  - "导航键, DataGridView 控件"
ms.assetid: 4519b928-bfc8-4e8b-bb9c-b1e76a0ca552
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Windows 窗体 DataGridView 控件中的默认键盘和鼠标处理
下表描述了用户如何通过键盘和鼠标与 <xref:System.Windows.Forms.DataGridView> 控件交互。  
  
> [!NOTE]
>  要自定义键盘行为，可以处理标准键盘事件，例如 <xref:System.Windows.Forms.Control.KeyDown>。  然而，在编辑模式下，寄宿的编辑控件接收键盘输入，而且对于 <xref:System.Windows.Forms.DataGridView> 控件，不发生键盘事件。  要处理编辑控件事件，请将处理程序附加到 <xref:System.Windows.Forms.DataGridView.EditingControlShowing> 事件处理程序中的编辑控件。  或者，可以通过重写 <xref:System.Windows.Forms.DataGridView.ProcessDialogKey%2A> 和 <xref:System.Windows.Forms.DataGridView.ProcessDataGridViewKey%2A> 方法，在 <xref:System.Windows.Forms.DataGridView> 子类中自定义键盘行为。  
  
## 默认键盘处理  
  
### 基本导航和输入键  
  
|键或组合键|说明|  
|-----------|--------|  
|向下键|将焦点移到在当前单元格正下方的单元格。  如果焦点位于最后一行，则不执行任何操作。|  
|向左键|将焦点移到行中的前一个单元格。  如果焦点位于行中的第一个单元格，则不执行任何操作。|  
|向右键|将焦点移到行中的下一个单元格。  如果焦点位于行中的最后一个单元格，则不执行任何操作。|  
|向上键|将焦点移到在当前单元格正上方的单元格。  如果焦点位于第一行，则不执行任何操作。|  
|Home|将焦点移到当前行的第一个单元格。|  
|End|将焦点移到当前行的最后一个单元格。|  
|Page Down|按照完全显示的行数向下滚动控件。  将焦点移到完全显示的最后一行，但不改变列。|  
|向上翻页|按照完全显示的行数向上滚动控件。  将焦点移到显示的第一行，但不改变列。|  
|TAB|如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `false`，则将焦点移到当前行的下一个单元格。  如果焦点已经位于此行的最后一个单元格，则将焦点移到下一行的第一个单元格。  如果焦点位于控件的最后一个单元格，则将焦点按父容器的 Tab 键顺序移到下一个控件。<br /><br /> 如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `true`，则将焦点按父容器的 Tab 键顺序移到下一个控件。|  
|Shift\+Tab|如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `false`，则将焦点移到当前行的前一个单元格。  如果焦点已经位于此行中的第一个单元格，则将焦点移到前一行的最后一个单元格。  如果焦点位于控件的第一个单元格，则将焦点按父容器的 Tab 键顺序移到前一个控件。<br /><br /> 如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `true`，则将焦点按父容器的 Tab 键顺序移到前一个控件。|  
|Ctrl\+Tab|如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `false`，则将焦点按父容器的 Tab 键顺序移到下一个控件。<br /><br /> 如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `true`，则将焦点移到当前行的下一个单元格。  如果焦点已经位于此行的最后一个单元格，则将焦点移到下一行的第一个单元格。  如果焦点位于控件的最后一个单元格，则将焦点按父容器的 Tab 键顺序移到下一个控件。|  
|Ctrl\+Shift\+Tab|如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `false`，则将焦点按父容器的 Tab 键顺序移到前一个控件。<br /><br /> 如果 <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 属性值为 `true`，则将焦点移到当前行的前一个单元格。  如果焦点已经位于此行中的第一个单元格，则将焦点移到前一行的最后一个单元格。  如果焦点位于控件的第一个单元格，则将焦点按父容器的 Tab 键顺序移到前一个控件。|  
|Ctrl\+方向键|按箭头的方向将焦点移到最远的一个单元格。|  
|Ctrl\+Home|将焦点移到控件的第一个单元格。|  
|Ctrl\+End|将焦点移到控件的最后一个单元格。|  
|Ctrl\+Page Down\/Up|与 Page Down 或 Page Up 相同。|  
|F2|如果 <xref:System.Windows.Forms.DataGridView.EditMode%2A> 属性值为 <xref:System.Windows.Forms.DataGridViewEditMode> 或 <xref:System.Windows.Forms.DataGridViewEditMode>，则使当前单元格进入单元格编辑模式。|  
|F4|如果当前单元格为 <xref:System.Windows.Forms.DataGridViewComboBoxCell>，则使单元格进入编辑模式并显示下拉列表。|  
|Alt\+向上键\/向下键|如果当前单元格为 <xref:System.Windows.Forms.DataGridViewComboBoxCell>，则使单元格进入编辑模式并显示下拉列表。|  
|空格键|如果当前单元格为 <xref:System.Windows.Forms.DataGridViewButtonCell>、<xref:System.Windows.Forms.DataGridViewLinkCell> 或 <xref:System.Windows.Forms.DataGridViewCheckBoxCell>，则引发 <xref:System.Windows.Forms.DataGridView.CellClick> 和 <xref:System.Windows.Forms.DataGridView.CellContentClick> 事件。  如果当前单元格为 <xref:System.Windows.Forms.DataGridViewButtonCell>，还会按下按钮。  如果当前单元格为 <xref:System.Windows.Forms.DataGridViewCheckBoxCell>，则还更改复选状态。|  
|Enter|提交对当前单元格和行的所有更改，并将焦点移到在当前单元格正下方的单元格。  如果焦点位于最后一行，则提交所有更改，而不移动焦点。|  
|Esc|如果控件处于编辑模式，则取消编辑。  如果控件未处于编辑模式，那么如果将控件绑定到支持编辑的数据源，或虚拟模式已经以行级提交范围实现，则还原对当前行所做的所有更改。|  
|Backspace|当编辑单元格时，删除插入点前的字符。|  
|Delete|当编辑单元格时，删除插入点后的字符。|  
|Ctrl\+Enter|提交对当前单元格的所有更改，而不移动焦点。  如果将控件绑定到支持编辑的数据源，或虚拟模式已经以行级提交范围实现，则还要提交对当前行的所有更改。|  
|CTRL\+0|如果单元格是可编辑的，则在当前单元格中输入 <xref:System.DBNull.Value?displayProperty=fullName> 值。  默认情况下，<xref:System.DBNull> 单元格值的显示值为对当前单元格有效的 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 属性值。|  
  
### 选择键  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 属性设置为 `false`，而且 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode>，通过使用导航键更改当前单元格时，会将选择点更改至新单元格。  Shift、Ctrl 和 Alt 键不影响此行为。  
  
 如果 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，将出现同样的行为，但还会增加以下行为。  
  
|键或组合键|说明|  
|-----------|--------|  
|Shift\+空格键|选择整行或整列（与单击行标头或列标头一样）。|  
|导航键（箭头键、Page Up\/Down、Home、End）|如果选择了整行或整列，将当前单元格更改至新行或新列时，会将选择点移到整个新行或新列（具体取决于选择模式）。|  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `false`，而且 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，通过键盘将当前单元格更改至一新行或新列时，会将选择点移到整个新行或新列。  Shift、Ctrl 和 Alt 键不影响此行为。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `true`，导航行为不会改变，但是在按 Shift 键（包括 Ctrl\+Shift 键）的同时使用键盘导航将修改多单元格选择。  导航开始前，控件将当前单元格标记为定位单元格。  在按 Shift 键的同时进行定位时，所选内容包括定位单元格和当前单元格之间的所有单元格。  对于控件中的其他单元格，若他们已选定则保持选定，但是如果键盘导航临时将其置于定位单元格和当前单元格之间，则会取消选定。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `true`，而且 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，则定位单元格和当前单元格行为相同，但是只有整行或整列被选定或取消选定。  
  
## 默认鼠标处理  
  
### 基本鼠标处理  
  
> [!NOTE]
>  用鼠标左键单击单元格总是会更改当前单元格。  用鼠标右击单元格会打开快捷菜单（如果可用）。  
  
|鼠标操作|说明|  
|----------|--------|  
|按下鼠标左键|使已单击的单元格成为当前单元格，并引发 <xref:System.Windows.Forms.DataGridView.CellMouseDown?displayProperty=fullName> 事件。|  
|释放鼠标左键|引发 <xref:System.Windows.Forms.DataGridView.CellMouseUp?displayProperty=fullName> 事件|  
|鼠标左键单击|引发 <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> 和 <xref:System.Windows.Forms.DataGridView.CellMouseClick?displayProperty=fullName> 事件|  
|按下鼠标左键，在列标头单元格上拖动|如果 <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName> 属性为 `true`，移动该列将其放入新的位置。|  
  
### 鼠标选择  
 没有任何选择行为与鼠标中键或鼠标轮相关联。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 属性设置为 `false`，而且 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode>，则出现下面的行为。  
  
|鼠标操作|说明|  
|----------|--------|  
|单击鼠标左键|如果用户单击单元格，则只选择当前单元格。  如果用户单击行标头或列标头，则无选择行为。|  
|单击鼠标右键|显示快捷菜单（如果可用）。|  
  
 当 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode> 时出现同样的行为。不同的是，根据选择模式，单击行标头或列标头将选择整行或整列，并将当前单元格设置为该行或列的第一个单元格。  
  
 如果 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，单击行或列中的任何单元格将选择整行或整列。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `true`，在按 Ctrl 或 Shift 的同时单击单元格将修改多单元格选择。  
  
 按 Ctrl 键的同时单击单元格时，单元格会更改其选择状态，而其他所有单元格均保持其当前选择状态。  
  
 按 Shift 的同时单击一个单元格或一系列单元格时，所选内容包括当前单元格与第一次单击之前处于当前单元格位置的定位单元格之间的所有单元格。  当单击并将指针拖过多个单元格时，定位单元格就是拖动操作开始时单击过的单元格。  随后按 Shift 键的同时单击会更改当前单元格，而不是定位单元格。  对于控件中其他的单元格，若他们已选定则保持选定，但是如果鼠标导航临时将其置于定位单元格和当前单元格之间，则会取消选定。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `true`，<xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，那么在按 Shift 的同时单击行或列标头（具体取决于选择模式）时，如果存在对整行或整列的选择，则会修改现有的这种选择。  否则，将清除这种选择并开始新的整行或整列选择。  然而，按 Ctrl 的同时单击行或列标头，会从当前所选内容中添加或移除被单击的行或列，而不用另外修改当前所选内容。  
  
 如果 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 设置为 `true`，<xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>，在按 Shift 或 Ctrl 的同时单击单元格具有同样的行为，不同的是仅整行或整列会受到影响。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)