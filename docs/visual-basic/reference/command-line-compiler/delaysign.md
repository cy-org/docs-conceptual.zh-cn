---
title: "/delaysign |Microsoft 文档"
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
- delaysign compiler option [Visual Basic]
- /delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
caps.latest.revision: 19
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
ms.openlocfilehash: 59d4ec227286c20b2b4ecf749a91f0c4ee8d25ca
ms.lasthandoff: 03/13/2017

---
# <a name="delaysign"></a>/delaysign
指定程序集是完全签名的还是部分签名的。  
  
## <a name="syntax"></a>语法  
  
```  
/delaysign[+ | -]  
```  
  
## <a name="arguments"></a>参数  
 `+` &#124; `-`  
 可选。 如果需要完全签名的程序集，则使用 `/delaysign-`。 使用`/delaysign+`如果想要将公钥放在有符号哈希的程序集和保留空间。 默认值为 `/delaysign-`。  
  
## <a name="remarks"></a>备注  
 `/delaysign`选项没有任何影响，除非用于[/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)或[/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)。  
  
 在请求完全签名的程序集时，编译器进行哈希的文件，包含清单 （程序集元数据） 并使用私钥进行签名的哈希处理。 产生的数字签名存储在包含清单的文件中。 在程序集延迟签名时，编译器不会不计算，并在文件中存储的签名，但保留空间以便稍后可添加签名。  
  
 例如，通过使用`/delaysign+`，在组织中的开发人员可以分发未签名的测试版本的程序集的测试人员可以全局程序集缓存中注册和使用。 针对程序集的工作完成后，负责组织的私钥的人员可以完全签名程序集。 这种划分保护组织的私钥泄露，同时允许所有开发人员能够在程序集上。  
  
 请参阅[创建和使用具有强名称程序集](https://msdn.microsoft.com/library/xwb8f617)有关程序集进行签名的详细信息。  
  
### <a name="to-set-delaysign-in-the-visual-studio-integrated-development-environment"></a>在 Visual Studio 中设置 /delaysign 集成开发环境  
  
1.  在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**签名**选项卡。  
  
3.  中的值设置**仅延迟签名**框。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
