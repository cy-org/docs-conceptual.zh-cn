---
title: "/filealign |Microsoft 文档"
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
- sections compiler option [Visual Basic]
- alignment compiler option [Visual Basic]
- -filealign compiler option [Visual Basic]
- section alignment
- /filealign compiler option [Visual Basic]
- filealign compiler option [Visual Basic]
ms.assetid: cc61ec3d-ad38-4b28-9659-099d73cad099
caps.latest.revision: 14
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
ms.openlocfilehash: 18d5c3e327e2e41f4786eda6c3e981125f87389d
ms.lasthandoff: 03/13/2017

---
# <a name="filealign"></a>/filealign
指定输出文件各节的对齐位置。  
  
## <a name="syntax"></a>语法  
  
```  
/filealign:number  
```  
  
## <a name="arguments"></a>参数  
 `number`  
 必需。 一个值，指定输出文件中的各节的对齐方式。 有效值为 512、 1024年、 2048年、 4096 和 8192。 这些值是以字节为单位。  
  
## <a name="remarks"></a>备注  
 您可以使用`/filealign`选项以指定输出文件中的各节的对齐方式。 节是包含代码或数据的可移植可执行文件 (PE) 文件中的连续内存块。 `/filealign`选项使您可以编译您的应用程序使用非标准的对齐方式; 大多数开发人员不需要使用此选项。  
  
 每个部分的倍数的边界上对齐`/filealign`值。 没有固定的默认值。 如果`/filealign`未指定，则编译器在编译时将选取默认值。  
  
 通过指定节的大小，可以更改输出文件的大小。 修改节的大小可能很有用的程序将在较小的设备上运行。  
  
> [!NOTE]
>  `/filealign`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)
