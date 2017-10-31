---
title: "指定字符集"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- platform invoke, attribute fields
- attribute fields in platform invoke, CharSet
- CharSet field
ms.assetid: a8347eb1-295f-46b9-8a78-63331f9ecc50
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a1b0e444ef73deac6f6e353c8e1b67d1cf361ab2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="specifying-a-character-set"></a>指定字符集
<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> 字段控制字符串封送，并确定平台调用在 DLL 中查找函数名的方式。 本主题将介绍这两种行为。  
  
 某些 API 导出采用字符串自变量的函数的两个版本：窄版 (ANSI) 和宽版 (Unicode)。 例如，Win32 API 包含“MessageBox”函数的以下入口点名称：  
  
-   **MessageBoxA**  
  
     提供 ANSI 格式的 1 字节字符，由附加到入口点名称后的“A”区分。 对“MessageBoxA”的调用始终采用 ANSI 格式封送字符串，这在 Windows 95 和 Windows 98 平台上很常见。  
  
-   **MessageBoxW**  
  
     提供 Unicode 格式的 2 字节字符，由附加到入口点名称后的“W”区分。 对“MessageBoxW”的调用始终采用 Unicode 格式封送字符串，这在 Windows NT、Windows 2000 和 Windows XP 平台上很常见。  
  
## <a name="string-marshaling-and-name-matching"></a>字符串封送和名称匹配  
 “CharSet”字段接受以下值：  
  
 **CharSet.Ansi**（默认值）  
  
-   字符串封送  
  
     平台调用将字符串从托管格式 (Unicode) 封送为 ANSI 格式。  
  
-   名称匹配  
  
     当 <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=fullName> 字段为“true”时（[!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] 中默认为此值），平台调用仅搜索你指定的名称。 例如，如果指定“MessageBox”，则平台调用搜索“MessageBox”，如果无法找到精确拼写，则将失败。  
  
     “ExactSpelling”字段为“false”时（C++ 和 C# 中默认为此值），平台调用首先搜索未损坏的别名（MessageBox），如果未找到未损坏的别名，再搜索损坏的名称（MessageBoxA）。 请注意，ANSI 名称匹配行为与 Unicode 名称匹配行为不同。  
  
 **CharSet.Unicode**  
  
-   字符串封送  
  
     平台调用将字符串从托管格式 (Unicode) 复制为 Unicode 格式。  
  
-   名称匹配  
  
     当“ExactSpelling”字段为“true”时（[!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] 中默认为此值），平台调用仅搜索你指定的名称。 例如，如果指定“MessageBox” ，则平台调用搜索“MessageBox”，如果无法找到精确拼写，则将失败。  
  
     当“ExactSpelling”字段为“false”时（C++ 和 C# 中默认为此值），平台调用首先搜索已损坏的名称（MessageBoxW），如果未找到已损坏的名称，再搜索未损坏的别名（MessageBox）。 请注意，Unicode 名称匹配行为与 ANSI 名称匹配行为不同。  
  
 **CharSet.Auto**  
  
-   平台调用在运行时根据目标平台在 ANSI 和 Unicode 格式之间进行选择。  
  
## <a name="specifying-a-character-set-in-visual-basic"></a>在 Visual Basic 中指定字符集  
 以下示例声明“MessageBox”函数三次，每次使用不同的字符集行为。 通过将“Ansi”、“Unicode”或“Auto”关键字添加到声明语句中，就可以在 Visual Basic 中指定字符集行为。  
  
 如果省略字符集关键字，正如在第一个声明语句中那样，则 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> 字段默认为 ANSI 字符集。 示例中的第二个和第三个语句使用关键字显式指定字符集。  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
   Declare Function MessageBoxA Lib "user32.dll"(ByVal hWnd As Integer, _  
       ByVal txt As String, ByVal caption As String, _  
       ByVal Typ As Integer) As Integer  
  
   Declare Unicode Function MessageBoxW Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String, _  
        ByVal caption As String, ByVal Typ As Integer) As Integer  
  
   Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String, _  
        ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
## <a name="specifying-a-character-set-in-c-and-c"></a>在 C# 和 C++ 中指定字符集  
 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> 字段将基础字符集标识为 ANSI 或 Unicode。 字符集控制应如何封送方法的字符串自变量。 使用以下形式之一来指示字符集：  
  
```csharp  
[DllImport("dllname", CharSet=CharSet.Ansi)]  
[DllImport("dllname", CharSet=CharSet.Unicode)]  
[DllImport("dllname", CharSet=CharSet.Auto)]  
```  
  
```cpp  
[DllImport("dllname", CharSet=CharSet::Ansi)]  
[DllImport("dllname", CharSet=CharSet::Unicode)]  
[DllImport("dllname", CharSet=CharSet::Auto)]  
```  
  
 以下示例显示“MessageBox”函数的三个托管定义，它们是指定字符集的结果。 在第一个定义中，通过省略，“CharSet”字段默认为 ANSI 字符集。  
  
```csharp  
[DllImport("user32.dll")]  
    public static extern int MessageBoxA(int hWnd, String text,   
        String caption, uint type);  
[DllImport("user32.dll", CharSet=CharSet.Unicode)]  
    public static extern int MessageBoxW(int hWnd, String text,   
        String caption, uint type);  
[DllImport("user32.dll", CharSet=CharSet.Auto)]  
    public static extern int MessageBox(int hWnd, String text,   
        String caption, uint type);  
```  
  
```cpp  
typedef void* HWND;  
  
//Can use MessageBox or MessageBoxA.  
[DllImport("user32")]  
extern "C" int MessageBox(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
  
//Can use MessageBox or MessageBoxW.  
[DllImport("user32", CharSet=CharSet::Unicode)]  
extern "C" int MessageBoxW(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
  
//Must use MessageBox.  
[DllImport("user32", CharSet=CharSet::Auto)]  
extern "C" int MessageBox(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [在托管代码中创建原型](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [平台调用示例](../../../docs/framework/interop/platform-invoke-examples.md)   
 [用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)

