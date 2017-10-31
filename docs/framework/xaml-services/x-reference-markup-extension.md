---
title: "x:Reference Markup Extension | Microsoft Docs"
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
  - "x:Reference markup extension [XAML Services]"
  - "XAML [XAML Services], x:Reference Markup Extension"
  - "Reference markup extension [XAML Services]"
ms.assetid: 2982e68b-d26b-4aa3-826a-34c57a9c5199
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# x:Reference Markup Extension
引用在 XAML 标记中其他地方声明的实例。  参考涉及元素的 `x:Name`。  
  
## XAML 属性用法  
  
```  
<object property="{x:Reference instancexName}" .../>  
```  
  
## XAML 对象元素用法  
  
```  
<object>  
  <object.property>  
    <x:Reference Name="instancexName"/>  
  </object.property>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`instancexName`|引用实例的 `x:Name` 值（或 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 标识的属性值）。|  
  
## 备注  
 `x:Reference` 为元素引用概念提供 XAML 语言级别支持，该概念会在具体框架（如 WPF）中实现。  
  
## x:Reference 和 WPF  
 在 WPF 和 XAML 2006，元素引用解决由框架级功能的 <xref:System.Windows.Data.Binding.ElementName%2A> 绑定中。  对于大多数 WPF 应用程序和方案，仍应使用 <xref:System.Windows.Data.Binding.ElementName%2A> 绑定。  此一般性指导的例外情况可能包括存在数据上下文或让数据绑定变得不切实际的其他范围考量的情况，以及不涉及标记编译的情况。  
  
 `x:Reference` 是 XAML 2009 中定义的一个构造。  在 WPF 中，可以使用 XAML 2009 功能，但仅针对未进行 WPF 标记编译的 XAML。  标记编译的 XAML 以及BAML 形式的 XAML 当前不支持 XAML 2009 关键字和功能。