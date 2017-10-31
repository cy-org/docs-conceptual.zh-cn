---
title: "-langversion（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /langversion
dev_langs:
- CSharp
helpviewer_keywords:
- /langversion compiler option [C#]
- -langversion compiler option [C#]
- langversion compiler option [C#]
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
caps.latest.revision: 33
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
ms.openlocfilehash: fc501c5532d27168d74d1a5f293abe59d3beeef1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="langversion-c-compiler-options"></a>/langversion（C# 编译器选项）
使编译器仅接受包含在所选 C# 语言规范中的语法。  
  
## <a name="syntax"></a>语法  
  
```console  
/langversion:option  
```  
  
## <a name="arguments"></a>参数  
 `option`  
 以下为有效值：  
  
|选项|含义|  
|------------|-------------|  
|default|编译器接受它可支持的所有有效语言语法。 <sup id="TDefault">[默认](#FDefault)</sup>| 
|ISO-1|编译器只接受 ISO/IEC 23270:2003 C# (1.0/1.1) 中所含的语法 <sup id="TISO1">[ISO1](#FISO1)</sup>|  
|ISO-2|编译器只接受 ISO/IEC 23270:2006 C# (2.0) 中所含的语法 <sup id="TISO2">[ISO2](#FISO2)</sup>|
|3|编译器只接受 C# 3.0 或更低版本中所含的语法 <sup id="TCS3">[CS3](#FCS3)</sup>|
|4|编译器只接受 C# 4.0 或更低版本中所含的语法 <sup id="TCS4">[CS4](#FCS4)</sup>|
|5|编译器只接受 C# 5.0 或更低版本中所含的语法 <sup id="TCS5">[CS5](#FCS5)</sup>|
|6|编译器只接受 C# 6.0 或更低版本中所含的语法 <sup id="TCS6">[CS6](#FCS6)</sup>|
|7|编译器只接受 C# 7.0 或更低版本中所含的语法 <sup id="TCS7">[CS7](#FCS7)</sup>|
|最新|编译器接受它可支持的所有有效语言语法。 <sup id="TLatest">[最新](#FLatest)</sup>|
<!--- Uncomment and move these above
|latest| once they're officially released
|7.1|The compiler accepts only syntax that is included in C# 7.1 or lower <sup id="TCS71">[CS71](#FCS71)</sup>|
|7.2|The compiler accepts only syntax that is included in C# 7.2 or lower <sup id="TCS71">[CS72](#FCS72)</sup>|
|8|The compiler accepts only syntax that is included in C# 8 or lower <sup id="TCS71">[CS8](#FCS8)</sup>|
-->

  
## <a name="remarks"></a>备注  
 C# 应用程序引用的元数据不受“/langversion”编译器选项约束。  
  
 每个版本的 C# 编译器都包含语言规范的扩展，因此 /langversion 不提供早期版本编译器的同等功能。  
 
 此外，虽然 C# 版本更新通常与主要的 .Net Framework 版本一致，但新的语法和功能不一定绑定到该特定的 Framework 版本。 虽然新功能肯定会需要与 C# 修订版一起发布的新编译器更新，但每项具体功能都有自己的最小 .Net API 或公共语言运行时要求，这些要求通过包括 NuGet 包或其他库允许功能本身在下层框架上运行。
  
 无论使用哪一项“/langversion”设置，都将使用当前版本的公共语言运行时来创建 .exe 或 .dll。 友元程序集和 [/moduleassemblyname（C# 编译器选项）](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)是一个例外，它们在“/langversion:ISO-1”下工作。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“生成”属性页。  
  
3.  单击 **“高级”** 按钮。  
  
4.  修改“语言版本”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>。  
    
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)   
 
### <a name="c-language-specification"></a>C# 语言规范
 [C# 语言规范参考](../../../csharp/language-reference/language-specification/index.md)：.NET Foundation   
 C# 1.0/1.1 [ISO/IEC 23270:2003](https://www.iso.org/standard/36768.html) 信息技术 - C# 语言规范：ISO 目录   
 C# 2.0 [ISO/IEC 23270:2006](https://www.iso.org/standard/42926.html) 信息技术 - C# 语言规范：ISO 目录   
 C# 2.0 [c042926_ISO_IEC_23270_2006(E).zip](http://go.microsoft.com/fwlink/?LinkId=144406) ISO/IEC 23270:2006（PDF 格式）：可免费获取的 ISO 标准   
 C# 3.0 [CSharp 语言规范.doc](http://download.microsoft.com/download/3/8/8/388e7205-bc10-4226-b2a8-75351c669b09/CSharp%20Language%20Specification.doc) C# 语言规范版本 3.0：Microsoft Corporation   
 C# 4.0 [Ecma-334.pdf](https://www.ecma-international.org/publications/files/ECMA-ST/Ecma-334.pdf) 标准 ECMA-334 第四版    
 C# 5.0 [CSharp 语言规范.docx](https://www.microsoft.com/en-us/download/details.aspx?id=7029) C# 语言规范 5.0 版：Microsoft Corporation   
 C# 6.0 [README.md](https://github.com/dotnet/csharplang/blob/master/spec/README.md) C# 语言规范版本 6 - 非官方草稿：.NET Foundation   
 C# 7.0（当前不可用）   

<!--- Uncomment and add to the above when they become officially released
 C# 7.1 (spec is not yet finished)   
 C# 7.2 (spec is not yet finished)   
 C# 8.0 (spec is not yet finished)   
-->

### <a name="minimum-compiler-version-needed-to-support-all-language-features"></a>支持所有语言功能所需的最低编译器版本   
[↩](#TDefault)<a name="FDefault">默认</a><a name="FISO1">ISO1</a>：Microsoft Visual Studio/生成工具 .Net 2002 或捆绑的 .Net Framework 1.0 编译器     
[↩](#TISO2)<a name="FISO2">ISO2</a>：Microsoft Visual Studio/生成工具 2005 或捆绑的 .Net Framework 2.0 编译器    
[↩](#TCS3)<a name="FCS3">CS3</a>：Microsoft Visual Studio/生成工具 2008 或捆绑的 .Net Framework 3.5 编译器    
[↩](#TCS4)<a name="FCS4">CS4</a>：Microsoft Visual Studio/生成工具 2010 或捆绑的 .Net Framework 4.0 编译器    
[↩](#TCS5)<a name="FCS5">CS5</a>：Microsoft Visual Studio/生成工具 2012 或捆绑的 .Net Framework 4.5 编译器    
[↩](#TCS6)<a name="FCS6">CS6</a>：Microsoft Visual Studio/生成工具 2015    
[↩](#TCS7)<a name="FCS7">CS7</a><a name="FLatest">最新</a>：Microsoft Visual Studio/生成工具 2017   

<!--- Uncomment and add to the above when they become officially released
[↩](#TCS71)<a name="FCS71">CS71</a>: Microsoft Visual Studio/Build Tools 20??    
[↩](#TCS72)<a name="FCS72">CS72</a>: Microsoft Visual Studio/Build Tools 20??    
[↩](#TCS8)<a name="FCS71">CS8</a>: Microsoft Visual Studio/Build Tools 20??    
-->

