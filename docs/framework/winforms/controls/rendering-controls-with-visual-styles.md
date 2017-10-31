---
title: "使用视觉样式呈现控件 | Microsoft Docs"
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
  - "专业的外观, 呈现 Windows 窗体控件"
  - "主题, Window 窗体中的 XP 视觉样式"
  - "自定义控件 [Windows 窗体], 呈现"
  - "自定义控件 [Windows 窗体], 绘画"
  - "视觉主题, 呈现 Windows 窗体控件"
  - "用户控件 [Windows 窗体], 绘画"
  - "视觉式样, 呈现 Windows 窗体控件"
ms.assetid: a5b178ba-610e-46c4-a6c0-509c0886a744
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 使用视觉样式呈现控件
[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 使用操作系统中受支持的视觉样式为呈现控件和其他 Windows 用户界面 \(UI\) 元素提供支持。 本主题讨论 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中对使用操作系统当前视觉样式的呈现控件和其他 UI 元素提供的多种级别的支持。  
  
## 公共控件的呈现类  
 呈现控件是指绘制控件的用户界面。<xref:System.Windows.Forms?displayProperty=fullName> 命名空间提供了用来呈现某些公共 Windows 窗体控件的 <xref:System.Windows.Forms.ControlPaint> 类。 但是，此类以经典 Windows 样式绘制的控件，当在启用了视觉样式的应用程序中绘制自定义控件时，难以维护 UI 体验的一致性。  
  
 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 包括 <xref:System.Windows.Forms?displayProperty=fullName> 命名空间中使用视觉样式呈现部件和公共控件状态的类。 每个这样的类都包括使用操作系统当前视觉样式绘制控件和特定状态控件部件的 `static` 方法。  
  
 其中一些类旨在绘制相关控件，而不考虑视觉样式是否可用。 如果启用了视觉样式，类成员将使用视觉样式绘制相关控件；如果禁用了视觉样式，类成员将以经典 Windows 样式绘制控件。 这些类包括：  
  
-   <xref:System.Windows.Forms.ButtonRenderer>  
  
-   <xref:System.Windows.Forms.CheckBoxRenderer>  
  
-   <xref:System.Windows.Forms.GroupBoxRenderer>  
  
-   <xref:System.Windows.Forms.RadioButtonRenderer>  
  
 视觉样式可用时，其他类才能绘制相关控件，如果禁用了视觉样式，则类成员会引发异常。 这些类包括：  
  
-   <xref:System.Windows.Forms.ComboBoxRenderer>  
  
-   <xref:System.Windows.Forms.ProgressBarRenderer>  
  
-   <xref:System.Windows.Forms.ScrollBarRenderer>  
  
-   <xref:System.Windows.Forms.TabRenderer>  
  
-   <xref:System.Windows.Forms.TextBoxRenderer>  
  
-   <xref:System.Windows.Forms.TrackBarRenderer>  
  
 有关使用这些类绘制控件的详细信息，请参阅 [如何：使用控件呈现类](../../../../docs/framework/winforms/controls/how-to-use-a-control-rendering-class.md)。  
  
## 视觉样式元素和呈现类  
 <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间包含用于绘制和获取视觉样式支持的任何控件或 UI 元素信息的类。 支持的控件包括在 <xref:System.Windows.Forms?displayProperty=fullName> 命名空间中具有呈现类的公共控件（请参阅上一节）以及诸如选项卡控件和 rebar 控件的其他控件。 其他受支持的 UI 元素包括“开始”菜单、任务栏和 Windows 非工作区的各部分。  
  
 <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间的主要类为 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 和 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>。<xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 是一个基础类，用于标识视觉样式支持的任何控件或用户界面元素。 除了 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 本身，<xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间包含许多 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 嵌套类，这些类具有为视觉样式支持的控件、控件部件或其他 UI 元素的状态返回 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 的 `static` 属性。  
  
 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 提供一些方法，这些方法可以绘制和获取由操作系统当前视觉样式定义的每个 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 的信息。 可以检索的元素信息包括其默认大小、背景类型和颜色定义。<xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 包装来自 Windows Platform SDK 的 Windows Shell 部分的视觉样式 \(UxTheme\) API 的功能。 有关详细信息，请参阅位于 [http:\/\/msdn.microsoft.com\/library](http://msdn.microsoft.com/library/) 上的 MSDN Library 的 Platform SDK 部分中的“使用 Windows XP 视觉样式”。  
  
 有关使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 和 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 的详细信息，请参阅 [如何：呈现视觉样式元素](../../../../docs/framework/winforms/controls/how-to-render-a-visual-style-element.md)。  
  
## 启用视觉样式  
 若要为针对 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 版本 1.0 编写的应用程序启用视觉样式，程序员必须将应用清单包含进来。该清单指定使用 ComCtl32.dll 版本 6 或更高版本绘制控件。 使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 版本 1.1 或更高版本生成的应用可以使用 <xref:System.Windows.Forms.Application> 类的 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法。  
  
## 检查视觉样式支持  
 <xref:System.Windows.Forms.Application> 类的 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 属性指示当前应用程序是否正在使用视觉样式绘制控件。 绘制自定义控件时，可以检查 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 的值来确定是否应使用视觉样式呈现控件。 下表列出了 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 返回 `true` 必须存在的四个条件。  
  
|条件|备注|  
|--------|--------|  
|操作系统支持视觉样式。|若要单独验证这种情况，请使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> 类的 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsSupportedByOS%2A> 属性。|  
|用户已在操作系统中启用视觉样式。|若要单独验证这种情况，请使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> 类的 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsEnabledByUser%2A> 属性。|  
|应用程序中已启用视觉样式。|可以通过调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法或使用指定用 ComCtl32.dll 版本 6 或更高版本绘制控件的应用程序清单来启用应用程序中的视觉样式。|  
|正在使用视觉样式来绘制应用程序窗口的工作区。|若要单独验证这种情况，请使用 <xref:System.Windows.Forms.Application> 类的 <xref:System.Windows.Forms.Application.VisualStyleState%2A> 属性，验证它是否具有 <xref:System.Windows.Forms.VisualStyles.VisualStyleState?displayProperty=fullName> 或 <xref:System.Windows.Forms.VisualStyles.VisualStyleState?displayProperty=fullName> 值。|  
  
 若要确定用户何时启用或禁用视觉样式，或何时从一种视觉样式切换到另种，请检查 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging?displayProperty=fullName> 或 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged?displayProperty=fullName> 事件处理程序中的 <xref:Microsoft.Win32.UserPreferenceCategory?displayProperty=fullName> 值。  
  
> [!IMPORTANT]
>  如果想要在用户启用或切换视觉样式时使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 来呈现控件或 UI 元素，请确保在处理 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 事件而非 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging> 事件时这样做。 处理 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging> 时如果使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 类，则会引发异常。  
  
## 请参阅  
 [自定义控件的绘制和呈现](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md)