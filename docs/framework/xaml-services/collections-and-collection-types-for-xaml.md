---
title: "Collections and Collection Types for XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
caps.latest.revision: 2
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 2
---
# Collections and Collection Types for XAML
本主题介绍如何定义用于支持集合类型的属性和支持实例化的集合项的 XAML 语法为父对象元素或属性元素的元素子级。  
  
## XAML 集合概念  
 从概念上而言， XAML 的必须实现任何关系在具有多个子项在 XAML 对象元素或 XAML 特性元素的范围内作为集合。  必须将该集合与该关系的父 XAML 类型的特定 XAML 特性。  ，因为 XAML 处理器需要分配标记中的每一项都是支持集合属性的一个新添加的项目中，属性必须是集合。  
  
 在 XAML 语言级别，集合的具体要求支持不完全定义。  后备类型表示或列表或的概念集合可以为、或列表或字典 \(，而不是两个\) 中定义的 XAML 语言级别，但是，字典未定义的由 XAML 语言。  
  
 在 .NET framework XAML 服务中， XAML 集合的概念支持是明确定义基于 .NET framework 后备类型。  具体而言， XAML 为集合支持基于多个 .NET framework 概念，以及使用 API 通常列表和字典 .NET framework 编程。  
  
1.  <xref:System.Collections.IList> 接口指示列表集合。  
  
2.  <xref:System.Collections.IDictionary> 接口指示 dicionary 集合。  
  
3.  <xref:System.Array> 表示数组，并且，数组支持 <xref:System.Collections.IList> 方法。  
  
 在这些概念集合中的每个元素， .NET framework XAML 服务 XAML 处理器需要调用在集合属性类型的特定实例的 `Add` 方法。  或者，在序列化方案， XAML 处理器会在列表、字典或数组中找到的每个项目的分离 XAML 类型的实例基于每个 “项目”集合的特定概念。  这些是: <xref:System.Collections.IList.Item%2A>; <xref:System.Collections.IDictionary.Item%2A>; <xref:System.Array>的显式 <xref:System.Array.System%23Collections%23IList%23Item%2A> 。  
  
## 泛型集合  
 泛型集合是用于编程常规 .NET framework，并且可用于 XAML 集合属性还使用。  但是，泛型接口 <xref:System.Collections.Generic.IList%601> 和 <xref:System.Collections.Generic.IDictionary%602> 不确定的是 .NET framework XAML 服务 XAML 处理器看成等效于非泛型 <xref:System.Collections.IList> 或 <xref:System.Collections.IDictionary>。  而不是实现接口，泛型集合属性类型的一个建议的方法是从类 <xref:System.Collections.Generic.List%601> 或 <xref:System.Collections.Generic.Dictionary%602>派生。  这些类实现非泛型接口从而包括预期的为基实现的 XAML 集合支持。  
  
## 只读集合和初始化逻辑  
 在编程 .NET framework，它是使表示集合的值作为只读集合的所有特性的常用设计模式。  此模式允许拥有集合属性改进控件的实例发生的集合。  具体地说，该模式通过设置属性来防止整个预先存在的集合的意外替换。  在此模式中，应通过调用方法或属性对集合的所有访问由调用方如支持由集合类型和相关集合接口例如 <xref:System.Collections.IList>。  
  
 使用此模式提示显示只读集合属性的任何类都必须先初始化该属性保存空集合。  为类的，构造行为的一部分通常初始化执行。  若要可用于 XAML，重要的此类逻辑由默认构造函数始终引用，，因为中的 XAML 处理属性之前通常调用默认构造函数 \(集合属性或\)。  
  
## XAML 类型系统支持和集合  
 在分析 XAML 和填充或序列化以外的集合属性的基本机制， XAML 类型系统为已实现在 .NET framework XAML 服务中包括与在 XAML 的集合的若干设计功能。  
  
1.  <xref:System.Xaml.XamlType.IsCollection%2A> 返回 true，则 XAML 类型由提供 XAML 集合支持的类型返回。  
  
2.  集合 模式 XAML 类型支持的<xref:System.Xaml.XamlType.IsDictionary%2A> 和 <xref:System.Xaml.XamlType.IsArray%2A> 进一步标识。  根据 .NET framework XAML 服务和 XAML 类型系统，但不基于现有 <xref:System.Xaml.XamlWriter> 实现的自定义 XAML 处理器，了解使用哪个集合模式可能需要才能知道哪个方法为集合的过程调用。  
  
3.  可能会影响每个前面的属性值会重写在 XAML 类型的 <xref:System.Xaml.XamlType.LookupCollectionKind%2A> 。