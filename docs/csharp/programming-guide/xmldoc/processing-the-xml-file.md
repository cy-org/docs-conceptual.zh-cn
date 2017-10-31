---
title: "处理 XML 文件（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- XML processing [C#]
- XML [C#], processing
ms.assetid: 60c71193-9dac-4cd3-98c5-100bd0edcc42
caps.latest.revision: 16
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
ms.openlocfilehash: 610f3ac5c88fb41a4b55f2990fecdc4c13074e19
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="processing-the-xml-file-c-programming-guide"></a>处理 XML 文件（C# 编程指南）
编译器为代码（已标记以生成文档）中的每个构造生成一个 ID 字符串。 （有关如何标记代码的信息，请参阅[文档注释的建议标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)。）ID 字符串唯一标识构造。 处理 XML 文件的程序可以使用 ID 字符串来标识文档应用于的相应 .NET Framework 元数据/反射项目。  
  
 XML 文件不是代码的分层表示形式；它是具有每个元素生成的 ID 的简单列表。  
  
 编译器在生成 ID 字符串时应遵循以下规则：  
  
-   字符串中没有空格。  
  
-   ID 字符串的第一部分标识被标识的成员类型，单个字符后跟一个冒号。 使用下面的成员类型：  
  
    |字符|描述|  
    |---------------|-----------------|  
    |N|namespace<br /><br /> 无法将文档注释添加到命名空间中，但可以在支持的情况下对它们进行 cref 引用。|  
    |T|类型：类、接口、结构、枚举、委托|  
    |F|Field — 字段|  
    |P|属性（包括索引器或其他的索引属性）|  
    |M|方法（包括构造函数、运算符等特殊方法）|  
    |E|Event — 事件|  
    |!|错误字符串<br /><br /> 字符串的其余部分提供有关错误的信息。 C# 编译器将生成无法解析的链接的错误信息。|  
  
-   该字符串的第二部分是项目的完全限定名称，从命名空间的根开始。 用句点分隔项目名称、其封闭类型和命名空间。 如果项目名称本身包含句点，会将其替换为哈希符号 ('#')。 假定没有名称中恰好包含哈希符号的项目。 例如，String 构造函数的完全限定名称将是“System.String.#ctor”。  
  
-   对于属性和方法，如果方法带有自变量，则后跟用括号括起来的自变量列表。 如果没有任何自变量，则不会出现括号。 确保自变量之间用逗号分隔。 每个自变量的编码直接遵循它在 .NET Framework 签名中的编码方式：  
  
    -   基类型。 常规的类型（ELEMENT_TYPE_CLASS 或 ELEMENT_TYPE_VALUETYPE）表示为该类型的完全限定名称。  
  
    -   内部类型（例如，ELEMENT_TYPE_I4、ELEMENT_TYPE_OBJECT、ELEMENT_TYPE_STRING、ELEMENT_TYPE_TYPEDBYREF 和 ELEMENT_TYPE_VOID）表示为对应的完整类型的完全限定名称。 例如，System.Int32 或 System.TypedReference。  
  
    -   ELEMENT_TYPE_PTR 表示为修改类型之后的“*”。  
  
    -   ELEMENT_TYPE_BYREF 表示为修改类型之后的“@”。  
  
    -   ELEMENT_TYPE_PINNED 表示为修改类型之后的“^”。 C# 编译器不会生成此类型。  
  
    -   ELEMENT_TYPE_CMOD_REQ 表示为“&#124;”和修饰符类的完全限定名称，前面是修改类型。 C# 编译器不会生成此类型。  
  
    -   ELEMENT_TYPE_CMOD_OPT 表示为“!”和修饰符类的完全限定名称，前面是修改类型。  
  
    -   ELEMENT_TYPE_SZARRAY 表示为“[]”，前面是数组的元素类型。  
  
    -   ELEMENT_TYPE_GENERICARRAY 表示为“[?]”，前面是数组的元素类型。 C# 编译器不会生成此类型。  
  
    -   ELEMENT_TYPE_ARRAY 表示为 [*lowerbound*:`size`,*lowerbound*:`size`]，其中逗号的数量是秩 - 1，每个维度的下限和大小（如果已知）以十进制形式表示。 如果未指定下限或大小，则只需将其省略。 如果省略某个特定维度的下限和大小，也会省略“:”。 例如，以 1 作为下限并且未指定大小的二维数组是 [1:,1:]。  
  
    -   ELEMENT_TYPE_FNPTR 表示为“=FUNC:`type`(*signature*)”，其中 `type` 是返回类型，*signature* 是方法的自变量。 如果没有任何自变量，则省略括号。 C# 编译器不会生成此类型。  
  
     不表示下列签名组件，因为它们永远不会用于区分重载方法：  
  
    -   调用约定  
  
    -   返回类型  
  
    -   ELEMENT_TYPE_SENTINEL  
  
-   仅适用于转换运算符（op_Implicit 和 op_Explicit），该方法的返回值被编码为“~”，后面是返回类型，如上面的编码所示。  
  
-   对于泛型类型，类型名称后跟反勾号，然后是指示泛型类型参数数量的一个数字。  例如，  
  
     `<member name="T:SampleClass`2">` is the tag for a type that is defined as `public class SampleClass\<T, U>`.  
  
     对于将泛型类型用作参数的方法，泛型类型参数被指定为前面加上反勾号的数字（例如 \`0,`1）。  每个数字表示该类型的泛型参数的从零开始的数组表示法。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何为类及其成员生成 ID 字符串：  
  
 [!code-cs[csProgGuidePointers#21](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/processing-the-xml-file_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [/doc（C# 编译器选项）](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)

