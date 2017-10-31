---
title: "-warn（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /warn
dev_langs:
- CSharp
helpviewer_keywords:
- warning level [C#]
- /w compiler option [C#]
- -w compiler option [C#]
- -warn compiler option [C#]
- /warn compiler option [C#]
- w compiler option [C#]
- warn compiler option [C#]
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
caps.latest.revision: 17
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
ms.openlocfilehash: e703060b7cc5f897ddf0b6764e9607460666e92c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="warn-c-compiler-options"></a>/warn（C# 编译器选项）
“/warn”选项指定编译器显示的警告等级。  
  
## <a name="syntax"></a>语法  
  
```console  
/warn:option  
```  
  
## <a name="arguments"></a>参数  
 `option`  
 想要为编译显示的警告等级：较低的数字仅显示高严重性警告；较高的数字显示更多警告。 有效值为 0-4：  
  
|警告级别|含义|  
|-------------------|-------------|  
|0|关闭发出所有警告消息。|  
|1|显示严重警告消息。|  
|2|显示等级 1 警告以及某些不太严重的警告，如有关隐藏类成员的警告。|  
|3|显示等级 2 警告以及某些不太严重的警告，如有关经常计算为 `true` 或 `false` 的表达式的警告。|  
|4（默认值）|显示所有等级 3 警告以及信息性警告。|  
  
## <a name="remarks"></a>备注  
 若要获取有关错误或警告的信息，可以在帮助索引中查找错误代码。 有关获取错误或警告信息的其他方法，请参阅 [C# 编译器错误](../../../csharp/language-reference/compiler-messages/index.md)。  
  
 使用 [/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md) 将所有警告视为错误。 使用 [/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) 禁用某些警告。  
  
 /w 是 /warn 的缩写形式。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“生成”属性页。  
  
3.  修改警告等级属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>。  
  
## <a name="example"></a>示例  
 编译 `in.cs` 并使编译器仅显示等级 1 警告：  
  
```console  
csc /warn:1 in.cs  
```  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

