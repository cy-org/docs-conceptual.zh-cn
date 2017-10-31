---
title: "应用特性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "程序集 [.NET Framework], 特性"
  - "特性 [.NET Framework], 应用"
ms.assetid: dd7604eb-9fa3-4b60-b2dd-b47739fa3148
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# 应用特性
通过下列过程将特性应用到代码元素。  
  
1.  定义新特性，或者通过从 .NET Framework 导入特性的命名空间，使用现有特性。  
  
2.  在紧邻代码元素之前放置特性，从而将该特性应用于代码元素。  
  
     每种语言都有自己的特性语法。  在 C\+\+ 和 C\# 中，特性由方括号括起来，并且通过空白（可包括换行符）与元素分隔。  在 Visual Basic 中，特性由尖括号括起来，并且必须处于同一逻辑行；如果需要加换行符，则可以使用行继续字符。  在 J\# 中，使用特殊注释语法附加特性。  
  
3.  为特性指定位置参数和命名参数。  
  
     位置参数是必需的，并且必须放在所有命名参数之前；位置参数对应于特性的构造函数之一的参数。  命名参数是可选的，对应于特性的读\/写属性。  在 C\+\+、C\# 和 J\# 中，为每个可选参数指定 `name`\=`value`，其中 `name` 是属性的名称。  在 Visual Basic 中，指定 `name`:\=`value`。  
  
 特性在您编译代码时被发送到元数据中，并可通过运行时反射服务用于公共语言运行时以及任何自定义工具或应用程序。  
  
 按照约定，所有特性名都以 Attribute 结尾。  但是，对于 Visual Basic、C\# 等以运行时为目标的语言，不要求指定特性的全名。  例如，如果要初始化 <xref:System.ObsoleteAttribute?displayProperty=fullName>，只需将其引用为 **Obsolete** 即可。  
  
## 将特性应用于方法  
 下面的代码示例显示如何声明 **System.ObsoleteAttribute**，该特性将代码标记为过时。  字符串 `"Will be removed in next version"` 被传递到该特性。  当调用该特性所描述的代码时，该特性将产生编译器警告以显示所传递的字符串。  
  
 [!code-cpp[Conceptual.Attributes.Usage#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#3)]
 [!code-csharp[Conceptual.Attributes.Usage#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#3)]
 [!code-vb[Conceptual.Attributes.Usage#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#3)]  
  
## 在程序集级别应用特性  
 如果要在程序集级别应用特性，请使用 **assembly**（Visual Basic中用`Assembly`）关键字。  下列代码显示在程序集级别应用的**AssemblyNameAttribute**。  
  
 [!code-cpp[Conceptual.Attributes.Usage#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#2)]
 [!code-csharp[Conceptual.Attributes.Usage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#2)]
 [!code-vb[Conceptual.Attributes.Usage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#2)]  
  
 应用该特性时，字符串 `"My Assembly"` 被放到文件元数据部分的程序集清单中。  可以使用 [MSIL 反汇编程序 \(Ildasm.exe\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 或通过创建检索该特性的自定义程序来查看该特性。  
  
## 请参阅  
 [特性](../../../docs/standard/attributes/index.md)   
 [检索存储在特性中的信息](../../../docs/standard/attributes/retrieving-information-stored-in-attributes.md)   
 [Concepts](../Topic/Attributed%20Programming%20Concepts.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)