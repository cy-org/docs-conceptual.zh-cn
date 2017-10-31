---
title: "如何：设置输入掩码 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "net.ComponentModel.MaskPropertyEditor"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "MaskedTextBox 控件 [Windows 窗体]"
ms.assetid: 779b3a12-cd74-4e58-b46e-04983bda5b2c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：设置输入掩码
掩码文本框控件是一个增强型的文本框控件，它支持用于接受或拒绝用户输入的声明性语法。  通过设置 Mask 属性，无需在应用程序中编写任何自定义验证逻辑，即可指定允许的用户输入。  有关更多信息，请参见 <xref:System.Windows.Forms.MaskedTextBox> 类的“备注”节。  
  
## 手动设置 Mask 属性  
 如果您熟悉 Mask 属性支持的字符，则可手动输入它。  有关 Mask 属性支持的字符的摘要，请参见 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 属性的“备注”节。  
  
#### 手动设置 Mask 属性  
  
1.  在**“设计”**视图中，选择 <xref:System.Windows.Forms.MaskedTextBox>。  
  
2.  在**“属性”**窗口中，找到 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 属性。  
  
3.  键入所需掩码。  例如，键入 `###`。  
  
## 使用“输入掩码”对话框  
 “输入掩码”对话框提供了一些预定义的输入掩码。  也可以更改预定义的掩码或手动输入自己的掩码。  
  
#### 打开“输入掩码”对话框  
  
1.  在**“设计”**视图中，选择 <xref:System.Windows.Forms.MaskedTextBox>。  
  
    1.  单击智能标记以打开**“MaskedTextBox 任务”**面板。  
  
    2.  单击**“设置掩码”**。  
  
     \- 或 \-  
  
    1.  在**“属性”**窗口中，选择 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 属性。  
  
    2.  在属性值列中，单击省略号按钮。  
  
     将出现**“输入掩码”**对话框。  
  
#### 使用“输入掩码”对话框  
  
1.  （可选）在列表中单击预定义掩码之一。  
  
2.  （可选）在**“掩码”**框中编辑预定义掩码。  
  
3.  （可选）在**“掩码”**框中键入新掩码。  也就是说，您无需使用预定义掩码之一。  
  
    > [!NOTE]
    >  “预览”框中将显示用户在 <xref:System.Windows.Forms.MaskedTextBox> 中看到的字符。  这些字符是帮助用户正确输入数据的指南。  
  
4.  选中或清除**“使用 ValidatingType”**复选框。  **“使用 ValidatingType”**复选框指定是否使用数据类型来验证用户的数据输入。  有关更多信息，请参见 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 属性。  
  
5.  单击**“确定”**。  
  
     在**“属性”**窗口的**“掩码”**属性中输入掩码。  
  
## 请参阅  
 [演练：使用 MaskedTextBox 控件](../../../../docs/framework/winforms/controls/walkthrough-working-with-the-maskedtextbox-control.md)