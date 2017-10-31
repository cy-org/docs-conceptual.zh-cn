---
title: "加密和解密在 Visual Basic 中的字符串 |Microsoft 文档"
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
- encryption, strings
- strings [Visual Basic], encrypting
- decryption, strings
- strings [Visual Basic], decrypting
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ae3d599f7173162c07fbaeda60435615f101b10d
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-encrypting-and-decrypting-strings-in-visual-basic"></a>演练：在 Visual Basic 中对字符串进行加密和解密
本演练演示如何使用<xref:System.Security.Cryptography.DESCryptoServiceProvider>类来加密和解密使用加密服务提供程序 (CSP) 版本的三重数据加密标准字符串 (<xref:System.Security.Cryptography.TripleDES>) 算法。</xref:System.Security.Cryptography.TripleDES> </xref:System.Security.Cryptography.DESCryptoServiceProvider> 第一步是创建一个简单的包装类，它封装 3DES 算法，并将已加密的数据存储为 base 64 编码的字符串。 然后，该包装用于安全地将私人用户数据存储在可公开访问的文本文件。  
  
 可以使用加密来保护用户的机密信息 （如密码） 并进行未经授权的用户无法读取凭据。 这样可防止授权的用户的标识从此被盗用、 它保护用户的资产并提供不可否认性。 加密还可保护用户的数据不被未经授权的用户的访问。  
  
 有关详细信息，请参阅[加密服务](http://msdn.microsoft.com/library/f96284bc-7b73-44b5-ac59-fac613ad09f8)。  
  
> [!IMPORTANT]
>  Rijndael （现在称为高级加密标准 [AES]） 和三重数据加密标准 (3DES) 算法提供更高的安全性比 DES，因为它们是多个计算密集型操作。 有关详细信息，请参阅<xref:System.Security.Cryptography.DES>和<xref:System.Security.Cryptography.Rijndael>。</xref:System.Security.Cryptography.Rijndael> </xref:System.Security.Cryptography.DES>  
  
### <a name="to-create-the-encryption-wrapper"></a>若要创建加密包装器  
  
1.  创建`Simple3Des`类来封装的加密和解密的方法。  
  
     [!code-vb[VbVbalrStrings #&38;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_1.vb)]  
  
2.  将加密命名空间导入添加到包含的文件的起始位置`Simple3Des`类。  
  
     [!code-vb[VbVbalrStrings #&77;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_2.vb)]  
  
3.  在`Simple3Des`类，添加一个私有字段来存储 3DES 加密服务提供程序。  
  
     [!code-vb[VbVbalrStrings #&39;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_3.vb)]  
  
4.  添加一个从指定的键的哈希值创建一个指定长度的字节数组的私有方法。  
  
     [!code-vb[VbVbalrStrings #&41;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_4.vb)]  
  
5.  添加一个构造函数来初始化 3DES 加密服务提供程序。  
  
     `key`参数控制`EncryptData`和`DecryptData`方法。  
  
     [!code-vb[VbVbalrStrings #&40;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_5.vb)]  
  
6.  添加对字符串进行加密的公共方法。  
  
     [!code-vb[VbVbalrStrings #&42;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_6.vb)]  
  
7.  添加对字符串进行解密的公共方法。  
  
     [!code-vb[VbVbalrStrings #&43;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_7.vb)]  
  
     包装类现在可以用于保护用户的资产。 在本示例中，它用于安全地将私人用户数据存储在可公开访问的文本文件。  
  
### <a name="to-test-the-encryption-wrapper"></a>若要测试加密包装器  
  
1.  在单独的类中，添加一个方法来使用该包装`EncryptData`方法加密字符串，并将其写入到用户的我的文档文件夹。  
  
     [!code-vb[VbVbalrStrings #&78;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_8.vb)]  
  
2.  添加从用户读取加密的字符串的方法的我的文档文件夹并使用包装器的字符串解密`DecryptData`方法。  
  
     [!code-vb[VbVbalrStrings #&79;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_9.vb)]  
  
3.  添加用户界面代码以调用`TestEncoding`和`TestDecoding`方法。  
  
4.  运行该应用程序。  
  
     测试应用程序时，请注意它将解密的数据，是否提供了错误的密码。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Security.Cryptography></xref:System.Security.Cryptography>   
 <xref:System.Security.Cryptography.DESCryptoServiceProvider></xref:System.Security.Cryptography.DESCryptoServiceProvider>   
 <xref:System.Security.Cryptography.DES></xref:System.Security.Cryptography.DES>   
 <xref:System.Security.Cryptography.TripleDES></xref:System.Security.Cryptography.TripleDES>   
 <xref:System.Security.Cryptography.Rijndael></xref:System.Security.Cryptography.Rijndael>   
 [加密服务](http://msdn.microsoft.com/library/f96284bc-7b73-44b5-ac59-fac613ad09f8)
