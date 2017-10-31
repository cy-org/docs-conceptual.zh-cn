---
title: "/codepage (Visual Basic 中) |Microsoft 文档"
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
- /codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
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
ms.openlocfilehash: 90dce6e34e52862807e2acdbf1850699316730d1
ms.lasthandoff: 03/13/2017

---
# <a name="codepage-visual-basic"></a>/codepage (Visual Basic)
指定要用于编译中所有源代码文件的代码页。  
  
## <a name="syntax"></a>语法  
  
```  
/codepage:id  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`id`|必需。 编译器将使用指定的代码页`id`解释源代码文件的编码。|  
  
## <a name="remarks"></a>备注  
 若要编译使用特定的编码保存的源代码，可以使用`/codepage`可指定应使用哪个代码页。 `/codepage`选项适用于在编译中的所有源代码文件。 有关详细信息，请参阅[.NET Framework 中的字符编码](http://msdn.microsoft.com/library/bf6d9823-4c2d-48af-b280-919c5af66ae9)。  
  
 `/codepage`如果源代码文件均已保存签名中使用的当前 ANSI 代码页、 Unicode 或 utf-8，则不需要选项。 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]保存所有源代码文件的当前 ANSI 代码页与默认情况下，除非用户指定了另一个编码中**编码**对话框。 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]使用**编码**对话框中，若要打开用不同的代码页保存的源代码文件。  
  
> [!NOTE]
>  `/codepage`选项不是可从[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]开发环境中; 只有当从命令行进行编译，它才可用。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)
