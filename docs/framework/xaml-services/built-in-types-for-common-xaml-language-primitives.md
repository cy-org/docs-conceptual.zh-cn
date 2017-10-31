---
title: "Built-in Types for Common XAML Language Primitives | Microsoft Docs"
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
  - "XAML language primitives [XAML Services]"
  - "XAML [XAML Services], built-in types"
  - "x:String [XAML Services]"
  - "x:TimeSpan [XAML Services]"
  - "x:Byte [XAML Services]"
  - "x:Double [XAML Services]"
  - "XAML [XAML Services], types"
  - "x:Uri [XAML Services]"
  - "XAML built-in types [XAML Services]"
  - "x:Int64 [XAML Services]"
  - "x:Single [XAML Services]"
  - "x:Int32 [XAML Services]"
ms.assetid: 11de2f08-5b95-4989-b5ec-5178eb968184
caps.latest.revision: 11
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 11
---
# Built-in Types for Common XAML Language Primitives
XAML 2009 引入了对多种数据类型的 XAML 语言级支持（这些数据类型是公共语言运行时 \(CLR\) 和其他编程语言中的常用基元）。 XAML 2009 增加了对以下基元的支持：`x:Object`、`x:Boolean`、`x:Char`、`x:String`、`x:Decimal`、`x:Single`、`x:Double`、`x:Int16`、`x:Int32`、`x:Int64`、`x:TimeSpan`、`x:Uri`、`x:Byte` 和 `x:Array`  
  
<a name="previous_techniques_for_language_primitives_in_xaml_markup"></a>   
## 用于 XAML 标记中语言基元的早期方法  
 在早期 WPF 版本的 XAML 中，可以通过映射程序集以及包含 .NET Framework 的 CLR 基元定义类的命名空间来引用 CLR 语言基元。 它们中的大部分都位于 mscorlib 程序集和 <xref:System> 命名空间中。 例如，要使用 <xref:System.Int32>，可以声明以下映射（用法示例如后面所示）：  
  
```  
<Application xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:sys="clr-namespace:System;assembly=mscorlib"> <Application.Resources> <sys:Int32 x:Key="intMeaning">42</sys:Int32> </Application.Resources> </Application>  
```  
  
<a name="xaml_2009_language_primitives"></a>   
## XAML 2009 语言基元  
 按照约定，将显示 XAML 的语言基元以及所有其他 XAML 语言元素，包括 `x:` 前缀。 这是 XAML 语言元素在实际标记中的典型用法。 WPF 中 XAML 的概念性文档以及 XAML 规范遵从此约定。  
  
### x:Object  
 对于 CLR 支持，`x:Object` 基元对应于 <xref:System.Object>。  
  
 此基元通常不在应用程序标记中使用，但对于某些情况（如检查 XAML 类型系统中的可分配性）可能非常有用。  
  
### x:Boolean  
 对于 CLR 支持，`x:Boolean` 基元对应于 <xref:System.Boolean>。  
  
 XAML 分析 `x:Boolean` 的值时不区分大小写。 请注意，`x:Bool` 不是可接受的备选基元。 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.17 节和第 5.4.11 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Char  
 对于 CLR 支持，`x:Char` 基元对应于 <xref:System.Char>。  
  
 String 和 char 类型在 XML 级别与文件的整个编码进行交互。 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.7 节和第 5.4.1 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:String  
 对于 CLR 支持，`x:String` 基元对应于 <xref:System.String>。  
  
 String 和 char 类型在 XML 级别与文件的整个编码进行交互。 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.6 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Decimal  
 对于 CLR 支持，`x:Decimal` 基元对应于 <xref:System.Decimal>。  
  
 请注意，XAML 分析本质上在 `en-US` 区域性设置下进行。 在 `en-US` 区域性设置下，小数部分的正确分隔符始终为句点 \(`.`\)，而与开发环境的区域性设置或在运行时加载 XAML 的最终客户端目标的区域性设置无关。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.14 节和第 5.4.8 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Single  
 对于 CLR 支持，`x:Single` 基元对应于 <xref:System.Single>。  
  
 除了数值之外，`x:Single` 的文本语法还允许使用标记 `Infinity`、`-Infinity` 和 `NaN`。 这些标记被视为区分大小写。  
  
 `x:Single` 支持采用科学记数法格式的值，条件是文本语法中的第一个字符为 `e` 或 `E`。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.8 节和第 5.4.2 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Double  
 对于 CLR 支持，`x:Double` 基元对应于 <xref:System.Double>。  
  
 除了数值之外，`x:Double` 的文本语法还允许使用标记 `Infinity`、`-Infinity` 和 `NaN`。 这些标记被视为区分大小写。  
  
 `x:Double` 支持采用科学记数法格式的值。 使用字符 `e` 或 `E` 可引入指数部分。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.9 节和第 5.4.3 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Int16  
 对于 CLR 支持，`x:Int16` 基元对应于 <xref:System.Int16>，并且 `x:Int16` 被视为带符号。 在 XAML 中，文本语法中没有加号 \(`+`\) 表示是一个带符号的正值。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.11 节和第 5.4.5 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Int32  
 对于 CLR 支持，`x:Int32` 基元对应于 <xref:System.Int32>。`x:Int32` 被视为带符号。 在 XAML 中，文本语法中没有加号 \(`+`\) 表示是一个带符号的正值。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.12 节和第 5.4.6 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Int64  
 对于 CLR 支持，`x:Int64` 基元对应于 <xref:System.Int64>。`x:Int64` 被视为带符号。 在 XAML 中，文本语法中没有加号 \(`+`\) 表示是一个带符号的正值。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.13 节和第 5.4.7 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:TimeSpan  
 对于 CLR 支持，`x:TimeSpan` 基元对应于 <xref:System.TimeSpan>。  
  
 请注意，时间日期格式的 XAML 分析本质上在 `en-US` 区域性设置下进行。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.16 节和第 5.4.10 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Uri  
 对于 CLR 支持，`x:Uri` 基元对应于 <xref:System.Uri>。  
  
 检查协议不是 `x:Uri` 的 XAML 定义的一部分。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.15 节和第 5.4.9 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Byte  
 对于 CLR 支持，`x:Byte` 基元对应于 <xref:System.Byte>。<xref:System.Byte>\/`x:Byte` 被视为无符号。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.10 节和第 5.4.4 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
### x:Array  
 对于 CLR 支持，`x:Array` 基元对应于 <xref:System.Array>。  
  
 可以在 XAML 2006 中使用标记扩展语法定义一个数组；而 XAML 2009 语法是语言定义的基元，不需要访问标记扩展。 有关 XAML 2006 支持的更多信息，请参阅 [x:Array Markup Extension](../../../docs/framework/xaml-services/x-array-markup-extension.md)。  
  
 有关 XAML 语言规范定义的信息，请参阅 [\[MS\-XAML\] 第 5.2.18 节](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
<a name="wpf_support"></a>   
## WPF 支持  
 在 WPF 中，可以使用 XAML 2009 功能，但仅针对未进行标记编译的 XAML。 WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
 可使用 XAML 2009 功能以及 WPF 的一种情况是创作宽松 XAML，然后使用 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName> 将该 XAML 加载到 WPF 运行时和对象图中。 WPF <xref:System.Windows.Markup.XamlReader?displayProperty=fullName> 及其 <xref:System.Windows.Markup.XamlReader.Load%2A> 可以将 XAML 2009 语言关键字和功能处理成一个有效的对象图表示形式。