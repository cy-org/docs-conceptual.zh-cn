---
title: "/reference (Visual Basic 中) |Microsoft 文档"
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
- /reference compiler option [Visual Basic]
- r compiler option [Visual Basic]
- -reference compiler option [Visual Basic]
- /r compiler option [Visual Basic]
- reference compiler option [Visual Basic]
- -r compiler option [Visual Basic]
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
caps.latest.revision: 16
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
ms.openlocfilehash: 12344dba82131d6be2c32127de287a6e9e3efa39
ms.lasthandoff: 03/13/2017

---
# <a name="reference-visual-basic"></a>/reference (Visual Basic)
使编译器将在指定的程序集的类型信息提供给当前正在编译项目。  
  
## <a name="syntax"></a>语法  
  
```  
/reference:fileList  
' -or-  
/r:fileList  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`fileList`|必需。 程序集文件名称的以逗号分隔列表。 如果文件名包含空格，则将名称括在引号内。|  
  
## <a name="remarks"></a>备注  
 在导入的文件必须包含程序集元数据。 仅将公共类型是在程序集外部可见的。 [/Addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)选项从模块导入元数据。  
  
 如果引用的程序集 （程序集 A） 其本身引用另一个程序集 (程序集 B)，如果需要引用程序集 B:  
  
-   程序集 A 中的类型继承自的类型或实现程序集 B 中的接口  
  
-   字段、 属性、 事件或程序集 B 中的返回类型或形参类型的方法被调用。  
  
 使用[/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)若要指定一个或多个程序集引用所在的目录。  
  
 编译器无法识别出的程序集 （而不是模块） 的类型，必须将它强制要解析的类型。 如何执行此操作的一个示例是定义类型的实例。 其他方法是可用于解析编译器的程序集中的类型名称。 例如，如果您从程序集中的类型继承，类型名称则将成为已知给编译器。  
  
 Vbc.rsp 响应文件引用常用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集，默认情况下使用。 使用`/noconfig`如果不希望使用 Vbc.rsp 的编译器。  
  
 缩写形式`/reference`是`/r`。  
  
## <a name="example"></a>示例  
 下面的代码编译源代码文件我`nput.vb`和引用程序集从 M`etad1.dll`和 M`etad2.dll`以生成 O`ut.exe`。  
  
```  
vbc /reference:metad1.dll,metad2.dll /out:out.exe input.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [公共](../../../visual-basic/language-reference/modifiers/public.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
