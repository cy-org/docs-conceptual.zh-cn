---
title: "内联样式和模板 | Microsoft Docs"
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
  - "内联样式"
  - "内联模板"
  - "样式, inline"
  - "模板, inline"
ms.assetid: 69a1a3f9-acb5-4e2c-9c43-2e376c055ac4
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 内联样式和模板
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供的 <xref:System.Windows.Style> 对象和模板对象（<xref:System.Windows.FrameworkTemplate> 子类）可用来定义资源中元素的可视外观，因此可以多次使用。  所以，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中采用 <xref:System.Windows.Style> 和 <xref:System.Windows.FrameworkTemplate> 类型的特性总是可以对现有的样式和模板进行资源引用，而不是定义新的内联样式和模板。  
  
## 内联样式和模板的限制  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，样式和模板属性在技术上可以通过以下两种方法之一来设置：  可以使用特性语法来引用在资源中定义的样式，例如，`<`*对象*`Style="{StaticResource`*我的资源键*`}" .../>`。  也可以使用属性元素语法来定义内联样式，例如：  
  
 `<` *object* `>`  
  
 `<` *object* `.Style>`  
  
 `<` `Style`  `.../>`  
  
 `</` *object* `.Style>`  
  
 `</` *object* `>`  
  
 特性用法更常见。  在定义为内联但是未在资源中定义的样式必须仅包括包含元素，而且无法方便地重用该样式，因为它没有资源键。  通常，由资源定义的样式更通用和有用，而且更符合通用的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 编程模型原理（将代码中的程序逻辑与标记中的设计分开）。  
  
 通常，即使您只打算在该位置使用样式和模板，也没有必要设置内联样式或模板。  采用样式或模板的大多数元素还支持一个内容属性和一个内容模型。  如果您对于通过样式或模板创建的逻辑树仅使用一次，则更方便的做法是，只需用直接标记中的等效子元素填充该内容属性。  这将完全跳过样式和模板机制。  
  
 对于样式和模板，也可以使用由那些返回一个对象的标记扩展启用的其他语法。  [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 和 <xref:System.Windows.Data.Binding> 就是两个具有可能方案的这样的扩展。  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)