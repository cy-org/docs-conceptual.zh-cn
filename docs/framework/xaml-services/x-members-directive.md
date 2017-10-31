---
title: "x:Members Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 155b393d-3b49-4c5a-8c9e-b3d9893af4e4
caps.latest.revision: 5
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 5
---
# x:Members Directive
保存标记中已定义成员集，其适用于父成员中的 x:Class。  
  
## XAML 属性用法  
  
```  
  
<object x:Class="className">  
  <x:Members>  
    oneOrMoreMembers  
  </x:Members  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`className`|XAML 生产的后备类或分部类的名称。  请参见"备注"。|  
|`oneOrMoreMembers`|表示成员定义的一个或多个对象元素。  通常，它们是 `x:Property` 对象元素。  请参见"备注"。|  
  
## 备注  
 在 .NET Framework XAML 服务实现中，没有 `x:Members` 的后备类或基础成员实现。  `x:Members` 是可以作为任何类型成员存在的特殊 XAML 成员。  在 XAML 节点流中，`x:Members` 表示为来自 XAML 语言 XAML 命名空间中的名为 `Members` 的成员。  成员 `Members` 包含 `Member` 对象的只读泛型列表。  在典型标记中，将单个成员指定为 `x:Property` 属性元素。  `x:Property` 是专用于属性类型的更精确类型，可分配给 `x:Member`。  有关更多信息，请参见 [x:Property Directive](../../../docs/framework/xaml-services/x-property-directive.md)。  
  
 要支持 `x:Members` 作为指定标记中成员定义方法的实际用途，成员必须与可以修改的类相关。  预期的模式 `x:Members` 作为指定 `x:Class` 的类型的成员而存在.  但是，相关联类型和成员机制或生成动态成员定义机制在 .NET 框架 XAML 服务层级不支持。  这将留给具有支持 XAML 中成员定义的应用程序模型的各个框架。  对 XAML 进行标记编译并使其与代码隐藏相集成或者生成来自 XAML 的纯程序集的 MSBUILD 生成操作通常不需要支持该功能。  
  
## Windows Workflow Foundation 的 x:Members  
 对于窗口基础工作流，`x:Members` 包含了完全在 XAML 中组成的自定义活动的成员或 XAML \-通过代码隐藏为活动设计器定义了动态成员。  `x:Class` 还必须在 XAML 生产的根元素上指定。  这不是 .NET Framework XAML 服务层级的要求，但当 XAML 生产由通常支持自定义活动和 Windows Workflow Foundation XAML 的 MSBUILD 生成操作进行加载时将成为 .NET Framework XAML 服务层级的要求。  `x:Members` 必须是声明 `x:Class` 的对象元素标记中的第一个子元素。