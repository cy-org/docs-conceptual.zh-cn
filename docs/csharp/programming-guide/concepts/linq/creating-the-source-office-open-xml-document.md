---
title: "创建源 Office Open XML 文档 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 653c8cdb-73be-4dc2-927f-924cfb4ed9ed
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1ea055d35982e364a6b77281aca1d1b03474aa0b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-the-source-office-open-xml-document-c"></a>创建源 Office Open XML 文档 (C#)
本主题演示如何创建本教程其他示例中使用的 Office Open XML WordprocessingML 文档。 如果您按照这些说明操作，您的输出结果将与每个示例中提供的输出相匹配。  
  
 不过，本教程中的示例可以使用任何有效的 WordprocessingML 文档。  
  
 若要创建本教程使用的文档，必须安装 Microsoft Office 2007 或更高版本，或者具有 Microsoft Office Word、Excel 和 PowerPoint 2007 文件格式兼容包的 Microsoft Office 2003。  
  
## <a name="creating-the-wordprocessingml-document"></a>创建 WordprocessingML 文档  
  
#### <a name="to-create-the-wordprocessingml-document"></a>创建 WordprocessingML 文档  
  
1.  创建一个新的 Microsoft Word 文档。  
  
2.  将以下文本粘贴到新文档中：  
  
    ```  
    Parsing WordprocessingML with LINQ to XML  
  
    The following example prints to the console.  
  
    using System;  
  
    class Program {  
        public static void Main(string[] args) {  
            Console.WriteLine("Hello World");  
        }  
    }  
  
    This example produces the following output:  
  
    Hello World  
    ```  
  
3.  用“标题 1”样式格式化第一行。  
  
4.  选择包含 C# 代码的行。 第一行以 `using` 关键字开头。 最后一行是最后一个右大括号。 用 courier 字体格式化这些行。 用新样式格式化这些行并将新样式命名为“Code”。  
  
5.  最后，选择包含输出的整个行，并用 `Code` 样式格式化该行。  
  
6.  保存文档，并将其命名为 SampleDoc.docx。  
  
    > [!NOTE]
    >  如果使用的是 Microsoft Word 2003，请在“保存类型”下拉列表中选择“Word 2007 文档”。  
  
## <a name="see-also"></a>请参阅  
 [教程：操作 WordprocessingML 文档中的内容 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)

