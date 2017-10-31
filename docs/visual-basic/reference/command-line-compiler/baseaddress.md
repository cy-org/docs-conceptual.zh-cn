---
title: "/baseaddress |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /baseaddress
- baseaddress
dev_langs:
- VB
helpviewer_keywords:
- -baseaddress compiler option [Visual Basic]
- /baseaddress compiler option [Visual Basic]
- baseaddress compiler option [Visual Basic]
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
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
ms.openlocfilehash: 527a7c348583498f46ee094ef9b9eec9abf1bcd0
ms.lasthandoff: 03/13/2017

---
# <a name="baseaddress"></a>/baseaddress
指定默认的基址时创建 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
/baseaddress:address  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`address`|必需。 此 DLL 的的基址。 必须将此地址指定为十六进制数。|  
  
## <a name="remarks"></a>备注  
 DLL 的默认基址将由[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]。  
  
 请注意，此地址中的较低序位字被舍入。 例如，如果指定 0x11110001，它是舍入为 0x11110000。  
  
 若要完成签名过程的 DLL，使用`–R`强命名工具 (Sn.exe) 的选项。  
  
 如果目标不是 DLL，则忽略此选项。  
  
|在 Visual Studio IDE 中设置 /baseaddress|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.单击 **“高级”**。<br />4.在修改此值**DLL 基址︰**框。 **注意︰** **DLL 基址︰**框是只读的除非目标是一个 DLL。|  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)
