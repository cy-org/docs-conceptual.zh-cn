---
title: "文件编码 (Visual Basic)"
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
- character encodings
- files, encoding
- Unicode, file encoding
- file encoding
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
caps.latest.revision: 8
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
ms.openlocfilehash: 6d4a12d3c6098271dad0a52a9c6799303b9fe81d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="file-encodings-visual-basic"></a>文件编码 (Visual Basic)
文件编码也称为字符编码，用于指定在处理文本时如何表示字符。 虽然 Unicode 是最常用的编码，但根据编码能否处理某种语言字符，另一种编码可能更优。  
  
 读取或写入文件时，未正确匹配文件编码可能会导致发生异常或产生不正确的结果。  
  
## <a name="types-of-encodings"></a>编码类型  
 处理文件时，Unicode 是首选编码。 Unicode 是全球范围的字符编码标准，使用 16 位代码值来表示现代计算中使用的所有字符，包括印刷中使用的技术符号和特殊字符。  
  
 以前的字符编码标准包括传统的字符集，如 Windows ANSI 字符集，该字符集使用 8 位代码值或 8 位值组合来表示特定语言或地理区域中使用的字符。  
  
## <a name="encoding-class"></a>编码类  
 <xref:System.Text.Encoding> 类表示字符编码。 下表列出并描述了每个可用的编码类型。  
  
|名称|描述|
|---|---|    
|<xref:System.Text.ASCIIEncoding>|表示 Unicode 字符的 ASCII 字符编码。|  
|<xref:System.Text.UnicodeEncoding>|表示 Unicode 字符的 UTF-16 编码。|  
|<xref:System.Text.UTF32Encoding>|表示 Unicode 字符的 UTF-32 编码。|  
|<xref:System.Text.UTF7Encoding>|表示 Unicode 字符的 UTF-7 编码。|  
|<xref:System.Text.UTF8Encoding>|表示 Unicode 字符的 UTF-8 编码。|  
  
## <a name="see-also"></a>另请参阅  
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)

