---
title: "-pdb（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /pdb
dev_langs:
- CSharp
helpviewer_keywords:
- -pdb compiler option [C#]
- pdb compiler option [C#]
- /pdb compiler option [C#]
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
caps.latest.revision: 8
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
ms.openlocfilehash: 7c72c12347a9096aeed063b84310356cb07b49c3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="pdb-c-compiler-options"></a>/pdb（C# 编译器选项）
/pdb 编译器选项指定调试符号文件的名称和位置。  
  
## <a name="syntax"></a>语法  
  
```console  
/pdb:filename  
```  
  
## <a name="arguments"></a>参数  
 `filename`  
 调试符号文件的名称和位置。  
  
## <a name="remarks"></a>备注  
 指定 [/debug（C# 编译器选项）](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)后，编译器将在创建输出文件（.exe 或 .dll）的目录中创建 .pdb 文件，且名称与输出文件的名称相同。  
  
 /pdb 允许为 .pdb 文件指定非默认的文件名和位置。  
  
 不能在 Visual Studio 开发环境中设置此编译器选项，也不能以编程方式对其进行更改。  
  
## <a name="example"></a>示例  
 编译 `t.cs` 并创建名为 tt.pdb 的 .pdb 文件：  
  
```console  
csc /debug /pdb:tt t.cs  
```  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

