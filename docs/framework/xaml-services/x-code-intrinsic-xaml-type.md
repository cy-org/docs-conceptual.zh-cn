---
title: "x:Code Intrinsic XAML Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Code"
  - "x:Code"
  - "xCode"
helpviewer_keywords: 
  - "Code directive in XAML [XAML Services]"
  - "x:Code XAML directive element [XAML Services]"
  - "XAML [XAML Services], x:Code directive element"
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
caps.latest.revision: 19
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 19
---
# x:Code Intrinsic XAML Type
允许在 XAML 生产内放置代码。  这样的代码既可由任何编译 XAML 的 XAML 处理器实现编译，也可以留在 XAML 产品中以备后用，例如由运行时解释。  
  
## XAML 对象元素用法  
  
```  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## 备注  
 `x:Code` XAML 指令元素中的代码仍然在所提供的一般 XML 命名空间和 XAML 命名空间内进行解释。  因此，通常必需将用于 `x:Code` 的代码放入 `CDATA` 段中。  
  
 XAML 生产的所有可能的部署机制都不允许 `x:Code`。  在特定的框架（例如 WPF）中，必须对代码进行编译。  在其他框架中，`x:Code` 用法通常可能会被禁止。  
  
 对于允许托管 `x:Code` 内容的框架，用于 `x:Code` 内容的正确语言编译器由用于编译应用程序的包含项目的设置和目标确定。  
  
## WPF 用法说明  
 在 WPF 的 `x:Code` 中声明的代码存在几个特别的限制：  
  
-   `x:Code` 指令元素必须是 XAML 生产的根元素的直接子元素。  
  
-   在父级根元素上必须提供 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)。  
  
-   在 `x:Code` 中放置的代码在编译时被视为已位于针对该 XAML 页创建的分部类的范围中。  因此，您定义的所有代码必须都是该分部类的成员或变量。  
  
-   除了将类嵌套在分部类外，无法定义其他类（允许嵌套，但不是常见情况，因为嵌套内无法在 XAML 中引用）。  不能定义或添加到现有分部类所用的 CLR 命名空间以外的命名空间。  
  
-   必须完全限定所有对分部类 CLR 命名空间之外的代码实体的引用。  如果所声明的成员是对分部类可重写成员的重写，则必须使用特定于语言的重写关键字指定。  如果 `x:Code` 范围声明的成员与从 XAML 创建的分部类的成员发生冲突，如编译器报告该冲突，则 XAML 文件将无法进行编译或加载。  
  
## 请参阅  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [WPF 中的代码隐藏和 XAML](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)