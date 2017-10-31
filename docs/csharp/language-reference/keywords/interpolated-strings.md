---
title: "内插字符串 (C#)"
ms.date: 2017-02-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 324f267e-1c61-431a-97ed-852c1530742d
caps.latest.revision: 9
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 29790cadd30e9aca56d7ba4c8d7a945b4f891f35
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="interpolated-strings-c-reference"></a>内插字符串（C# 参考）

用于构造字符串。  内插字符串类似于包含内插表达式的模板字符串。  内插字符串返回的字符串可替换内插表达式并且包含其字符串表示形式。  

与[复合格式字符串](../../../standard/base-types/composite-formatting.md#composite-format-string)相比，内插字符串的参数更易于理解。  例如，内插字符串  
  
```csharp  
Console.WriteLine($"Name = {name}, hours = {hours:hh}"); 
```  
包含 2 个内插表达式：“{name}”和“{hours:hh}”。 等效复合格式字符串为：

```csharp
Console.WriteLine("Name = {0}, hours = {1:hh}", name, hours);  
```  

内插字符串的结构为：  
  
```  
$"<text> {<interpolated-expression> [,<field-width>] [:<format-string>] } <text> ..."  
```  

其中： 

- *field-width* 是一个带符号整数，表示字段中的字符数。 如果为正数，则字段右对齐；如果为负数，则左对齐。 

- “格式字符串”是适合正在设置格式的对象类型的格式字符串。 例如，对于 @System.DateTime 值，它可能是标准的日期和时间格式字符串，例如“D”或“d”。

 可以在可使用字符串的任何位置使用内插字符串。  每次执行带内插字符串的代码时，都会计算内插字符串。 这有助于分隔内插字符串的定义和计算结果。  
  
 若要在内插字符串中包含大括号（“{”或“}”），请使用两个大括号，即“{{”或“}}”。  请参阅“隐式转换”部分以获取详细信息。  

如果内插字符串包含在内插字符串中具有特殊意义的其他字符，例如引号 (")、冒号 (:) 或逗号 (,)，则出现在文本中时应转义这些字符；如果它们是内插表达式中随附的语言元素，则应将其包括在由括号分隔的表达式内。 以下示例转义了引号以将其包括在结果字符串中，并使用括号来分隔表达式 `(age == 1 ? "" : "s")`，以防冒号被解读为格式字符串的开头。

[!code-cs[interpolated-strings4](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings4.cs#1)]  

## <a name="implicit-conversions"></a>隐式转换  

内插字符串有 3 种隐式类型转换：  

1. 将内插字符串转换为 @System.String。 下例返回一个字符串，其内插字符串表达式已替换为字符串表示形式。 例如: 

   [!code-cs[interpolated-strings1](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings1.cs#1)]  

   这是字符串解释的最终结果。 出现的所有双大括号（“{{”和“}}”）都转换为单大括号。 

2. 将内插字符串转换为 <xref:System.IFormattable> 变量，使用此变量可通过单个 <xref:System.IFormattable> 实例创建多个包含区域性特定内容的结果字符串。 对于包括诸如各区域性的正确数字和日期格式之类的内容，这种转换很有用。  出现的所有双大括号（“{{”和“}}”）仍保留为双大括号，直至通过显式或隐式调用 @System.Object.ToString 方法格式化字符串。  包含的所有内插表达式都转换为 {0}、{1} 等等。  

   以下示例使用反射来显示内插字符串中所创建的 <xref:System.IFormattable> 变量的成员以及字段和属性值。 并将 <xref:System.IFormattable> 变量传递给 @System.Console(System.String) 方法。

   [!code-cs[interpolated-strings2](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings2.cs#1)]  

   请注意，只能通过使用反射来检查内插字符串。 如果将其传递给字符串格式设置方法，例如 @System.Console.WriteLine(System.String)，则会解析其格式项并返回结果字符串。 

3. 将内插字符串转换为表示复合格式字符串的 <xref:System.FormattableString> 变量。 例如，检查复合格式字符串及其呈现为结果字符串的方式可能有助于在生成查询时防止注入攻击。  <xref:System.FormattableString> 还包括 <xref:System.FormattableString.ToString> 重载，可为 @System.Globalization.InvariantCulture 和 @System.Globalization.CurrentCulture 生成结果字符串。  出现的所有双大括号（“{{”和“}}”）都保留为双大括号，直至格式化。  包含的所有内插表达式都转换为 {0}、{1} 等等。  

   [!code-cs[interpolated-strings3](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings3.cs#1)]  

## <a name="language-specification"></a>语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IFormattable?displayProperty=fullName>   
 <xref:System.FormattableString?displayProperty=fullName>   
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)

