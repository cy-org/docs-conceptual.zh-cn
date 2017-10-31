---
title: "ToolStrip 控件体系结构 | Microsoft Docs"
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
  - "ToolStrip 控件 [Windows 窗体], 体系结构"
ms.assetid: 71df2d18-862e-4701-9ff9-c1fe606f94f2
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# ToolStrip 控件体系结构
<xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.ToolStripItem> 类提供灵活的可扩展系统，用于显示工具栏、状态和菜单项。  所有这些类均包含在 <xref:System.Windows.Forms> 命名空间中，并且类名中通常带有“ToolStrip”前缀（如 <xref:System.Windows.Forms.ToolStripOverflow>）或“Strip”后缀（如 <xref:System.Windows.Forms.MenuStrip>）。  
  
## ToolStrip  
 下面的主题描述 <xref:System.Windows.Forms.ToolStrip> 以及从中派生的控件。  
  
 <xref:System.Windows.Forms.ToolStrip> 是 <xref:System.Windows.Forms.MenuStrip>、<xref:System.Windows.Forms.StatusStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 的抽象基类。  下面的对象模型演示了 <xref:System.Windows.Forms.ToolStrip> 继承层次结构。  
  
 ![ToolStrip 对象模型](../../../../docs/framework/winforms/controls/media/toolstripobjectmodel.png "ToolStripObjectModel")  
ToolStrip 对象模型  
  
 可以通过 <xref:System.Windows.Forms.ToolStrip.Items%2A> 集合，访问 <xref:System.Windows.Forms.ToolStrip> 中的所有项。  可以通过 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A> 集合，访问 <xref:System.Windows.Forms.ToolStripDropDownItem> 中的所有项。  在从 <xref:System.Windows.Forms.ToolStrip> 派生的类中，还可以使用 <xref:System.Windows.Forms.ToolStrip.DisplayedItems%2A> 属性来只访问那些当前显示的项。  这些项是当前不在溢出菜单中的项。  
  
 下面各项专门设计用于与 <xref:System.Windows.Forms.ToolStripSystemRenderer> 和 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 在所有方向上无缝地结合使用。  默认情况下，它们在设计时可用于 <xref:System.Windows.Forms.ToolStrip> 控件：  
  
-   <xref:System.Windows.Forms.ToolStripButton>  
  
-   <xref:System.Windows.Forms.ToolStripSeparator>  
  
-   <xref:System.Windows.Forms.ToolStripLabel>  
  
-   <xref:System.Windows.Forms.ToolStripDropDownButton>  
  
-   <xref:System.Windows.Forms.ToolStripSplitButton>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### MenuStrip  
 <xref:System.Windows.Forms.MenuStrip> 是取代 <xref:System.Windows.Forms.MainMenu> 的顶级容器。  它还提供主要的处理和多文档界面 \(MDI\) 功能。  在功能上，<xref:System.Windows.Forms.ToolStripDropDownItem> 和 <xref:System.Windows.Forms.ToolStripMenuItem> 与 <xref:System.Windows.Forms.MenuStrip> 一起工作，尽管它们是从 <xref:System.Windows.Forms.ToolStripItem> 派生的。  
  
 下面各项专门设计用于与 <xref:System.Windows.Forms.ToolStripSystemRenderer> 和 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 在所有方向上无缝地结合使用。  默认情况下，它们在设计时可用于 <xref:System.Windows.Forms.MenuStrip> 控件：  
  
-   <xref:System.Windows.Forms.ToolStripMenuItem>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### StatusStrip  
 <xref:System.Windows.Forms.StatusStrip> 替换 <xref:System.Windows.Forms.StatusBar> 控件。  <xref:System.Windows.Forms.StatusStrip> 的特殊功能包括：自定义表布局、窗体的大小调整和移动手柄支持，以及 `Spring` 属性（允许 <xref:System.Windows.Forms.ToolStripStatusLabel> 自动填充可用空间）。  
  
 下面各项专门设计用于与 <xref:System.Windows.Forms.ToolStripSystemRenderer> 和 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 在所有方向上无缝地结合使用。  默认情况下，它们在设计时可用于 <xref:System.Windows.Forms.StatusStrip> 控件：  
  
-   <xref:System.Windows.Forms.ToolStripStatusLabel>  
  
-   <xref:System.Windows.Forms.ToolStripDropDownButton>  
  
-   <xref:System.Windows.Forms.ToolStripSplitButton>  
  
-   <xref:System.Windows.Forms.ToolStripProgressBar>  
  
### ContextMenuStrip  
 <xref:System.Windows.Forms.ContextMenuStrip> 替换 <xref:System.Windows.Forms.ContextMenu>。  可以将 <xref:System.Windows.Forms.ContextMenuStrip> 与任何控件关联，而且单击鼠标右键会自动显示上下文菜单（或快捷菜单）。  您可以通过使用 <xref:System.Windows.Forms.ToolStripDropDown.Show%2A> 方法以编程方式显示 <xref:System.Windows.Forms.ContextMenuStrip>。  <xref:System.Windows.Forms.ContextMenuStrip> 支持可取消的 <xref:System.Windows.Forms.ToolStripDropDown.Opening> 和 <xref:System.Windows.Forms.ToolStripDropDown.Closing> 事件以处理动态填充和多次单击方案。  <xref:System.Windows.Forms.ContextMenuStrip> 支持图像、菜单项复选状态、文本、访问键、快捷键和级联菜单。  
  
 下面各项专门设计用于与 <xref:System.Windows.Forms.ToolStripSystemRenderer> 和 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 在所有方向上无缝地结合使用。  默认情况下，它们在设计时可用于 <xref:System.Windows.Forms.ContextMenuStrip> 控件：  
  
-   <xref:System.Windows.Forms.ToolStripMenuItem>  
  
-   <xref:System.Windows.Forms.ToolStripSeparator>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### ToolStrip 一般功能  
 下面的主题描述 <xref:System.Windows.Forms.ToolStrip> 和派生控件的一般功能和行为。  
  
#### 绘制  
 可以通过多种方式在 <xref:System.Windows.Forms.ToolStrip> 控件中进行自定义绘制。  与其他 Windows 窗体控件一样，<xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.ToolStripItem> 两者都具有可重写的 `OnPaint` 方法和 `Paint` 事件。  与常规的绘制操作一样，坐标系是相对于控件的工作区的，也就是说，控件的左上角为 0, 0。  <xref:System.Windows.Forms.ToolStripItem> 的 `Paint` 事件和 `OnPaint` 方法的行为与其他控件绘制事件类似。  
  
 <xref:System.Windows.Forms.ToolStrip> 控件还通过 <xref:System.Windows.Forms.ToolStripRenderer> 类对项和容器的呈现提供更细致的访问，该类具有可重写的方法，用于绘制背景、项背景、项图像、项箭头、项文本以及 <xref:System.Windows.Forms.ToolStrip> 的边框。  这些方法的事件参数公开了多个属性，如矩形、颜色和文本格式，以便您可以根据需要进行调整。  
  
 要仅仅调整项绘制方式的几个方面，通常可以重写 <xref:System.Windows.Forms.ToolStripRenderer>。  
  
 如果正在编写新项并希望控制绘制的各个方面，则应重写 `OnPaint` 方法。  可以从 `OnPaint` 中使用 <xref:System.Windows.Forms.ToolStripRenderer> 的方法。  
  
 默认情况下，<xref:System.Windows.Forms.ToolStrip> 利用 <xref:System.Windows.Forms.ControlStyles> 设置进行双缓冲。  
  
#### 父级关系  
 与其他 Windows 窗体容器控件相比，<xref:System.Windows.Forms.ToolStrip> 控件中的容器所属权及父级关系的概念更为复杂。  要支持诸如溢出等动态方案、在多个 <xref:System.Windows.Forms.ToolStrip> 项之间共享下拉项并支持从控件生成 <xref:System.Windows.Forms.ContextMenuStrip>，这是必不可少的。  
  
 下面的列表描述与父级关系相关的成员并解释其使用。  
  
-   <xref:System.Windows.Forms.ToolStripDropDown.OwnerItem%2A> 访问作为下拉项源的项。  这与 <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A> 类似，但它并不返回控件，而是返回 <xref:System.Windows.Forms.ToolStripItem>。  
  
-   当多个控件共享相同的 <xref:System.Windows.Forms.ContextMenuStrip> 时，<xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A> 决定哪个控件是 <xref:System.Windows.Forms.ContextMenuStrip> 的源。  
  
-   <xref:System.Windows.Forms.ToolStripItem.GetCurrentParent%2A> 是 <xref:System.Windows.Forms.ToolStripItem.Parent%2A> 属性的只读访问器。  父级与所有者的不同之处在于，父级表示返回的当前 <xref:System.Windows.Forms.ToolStrip>（项可能显示在其中的溢出区域中）。  
  
-   <xref:System.Windows.Forms.ToolStripItem.Owner%2A> 返回 <xref:System.Windows.Forms.ToolStrip>，其项集合包含当前 <xref:System.Windows.Forms.ToolStripItem>。  要在不编写特殊代码处理溢出的情况下在顶级 <xref:System.Windows.Forms.ToolStrip> 中引用 <xref:System.Windows.Forms.ToolStrip.ImageList%2A> 或其他属性，这是最好的方法。  
  
#### 继承控件的行为  
 以下控件将在用于继承时被锁定：  
  
-   <xref:System.Windows.Forms.ToolStrip>  
  
-   <xref:System.Windows.Forms.MenuStrip>  
  
-   <xref:System.Windows.Forms.ContextMenuStrip>  
  
-   <xref:System.Windows.Forms.StatusStrip>  
  
-   <xref:System.Windows.Forms.ToolStripPanel>，包含 <xref:System.Windows.Forms.ToolStripContainer> 中的面板，也能包含单个 <xref:System.Windows.Forms.ToolStripPanel> 控件。  
  
 例如，通过使用上述列表中的一个或多个控件来创建新的 Windows 窗体应用程序。  将一个或多个控件的访问修饰符设置为 `public` 或 `protected`，然后生成项目。  添加从第一个窗体继承的窗体，然后选择一个继承的控件。  该控件显示为锁定，它的行为与其访问修饰符为 `private` 时一样。  
  
#### 对继承的 ToolStripContainer 支持  
 <xref:System.Windows.Forms.ToolStripContainer> 控件支持受限制的继承方案，与以下示例类似：  
  
1.  创建新的 Windows 窗体应用程序。  
  
2.  将一个 <xref:System.Windows.Forms.ToolStripContainer> 添加到窗体中。  
  
3.  将 <xref:System.Windows.Forms.ToolStripContainer> 的访问修饰符设置为 `public` 或 `protected`。  
  
4.  将 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 控件的任何组合添加到 <xref:System.Windows.Forms.ToolStripContainer> 的 <xref:System.Windows.Forms.ToolStripPanel> 区域中。  
  
5.  生成项目。  
  
6.  添加从第一个窗体继承的窗体。  
  
7.  选择窗体上继承的 <xref:System.Windows.Forms.ToolStripContainer>。  
  
#### 子控件的继承行为  
 完成上述步骤后，将发生以下继承行为：  
  
-   在设计器中，控件显示时带有继承图标。  
  
-   <xref:System.Windows.Forms.ToolStripPanel> 控件锁定；不能选择或重新排列其内容。  
  
-   可以向 <xref:System.Windows.Forms.ToolStripContentPanel> 添加控件、移动控件，并使其成为 <xref:System.Windows.Forms.ToolStripContentPanel> 的子控件。  
  
-   生成窗体后保留将更改。  
  
    > [!NOTE]
    >  将访问修饰符从作为 <xref:System.Windows.Forms.ToolStripContainer> 一部分的所有 <xref:System.Windows.Forms.ToolStripPanel> 控件上移除。  <xref:System.Windows.Forms.ToolStripContainer> 的访问修饰符控制整个控件。  
  
#### 部分信任  
 在部分信任环境下对 `ToolStrip` 进行限制，旨在防止无意中输入个人信息而被未经授权的人员或服务使用。  保护措施如下：  
  
-   `ToolStripDropDown` 控件需要 <xref:System.Security.Permissions.UIPermissionWindow> 才能显示 <xref:System.Windows.Forms.ToolStripControlHost> 中的项。  这适用于内部控件（例如 <xref:System.Windows.Forms.ToolStripTextBox>、<xref:System.Windows.Forms.ToolStripComboBox> 和 <xref:System.Windows.Forms.ToolStripProgressBar>）以及用户创建的控件。  如果没有达到此要求，这些项就不会显示。  不引发异常。  
  
-   不允许将 <xref:System.Windows.Forms.ToolStripDropDown.AutoClose%2A> 属性设置为 `false`，可取消的 <xref:System.Windows.Forms.ToolStripDropDown.Closing> 事件参数将被忽略。  这样，如果不关闭下拉项，就无法输入一个以上的键击。  如果没有达到此要求，此类项就不会显示。  不引发异常。  
  
-   许多键击处理事件如果是在部分信任的上下文中发生的，而非在 <xref:System.Security.Permissions.UIPermissionWindow> 中发生，就不会被引发。  
  
-   如果不授予 <xref:System.Security.Permissions.UIPermissionWindow>，将不处理访问键。  
  
#### 用法  
 以下使用模式与 <xref:System.Windows.Forms.ToolStrip> 布局、键盘交互和最终用户行为有关：  
  
-   联接在 <xref:System.Windows.Forms.ToolStripPanel> 中  
  
     可以在 <xref:System.Windows.Forms.ToolStripPanel> 内部和 <xref:System.Windows.Forms.ToolStripPanel> 之间重新定位 <xref:System.Windows.Forms.ToolStrip>。  `Dock` 属性将被忽略；如果 <xref:System.Windows.Forms.ToolStrip.Stretch%2A> 属性为 `false`，则在向 <xref:System.Windows.Forms.ToolStripPanel> 添加项时，<xref:System.Windows.Forms.ToolStrip> 的大小会随之增长。  通常，<xref:System.Windows.Forms.ToolStrip> 不按 Tab 键顺序参与。  
  
-   停靠  
  
     <xref:System.Windows.Forms.ToolStrip> 放置在容器一侧的固定位置，其大小扩展到它停靠到的整条边上。  通常，<xref:System.Windows.Forms.ToolStrip> 不按 Tab 键顺序参与。  
  
-   绝对定位  
  
     <xref:System.Windows.Forms.ToolStrip> 与其他控件的相同之处在于，它由 <xref:System.Windows.Forms.Control.Location%2A> 属性放置，具有固定大小，并且通常以 Tab 键顺序参与。  
  
#### 键盘交互  
  
##### 访问键  
 通过将访问键与 Alt 键组合使用或紧随 Alt 键使用，可利用键盘激活控件。  <xref:System.Windows.Forms.ToolStrip> 支持显式和隐式访问键。  显式定义在字母之前使用“and”符 \(&\)。  隐式定义使用的算法是：尝试根据给定 `Text` 属性中的字符顺序来查找匹配项。  
  
##### 快捷键  
 <xref:System.Windows.Forms.MenuStrip> 所用的快捷键使用 <xref:System.Windows.Forms.Keys> 枚举的组合（非特定于顺序）来定义快捷键。  也可以使用 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> 属性，仅以文本显示快捷键，例如显示“Del”而不是“Delete”。  
  
##### 导航  
 ALT 键激活 <xref:System.Windows.Forms.Form.MainMenuStrip%2A> 指向的 <xref:System.Windows.Forms.MenuStrip>。  然后，使用 Ctrl\+Tab 可在 `ToolStripPanel` 中的 <xref:System.Windows.Forms.ToolStrip> 控件之间导航。  使用 Tab 键和数字小键盘上的箭头键可在 <xref:System.Windows.Forms.ToolStrip> 中的各项之间导航。  特殊算法处理溢出区域中的导航。  空格键选择 <xref:System.Windows.Forms.ToolStripButton>、<xref:System.Windows.Forms.ToolStripDropDownButton> 或 <xref:System.Windows.Forms.ToolStripSplitButton>。  
  
##### 焦点和验证  
 当 <xref:System.Windows.Forms.MenuStrip> 或 <xref:System.Windows.Forms.ToolStrip> 被 ALT 键激活时，通常不会从当前具有焦点的控件中获取或移除焦点。  如果有寄宿在 <xref:System.Windows.Forms.MenuStrip> 中的某个控件或 <xref:System.Windows.Forms.MenuStrip> 的某个下拉控件，则用户按 Tab 键时该控件会获取焦点。  通常，键盘激活 <xref:System.Windows.Forms.MenuStrip> 的 <xref:System.Windows.Forms.Control.GotFocus>、<xref:System.Windows.Forms.Control.LostFocus>、<xref:System.Windows.Forms.Control.Enter> 和 <xref:System.Windows.Forms.Control.Leave> 事件时，可能不会引发这些事件。  在这种情况下，请改用 <xref:System.Windows.Forms.MenuStrip.MenuActivate> 和 <xref:System.Windows.Forms.MenuStrip.MenuDeactivate> 事件。  
  
 默认情况下，<xref:System.Windows.Forms.ToolStrip.CausesValidation%2A> 为 `false`。  在窗体上显式调用 <xref:System.Windows.Forms.ContainerControl.Validate%2A> 来执行验证。  
  
#### 布局  
 通过使用 <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A> 属性选择 <xref:System.Windows.Forms.ToolStripLayoutStyle> 的成员之一，从而控制 <xref:System.Windows.Forms.ToolStrip> 布局。  
  
##### 堆栈布局  
 堆栈是在 <xref:System.Windows.Forms.ToolStrip> 的两端并排排列项。  下面的列表描述堆栈布局。  
  
-   默认值为 <xref:System.Windows.Forms.ToolStripLayoutStyle>。  此设置导致 <xref:System.Windows.Forms.ToolStrip> 根据 <xref:System.Windows.Forms.ToolStrip.Orientation%2A> 属性自动改变其布局以处理拖动和停靠方案。  
  
-   <xref:System.Windows.Forms.ToolStripLayoutStyle> 垂直并排呈现 <xref:System.Windows.Forms.ToolStrip> 项。  
  
-   <xref:System.Windows.Forms.ToolStripLayoutStyle> 水平并排呈现 <xref:System.Windows.Forms.ToolStrip> 项。  
  
##### 堆栈布局的其他功能  
 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 确定该项与 <xref:System.Windows.Forms.ToolStrip> 的哪端对齐。  
  
 如果 <xref:System.Windows.Forms.ToolStrip> 中无法容纳项，则溢出按钮会自动出现。  项在溢出区域中的显示方式（始终显示、需要时显示或从不显示）由 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 属性的设置决定。  
  
 在 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 事件中，可检查 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 属性以确定项是位于主 <xref:System.Windows.Forms.ToolStrip> 上、溢出 <xref:System.Windows.Forms.ToolStrip> 上还是当前根本不显示。  项没有显示出来的通常原因是，主 <xref:System.Windows.Forms.ToolStrip> 中无法容纳该项，而且它的 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemOverflow>。  
  
 通过将 <xref:System.Windows.Forms.ToolStrip> 放入 <xref:System.Windows.Forms.ToolStripPanel> 中并将其 <xref:System.Windows.Forms.ToolStrip.GripStyle%2A> 设置为 <xref:System.Windows.Forms.ToolStripGripStyle> 可使其移动。  
  
##### 其他布局选项  
 其他布局选项是 <xref:System.Windows.Forms.ToolStripLayoutStyle> 和 <xref:System.Windows.Forms.ToolStripLayoutStyle>。  
  
##### 流布局  
 <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局是 <xref:System.Windows.Forms.ContextMenuStrip>、<xref:System.Windows.Forms.ToolStripDropDownMenu> 和 <xref:System.Windows.Forms.ToolStripOverflow> 的默认布局。  它类似于 <xref:System.Windows.Forms.FlowLayoutPanel>。  <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局的功能如下：  
  
-   <xref:System.Windows.Forms.FlowLayoutPanel> 的所有功能由 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A> 属性公开。  必须将 <xref:System.Windows.Forms.LayoutSettings> 类强制转换为 <xref:System.Windows.Forms.FlowLayoutSettings> 类。  
  
-   可在代码中使用 <xref:System.Windows.Forms.ToolStripItem.Dock%2A> 和 <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> 属性以对齐行中的项。  
  
-   将忽略 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 属性。  
  
-   在 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 事件中，可检查 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 属性以确定项是位于主 <xref:System.Windows.Forms.ToolStrip> 上还是无法容纳该项。  
  
-   不呈现手柄，因此无法移动 <xref:System.Windows.Forms.ToolStripPanel> 的 <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局样式中的 <xref:System.Windows.Forms.ToolStrip>。  
  
-   <xref:System.Windows.Forms.ToolStrip> 溢出按钮未呈现，且 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 被忽略。  
  
##### 表布局  
 <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局是 <xref:System.Windows.Forms.StatusStrip> 的默认布局。  它类似于 <xref:System.Windows.Forms.TableLayoutPanel>。  <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局的功能如下：  
  
-   <xref:System.Windows.Forms.TableLayoutPanel> 的所有功能由 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A> 属性公开。  必须将 <xref:System.Windows.Forms.LayoutSettings> 类强制转换为 <xref:System.Windows.Forms.TableLayoutSettings> 类。  
  
-   可在代码中使用 <xref:System.Windows.Forms.ToolStripItem.Dock%2A> 和 <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> 属性以对齐表单元格中的项。  
  
-   将忽略 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 属性。  
  
-   在 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 事件中，可检查 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 属性以确定项是位于主 <xref:System.Windows.Forms.ToolStrip> 上还是无法容纳该项。  
  
-   手柄未呈现，因此 <xref:System.Windows.Forms.ToolStripPanel> 中 <xref:System.Windows.Forms.ToolStripLayoutStyle> 布局样式的 <xref:System.Windows.Forms.ToolStrip> 不能移动。  
  
-   <xref:System.Windows.Forms.ToolStrip> 溢出按钮未呈现，且 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 被忽略。  
  
## ToolStripItem  
 下面的主题描述 <xref:System.Windows.Forms.ToolStripItem> 以及从中派生的控件。  
  
 <xref:System.Windows.Forms.ToolStripItem> 是进入 <xref:System.Windows.Forms.ToolStrip> 的所有项的抽象基类。  下面的对象模型演示了 <xref:System.Windows.Forms.ToolStripItem> 继承层次结构。  
  
 ![ToolStripItem 对象模型](../../../../docs/framework/winforms/controls/media/toolstripitemobjectmodel.png "ToolStripItemObjectModel")  
ToolStripItem 对象模型  
  
 <xref:System.Windows.Forms.ToolStripItem> 类直接从 <xref:System.Windows.Forms.ToolStripItem> 继承，或者通过 <xref:System.Windows.Forms.ToolStripControlHost> 或 <xref:System.Windows.Forms.ToolStripDropDownItem> 从 <xref:System.Windows.Forms.ToolStripItem> 间接继承。  
  
 <xref:System.Windows.Forms.ToolStripItem> 控件必须包含在 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip>、<xref:System.Windows.Forms.StatusStrip> 或 <xref:System.Windows.Forms.ContextMenuStrip> 中，而不能直接添加到窗体中。  各种容器类用于包含 <xref:System.Windows.Forms.ToolStripItem> 控件的相应子集。  
  
 下表列出常用的 <xref:System.Windows.Forms.ToolStripItem> 控件及相应的容器，所列控件在这些容器中的显示效果最好。  虽然任何 <xref:System.Windows.Forms.ToolStrip> 项都可以寄宿在任何 <xref:System.Windows.Forms.ToolStrip> 派生的容器中，但这些项在下列容器中的显示效果最好：  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStripDropDown> 不出现在设计器工具箱中。  
  
|包含的项|ToolStrip|MenuStrip|ContextMenuStrip|StatusStrip|ToolStripDropDown|  
|----------|---------------|---------------|----------------------|-----------------|-----------------------|  
|<xref:System.Windows.Forms.ToolStripButton>|是|否|否|否|是|  
|<xref:System.Windows.Forms.ToolStripComboBox>|是|是|是|否|是|  
|<xref:System.Windows.Forms.ToolStripSplitButton>|是|否|否|是|是|  
|<xref:System.Windows.Forms.ToolStripLabel>|是|否|否|是|是|  
|<xref:System.Windows.Forms.ToolStripSeparator>|是|是|是|否|是|  
|<xref:System.Windows.Forms.ToolStripDropDownButton>|是|否|否|是|是|  
|<xref:System.Windows.Forms.ToolStripTextBox>|是|是|是|否|是|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|否|是|是|否|否|  
|<xref:System.Windows.Forms.ToolStripStatusLabel>|否|否|否|是|否|  
|<xref:System.Windows.Forms.ToolStripProgressBar>|是|否|否|是|否|  
|<xref:System.Windows.Forms.ToolStripControlHost>|是|是|否|是|是|  
  
### ToolStripButton  
 <xref:System.Windows.Forms.ToolStripButton> 是 <xref:System.Windows.Forms.ToolStrip> 的按钮项。  可以用不同的边框样式显示该项，并可将它用于表示和激活操作状态。  还可以将其定义为默认具有焦点。  
  
### ToolStripLabel  
 <xref:System.Windows.Forms.ToolStripLabel> 在 <xref:System.Windows.Forms.ToolStrip> 控件中提供标签功能。  <xref:System.Windows.Forms.ToolStripLabel> 与 <xref:System.Windows.Forms.ToolStripButton> 一样，默认不获得焦点，而且不呈现为下压或突出显示。  
  
 <xref:System.Windows.Forms.ToolStripLabel> 作为被承载项支持访问键。  
  
 使用 <xref:System.Windows.Forms.ToolStripLabel> 上的 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>、<xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 和 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> 属性来支持 <xref:System.Windows.Forms.ToolStrip> 中的链接控件。  
  
### ToolStripStatusLabel  
 <xref:System.Windows.Forms.ToolStripStatusLabel> 是专为在 <xref:System.Windows.Forms.StatusStrip> 中使用而设计的 <xref:System.Windows.Forms.ToolStripLabel> 版本。  特殊功能包括 <xref:System.Windows.Forms.ToolStripStatusLabel.BorderStyle%2A>、<xref:System.Windows.Forms.ToolStripStatusLabel.BorderSides%2A> 和 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>。  
  
### ToolStripSeparator  
 <xref:System.Windows.Forms.ToolStripSeparator> 根据方向将垂直线和水平线添加到工具栏和菜单中。  它提供项的分组以及项之间的区分（例如菜单上的那些项）。  
  
 可以通过从下拉列表中进行选择，在设计时添加 <xref:System.Windows.Forms.ToolStripSeparator>。  然而，也可以通过在设计器模板节点或 <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> 方法中键入连字符 \(\-\)，自动创建 <xref:System.Windows.Forms.ToolStripSeparator>。  
  
### ToolStripControlHost  
 <xref:System.Windows.Forms.ToolStripControlHost> 是 <xref:System.Windows.Forms.ToolStripComboBox>、<xref:System.Windows.Forms.ToolStripTextBox> 和 <xref:System.Windows.Forms.ToolStripProgressBar> 的抽象基类。  <xref:System.Windows.Forms.ToolStripControlHost> 可以通过两种方法承载其他控件（包括自定义控件）：  
  
-   从派生自 <xref:System.Windows.Forms.Control> 的类构造 <xref:System.Windows.Forms.ToolStripControlHost>。  要完全访问寄宿的控件和属性，必须将 <xref:System.Windows.Forms.ToolStripControlHost.Control%2A> 属性强制转换回它所表示的实际类。  
  
-   扩展 <xref:System.Windows.Forms.ToolStripControlHost>，并在继承类的默认构造函数中，调用基类构造函数并传递一个从 <xref:System.Windows.Forms.Control> 派生的类。  此选项允许您对公共控件方法和属性进行包装，以使 <xref:System.Windows.Forms.ToolStrip> 中的访问更加容易。  
  
### ToolStripComboBox  
 <xref:System.Windows.Forms.ToolStripComboBox> 是为在 <xref:System.Windows.Forms.ToolStrip> 中进行承载而优化的 <xref:System.Windows.Forms.ComboBox>。  被承载控件的属性和事件的子集在 <xref:System.Windows.Forms.ToolStripComboBox> 级上公开，但是基础 <xref:System.Windows.Forms.ComboBox> 控件可通过 <xref:System.Windows.Forms.ToolStripComboBox.ComboBox%2A> 属性进行完全访问。  
  
### ToolStripTextBox  
 <xref:System.Windows.Forms.ToolStripTextBox> 是为在 <xref:System.Windows.Forms.ToolStrip> 中进行承载而优化的 <xref:System.Windows.Forms.TextBox>。  被承载控件的属性和事件的子集在 <xref:System.Windows.Forms.ToolStripTextBox> 级上公开，但是基础 <xref:System.Windows.Forms.TextBox> 控件可通过 <xref:System.Windows.Forms.ToolStripTextBox.TextBox%2A> 属性进行完全访问。  
  
### ToolStripProgressBar  
 <xref:System.Windows.Forms.ToolStripProgressBar> 是为在 <xref:System.Windows.Forms.ToolStrip> 中进行承载而优化的 <xref:System.Windows.Forms.ProgressBar>。  被承载控件的属性和事件的子集在 <xref:System.Windows.Forms.ToolStripProgressBar> 级上公开，但是基础 <xref:System.Windows.Forms.ProgressBar> 控件可通过 <xref:System.Windows.Forms.ToolStripProgressBar.ProgressBar%2A> 属性进行完全访问。  
  
### ToolStripDropDownItem  
 <xref:System.Windows.Forms.ToolStripDropDownItem> 是 <xref:System.Windows.Forms.ToolStripMenuItem>、<xref:System.Windows.Forms.ToolStripDropDownButton> 和 <xref:System.Windows.Forms.ToolStripSplitButton> 的抽象基类，可直接承载项或者在下拉容器中承载附加项。  可以通过将 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDown%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripDropDown> 以及设置 <xref:System.Windows.Forms.ToolStripDropDown> 的 <xref:System.Windows.Forms.ToolStrip.Items%2A> 属性来执行此操作。  通过 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A> 属性直接访问这些下拉项。  
  
### ToolStripMenuItem  
 <xref:System.Windows.Forms.ToolStripMenuItem> 是与 <xref:System.Windows.Forms.ToolStripDropDownMenu> 和 <xref:System.Windows.Forms.ContextMenuStrip> 一起使用的 <xref:System.Windows.Forms.ToolStripDropDownItem>，用于处理菜单的特殊突出显示、布局以及列排列。  
  
### ToolStripDropDownButton  
 <xref:System.Windows.Forms.ToolStripDropDownButton> 看起来类似于 <xref:System.Windows.Forms.ToolStripButton>，但在用户单击它时，它会显示一个下拉区域。  通过设置 <xref:System.Windows.Forms.ToolStripDropDownButton.ShowDropDownArrow%2A> 属性可以隐藏或显示下拉箭头。  <xref:System.Windows.Forms.ToolStripDropDownButton> 承载用于显示溢出 <xref:System.Windows.Forms.ToolStrip> 的项的 <xref:System.Windows.Forms.ToolStripOverflowButton>。  
  
### ToolStripSplitButton  
 <xref:System.Windows.Forms.ToolStripSplitButton> 结合了按钮和下拉按钮功能。  
  
 使用 <xref:System.Windows.Forms.ToolStripSplitButton.DefaultItem%2A> 属性，将所选下拉项的 <xref:System.Windows.Forms.Control.Click> 事件与按钮上显示的项同步。  
  
### ToolStripItem 一般功能  
 <xref:System.Windows.Forms.ToolStripItem> 向进行继承的控件提供下列一般功能和选项：  
  
-   核心事件  
  
-   图像处理  
  
-   对齐方式  
  
-   文本和图像关系  
  
-   显示样式  
  
#### 核心事件  
 <xref:System.Windows.Forms.ToolStripItem> 控件接收自己的单击、鼠标和绘制事件，还可以执行某些键盘预处理。  
  
#### 图像处理  
 <xref:System.Windows.Forms.ToolStripItem.Image%2A>、<xref:System.Windows.Forms.ToolStripItem.ImageAlign%2A>、<xref:System.Windows.Forms.ToolStripItem.ImageIndex%2A>、<xref:System.Windows.Forms.ToolStripItem.ImageKey%2A> 和 <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> 属性适用于图像处理的多个方面。  可通过直接设置这些属性或者通过设置仅运行时有效的 <xref:System.Windows.Forms.ToolStrip.ImageList%2A> 属性，在 <xref:System.Windows.Forms.ToolStrip> 控件中使用图像。  
  
 图像缩放由 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.ToolStripItem> 中的属性交互来决定，如下所述：  
  
-   <xref:System.Windows.Forms.ToolStrip.ImageScalingSize%2A> 是最终图像的比例，由图像的 <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> 设置和容器的 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 设置共同决定。  
  
    -   如果 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 为 `true`（默认）且 <xref:System.Windows.Forms.ToolStripItemImageScaling> 为 <xref:System.Windows.Forms.ToolStripItemImageScaling>，则不会发生图像缩放，而且 <xref:System.Windows.Forms.ToolStrip> 尺寸是最大项的尺寸或规定的最小尺寸。  
  
    -   如果 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 为 `false` 且 <xref:System.Windows.Forms.ToolStripItemImageScaling> 为 <xref:System.Windows.Forms.ToolStripItemImageScaling>，则不会发生图像或 <xref:System.Windows.Forms.ToolStrip> 缩放。  
  
#### 对齐方式  
 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 属性的值决定了将显示项的 <xref:System.Windows.Forms.ToolStrip> 的末尾。  <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 属性仅在 <xref:System.Windows.Forms.ToolStrip> 的布局样式设置为堆栈溢出值之一时才起作用。  
  
 项在 <xref:System.Windows.Forms.ToolStrip> 上的放置顺序就是项在项集合中的显示顺序。  要以编程方式更改项的布局位置，请使用 <xref:System.Windows.Forms.ToolStripItemCollection.Insert%2A> 方法移动集合中的项。  此方法移动项，但不进行复制。  
  
#### 文本和图像关系  
 <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A> 属性根据 <xref:System.Windows.Forms.ToolStripItem> 上的文本定义图像的相对位置。  缺少图像、文本或两者都缺少的项将被视为特殊情况，因此 <xref:System.Windows.Forms.ToolStripItem> 不会为缺少的元素显示空白点。  
  
#### 显示样式  
 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 允许设置项的 Text 和 Image 属性的值，同时只显示需要的内容。  这通常用于当在不同的上下文中显示相同的项时，仅更改显示样式。  
  
## 附属类  
 提供各种其他功能的类包括：  
  
-   <xref:System.Windows.Forms.ToolStripManager> 支持整个应用程序的 <xref:System.Windows.Forms.ToolStrip> 相关任务，例如合并、设置和呈现程序选项。  
  
-   <xref:System.Windows.Forms.ToolStripRenderer> 允许将特定样式或主题轻松应用到 <xref:System.Windows.Forms.ToolStrip>。  
  
-   <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 根据可替换颜色表 \(<xref:System.Windows.Forms.ProfessionalColorTable>\) 创建钢笔和画笔。  
  
-   <xref:System.Windows.Forms.ToolStripSystemRenderer> 将系统颜色和平面视觉样式应用到 <xref:System.Windows.Forms.ToolStrip> 应用程序。  
  
-   <xref:System.Windows.Forms.ToolStripContainer> 类似于 <xref:System.Windows.Forms.SplitContainer>。  它使用四个停靠侧面板（<xref:System.Windows.Forms.ToolStripPanel> 的实例）和一个中间面板（<xref:System.Windows.Forms.ToolStripContentPanel> 的实例）来创建典型排列。  侧面板无法移除，但可以隐藏。  中间面板既不能删除，也不能隐藏。  可以在侧面板中排列一个或多个 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip> 或 <xref:System.Windows.Forms.StatusStrip> 控件，并且可以将中间面板用于其他控件。  <xref:System.Windows.Forms.ToolStripContentPanel> 还提供一种方法，能够在窗体的主体中支持呈现程序以获得一致的外观。  <xref:System.Windows.Forms.ToolStripContainer> 不支持多文档界面 \(MDI\)。  
  
-   <xref:System.Windows.Forms.ToolStripPanel> 为移动和排列 <xref:System.Windows.Forms.ToolStrip> 控件提供了空间。  可以只使用一块面板（如果这样选择的话），而且 <xref:System.Windows.Forms.ToolStripPanel> 很适合 MDI 方案。  
  
## 请参阅  
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)   
 [ToolStrip 控件](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)   
 [MenuStrip 控件](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [StatusStrip 控件](../../../../docs/framework/winforms/controls/statusstrip-control.md)   
 [ContextMenuStrip 控件](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)   
 [BindingNavigator 控件](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)