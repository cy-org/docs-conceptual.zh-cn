---
title: "XamlName 语法 | Microsoft Docs"
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
  - "DottedXamlName 语法 [XAML 服务]"
  - "语法 [XAML 服务]，DottedXamlName"
  - "语法 [XAML 服务]，XamlName"
  - "XAML 中的名称 [XAML 服务]"
  - "XamlName 语法 [XAML 服务]"
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# XamlName 语法
XamlName 语法是 XAML 语言规范 \[MS\-XAML\] 中定义的特定语法，为方便起见在此处重现。  
  
## 基于 XAML 规范  
 \[MS\-XAML\] 规范定义语法 XamlName 来标识用于类型和属性的合法符号标识符集合。  
  
 类型为 XamlName 的字符串值必须符合以下语法：  
  
```  
XamlName ::= NameStartChar ( NameChar )*   
NameStartChar ::= LetterCharacter | '_'   
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter   
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl   
DecimalDigit ::= UnicodeNd   
CombiningCharacter ::= UnicodeMn | UnicodeMc  
  
```  
  
 该语法假定 Unicode 字符数据库中定义了以下通用类别值  
  
```  
  
Lu  
Letter, Uppercase  
Ll  
Letter, Lowercase  
Lt  
Letter, Titlecase  
Lm  
Letter, Modifier  
Lo  
Letter, Other  
Mn  
Mark, Non-Spacing  
Mc  
Mark, Spacing Combining  
Nd  
Number, Decimal  
Nl  
Number, Letter  
```  
  
 XAML 定义第二个语法 DottedXamlName，该语法用于属性和事件限定引用，还用于附加成员。  有关更多信息，请参见<xref:System.Windows.DependencyProperty>和[XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
 类型为 DottedXamlName 的字符串值必须符合以下语法：  
  
```  
DottedXamlName ::= XamlName '.' XamlName  
```  
  
## 备注  
 有关完整规范，请参见 [\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525)\(\[MS\-XAML\]\)。