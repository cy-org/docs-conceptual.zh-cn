---
title: "如何：在 Visual Basic 中将文本写入“我的文档”目录中的文件"
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
- files, writing to
- text, writing to files
- examples [Visual Basic], text files
- writing to files, in My Documents
ms.assetid: 1c726124-781d-4976-9baa-ed46814ff3fe
caps.latest.revision: 19
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
ms.openlocfilehash: c900072d184469ead75bb76a3e152edce357a34f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-write-text-to-files-in-the-my-documents-directory-in-visual-basic"></a>如何：在 Visual Basic 中将文本写入“我的文档”目录中的文件
`My.Computer.FileSystem.SpecialDirectories` 对象允许用户访问特殊目录，如 MyDocuments 目录。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-write-new-text-files-in-the-my-documents-directory"></a>在“我的文档”目录中写入新的文本文件  
  
1.  使用 `My.Computer.FileSystem.SpecialDirectories.MyDocuments` 属性提供路径。  
  
     [!code-vb[VbFileIOWrite#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_1.vb)]  
  
2.  使用 `WriteAllText` 方法将文本写入指定文件。  
  
     [!code-vb[VbVbcnMyFileSystem#14](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_2.vb)]  
  
## <a name="example"></a>示例  
 [!code-vb[VbFileIOWrite#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_3.vb)]  
  
## <a name="compiling-the-code"></a>编译代码  
 将 `test.txt` 替换为要写入的文件的名称。  
  
## <a name="robust-programming"></a>可靠编程  
 此代码会重新引发向文件写入文本时可能发生的所有异常。 可以通过使用 Windows 窗体控件（如限制用户选择有效文件名的 [OpenFileDialog](../../../../framework/winforms/controls/openfiledialog-component-windows-forms.md) 和 [SaveFileDialog](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md) 组件）减少引发异常的可能性。 但是，使用这些控件并不能做到万无一失。 文件系统可以在用户选择文件和代码执行的间隙时间内更改。 因此，处理文件时，几乎总是需要处理异常。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果在部分信任上下文中运行，该代码可能会因特权不足而引发异常。 有关详细信息，请参阅[代码访问安全性基础知识](https://msdn.microsoft.com/library/33tceax8)。  
  
 此示例创建一个新文件。 如果某个应用程序需要创建文件，则该应用程序需要文件夹的“创建”权限。 可使用访问控制列表设置权限。 如果文件已存在，则该应用程序只需要“写入”权限（这是较弱的权限）。 如有可能，在部署过程中创建文件，并且仅授予针对单个文件的“读取”权限（而不是针对文件夹授予“创建”权限）会更加安全。 此外，较安全的做法是将数据写入用户文件夹，而不是根文件夹或“Program Files”文件夹。 有关详细信息，请参阅 [ACL 技术概述](http://msdn.microsoft.com/en-us/06fbf66d-6f02-4378-b863-b2f12e349045)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IO.Path.Combine%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>

