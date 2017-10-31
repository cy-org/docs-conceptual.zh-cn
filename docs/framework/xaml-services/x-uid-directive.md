---
title: "x:Uid Directive | Microsoft Docs"
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
  - "XAML [XAML Services], localizable content attribute"
  - "XAML [XAML Services], x:Uid attribute"
  - "x:Uid attribute [XAML Services]"
  - "Uid attribute [XAML Services]"
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# x:Uid Directive
为标记元素提供唯一的标识符。  在许多情况下，此唯一标识符由 XAML 本地化过程和工具使用。  
  
## XAML 属性用法  
  
```  
<object x:Uid="identifier"... />  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`identifier`|一个手动创建的或自动生成的字符串，当 `x:Uid` 使用者解释该字符串，它在文件中应是唯一的。|  
  
## 备注  
 在 \[MS\-XAML\]，`x:Uid` 被定义为指令。  有关更多信息，请参见 [\[MS\-XAML\] Section 5.3.6](http://go.microsoft.com/fwlink/?LinkId=114525)（\[MS\-XAML\] 第 5.3.6 节）。  
  
 `x:Uid` 是从 `x:Name` 分离出来的，原因有两个，一是启动的 XAML 本地化方案；另外一个是：因此用于本地化的标识符没有对 `x:Name` 的编程模型含义的依赖性。  此外，`x:Name` 受 XAML 名称范围控制，而 `x:Uid` 不受任何 XAML 语言定义的唯一性强制概念控制。  广义上的 XAML 处理器（不是本地化进程的一部分的处理器）不会强制保证 `x:Uid` 值的唯一性。  从概念上讲，该责任在于该值的发信方。  单一 XAML 源中的 `x:Uid` 值的唯一性的预期对于值的使用方（如专门的全球化进程或工具）是合理的。  典型的唯一性模型是：`x:Uid` 值是代表 XAML 的 XML 编码的文件中的唯一值。  
  
 具有特定 XAML 架构的重要知识的工具可以只对确实可以本地化的字符串，而不是为所有在标记中遇到文本字符串值的情况选择应用 `x:Uid`。  
  
 通过对定义类型应用特性 <xref:System.Windows.Markup.UidPropertyAttribute>，Frameworks 可以将其对象模型中的特定属性指定为 `x:Uid` 的别名。  如果框架指定了一个特定属性，则在同一对象上指定 `x:Uid` 和具有别名的成员是非法的。  如果指定 `x:Uid` 和别名，则该用例的 .NET 框架 XAML 服务 API 通常会引发 <xref:System.Xaml.XamlDuplicateMemberException>。  
  
## WPF 用法说明  
 有关 WPF 本地化过程和 XAML 的 BAML 窗体中 `x:Uid` 的角色的更多信息，请参见 [WPF 的全球化](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md)或 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>  
  
## 请参阅  
 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>   
 <xref:Microsoft.Build.Tasks.Windows.UidManager>   
 [WPF 的全球化](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md)