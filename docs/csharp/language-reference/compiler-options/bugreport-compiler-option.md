---
title: "-bugreport（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /bugreport
dev_langs:
- CSharp
helpviewer_keywords:
- /bugreport compiler option [C#]
- -bugreport compiler option [C#]
- bugreport compiler option [C#]
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
caps.latest.revision: 20
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
ms.openlocfilehash: ccfea1aa7e51ad013418f61bc4478034c9a5d830
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="bugreport-c-compiler-options"></a>/bugreport（C# 编译器选项）
指定应使调试信息置于文件中供以后分析。  
  
## <a name="syntax"></a>语法  
  
```console  
/bugreport:file  
```  
  
## <a name="arguments"></a>参数  
 `file`  
 要包含 Bug 报告的文件的名称。  
  
## <a name="remarks"></a>备注  
 /bugreport 选项指定以下信息应置于 `file` 中：  
  
-   编译中所有源代码文件副本。  
  
-   编译中使用的编译器选项列表。  
  
-   有关编译器、运行时和操作系统的版本信息。  
  
-   引用的程序集和模块（保存为十六进制数字），.NET Framework 和 SDK 随附的程序集除外。  
  
-   编译器输出（如有）。  
  
-   问题说明（系统会提示你提供此信息）。  
  
-   有关你认为应如何修复问题的说明（系统会提示你提供此信息）。  
  
 如果此选项与 /errorreport: prompt 或 /errorreport:send 一起使用，文件中的信息将发送到 Microsoft Corporation。  
  
 所有源代码文件的副本将放入 `file`，因此你可能希望在尽可能短小的程序中重现可疑代码缺陷。  
  
 此编译器选项在 Visual Studio 中不可用，并且无法以编程方式更改。  
  
 请注意，生成文件的内容会公开源代码，这可能会导致意外信息泄露。  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [/errorreport（C# 编译器选项）](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

