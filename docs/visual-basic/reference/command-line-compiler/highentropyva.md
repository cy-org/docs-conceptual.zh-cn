---
title: "/highentropyva (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
caps.latest.revision: 12
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
ms.openlocfilehash: 34987930b3afd6d95d12190172a5a5e512106f8a
ms.lasthandoff: 03/13/2017

---
# <a name="highentropyva-visual-basic"></a>/highentropyva (Visual Basic)
指示是否是 64 位可执行文件或可执行文件标记的[/platform:anycpu](../../../visual-basic/reference/command-line-compiler/platform.md)编译器选项支持高熵地址空间布局随机化 (ASLR)。  
  
## <a name="syntax"></a>语法  
  
```  
/highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>参数  
 `+` &#124; `-`  
 可选。 选项默认情况下处于关闭状态，或者您指定`/highentropyva-`。 如果您指定该选项位于`/highentropyva`或`/highentropyva+`。  
  
## <a name="remarks"></a>备注  
 如果指定此选项，Windows 内核的兼容版本可以使用更高程度的熵 aslr 内核随机排列的进程的地址空间布局时。 如果内核使用更高程度的熵，则可以向内存区域，例如堆栈或堆分配更多的地址。 因此，猜测特定内存区域的位置会更加困难。  
  
 在选项上处于打开状态，目标可执行文件和任何模块时它所依赖的必须能够处理这些模块作为 64 位进程运行时大于 4 千兆字节 (GB) 的指针值。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
