---
title: "创建源 Office Open XML 文档 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 61ccd6fb-0c47-4075-afdf-5b5021330f21
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 928a3c34836464e7603c485b64c9c426913ae7b2
ms.lasthandoff: 03/13/2017


---
# <a name="creating-the-source-office-open-xml-document-visual-basic"></a>创建源 Office Open XML 文档 (Visual Basic)
本主题演示如何创建本教程其他示例中使用的 Office Open XML WordprocessingML 文档。 如果您按照这些说明操作，您的输出结果将与每个示例中提供的输出相匹配。  
  
 不过，本教程中的示例可以使用任何有效的 WordprocessingML 文档。  
  
 若要创建本教程使用的文档，您必须或者具有 Microsoft Office 2007 或更高版本安装，或者必须使用 Microsoft Office 兼容包的 Microsoft Office 2003 的 Word、 Excel 和 PowerPoint 2007 文件格式。  
  
## <a name="creating-the-wordprocessingml-document"></a>创建 WordprocessingML 文档  
  
#### <a name="to-create-the-wordprocessingml-document"></a>创建 WordprocessingML 文档  
  
1.  创建一个新的 Microsoft Word 文档。  
  
2.  将以下文本粘贴到新文档中：  
  
    ```  
    Parsing WordprocessingML with LINQ to XML  
  
    The following example prints to the console.  
  
    Imports System  
  
    Class Program  
        Public Shared  Sub Main(ByVal args() As String)  
            Console.WriteLine("Hello World")  
        End Sub  
    End Class  
  
    This example produces the following output:  
  
    Hello World  
    ```  
  
3.  用“标题 1”样式格式化第一行。  
  
4.  选择包含 Visual Basic 代码的行。 第一行以 `Imports` 关键字开头。 最后一行是"End Class"。 用 courier 字体格式化这些行。 用新样式格式化这些行并将新样式命名为“Code”。  
  
5.  最后，选择包含输出的整个行，并用 `Code` 样式格式化该行。  
  
6.  保存文档，并将其命名为 SampleDoc.docx。  
  
    > [!NOTE]
    >  如果在使用 Microsoft Word 2003，选择**Word 2007 文档**中**另存为类型**下拉列表。  
  
## <a name="see-also"></a>另请参阅  
 [教程︰ 操作 WordprocessingML 文档 (Visual Basic 中) 中的内容](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
