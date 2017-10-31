---
title: "/verbose |Microsoft 文档"
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
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
caps.latest.revision: 11
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
ms.openlocfilehash: f6d8a8b914ccffff72128bbc907482816b95b8a0
ms.lasthandoff: 03/13/2017

---
# <a name="verbose"></a>/verbose
使编译器来生成详细的状态和错误消息。  
  
## <a name="syntax"></a>语法  
  
```  
/verbose[+ | -]  
```  
  
## <a name="arguments"></a>参数  
 `+` &#124; `-`  
 可选。 指定`/verbose`相当于将指定`/verbose+`，这将导致编译器发出详细消息。 此选项的默认值是`/verbose-`。  
  
## <a name="remarks"></a>备注  
 `/verbose`选项显示有关由编译器发出的错误总数的信息、 报告哪些程序集正在加载的模块，并显示当前正在编译的文件。  
  
> [!NOTE]
>  `/verbose`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`并指示编译器以显示详细的状态信息。  
  
```  
vbc /verbose in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
