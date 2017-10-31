---
title: "演练：设计时在 Windows 窗体上排列 WPF 内容 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "互操作性 [WPF]"
  - "Windows 窗体, 锚定和停靠 WPF 内容"
  - "Windows 窗体, 在设计时排列 WPF 内容"
  - "WPF 内容 [Windows 窗体], 在设计时排列"
  - "WPF 内容, 在 Windows 窗体中承载"
  - "WPF 用户控件 [Windows 窗体], 在布局面板中承载"
ms.assetid: 5efb1c53-1484-43d6-aa8a-f4861b99bb8a
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 演练：设计时在 Windows 窗体上排列 WPF 内容
本演练演示如何使用 Windows 窗体布局功能（例如锚定和对齐线）排列 Windows Presentation Foundation \(WPF\) 控件。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   创建 WPF 控件。  
  
-   在布局面板中承载 WPF 控件。  
  
-   使用对齐线对齐 WPF 控件。  
  
-   锚定和停靠 WPF 控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)]。  
  
## 创建项目  
 第一步是创建 Windows 窗体项目。  
  
> [!NOTE]
>  承载 WPF 内容时，仅支持 C\# 和 Visual Basic 项目。  
  
#### 创建项目  
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `CopyElementHost` 的新 Windows 窗体应用程序项目。  
  
## 创建 WPF 控件  
 将 WPF 控件添加到项目后，就可以在窗体上对其进行排列。  
  
#### 创建 WPF 控件  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 添加到项目。  使用控件类型的默认名称，`UserControl1.xaml`。  有关详细信息，请参阅[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在设计视图中，请确保已选中 `UserControl1`。  有关详细信息，请参阅[如何：在设计图面上选择和移动元素](http://msdn.microsoft.com/zh-cn/54cb70b6-b35b-46e4-a0cc-65189399c474)。  
  
3.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
4.  将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为`蓝色`。  
  
5.  生成项目。  
  
## 在布局面板中承载 WPF 控件  
 在布局面板中使用 WPF 控件与使用其他 Windows 窗体控件的方式可以相同。  
  
#### 若要在布局面板中承载 WPF 控件  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在“工具箱”中，将 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
3.  在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的智能标记面板上，选择“移除最后一行”。  
  
4.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为更大的宽度和高度。  
  
5.  在“工具箱”中，双击`UserControl1` 在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的第一个单元格中创建 `UserControl1` 的实例。  
  
     `UserControl1` 的实例承载在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
6.  在“工具箱”中，双击`UserControl1` 在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的第二个单元格中创建另一个实例。  
  
7.  在“文档大纲”窗口中，选择 `tableLayoutPanel1`。  有关信息信息，请参阅[Document Outline Window](http://msdn.microsoft.com/zh-cn/9054f2bc-f6f8-4242-9fe0-be71089b12f8)。  
  
8.  在“属性”窗口中，将 <xref:System.Windows.Forms.Control.Padding%2A> 属性的值设置为 `10、10、10、10`。  
  
     调整两个 <xref:System.Windows.Forms.Integration.ElementHost> 控件的大小以适应新的布局。  
  
## 使用对齐线对齐 WPF 控件  
 使用对齐线能够轻松对齐窗体上的控件。  还可以使用对齐线对齐 WPF 控件。  有关详细信息，请参阅[演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)。  
  
#### 若要使用对齐线对齐 WPF 控件  
  
1.  从“工具箱”中，将 `UserControl1` 的实例拖到窗体上，并将其放在 <xref:System.Windows.Forms.TableLayoutPanel> 控件下的空间中。  
  
     `UserControl1` 的实例承载在名为 `elementHost3` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
2.  使用对齐线，将 `elementHost3` 的左边缘与 <xref:System.Windows.Forms.TableLayoutPanel> 控件的左边缘对齐。  
  
3.  使用对齐线，将 `elementHost3` 按与 <xref:System.Windows.Forms.TableLayoutPanel> 控件相同的宽度排列。  
  
4.  朝着 <xref:System.Windows.Forms.TableLayoutPanel> 控件移动 `elementHost3`，直到控件间显示居中对齐线。  
  
5.  在“属性”窗口中，将 Margin 属性的值设置为 `20、20、20、20`。  
  
6.  向远离 <xref:System.Windows.Forms.TableLayoutPanel> 控件的方向移动 `elementHost3`，直到再次显示居中对齐线。  现在，居中对齐线指示边距为 20。  
  
7.  向右移动 `elementHost3`，直到其左边缘与 `elementHost1` 的左边缘对齐。  
  
8.  更改 `elementHost3` 的宽度，直到其右边缘与 `elementHost2` 的右边缘对齐。  
  
## 锚定和停靠 WPF 控件  
 窗体上承载的 WPF 控件具有与其他 Windows 窗体控件相同的锚定和停靠行为。  
  
#### 若要锚定和停靠 WPF 控件  
  
1.  选择 `elementHost1`。  
  
2.  在“属性”窗口中，将<xref:System.Windows.Forms.Control.Anchor%2A> 属性的值设置为“上、下、左、右”。  
  
3.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为更大。  
  
     调整 `elementHost1` 控件大小，以填充单元格。  
  
4.  选择 `elementHost2`。  
  
5.  在**属性**窗口中，将 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle>。  
  
     调整 `elementHost2` 控件大小，以填充单元格。  
  
6.  选择 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
7.  将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle>。  
  
8.  选择 `elementHost3`。  
  
9. 将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle>。  
  
     调整 `elementHost3` 控件大小，以填充窗体上的剩余空间。  
  
10. 调整窗体大小。  
  
     所有三个 <xref:System.Windows.Forms.Integration.ElementHost> 控件将相应地调整大小。  
  
     有关详细信息，请参阅[如何：在 TableLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [如何：在 TableLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [如何：设计时将控件与窗体边缘对齐](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)