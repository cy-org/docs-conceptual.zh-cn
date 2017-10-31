---
title: "如何：将 RTF 转换为纯文本（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], converting from RTF
ms.assetid: 3b386a87-899d-4d98-bc82-a980526ddaac
caps.latest.revision: 21
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
ms.openlocfilehash: 9e4c7b48467f3b260526c604fa3a36fc5d80374e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-convert-rtf-to-plain-text-c-programming-guide"></a>如何：将 RTF 转换为纯文本（C# 编程指南）
RTF 格式 (RTF) 是 Microsoft 在 20 世纪 80 年代末开发的一种文档格式，允许跨操作系统交换文档。 Microsoft Word 和写字板均可读取和写入 RTF 文档。 在 .NET Framework 中，可以使用 <xref:System.Windows.Forms.RichTextBox> 控件创建一个支持 RTF 并使用户能够以一种所见即所得的方式将格式应用于文本的 word 处理器。  
  
 还可以使用 <xref:System.Windows.Forms.RichTextBox> 控件以编程方式从文档中删除 RTF 格式代码，并将其转换为纯文本。 无需将控件嵌入 Windows 窗体即可执行这种类型的操作。  
  
### <a name="to-use-the-richtextbox-control-in-a-project"></a>在项目中使用 RichTextBox 控件  
  
1.  添加对 System.Windows.Forms.dll 的引用。  
  
2.  为 `System.Windows.Forms` 命名空间添加一条 using 指令（可选）。  
  
## <a name="example"></a>示例  
 以下示例将示例 RTF 文件转换为纯文本。 该文件包含 RTF 格式（如字体信息）、四个 Unicode 字符和四个扩展的 ASCII 字符。 此示例代码打开文件，将其内容传递到 <xref:System.Windows.Forms.RichTextBox> 作为 RTF，检索内容作为文本，在 <xref:System.Windows.Forms.MessageBox> 中显示文本，并将文本输出到 UTF-8 格式的文件。  
  
 `MessageBox` 和输出文件包含以下文本：  
  
```  
The Greek word for "psyche" is spelled ψυχή. The Greek letters are encoded in Unicode.  
These characters are from the extended ASCII character set (Windows code page 1252):  âäӑå  
```  
  
 [!code-cs[csProgGuideStrings#33](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-rtf-to-plain-text_1.cs)]  
  
 RTF 字符以八位为单位进行编码。 但是，除了指定代码页中的扩展的 ASCII 字符外，用户还可以指定 Unicode 字符。 因为 <xref:System.Windows.Forms.RichTextBox.Text%2A?displayProperty=fullName> 属性的类型为[字符串](../../../csharp/language-reference/keywords/string.md)，因此字符被编码为 Unicode UTF-16。 来自源 RTF 文档的任何扩展的 ASCII 字符和 Unicode 字符均在文本输出中进行了正确编码。  
  
 如果使用 <xref:System.IO.File.WriteAllText%2A?displayProperty=fullName> 方法将文本写入到磁盘，则文本将被编码为 UTF-8（无字节顺序标记）。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.RichTextBox?displayProperty=fullName>   
 [字符串](../../../csharp/programming-guide/strings/index.md)

