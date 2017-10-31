---
title: "数据类型摘要 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Boolean 数据类型, Visual Basic 中受支持的类型"
  - "Byte 数据类型, Visual Basic 数据类型"
  - "Char 数据类型, Visual Basic 数据类型"
  - "数据类型 [Visual Basic], 内存需求"
  - "数据类型 [Visual Basic], 存储顺序"
  - "数据类型 [Visual Basic], 存储分配"
  - "数据类型 [Visual Basic], 汇总"
  - "数据类型 [Visual Basic], Visual Basic"
  - "日期数据类型, Visual Basic"
  - "日期 [Visual Basic], 数据类型"
  - "Double 数据类型, Visual Basic 数据类型"
  - "双精度数字"
  - "Integer 数据类型, Visual Basic 数据类型"
  - "内部数据类型"
  - "Long 数据类型, Visual Basic 中受支持的类型"
  - "内存消耗"
  - "内存消耗, 数据类型"
  - "内存需求, 数据类型"
  - "notation, 科学"
  - "Object 数据类型, Visual Basic 中受支持的类型"
  - "科学记数法"
  - "Single 数据类型, Visual Basic 中受支持的类型"
  - "单精度数"
  - "存储顺序, 在 Visual Basic 中控制"
  - "存储顺序, 数据类型"
  - "存储, 分配"
  - "存储, 存储顺序"
  - "存储, 空间"
  - "String 数据类型, Visual Basic 数据类型"
  - "字符串 [Visual Basic], 数据类型"
  - "StructLayoutAttribute 类, Visual Basic 数据类型存储"
  - "用户定义的数据类型, Visual Basic"
  - "Variant 数据类型, Visual Basic 中受支持的类型"
  - "Visual Basic, 数据类型"
ms.assetid: e975cdb6-64d8-4a4a-ae27-f3b3ed198ae0
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 数据类型摘要 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

下表显示了 Visual Basic 的数据类型及其支持的公共语言运行时类型、名义存储分配和取值范围。  
  
|Visual Basic 类型|公共语言运行时类型结构|名义存储分配|取值范围|  
|---------------------|-----------------|------------|----------|  
|[Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|<xref:System.Boolean>|取决于实现平台|`True` 或 `False`|  
|[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)|<xref:System.Byte>|1 个字节|0 到 255（无符号）|  
|[Char](../../../visual-basic/language-reference/data-types/char-data-type.md)（单个字符）|<xref:System.Char>|2 个字节|0 到 65535（无符号）|  
|[日期](../../../visual-basic/language-reference/data-types/date-data-type.md)|<xref:System.DateTime>|8 个字节|0001 年 1 月 1 日午夜 0:00:00 到 9999 年 12 月 31 日晚上 11:59:59|  
|[Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|<xref:System.Decimal>|16 个字节|0 到 \+\/\-79,228,162,514,264,337,593,543,950,335 \(\+\/\-7.9...E\+28\) <sup>†</sup>，不包含小数点；0 到 \+\/\-7.9228162514264337593543950335，包含小数点右边 28 位<br /><br /> 最小非零数为 \+\/\-0.0000000000000000000000000001 \(\+\/\-1E\-28\) <sup>†</sup>|  
|[Double](../../../visual-basic/language-reference/data-types/double-data-type.md)（双精度浮点型）|<xref:System.Double>|8 个字节|对于负值，为  \-1.79769313486231570E\+308 到 \-4.94065645841246544E\-324 <sup>†</sup><br /><br /> 对于正值，为 4.94065645841246544E\-324 到 1.79769313486231570E\+308 <sup>†</sup>|  
|[Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)|<xref:System.Int32>|4 个字节|\-2,147,483,648 到 2,147,483,647（有符号）|  
|[Long](../../../visual-basic/language-reference/data-types/long-data-type.md) （长整型）|<xref:System.Int64>|8 个字节|（有符号）\-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 \(9.2...E\+18 <sup>†</sup>\)|  
|[对象](../../../visual-basic/language-reference/data-types/object-data-type.md)|<xref:System.Object>（类）|4 个字节（32 位平台上）<br /><br /> 8 个字节（64 位平台上）|任何类型都可以存储在 `Object` 类型的变量中|  
|[SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|<xref:System.SByte>|1 个字节|\-128 到 127（有符号）|  
|[Short](../../../visual-basic/language-reference/data-types/short-data-type.md)（短整型）|<xref:System.Int16>|2 个字节|\-32,768 到 32,767（有符号）|  
|[Single](../../../visual-basic/language-reference/data-types/single-data-type.md) （单精度浮点型）|<xref:System.Single>|4 个字节|对于负值，为 \-3.4028235E\+38 到 \-1.401298E\-45 <sup>†</sup><br /><br /> 对于正值，为 1.401298E\-45 到 3.4028235E\+38 <sup>†</sup>|  
|[String](../../../visual-basic/language-reference/data-types/string-data-type.md) （变长）|<xref:System.String>（类）|取决于实现平台|0 到大约 20 亿个 Unicode 字符|  
|[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|<xref:System.UInt32>|4 个字节|0 到 4,294,967,295（无符号）|  
|[ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|<xref:System.UInt64>|8 个字节|0 到 18,446,744,073,709,551,615 \(1.8...E\+19 <sup>†</sup>\)（无符号）|  
|[用户定义的](../../../visual-basic/language-reference/data-types/user-defined-data-type.md)（结构）|（继承自 <xref:System.ValueType>）|取决于实现平台|结构中的每个成员都有由自身数据类型决定的取值范围，与其他成员的取值范围无关|  
|[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|<xref:System.UInt16>|2 个字节|0 到 65,535（无符号）|  
  
 <sup>†</sup> 在科学记数法中，“E”表示以 10 为底的幂。  因此 3.56E\+2 表示 3.56 x 10<sup>2</sup> 或 356，3.56E\-2 表示 3.56 \/ 10<sup>2</sup> 或 0.0356。  
  
> [!NOTE]
>  对于包含文本的字符串，请使用 <xref:Microsoft.VisualBasic.Strings.StrConv%2A> 函数从一种文本格式转换为另一种格式。  
  
 使用类型字符，除了声明语句中指定数据类型外，可以强制某些编程元素的数据类型。  请参见 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)。  
  
## 内存消耗  
 在声明一个基本数据类型时，假定该数据类型的内存消耗等于其名义存储分配是不安全的。  这是因为下面的注意事项：  
  
-   **存储分配。**公共语言运行时根据执行应用程序的平台的当前特性来分配存储。  如果内存几乎用完，它可能会将声明的元素尽可能紧密地打包到一起。  在其他情况下，它可能会将内存地址与实际硬件边界对齐以优化性能。  
  
-   **平台宽度。**64 位平台上的存储分配与 32 位平台上的存储分配不同。  
  
### 复合数据类型  
 这些注意事项也同样适用于复合数据类型的每个成员，如结构或数组。  不能简单地将类型的各成员的名义存储分配相加。  此外，还有其他一些事项需要注意，如下所示：  
  
-   **开销。**某些复合类型需要更多内存。  例如，数组需要为其本身和每个维使用额外的内存。  在 32 位平台上，这种开销目前为 12 个字节，外加每维 8 个字节。  在 64 位平台上，此需求增加了一倍。  
  
-   **存储布局。**不能完全假定成员在内存中的存储顺序与声明的顺序相同。  甚至不能假定字节对齐方式，例如 2 字节或 4 字节边界。  如果要定义类或结构，并需要控制其成员的存储布局，则可以将 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性应用于该类或结构。  
  
### Object 开销  
 引用任何基本或复合数据类型的 `Object` 在除了该数据类型中包含的数据之外还要额外使用 4 个字节。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Strings.StrConv%2A>   
 <xref:System.Runtime.InteropServices.StructLayoutAttribute>   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)