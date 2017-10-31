---
title: "疑难解答：读取和写入文本文件 (Visual Basic)"
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
- troubleshooting file I/O
- writing text to files, troubleshooting
- troubleshooting Visual Basic, text files
- I/O [Visual Basic], troubleshooting text files
- writing to files, troubleshooting
- reading text files, troubleshooting
ms.assetid: a8e9b44d-facb-4718-8c0f-466537171182
caps.latest.revision: 10
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
ms.openlocfilehash: 7f1d26df53445ee9711ebb2840071d2560c5380d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="troubleshooting-reading-from-and-writing-to-text-files-visual-basic"></a>疑难解答：读取和写入文本文件 (Visual Basic)
本主题讨论处理文本文件时遇到的常见问题，并针对每个问题提供建议解决方法。  
  
## <a name="common-problems"></a>常见问题  
 处理文本文件时遇到的最常见问题包括安全异常、文件编码和无效路径。  
  
### <a name="security-exceptions"></a>安全异常  
 安全错误发生时引发 <xref:System.Security.SecurityException>。 这通常是由用户缺少必要权限导致的，通过添加权限或者在独立存储中处理文件可以解决该问题。  
  
### <a name="file-encodings"></a>文件编码  
 文件编码也称为字符编码，用于指定在处理文本时如何表示字符。 文本文件中的意外字符可能是由于不正确的编码导致的。 对于大多数文件，一种编码可能优于另一种编码主要取决于它能处理或不能处理哪些语言字符，不过通常首选的是 Unicode。 有关详细信息，请参阅[文件编码](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)和 <xref:System.Text.Encoding>。  
  
### <a name="incorrect-paths"></a>错误路径  
 分析文件路径尤其是相对路径时，很容易提供错误的数据。 请确保提供正确的路径，这样可以纠正许多问题。 有关详细信息，请参阅[如何：分析文件路径](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)   
 [使用 TextFieldParser 对象分析文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)

