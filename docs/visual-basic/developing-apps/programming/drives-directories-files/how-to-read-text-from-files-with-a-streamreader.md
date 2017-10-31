---
title: "如何：使用 StreamReader 读取文件中的文本 (Visual Basic)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- reading files, text
- text, reading from files
- reading text from files
- files, reading
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: d895b32b1613462a6c8dedcc19040b5040f936ec
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-read-text-from-files-with-a-streamreader-visual-basic"></a>如何：使用 StreamReader 读取文件中的文本 (Visual Basic)
`My.Computer.FileSystem` 对象提供打开 <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter> 的方法。 这些方法（`OpenTextFileWriter` 和 `OpenTextFileReader`）是高级方法，除非选择“全部”选项卡，否则它们不会出现在 IntelliSense 中。  
  
### <a name="to-read-a-line-from-a-file-with-a-text-reader"></a>使用文本读取器从文件读取一行  
  
-   使用 `OpenTextFileReader` 方法打开 <xref:System.IO.TextReader> 并指定文件。 此示例打开名为 `testfile.txt` 的文件、从中读取一行，然后在消息框中显示该行。  
  
     [!code-vb[VbFileIORead#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-text-from-files-with-a-streamreader_1.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 读取的文件必须是文本文件。  
  
 不要根据文件的名称来判断文件的内容。 例如，文件 Form1.vb 可能不是 Visual Basic 源文件。  
  
 在应用程序中使用输入的数据之前，需验证所有的输入内容。 文件的内容可能不是预期内容，并且用来读取该文件的方法可能失败。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 若要从文件中读取，程序集需要 <xref:System.Security.Permissions.FileIOPermission> 类授予的特权等级。 如果在部分信任上下文中运行，该代码可能会因特权不足而引发异常。 有关详细信息，请参阅[代码访问安全性基础知识](https://msdn.microsoft.com/library/33tceax8)。 用户还需要具有对文件的访问权限。 有关详细信息，请参阅 [ACL 技术概述](http://msdn.microsoft.com/en-us/06fbf66d-6f02-4378-b863-b2f12e349045)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:System.Windows.Forms.OpenFileDialog>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>   
 [SaveFileDialog 组件](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md)   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)

