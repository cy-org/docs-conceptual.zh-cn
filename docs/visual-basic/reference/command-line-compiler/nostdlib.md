---
title: "/nostdlib (Visual Basic 中) |Microsoft 文档"
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
- nostdlib compiler option [Visual Basic]
- -nostdlib compiler option [Visual Basic]
- /nostdlib compiler option [Visual Basic]
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
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
ms.openlocfilehash: 3bacd7d51d12ec6c48dc11ff4b83d842a9e78a30
ms.lasthandoff: 03/13/2017

---
# <a name="nostdlib-visual-basic"></a>/nostdlib (Visual Basic)
使编译器不会自动引用标准库。  
  
## <a name="syntax"></a>语法  
  
```  
/nostdlib  
```  
  
## <a name="remarks"></a>备注  
 `/nostdlib`选项删除对 System.dll 程序集的自动引用，可防止编译器读取 Vbc.rsp 文件。 Vbc.rsp 文件 — — 位于 Vbc.exe 文件所在的同一个目录 — 引用常用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集和导入`System`和`Microsoft.VisualBasic`命名空间。  
  
> [!NOTE]
>  始终引用 Mscorlib.dll 和 Microsoft.VisualBasic.dll 的程序集。  
  
> [!NOTE]
>  `/nostdlib`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`而不引用标准库。 必须设置`_MYTYPE`为字符串"空"若要删除的条件编译常数`My`对象。  
  
```  
vbc /nostdlib /define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [自定义 My 中可用的对象](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
