---
title: "-baseaddress（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /dllbase
dev_langs:
- CSharp
helpviewer_keywords:
- baseaddress compiler option [C#]
- /baseaddress compiler option [C#]
- -baseaddress compiler option [C#]
ms.assetid: ce13c965-dfe4-4433-94f5-63b476e3a608
caps.latest.revision: 18
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 91193ae794957b5045a225614d6322e86d18d459
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="baseaddress-c-compiler-options"></a>/baseaddress（C# 编译器选项）
通过 /baseaddress 选项可指定加载 DLL 的首选基址。 有关为何及何时使用此选项的详细信息，请参阅[缩减应用程序启动时间](http://go.microsoft.com/fwlink/?LinkId=107043)和 [Larry Osterman 的网络日志](http://go.microsoft.com/fwlink/?LinkId=107044)。  
  
## <a name="syntax"></a>语法  
  
```console  
/baseaddress:address  
```  
  
## <a name="arguments"></a>参数  
 `address`  
 DLL 的基址。 可将此地址指定为十进制数、十六进制数或八进制数。  
  
## <a name="remarks"></a>备注  
 DLL 的默认基址由 .NET Framework 公共语言运行时设置。  
  
 请注意，此地址中的低序字将被舍入取整。 例如，如果指定 0x11110001，它将被舍入为 0x11110000。  
  
 要完成 DLL 的签名过程，请使用具有 -R 选项的 SN.EXE。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“生成”属性页。  
  
3.  单击 **“高级”** 按钮。  
  
4.  修改“DLL 基址”属性。  
  
     若要以编程方式设置此编译器选项，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.BaseAddress%2A>。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Diagnostics.ProcessModule.BaseAddress%2A?displayProperty=fullName>   
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

