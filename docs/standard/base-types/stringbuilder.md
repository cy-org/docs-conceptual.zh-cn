---
title: "在 .NET Framework 中使用 StringBuilder 类 | Microsoft Docs"
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
  - "Remove 方法"
  - "字符串 [.NET Framework]，容量"
  - "StringBuilder 对象"
  - "Replace 方法"
  - "AppendFormat 方法"
  - "Append 方法"
  - "Insert 方法"
  - "字符串 [.NET Framework]，StringBuilder 对象"
ms.assetid: 5c14867c-9a99-45bc-ae7f-2686700d377a
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# 在 .NET Framework 中使用 StringBuilder 类
<xref:System.String> 对象是不可变的。 每次使用 <xref:System.String?displayProperty=fullName> 类中的一个方法时，都要在内存中创建一个新的字符串对象，这就需要为该新对象分配新的空间。 在需要对字符串执行重复修改的情况下，与创建新的 <xref:System.String> 对象关联的系统开销可能会非常大。 如果要修改字符串而不创建新的对象，则可以使用 <xref:System.Text.StringBuilder?displayProperty=fullName> 类。 例如，当在一个循环中将许多字符串连接在一起时，使用 <xref:System.Text.StringBuilder> 类可以提升性能。  
  
## 导入 System.Type 命名空间  
 <xref:System.Text.StringBuilder> 类位于 <xref:System.Text> 命名空间中。  为了避免必须在代码中提供完全限定的类型名称，可以导入 <xref:System.Text> 命名空间：  
  
 [!code-cpp[Conceptual.StringBuilder#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#11)]
 [!code-csharp[Conceptual.StringBuilder#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#11)]
 [!code-vb[Conceptual.StringBuilder#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#11)]  
  
## 实例化 StringBuilder 对象  
 通过用一个重载的构造函数方法初始化变量，可以创建 <xref:System.Text.StringBuilder> 类的新实例，如下面的示例所示。  
  
 [!code-cpp[Conceptual.StringBuilder#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#1)]
 [!code-csharp[Conceptual.StringBuilder#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#1)]
 [!code-vb[Conceptual.StringBuilder#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#1)]  
  
## 设置容量和长度  
 虽然 <xref:System.Text.StringBuilder> 是动态对象，允许扩充它所封装的字符串中的字符数，但你可以通过一个值来指定该对象可保留的最大字符数。 此值称为该对象的容量，不要将它与当前 <xref:System.Text.StringBuilder> 所保留的字符串的长度相混淆。 例如，可以使用长度为 5 的字符串“Hello”创建 <xref:System.Text.StringBuilder> 类的一个新实例，同时可以指定该对象的最大容量为 25。 当修改 <xref:System.Text.StringBuilder> 时，在达到容量之前，该对象不会为自己重新分配空间。 当达到容量时，将自动分配新的空间且容量翻倍。 可以使用重载的构造函数之一来指定 <xref:System.Text.StringBuilder> 类的容量。 下面的示例指定可以将 `MyStringBuilder` 对象扩充到最大 25 个空间。  
  
 [!code-cpp[Conceptual.StringBuilder#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#2)]
 [!code-csharp[Conceptual.StringBuilder#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#2)]
 [!code-vb[Conceptual.StringBuilder#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#2)]  
  
 另外，可以使用读\/写 <xref:System.Text.StringBuilder.Capacity%2A> 属性来设置对象的最大长度。 下面的示例使用 **Capacity** 属性来定义对象的最大长度。  
  
 [!code-cpp[Conceptual.StringBuilder#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#3)]
 [!code-csharp[Conceptual.StringBuilder#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#3)]
 [!code-vb[Conceptual.StringBuilder#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#3)]  
  
 <xref:System.Text.StringBuilder.EnsureCapacity%2A> 方法可用来检查当前 **StringBuilder** 的容量。 如果容量大于传递的值，则不进行任何更改；但是，如果容量小于传递的值，则会更改当前的容量以使其与传递的值匹配。  
  
 也可以查看或设置 <xref:System.Text.StringBuilder.Length%2A> 属性。 如果将 **Length** 属性设置为大于 **Capacity** 属性的值，则自动将 **Capacity** 属性更改为与 **Length** 属性相同的值。 如果将 **Length** 属性设置为小于当前 **StringBuilder** 对象内的字符串长度的值，则会缩短该字符串。  
  
## 修改 StringBuilder 字符串  
 下表列出了可用于修改 **StringBuilder** 的内容的方法。  
  
|方法名称|使用|  
|----------|--------|  
|<xref:System.Text.StringBuilder.Append%2A?displayProperty=fullName>|将信息追加到当前 **StringBuilder** 的末尾。|  
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>|用带格式文本替换字符串中传递的格式说明符。|  
|<xref:System.Text.StringBuilder.Insert%2A?displayProperty=fullName>|将字符串或对象插入到当前 **StringBuilder** 的指定索引中。|  
|<xref:System.Text.StringBuilder.Remove%2A?displayProperty=fullName>|从当前 **StringBuilder** 中删除指定数量的字符。|  
|<xref:System.Text.StringBuilder.Replace%2A?displayProperty=fullName>|替换指定索引处的指定字符。|  
  
### 追加  
 **Append** 方法可用来将文本或对象的字符串表示形式添加到由当前 **StringBuilder** 表示的字符串的末尾。 下面的示例将一个 **StringBuilder** 对象初始化为“Hello World”，然后将一些文本追加到该对象的末尾。 将根据需要自动分配空间。  
  
 [!code-cpp[Conceptual.StringBuilder#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#4)]
 [!code-csharp[Conceptual.StringBuilder#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#4)]
 [!code-vb[Conceptual.StringBuilder#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#4)]  
  
### AppendFormat  
 <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName> 方法将文本添加到 <xref:System.Text.StringBuilder> 对象的末尾。 该方法通过调用要设置格式的对象的 <xref:System.IFormattable> 实现来支持复合格式设置功能（有关详细信息，请参阅[复合格式设置](../../../docs/standard/base-types/composite-formatting.md)）。 因此，它接受数字、日期和时间以及枚举值的标准格式字符串、数字以及日期和时间值的自定义格式字符串，以及为自定义类型定义的格式字符串。 （有关格式设置的信息，请参阅 [格式化类型](../../../docs/standard/base-types/formatting-types.md)。） 可以使用此方法来自定义变量的格式并将这些值追加到 <xref:System.Text.StringBuilder>。 下面的示例使用 <xref:System.Text.StringBuilder.AppendFormat%2A> 方法，将一个设置为货币值格式的整数值放到 <xref:System.Text.StringBuilder> 对象的末尾。  
  
 [!code-cpp[Conceptual.StringBuilder#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#5)]
 [!code-csharp[Conceptual.StringBuilder#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#5)]
 [!code-vb[Conceptual.StringBuilder#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#5)]  
  
### Insert  
 <xref:System.Text.StringBuilder.Insert%2A> 方法将字符串或对象添加到当前 <xref:System.Text.StringBuilder> 对象中的指定位置。 下面的示例使用此方法将一个单词插入到 <xref:System.Text.StringBuilder> 对象的第六个位置。  
  
 [!code-cpp[Conceptual.StringBuilder#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#6)]
 [!code-csharp[Conceptual.StringBuilder#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#6)]
 [!code-vb[Conceptual.StringBuilder#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#6)]  
  
### 删除  
 可以使用 **Remove** 方法从当前 <xref:System.Text.StringBuilder> 对象中删除指定数量的字符，删除过程从指定的从零开始的索引处开始。 下面的示例使用 **Remove** 方法缩短 <xref:System.Text.StringBuilder> 对象。  
  
 [!code-cpp[Conceptual.StringBuilder#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#7)]
 [!code-csharp[Conceptual.StringBuilder#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#7)]
 [!code-vb[Conceptual.StringBuilder#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#7)]  
  
### 替换  
 使用 **Replace** 方法可以用另一个指定的字符来替换 <xref:System.Text.StringBuilder> 对象内的字符。 下面的示例使用 **Replace** 方法在 <xref:System.Text.StringBuilder> 对象中搜索感叹号字符 \(\!\) 的所有实例，并将其替换为问号字符 \(?\)。  
  
 [!code-cpp[Conceptual.StringBuilder#8](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#8)]
 [!code-csharp[Conceptual.StringBuilder#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#8)]
 [!code-vb[Conceptual.StringBuilder#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#8)]  
  
## 将 StringBuilder 对象转换为字符串  
 必须先将 <xref:System.Text.StringBuilder> 对象转换为 <xref:System.String> 对象，然后才能将 <xref:System.Text.StringBuilder> 对象表示的字符串传递给具有 <xref:System.String> 参数的方法，或在用户界面中显示它。 可通过调用 <xref:System.Text.StringBuilder.ToString%2A?displayProperty=fullName> 方法来执行此转换。 下面的示例调用许多 <xref:System.Text.StringBuilder> 方法，然后调用 <xref:System.Text.StringBuilder.ToString?displayProperty=fullName> 方法来显示字符串。  
  
 [!code-csharp[Conceptual.StringBuilder#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/tostringexample1.cs#10)]
 [!code-vb[Conceptual.StringBuilder#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/tostringexample1.vb#10)]  
  
## 请参阅  
 <xref:System.Text.StringBuilder?displayProperty=fullName>   
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)   
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)