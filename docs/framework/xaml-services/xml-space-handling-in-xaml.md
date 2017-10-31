---
title: "xml:space Handling in XAML | Microsoft Docs"
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
  - "XAML [XAML Services], xml:space attribute"
  - "XAML [XAML Services], whitespace processing"
  - "xml:space attribute [XAML Services]"
  - "whitespace processing [XAML Services]"
ms.assetid: 5e1814f0-5b30-43d5-8c88-dede335a89d7
caps.latest.revision: 15
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 15
---
# xml:space Handling in XAML
`xml:space` 特性是 XML 定义的特性，该特性在对象元素中声明有效的空白处理行为。  此行为与声明 `xml:space` 的元素内包含的所有内容（内部文本）有关，并且范围限于子元素。  
  
## XAML 属性用法  
  
```  
<object xml:space="preserve" />  
```  
  
 \- 或 \-  
  
```  
<object xml:space="default" />  
```  
  
## 备注  
 XAML 中的 `xml:space` 特性的定义（包括两个可能的值）是从 `xml:space` 派生的，后者被 W3C 规范定义为用于 XML 的“特殊特性”。  
  
 `xml:space` 特性的默认值是文本值 `"default"`。  如果使用值 `"default"`，或者根本未指定 `xml:space`，则有效空白分析行为将是默认处理，如主题 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)中所述。  
  
 若要在对象元素内容内保留空白，请对该对象元素指定 `xml:space="preserve"`。  
  
 在大多数解释下，`xml:space` 特性效果和该特性值的范围限于子元素。  
  
 有关 XAML 中的空白处理的完整讨论，请参见 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)。  
  
## 请参阅  
 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)