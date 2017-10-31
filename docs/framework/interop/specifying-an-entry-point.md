---
title: "指定入口点"
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
- EntryPoint field
- platform invoke, attribute fields
- attribute fields in platform invoke, EntryPoint
ms.assetid: d1247f08-0965-416a-b978-e0b50652dfe3
caps.latest.revision: 9
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f8d8f4a561248b7022b08ee15c9a726a58b80318
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="specifying-an-entry-point"></a>指定入口点
入口点标识 DLL 中的函数位置。 在托管项目中，目标函数的原始名称或序号入口点跨越互操作边界标识该函数。 此外，可将入口点映射到其他名称，有效地重命名该函数。  
  
 以下列表列出了重命名 DLL 函数的可能原因：  
  
-   避免使用区分大小写的 API 函数名  
  
-   符合现有的命名标准  
  
-   提供采用不同数据类型的函数（通过声明同一 DLL 函数的多个版本）  
  
-   简化对包含 ANSI 和 Unicode 版本的 API 的使用  
  
 本主题说明如何在托管代码中重命名 DLL 函数。  
  
## <a name="renaming-a-function-in-visual-basic"></a>重命名 Visual Basic 中的函数  
 Visual Basic 在 Declare 语句中使用 Function 关键字设置 <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName> 字段。 下面的示例演示了一个基本声明。  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
 如下例所示，通过在定义中包括 Alias 关键字，可以用 MsgBox 替换 MessageBox 入口点。 在这两个示例中，Auto 关键字使你无需指定入口点的字符集版本。 有关选择字符集的详细信息，请参阅[指定字符集](../../../docs/framework/interop/specifying-a-character-set.md)。  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MsgBox Lib "user32.dll" _  
       Alias "MessageBox" (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
## <a name="renaming-a-function-in-c-and-c"></a>重命名 C# 和 C++ 中的函数  
 可使用 <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName> 字段通过名称或序号指定 DLL 函数。 如果方法定义中函数的名称与 DLL 中入口点的名称相同，则不必使用 EntryPoint 字段显式地标识函数。 否则，使用以下属性形式之一指示名称或序号：  
  
```  
[DllImport("dllname", EntryPoint="Functionname")]  
[DllImport("dllname", EntryPoint="#123")]  
```  
  
 请注意，序号前必须带有井号 (#)。  
  
 下面的示例演示如何使用 EntryPoint 字段将代码中的 MessageBoxA 替换为 MsgBox。  
  
```csharp  
using System.Runtime.InteropServices;  
  
public class Win32 {  
    [DllImport("user32.dll", EntryPoint="MessageBoxA")]  
    public static extern int MsgBox(int hWnd, String text, String caption,  
                                    uint type);  
}  
```  
  
```cpp  
using namespace System::Runtime::InteropServices;  
  
typedef void* HWND;  
[DllImport("user32", EntryPoint="MessageBoxA")]  
extern "C" int MsgBox(HWND hWnd,  
                      String*  pText,  
                      String*  pCaption,  
                      unsigned int uType);  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [在托管代码中创建原型](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [平台调用示例](../../../docs/framework/interop/platform-invoke-examples.md)   
 [用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)

