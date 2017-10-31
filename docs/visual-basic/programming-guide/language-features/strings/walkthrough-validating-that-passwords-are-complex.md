---
title: "验证密码复杂性 (Visual Basic 中) |Microsoft 文档"
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
helpviewer_keywords:
- String data type, validation
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
caps.latest.revision: 17
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e899900d60bddb83fb640abcc7f11f333c1af870
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-validating-that-passwords-are-complex-visual-basic"></a>演练：验证密码是否复杂 (Visual Basic)
此方法检查某些强密码特征，并使用哪些检查密码失败的信息更新的字符串参数。  
  
 密码可以在一个安全的系统，用于对用户授权。 但是，密码必须是未经授权的用户猜测困难。 攻击者可以使用*字典攻击*的程序，该循环访问所有字典 （或多个不同的语言字典） 中的单词，并测试是否有任何单词就是用户的密码。 例如，"杨基棒球队"或"Mustang"弱密码可以快速猜到。 更强的密码，如"？您L1N3vaFiNdMeyeP@sSWerd！"，也更不容易被猜到。 受密码保护的系统应确保用户选择强密码。  
  
 强密码很复杂 （包含大写、 小写字母、 数字和特殊字符的组合），不是一个单词。 此示例演示如何验证复杂性。  
  
## <a name="example"></a>示例  
  
### <a name="code"></a>代码  
 [!code-vb[VbVbcnRegEx #&1;](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/walkthrough-validating-that-passwords-are-complex_1.vb)]  
  
## <a name="compiling-the-code"></a>编译代码  
 调用此方法通过传递包含该密码的字符串。  
  
 此示例需要：  
  
-   对成员的访问<xref:System.Text.RegularExpressions>命名空间。</xref:System.Text.RegularExpressions> 添加`Imports`如果在代码中的成员名称不完全限定，您需要的语句。 有关详细信息，请参阅 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
## <a name="security"></a>安全性  
 如果在通过网络迁移密码，您需要使用安全的方法来传输数据。 有关详细信息，请参阅[ASP.NET Web 应用程序安全性](https://msdn.microsoft.com/library/330a99hc)。  
  
 您可以提高准确性`ValidatePassword`通过添加额外的复杂性检查函数︰  
  
-   将密码和针对用户的名称、 用户标识符和应用程序定义的字典及其子字符串进行比较。 在执行比较此外，将看上去很相似字符视为等效。 例如，将字母"l"和"e"视为等效于数字"1"和"3"。  
  
-   如果只有一个大写字符，请确保它不是第一个字符的密码。  
  
-   请确保密码的最后两个字符的字母字符。  
  
-   不允许从键盘上的首行输入所有符号的密码。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Text.RegularExpressions.Regex></xref:System.Text.RegularExpressions.Regex>   
 [ASP.NET Web 应用程序安全性](https://msdn.microsoft.com/library/330a99hc)
