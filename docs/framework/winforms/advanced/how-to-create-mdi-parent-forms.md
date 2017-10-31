---
title: "如何：创建 MDI 父窗体 | Microsoft Docs"
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
  - "MDI, 创建窗体"
  - "父窗体"
ms.assetid: 12c71221-2377-4bb6-b10b-7b4b300fd462
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：创建 MDI 父窗体
> [!IMPORTANT]
>  该话题使用 <xref:System.Windows.Forms.MainMenu> 控制（已由 <xref:System.Windows.Forms.MenuStrip> 控制取代）。  如果你选择的话，就会保留 <xref:System.Windows.Forms.MainMenu> 控制以便实现后向兼容性和未来使用。  有关使用 <xref:System.Windows.Forms.MenuStrip> 创建 MDI 父窗体的信息，请参阅[如何：使用 MenuStrip 创建 MDI 窗口列表](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)。  
  
 多文档界面 \(MDI\) 应用程序的基础为 MDI 父窗体。  这是包含 MDI 子窗口（用户与 MDI 应用程序交流所在的子窗口）的窗口。  在“Windows 窗体设计器”中采用编程方式可轻松创建一个 MDI 父窗体。  
  
### 要在设计时创建 MDI 父窗体  
  
1.  创建一个 Windows 应用程序项目。  
  
2.  在“属性”窗口中，将 [IsMDIContainer](frlrfSystemWindowsFormsFormClassIsMDIContainerTopic) 属性设为“true”。  
  
     这将该表单指定为适合子窗口的 MDI 容器。  
  
    > [!NOTE]
    >  在“属性”窗口中设置属性时，如果你喜欢的话，也可以将 `WindowState` 属性设置为“最大化”，因为父窗体最大化时最容易操作 MDI 子窗口。  此外，注意 MDI 父窗体的边缘将获得系统颜色（在 Windows“系统控制面板”中进行设置），而非你使用 <xref:System.Windows.Forms.Control.BackColor%2A?displayProperty=fullName> 属性设置的背景颜色。  
  
3.  从“工具箱”中，将“菜单条”控件拖到表格。  创建一个顶级菜单项，将“文本”属性设置为包含子菜单项名为“&New”和“&Close”的“&File”。  并创建一个名为“&Window”的顶级菜单项。  
  
     第一个菜单将在运行时创建并隐藏菜单项，第二个菜单将跟踪打开的 MDI 子窗口。  这时，你已经创建了一个 MDI 父窗口。  
  
4.  按**“F5”**运行应用程序。  有关创建在 MDI 父窗体内运行的 MDI 子窗口的信息，请参阅 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)。  
  
## 请参阅  
 [多文档界面 \(MDI\) 应用程序](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [如何：确定活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)   
 [如何：将数据发送到活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)   
 [如何：排列 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)