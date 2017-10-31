---
title: "PresentationOptions:Freeze 特性 | Microsoft Docs"
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
  - "Freezable 元素"
  - "Freeze 特性"
  - "PresentationOptions 前缀"
ms.assetid: 391032dd-2fba-4804-bb8a-3b071797a9f4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# PresentationOptions:Freeze 特性
将包含 <xref:System.Windows.Freezable> 元素上的 <xref:System.Windows.Freezable.IsFrozen%2A> 状态设置为 `true`。  未指定 `PresentationOptions:Freeze` 特性的 <xref:System.Windows.Freezable> 的默认行为是：<xref:System.Windows.Freezable.IsFrozen%2A> 在加载时为 `false`，在运行时则依赖于一般 <xref:System.Windows.Freezable> 行为。  
  
## XAML 属性用法  
  
```  
<object  
  xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="PresentationOptions">  
    <freezableElement PresentationOptions:Freeze="true"/>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`PresentationOptions`|符合 XML 1.0 规范的 XML 命名空间前缀，可以是任何有效的前缀字符串。  前缀 `PresentationOptions` 在本文档中用于标识目的。|  
|`freezableElement`|实例化 <xref:System.Windows.Freezable> 的任何派生类的元素。|  
  
## 备注  
 `Freeze` 特性是在 `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options` XML 命名空间中定义的唯一一个特性或其他编程元素。  `Freeze` 特性只存在于这个特殊的命名空间中，所以可以指定为可忽略，而将 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)用作根元素声明的一部分。  `Freeze` 必须可以忽略的原因是因为并非所有 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器实现都能在加载时冻结 <xref:System.Windows.Freezable>；此功能不属于 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 规范的一部分。  
  
 处理 `Freeze` 特性的能力专门内置于为编译的应用程序处理 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器中。  该特性不受任何类的支持，而且特性语法既不可以扩展，也不可以修改。  如果您要实现自己的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器，可以在加载时选择处理 <xref:System.Windows.Freezable> 元素的 `Freeze` 特性的同时，并行 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器的冻结行为。  
  
 对于 `Freeze` 特性，除 `true`（不区分大小写）之外的任何值都将产生加载时错误。  （将 `Freeze` 特性指定为 `false` 并不是错误，但它已经是默认值，所以设置为 `false` 不会执行任何操作。）  
  
## 请参阅  
 <xref:System.Windows.Freezable>   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [mc:Ignorable 特性](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)