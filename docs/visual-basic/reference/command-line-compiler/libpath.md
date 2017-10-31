---
title: "/libpath |Microsoft 文档"
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
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
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
ms.openlocfilehash: cc534e782cff34f0c4882f3da2af973fed69ff80
ms.lasthandoff: 03/13/2017

---
# <a name="libpath"></a>/libpath
指定引用的程序集的位置。  
  
## <a name="syntax"></a>语法  
  
```  
/libpath:dirList  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`dirList`|必需。 以分号分隔的编译器进行查找的引用的程序集的目录列表中未找到任何一个当前工作目录 （调用编译器的目录） 或公共语言运行时的系统目录。 如果目录名称包含空格，则将名称括在双引号 ("")。|  
  
## <a name="remarks"></a>备注  
 `/libpath`选项指定引用的程序集的位置[/引用](../../../visual-basic/reference/command-line-compiler/reference.md)选项。  
  
 编译器将搜索未按以下顺序完全限定的程序集引用︰  
  
1.  当前工作目录。 这是从中调用编译器的目录。  
  
2.  公共语言运行时的系统目录。  
  
3.  由指定的目录`/libpath`。  
  
4.  LIB 环境变量所指定的目录。  
  
 `/libpath`选项是累加性; 指定其超过一次将追加到任何以前的值。  
  
 使用`/reference`来指定程序集引用。  
  
|在 Visual Studio 中设置 /libpath 集成开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击**引用**选项卡。<br />3.单击**引用路径...**按钮。<br />4.在**引用路径**对话框框中，输入中的目录名称**文件夹︰**框。<br />5.单击**将文件夹添加**。|  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`若要创建的.exe 文件。 对于程序集引用，则编译器查找的工作目录中、 c︰ 驱动器的根目录中和 c︰ 驱动器的新的程序集目录中。  
  
```  
vbc /libpath:c:\;"c:\New Assemblies" /reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
