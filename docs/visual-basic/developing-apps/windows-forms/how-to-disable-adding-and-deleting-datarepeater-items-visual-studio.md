---
title: "如何：禁止添加和删除 DataRepeater 项 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 禁用添加"
  - "DataRepeater, 禁用删除"
ms.assetid: 298d8f60-ddfe-4361-ab66-cf76d0df5220
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 如何：禁止添加和删除 DataRepeater 项 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

默认情况下，用户可以在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中添加和删除项。  用户可以在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItemEventArgs.DataRepeaterItem%2A> 具有焦点时通过按 Ctrl\+N 来添加新项，或通过单击 <xref:System.Windows.Forms.BindingNavigator> 控件上的**“添加新项”**按钮来添加新项。  用户可以在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItemEventArgs.DataRepeaterItem%2A> 具有焦点时通过按 Delete 来删除项，或通过单击 <xref:System.Windows.Forms.BindingNavigator> 控件上的**“删除项”**按钮来删除项。  
  
 您可以在设计时或运行时禁止添加和\/或删除项。  
  
### 禁止在设计时添加和删除项  
  
1.  在 Windows 窗体设计器中，选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  
  
    > [!NOTE]
    >  必须选择控件的下半部分。  如果选择项模板部分，将显示一组不同的属性。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.AllowUserToAddItems%2A> 属性设置为**“False”**。  
  
3.  将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.AllowUserToDeleteItems%2A> 属性设置为**“False”**。  
  
4.  在 Windows 窗体设计器中选择 <xref:System.Windows.Forms.BindingNavigator> 控件，然后单击**“添加新项”**按钮（该按钮上有一个加号）。  
  
5.  在“属性”窗口中，将 <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> 属性设置为**“False”**。  
  
6.  在 Windows 窗体设计器中选择 <xref:System.Windows.Forms.BindingNavigator> 控件，然后单击**“删除项”**按钮（该按钮上有一个红色的 X）。  
  
7.  在“属性”窗口中，将 <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> 属性设置为**“False”**。  
  
8.  在组件栏中选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 将要绑定到的 <xref:System.Windows.Forms.BindingSource>。  
  
9. 在“属性”窗口中，将 <xref:System.Windows.Forms.BindingSource.AllowNew%2A> 属性设置为**“False”**。  
  
10. 在 Windows 窗体设计器中双击**“删除项”**按钮打开代码编辑器。  
  
11. 在“事件”下拉列表中选择 `BindingNavigatorDeleteItem_EnabledChanged` 事件。  
  
12. 将以下代码添加到 `BindingNavigatorDeleteItem_EnabledChanged` 事件处理程序中：  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_1.vb)]  
  
    > [!NOTE]
    >  此步骤是必需的，因为每当当前记录发生更改时，<xref:System.Windows.Forms.BindingSource> 都将启用**“删除项”**按钮。  
  
### 禁止在运行时添加和删除项  
  
1.  在 Windows 窗体设计器中双击窗体打开代码编辑器。  
  
2.  将下面的代码添加到 `Form_Load` 事件中：  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_2.cs)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_2.vb)]  
  
3.  将以下代码添加到 `BindingNavigatorDeleteItem_EnabledChanged` 事件处理程序中：  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio_1.vb)]  
  
    > [!NOTE]
    >  此步骤是必需的，因为每当当前记录发生更改时，<xref:System.Windows.Forms.BindingSource> 都将启用**“删除项”**按钮。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)