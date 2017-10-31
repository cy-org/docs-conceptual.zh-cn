---
title: "如何：使用正则表达式搜索字符串（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- searching strings [C#]
- strings [C#], searching with RegEx
ms.assetid: dcab2150-a4a2-4fe4-87e3-83b83b58d84a
caps.latest.revision: 19
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
ms.openlocfilehash: fb05d1702c75be8fd224ee0f34d7d8d3fe71f207
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-search-strings-using-regular-expressions-c-programming-guide"></a>如何：使用正则表达式搜索字符串（C# 编程指南）
<xref:System.Text.RegularExpressions.Regex?displayProperty=fullName> 类可用于搜索字符串。 从简单搜索到充分利用正则表达式，搜索可以采用不同的复杂模式。 以下是使用 <xref:System.Text.RegularExpressions.Regex> 类执行字符串搜索的两个示例。 有关详细信息，请参阅 [.NET Framework 正则表达式](https://msdn.microsoft.com/library/hs600312)。  
  
## <a name="example"></a>示例  
 以下代码是一个控制台应用程序，用于在数组中执行不区分大小写的简单字符串搜索。 静态方法 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> 执行已给定要搜索的字符串和包含搜索模式的字符串的搜索。 在这种情况下，第三个参数将用于指示应忽略大小写。 有关更多信息，请参见<xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>。  
  
 [!code-cs[csProgGuideStrings#17](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-search-strings-using-regular-expressions_1.cs)]  
  
## <a name="example"></a>示例  
 以下代码是一个控制台应用程序，可使用正则表达式验证数组中每个字符串的格式。 验证要求每个字符串采用电话号码的形式：用短划线分隔成三组数字，前两组包含 3 个数字，而第三组包含 4 个数字。 使用正则表达式 `^\\d{3}-\\d{3}-\\d{4}$` 可以实现此操作。 有关更多信息，请参见[正则表达式语言 - 快速参考](http://msdn.microsoft.com/library/930653a6-95d2-4697-9d5a-52d11bb6fd4c)。  
  
 [!code-cs[csProgGuideStrings#18](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-search-strings-using-regular-expressions_2.cs)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [.NET Framework 正则表达式](https://msdn.microsoft.com/library/hs600312)   
 [正则表达式语言 - 快速参考](http://msdn.microsoft.com/library/930653a6-95d2-4697-9d5a-52d11bb6fd4c)

