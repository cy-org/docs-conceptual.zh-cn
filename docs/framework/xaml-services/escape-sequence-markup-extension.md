---
title: "{} Escape Sequence / Markup Extension | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "{}"
helpviewer_keywords: 
  - "XAML [XAML Services], quotation mark (")"
  - "{} escape sequence [XAML Services]"
  - "XAML [XAML Services], {} escape sequence"
  - "XAML [XAML Services], escape sequence"
  - "quotation mark (") [XAML Services]"
  - "escape sequence [XAML Services]"
ms.assetid: 3ce3e2ad-a868-43f9-9c98-b29561cb146e
caps.latest.revision: 21
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
---
# {} Escape Sequence / Markup Extension
提供属性值的 XAML 转义序列。  转义序列允许将属性中的序列值解释为文本。  
  
## XAML 属性用法  
  
```  
<object property="{} literalValue" .../>  
```  
  
## XAML 属性元素用法  
  
```  
<object>  
  <object.property>  
    {} literalValue  
  </object.property>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|*literalValue*|遵循转义序列的字符串。  通常，此字符串包含一个打开或关闭大括号 \({ 或 }\)。|  
  
## 备注  
 使用转义序列 \({}\) ，以使左大括号“{”可以被用作 XAML 中的原义字符。  
  
 XAML 读者通常使用大括号 \({}\) 表示的入口点的标记扩展 ； 但是，他们首先检查以确定它是否是一个右大括号 \(}\) 的下一个字符。  只有在两个大括号 \({}\) 相邻时，它们被视为转义序列。  
  
 如果遇到转义序列，XAML 读取器应以字符串形式处理其余字符串。  但是，如果对具有类型转换器的成员使用转义序列，则仍有可能在由 XAML 编写器进行解释时，该字符串会被类型转换器转换。  
  
 转义序列不是标记扩展，不受类的支持。  但是，XAML 读取器（包括自定义 XAML 读取器）应遵守该约定。  
  
 不能按此方式将引号 \("\) 用作转义序列。  如果需要将引号设置为非内容属性的属性值，请使用属性元素语法，并将引号作为一个字符串放在属性元素内，或者使用 XML 字符实体。  对于内容属性，引号可以是全部内容。  
  
 在可能会出现 XAML 标记扩展的位置指定必须包含命名空间限定符的 XML 类型时，经常需要使用 \({}\) 转义序列。  这包括 XAML 特性值的开头、标记扩展的内部以及紧跟着等号 \(\=\) 的位置。  下面的示例显示了出现在 XAML 特性值开头的 XML 命名空间的转义序列。  
  
 [!code-xml[XLINQExample#StackPanelResources](../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
  
## 请参阅  
 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)   
 [XML Character Entities and XAML](../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)