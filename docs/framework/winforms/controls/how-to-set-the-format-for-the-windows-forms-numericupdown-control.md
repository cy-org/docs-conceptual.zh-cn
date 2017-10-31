---
title: "如何：设置 Windows 窗体 NumericUpDown 控件的格式 | Microsoft Docs"
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
  - "NumericUpDown 控件 [Windows 窗体], 格式化值"
  - "up-down 控件, 格式化数值"
ms.assetid: fa7c5557-6bfb-45b2-975d-8887b23b0ba0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：设置 Windows 窗体 NumericUpDown 控件的格式
可以配置值在 Windows 窗体 <xref:System.Windows.Forms.NumericUpDown> 控件中显示的方式。  <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> 属性确定在小数点后显示几位数字，默认值为 0。  <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> 属性确定是否每隔 3 个十进制数字就插入一个分隔符，默认情况下为 `false`。  如果将 <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> 属性设置为 `true`，则该控件可以用十六进制（而不是十进制格式）显示值；默认情况下为 `false`。  
  
### 格式化数值  
  
-   通过将 <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> 属性设置为一个整数，并将 <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> 属性设置为 `true` 或 `false`，显示十进制数值。  
  
    ```vb  
    NumericUpDown1.DecimalPlaces = 2  
    NumericUpDown1.ThousandsSeparator = True  
  
    ```  
  
    ```csharp  
    numericUpDown1.DecimalPlaces = 2;  
    numericUpDown1.ThousandsSeparator = true;  
  
    ```  
  
    ```cpp  
    numericUpDown1->DecimalPlaces = 2;  
    numericUpDown1->ThousandsSeparator = true;  
    ```  
  
     \- 或 \-  
  
-   通过将 <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> 属性设置为 `true`，显示十六进制数值。  
  
    ```vb  
    NumericUpDown1.Hexadecimal = True  
  
    ```  
  
    ```csharp  
    numericUpDown1.Hexadecimal = true;  
  
    ```  
  
    ```cpp  
    numericUpDown1->Hexadecimal = true;  
    ```  
  
    > [!NOTE]
    >  即使值在窗体中显示为十六进制值，对 <xref:System.Windows.Forms.NumericUpDown.Value%2A> 属性执行的任何测试所测试的都是其十进制值。  
  
## 请参阅  
 <xref:System.Windows.Forms.NumericUpDown>   
 [NumericUpDown 控件](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)   
 [NumericUpDown 控件概述](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)