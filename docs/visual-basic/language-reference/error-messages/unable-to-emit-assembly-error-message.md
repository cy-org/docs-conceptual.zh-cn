---
title: "无法发出程序集︰&lt;错误信息&gt;|Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30145
- bc30145
dev_langs:
- VB
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
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
ms.openlocfilehash: dac4b133882c043f9c84e936bad2e36f35fc4c33
ms.lasthandoff: 03/13/2017

---
# <a name="unable-to-emit-assembly-lterror-messagegt"></a>无法发出程序集︰&lt;错误消息&gt;
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器调用程序集链接器 (Al.exe，也称作 Alink) 生成的程序集与一个清单，而该链接器创建程序集的发出阶段报告一个错误。  
  
 **错误 ID:** BC30145  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查引用的错误信息并参考主题[Al.exe 工具错误和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)的进一步解释和建议。  
  
2.  请尝试手动签名程序集使用[Al.exe （程序集链接器）](https://msdn.microsoft.com/library/c405shex)或[Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)。  
  
3.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
### <a name="to-sign-the-assembly-manually"></a>手动对程序集进行签名  
  
1.  使用[Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)创建公钥/私钥对文件。  
  
     此文件的扩展名为 .snk。  
  
2.  从项目中删除生成错误的 COM 引用。  
  
3.  从 Windows**启动**菜单上，指向**程序**，指向**Microsoft Visual Studio 2008**，指向**Visual Studio Tools**，然后单击**Visual Studio 2008 命令提示**。  
  
4.  移动到要放置程序集包装的目录。  
  
5.  键入以下代码。  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     下面是你可能会输入的代码的示例。  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     如果路径或文件包含空格，则使用双引号 (")。  
  
6.  在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 中，添加对刚创建的文件的 .NET 程序集引用。  
  
## <a name="see-also"></a>另请参阅  
 [Al.exe （程序集链接器）](https://msdn.microsoft.com/library/c405shex)   
 [Al.exe 工具错误和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)   
 [如何：创建公钥/私钥对](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)   
 [与我们交流](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
