---
title: "如何：在旧式编码与 Unicode 之间转换（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- conversions [C#], legacy to unicode encoding
- strings [C#], converting between encodings
ms.assetid: 4eed7d8e-47ab-4a7c-8b95-9645a0ef000b
caps.latest.revision: 11
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
ms.openlocfilehash: a016f4ab7de25eec408243cb9b467f9255556bba
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-convert-between-legacy-encodings-and-unicode-c-programming-guide"></a>如何：在旧式编码与 Unicode 之间转换（C# 编程指南）
在 C# 中，内存中的所有字符串都被编码为 Unicode (UTF-16)。 将数据从存储加入到 `string` 对象时，数据将被自动转换为 UTF-16。 如果数据仅包含从 0 到 127 的 ASCII 值，则无需其他操作即可转换。 但是，如果源文本包含扩展的 ASCII 字节值（从 128 到 255），则将默认根据当前代码页解释扩展字符。 若要指定应根据其他代码页解释源文本，请使用 <xref:System.Text.Encoding?displayProperty=fullName> 类，如以下示例所示。  
  
## <a name="example"></a>示例  
 以下示例演示如何转换在 8 位 ASCII 中编码的文本文件，根据 Windows 代码页 737 解释源文本。  
  
 [!code-cs[csProgGuideStrings#34](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-between-legacy-encodings-and-unicode_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [字符串](../../../csharp/programming-guide/strings/index.md)

