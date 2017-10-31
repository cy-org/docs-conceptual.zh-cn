---
title: "字符串（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, strings
- strings [C#]
ms.assetid: 21580405-cb25-4541-89d5-037846a38b07
caps.latest.revision: 41
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e41a7b68d890aa7a96aeddd660e0dca90596d998
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="strings-c-programming-guide"></a>字符串（C# 编程指南）
字符串是值为文本的 <xref:System.String> 类型对象。 文本在内部存储为 <xref:System.Char> 对象的依序只读集合。 在 C# 字符串末尾没有 null 终止字符；因此，一个 C# 字符串可以包含任何数量的嵌入的 null 字符 ('\0')。 字符串的 <xref:System.String.Length%2A> 属性表示其包含的 `Char` 对象数量，而非 Unicode 字符数。 若要访问字符串中的各个 Unicode 码位，请使用 <xref:System.Globalization.StringInfo> 对象。  
  
## <a name="string-vs-systemstring"></a>string 与System.String  
 在 C# 中，`string` 关键字是 <xref:System.String> 的别名。 因此，`String` 和 `string` 是等效的，你可以使用你所喜欢的任何一种命名约定。 `String` 类提供了安全创建、操作和比较字符串的多种方法。 此外，C# 语言重载了部分运算符，以简化常见字符串操作。 有关关键字的详细信息，请参阅 [string](../../../csharp/language-reference/keywords/string.md)。 有关类型及其方法的详细信息，请参阅 <xref:System.String>。  
  
## <a name="declaring-and-initializing-strings"></a>声明和初始化字符串  
 可以使用各种方法声明和初始化字符串，如以下示例中所示：  
  
 [!code-cs[csProgGuideStrings#1](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_1.cs)]  
  
 请注意，不要使用 [new](../../../csharp/language-reference/keywords/new-operator.md) 运算符创建字符串对象，除非使用字符数组初始化字符串。  
  
 使用 <xref:System.String.Empty> 常量值初始化字符串，以新建字符串长度为零的 <xref:System.String> 对象。 长度为零的字符串文本表示法是“”。 通过使用 <xref:System.String.Empty> 值（而不是 [null](../../../csharp/language-reference/keywords/null.md)）初始化字符串，可以减少 <xref:System.NullReferenceException> 发生的可能性。 尝试访问字符串前，先使用静态 <xref:System.String.IsNullOrEmpty%28System.String%29> 方法验证字符串的值。  
  
## <a name="immutability-of-string-objects"></a>字符串对象的不可变性  
 字符串对象是“不可变的”：它们在创建后无法更改。 看起来是在修改字符串的所有 <xref:System.String> 方法和 C# 运算符实际上都是在新的字符串对象中返回结果。 在下面的示例中，当 `s1` 和 `s2` 的内容被串联在一起以形成单个字符串时，两个原始字符串没有被修改。 `+=` 运算符创建一个新的字符串，其中包含组合的内容。 这个新对象被分配给变量 `s1`，而分配给 `s1` 的原始对象被释放，以供垃圾回收，因为没有任何其他变量包含对它的引用。  
  
 [!code-cs[csProgGuideStrings#2](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_2.cs)]  
  
 由于字符串“modification”实际上是一个新创建的字符串，因此，必须在创建对字符串的引用时使用警告。 如果创建了字符串的引用，然后“修改”了原始字符串，则该引用将继续指向原始对象，而非指向修改字符串时所创建的新对象。 以下代码阐释了此行为：  
  
 [!code-cs[csProgGuideStrings#25](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_3.cs)]  
  
 有关如何创建基于修改的新字符串的详细信息，例如原始字符串上的搜索和替换操作，请参阅[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)。  
  
## <a name="regular-and-verbatim-string-literals"></a>常规和逐字字符串文本  
 在必须嵌入 C# 提供的转义字符时，使用常规字符串文本，如以下示例所示：  
  
 [!code-cs[csProgGuideStrings#3](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_4.cs)]  
  
 当字符串文本包含反斜杠字符（例如在文件路径中）时，出于便捷性和更强的可读性的考虑，使用逐字字符串。 由于逐字字符串将新的行字符作为字符串文本的一部分保留，因此可将其用于初始化多行字符串。 使用双引号在逐字字符串内部嵌入引号。 下面的示例演示逐字字符串的一些常见用法：  
  
 [!code-cs[csProgGuideStrings#4](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_5.cs)]  
  
## <a name="string-escape-sequences"></a>字符串转义序列  
  
|转义序列|字符名称|Unicode 编码|  
|---------------------|--------------------|----------------------|  
|\\'|单引号|0x0027|  
|\\"|双引号|0x0022|  
|\\\\ |反斜杠|0x005C|  
|\0|null|0x0000|  
|\a|警报|0x0007|  
|\b|Backspace|0x0008|  
|\f|换页|0x000C|  
|\n|换行|0x000A|  
|\r|回车|0x000D|  
|\t|水平制表符|0x0009|  
|\U|代理项对的 Unicode 转义序列。|\Unnnnnnnn|  
|\u|Unicode 转义序列|\u0041 = "A"|  
|\v|垂直制表符|0x000B|  
|\x|除长度可变外，Unicode 转义序列与“\u”类似。|\x0041 = "A"|  
  
> [!NOTE]
>  在编译时，逐字字符串被转换为普通字符串，并具有所有相同的转义序列。 因此，如果在调试器监视窗口中查看逐字字符串，将看到由编译器添加的转义字符，而不是来自你的源代码的逐字字符串版本。 例如，逐字字符串 @"C:\files.txt" 在监视窗口中显示为 "C:\\\files.txt"。  
  
## <a name="format-strings"></a>格式字符串  
 格式字符串是可以在运行时以动态方式确定其内容的字符串。 使用静态 <xref:System.String.Format%2A> 方法，并在大括号中嵌入将在运行时被其他值替换的占位符，从而创建格式字符串。 下面的示例使用格式字符串来输出每个循环迭代的结果：  
  
 [!code-cs[csProgGuideStrings#26](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_6.cs)]  
  
 <xref:System.Console.WriteLine%2A> 方法的一个重载将格式字符串用作参数。 因此，可以仅嵌入格式字符串文本，而无需显式调用该方法。 不过，如果使用 <xref:System.Diagnostics.Trace.WriteLine%2A> 方法在 Visual Studio“输出”窗口中显示调试输出，必须显式调用 <xref:System.String.Format%2A> 方法，因为 <xref:System.Diagnostics.Trace.WriteLine%2A> 仅接受字符串，而不接受格式字符串。 有关格式字符串的详细信息，请参阅[格式设置类型](../../../standard/base-types/formatting-types.md)。  
  
## <a name="substrings"></a>子字符串  
 子字符串是包含在字符串中的任何字符序列。 使用 <xref:System.String.Substring%2A> 方法可以通过原始字符串的一部分新建字符串。 可以使用 <xref:System.String.IndexOf%2A> 方法搜索一次或多次出现的子字符串。 使用 <xref:System.String.Replace%2A> 方法可以将出现的所有指定子字符串替换为新字符串。 与 <xref:System.String.Substring%2A> 方法一样，<xref:System.String.Replace%2A> 实际返回的是新字符串，且不修改原始字符串。 有关详细信息，请参阅[如何：使用字符串方法搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md)和[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)。  
  
 [!code-cs[csProgGuideStrings#7](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_7.cs)]  
  
## <a name="accessing-individual-characters"></a>访问单个字符  
 可以使用包含索引值的数组表示法来获取对单个字符的只读访问权限，如下面的示例中所示：  
  
 [!code-cs[csProgGuideStrings#9](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_8.cs)]  
  
 如果 <xref:System.String> 方法不提供修改字符串中的各个字符所需的功能，可以使用 <xref:System.Text.StringBuilder> 对象“就地”修改各个字符，再新建字符串来使用 <xref:System.Text.StringBuilder> 方法存储结果。 在下面的示例中，假定必须以特定方式修改原始字符串，然后存储结果以供未来使用：  
  
 [!code-cs[csProgGuideStrings#8](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_9.cs)]  
  
## <a name="null-strings-and-empty-strings"></a>Null 字符串和空字符串  
 空字符串是包含零个字符的 <xref:System.String?displayProperty=fullName> 对象实例。 空字符串常用在各种编程方案中，表示空文本字段。 可以对空字符串调用方法，因为它们是有效的 <xref:System.String?displayProperty=fullName> 对象。 对空字符串进行了初始化，如下所示：  
  
```  
string s = String.Empty;  
```  
  
 相比较而言，null 字符串并不指 <xref:System.String?displayProperty=fullName> 对象实例，只要尝试对 null 字符串调用方法，都会引发 <xref:System.NullReferenceException>。 但是，可以在串联和与其他字符串的比较操作中使用 null 字符串。 以下示例说明了对 null 字符串的引用会引发和不会引发意外的某些情况：  
  
 [!code-cs[csProgGuideStrings#27](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_10.cs)]  
  
## <a name="using-stringbuilder-for-fast-string-creation"></a>使用 StringBuilder 快速创建字符串  
 .NET 中的字符串操作进行了高度的优化，在大多数情况下不会显著影响性能。 但是，在某些情况下（例如，执行数百次或数千次的紧密循环），字符串操作可能影响性能。 <xref:System.Text.StringBuilder> 类创建字符串缓冲区，用于在程序执行多个字符串操控时提升性能。 使用 <xref:System.Text.StringBuilder> 字符串，还可以重新分配各个字符，而内置字符串数据类型则不支持这样做。 例如，此代码更改字符串的内容，而无需创建新的字符串：  
  
 [!code-cs[csProgGuideStrings#20](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_11.cs)]  
  
 在以下示例中，<xref:System.Text.StringBuilder> 对象用于通过一组数字类型创建字符串：  
  
 [!code-cs[csProgGuideStrings#15](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_12.cs)]  
  
## <a name="strings-extension-methods-and-linq"></a>字符串、扩展方法和 LINQ  
 由于 <xref:System.String> 类型实现 <xref:System.Collections.Generic.IEnumerable%601>，因此可以对字符串使用 <xref:System.Linq.Enumerable> 类中定义的扩展方法。 为了避免视觉干扰，这些方法已从 <xref:System.String> 类型的 IntelliSense 中排除，但它们仍然可用。 此外，还可以使用字符串上的 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式。 有关详细信息，请参阅 [LINQ 和字符串](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)。  
  
## <a name="related-topics"></a>相关主题  
  
|主题|描述|  
|-----------|-----------------|  
|[如何：修改字符串内容](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)|提供了演示如何修改字符串内容的代码示例。|  
|[如何：串联多个字符串](../../../csharp/programming-guide/strings/how-to-concatenate-multiple-strings.md)|阐释如何使用 `+` 运算符和 `Stringbuilder` 类在编译时和运行时将字符串连接在一起。|  
|[如何：比较字符串](../../../csharp/programming-guide/strings/how-to-compare-strings.md)|演示如何执行字符串的序号比较。|  
|[如何：使用 String.Split 分析字符串](../../../csharp/programming-guide/strings/how-to-parse-strings-using-string-split.md)|包含一个代码示例，演示了如何使用 `String.Split` 方法来分析字符串。|  
|[如何：使用字符串方法搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md)|介绍如何使用特定方法来搜索字符串。|  
|[如何：使用正则表达式搜索字符串](../../../csharp/programming-guide/strings/how-to-search-strings-using-regular-expressions.md)|介绍如何使用正则表达式来搜索字符串。|  
|[如何：确定字符串是否表示数值](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)|演示如何安全地分析一个字符串，以查看其是否具有有效的数值。|  
|[如何：将字符串转换为 DateTime](../../../csharp/programming-guide/strings/how-to-convert-a-string-to-a-datetime.md)|展示了如何将字符串（如“01/24/2008”）转换为 <xref:System.DateTime?displayProperty=fullName> 对象。|  
|[基本字符串操作](https://msdn.microsoft.com/library/a292he7t)|收录了介绍如何使用 <xref:System.String?displayProperty=fullName> 和 <xref:System.Text.StringBuilder?displayProperty=fullName> 方法执行基本字符串操作的主题链接。|  
|[分析字符串](https://msdn.microsoft.com/library/b4w53z0y)|介绍如何将字符或空格插入到字符串中。|  
|[比较字符串](https://msdn.microsoft.com/library/fbh501kz)|包括有关如何比较字符串的信息，并提供 C# 和 Visual Basic 中的示例。|  
|[使用 StringBuilder 类](../../../standard/base-types/stringbuilder.md)|介绍了如何使用 <xref:System.Text.StringBuilder> 类创建和修改动态字符串对象。|  
|[LINQ 和字符串](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)|提供有关如何使用 LINQ 查询来执行各种字符串操作的信息。|  
|[C# 编程指南](../../../csharp/programming-guide/index.md)|提供介绍在 C# 中编程构造的主题的链接。|  

