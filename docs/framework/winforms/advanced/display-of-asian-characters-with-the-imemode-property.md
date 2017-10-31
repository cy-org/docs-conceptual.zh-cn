---
title: "通过 ImeMode 属性显示亚洲字符 | Microsoft Docs"
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
  - "亚洲语言"
  - "亚洲语言, 使用 ImeMode 显示"
  - "中文字符, 使用 ImeMode 显示"
  - "全球化 [Windows 窗体], 字符集"
  - "IME "
  - "IMEMode 属性"
  - "输入法编辑器 (IME), mode"
  - "国际应用程序 [Windows 窗体], 字符显示"
  - "国际字符"
  - "日语字符, 使用 ImeMode 显示"
  - "朝鲜语字符"
  - "本地化 [Windows 窗体], 字符集"
ms.assetid: c60ae399-0dab-4f07-9dea-6dbfb15ec0ae
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 通过 ImeMode 属性显示亚洲字符
窗体和控件可以使用 <xref:System.Windows.Forms.Control.ImeMode%2A> 属性来强制对输入法编辑器 \(IME\) 使用特定模式。  IME 是编写中文、日文和朝鲜语脚本的基本组件，因为这些编写系统所具有的字符多于可以为常规键盘编码的字符。  例如，您可能想要在特定文本框中只允许 ASCII 字符。  在这种情况下，可以将 <xref:System.Windows.Forms.Control.ImeMode%2A> 属性设置为 <xref:System.Windows.Forms.ImeMode>，这样，用户将只能在该特定文本框中输入 ASCII 字符。  <xref:System.Windows.Forms.Control.ImeMode%2A> 属性的默认值是 <xref:System.Windows.Forms.ImeMode>，因此，如果您设置窗体的属性，窗体中的所有控件都将继承该设置。  有关更多信息，请参见 [Control.ImeMode 属性](frlrfSystemWindowsFormsControlClassImeModeTopic)和 [ImeMode 枚举](frlrfSystemWindowsFormsImeModeClassTopic)。  
  
## 请参阅  
 [全球化 Windows 窗体](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)