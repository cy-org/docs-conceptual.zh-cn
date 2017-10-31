---
title: "通用命名约定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "冲突的名称 [.NET Framework]"
  - "冲突的类型名称"
  - "语言特定的类型名称"
  - "名称 [.NET Framework]，关于命名准则"
  - "缩写的名称 [.NET Framework]"
  - "缩写命名准则"
  - "首字母缩写词命名准则"
  - "匈牙利表示法"
  - "名称 [.NET Framework]，类型名称"
  - "名称 [.NET Framework] 首字母缩写词"
ms.assetid: d3a77ea1-75d2-4969-a8c3-3e1e3e1aaedc
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# 通用命名约定
本部分介绍通用命名约定与 word 的选择，如何使用有关如何避免使用特定于语言的名称的缩写和首字母缩写词和建议的指南。  
  
## Word 选项  
 **✓ 执行** 选择易读的标识符名称。  
  
 例如，一个名为的属性 `HorizontalAlignment` 是英语\-比更易读 `AlignmentHorizontal`。  
  
 **✓ 执行** 可读性比简洁性更。  
  
 属性名称 `CanScrollHorizontally` 优于 `ScrollableX` （对 x 轴不明确引用）。  
  
 **X 不** 使用下划线、 连字符或任何其他非字母数字字符。  
  
 **X 不** 使用匈牙利表示法。  
  
 **X 避免** 使用广泛使用的关键字冲突的标识符使用编程语言。  
  
 根据规则 4 的公共语言规范 \(CLS\)，所有兼容的语言必须提供一种机制，允许访问该语言的关键字用作标识符的命名项。 C\# 中，例如，使用 @ 符号作为在此情况下转义机制。 但是，它仍是一个很好的主意，以避免常见的关键字，因为它是用于一种方法比另一个没有它的转义序列困难得多。  
  
## 使用缩写和首字母缩写词  
 **X 不** 缩写或缩略形式用作标识符名称的一部分。  
  
 例如，使用 `GetWindow` 而不是 `GetWin`。  
  
 **X 不** 使用并不被广泛接受，即使它们是，仅在必要时任何首字母缩写词。  
  
## 避免特定于语言的名称  
 **✓ 执行** 使用类型名称在语义上是有意义的名称，而不是特定于语言的关键字。  
  
 例如， `GetLength` 是一个合适的名称 `GetInt`。  
  
 **✓ 执行** 在极少数情况下在标识符的语义含义仅限于其类型中使用一般的 CLR 类型名称，而不是使用语言特定的名称。  
  
 例如，将转换为方法 <xref:System.Int64> 应命名为 `ToInt64`, ，而不 `ToLong` \(因为 <xref:System.Int64> 是 C\# 的 CLR 名称的特定别名 `long`\)。 下表列出了一些基本数据类型使用的 CLR 类型名称 （以及相应的类型名称为 C\#、 Visual Basic 和 c \+ \+）。  
  
|C\#|Visual Basic|C\+\+|CLR|  
|---------|------------------|-----------|---------|  
|**sbyte**|**SByte**|**char**|**SByte**|  
|**byte**|**Byte**|**unsigned char**|**Byte**|  
|**short**|**简短**|**short**|**Int16**|  
|**ushort**|**UInt16**|**unsigned short**|**UInt16**|  
|**int**|**Integer**|**int**|**Int32**|  
|**uint**|**UInt32**|**unsigned int**|**UInt32**|  
|**long**|**Long**|**\_\_int64**|**Int64**|  
|**ulong**|**UInt64**|**unsigned \_\_int64**|**UInt64**|  
|**float**|**Single**|**float**|**Single**|  
|**double**|**Double**|**double**|**Double**|  
|**bool**|**Boolean**|**bool**|**Boolean**|  
|**char**|**Char**|**wchar\_t**|**Char**|  
|**string**|**String**|**String**|**String**|  
|**object**|**对象**|**对象**|**对象**|  
  
 **✓ 执行**  使用公用名，如 `value` 或 `item`, ，而不是重复的类型名称，在标识符的语义含义和参数的类型并不重要的极少数情况下。  
  
## 命名新版本的现有 Api  
 **✓ 执行** 时创建新版本的现有 API 的使用类似于旧 API 的名称。  
  
 这有助于突出显示 Api 之间的关系。  
  
 **✓ 执行** 喜欢添加一个后缀，而不是用于指示现有 API 的新版本的前缀。  
  
 这将有助于发现，当浏览文档，也可以使用 Intellisense。 旧版本的 API 将组织接近的新 Api，因为大多数浏览器和 Intellisense 显示按字母顺序的标识符。  
  
 **✓ 请考虑** 使用全新，但有意义的标识符，而不添加一个后缀或前缀。  
  
 **✓ 执行** 使用数字后缀来指示的现有 API 的新版本，尤其是 API 的现有名称 （例如，如果它是一种行业标准） 有意义的唯一名称，如果添加任何有意义后缀 （或更改的名称） 不是一个适当的选项。  
  
 **X 不** "Ex"（或类似） 使用一个标识符，以使其不同于早期版本的相同的 API 的后缀。  
  
 **✓ 执行** 引入操作而不是 32 位整数的 64 位整数 （长整型） 的 Api 的版本时使用"64"后缀。 只需采用此方法，如果存在现有的 32 位 API;千万别那么做为使用 64 位版本的全新 Api。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)