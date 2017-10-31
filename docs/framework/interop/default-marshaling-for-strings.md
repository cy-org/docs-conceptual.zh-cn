---
title: "字符串的默认封送处理"
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
- strings, interop marshaling
- interop marshaling, strings
ms.assetid: 9baea3ce-27b3-4b4f-af98-9ad0f9467e6f
caps.latest.revision: 18
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d5e78bebf15630589a90a684f2299565728728c7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="default-marshaling-for-strings"></a>字符串的默认封送处理
<xref:System.String?displayProperty=fullName> 和 <xref:System.Text.StringBuilder?displayProperty=fullName> 类均具有类似的封送处理行为。  
  
 字符串以 COM 样式 `BSTR` 类型或以 null 结尾的字符串（以 null 字符结尾的字符数组）进行封送。 字符串中的字符可以采用 Unicode（Windows 系统上的默认值）或 ANSI 进行封送。  
  
 本主题提供字符串类型封送处理的以下信息：  
  
-   [在接口中使用的字符串](#cpcondefaultmarshalingforstringsanchor1)  
  
-   [在平台调用中使用的字符串](#cpcondefaultmarshalingforstringsanchor5)  
  
-   [在结构中使用的字符串](#cpcondefaultmarshalingforstringsanchor2)  
  
-   [定长字符串缓冲区](#cpcondefaultmarshalingforstringsanchor3)  
  
<a name="cpcondefaultmarshalingforstringsanchor1"></a>   
## <a name="strings-used-in-interfaces"></a>在接口中使用的字符串  
 下表显示以非托管代码的方法参数封送字符串数据类型时的封送处理选项。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性向 COM 接口的封送字符串提供若干个 <xref:System.Runtime.InteropServices.UnmanagedType> 枚举值。  
  
|枚举类型|非托管格式说明|  
|----------------------|-------------------------------------|  
|`UnmanagedType.BStr`（默认值）|具有预先固定长度和 Unicode 字符的 COM 样式 `BSTR`。|  
|`UnmanagedType.LPStr`|指向以 null 终止的 ANSI 字符数组的指针。|  
|`UnmanagedType.LPWStr`|指向以 null 终止的 Unicode 字符数组的指针。|  
  
 此表适用于字符串。 但是，对于 <xref:System.Text.StringBuilder>，仅允许 `UnmanagedType.LPStr` 和 `UnmanagedType.LPWStr` 两个选项。  
  
 以下示例演示在 `IStringWorker` 接口中声明的字符串。  
  
```cpp  
public interface IStringWorker {  
void PassString1(String s);  
void PassString2([MarshalAs(UnmanagedType.BStr)]String s);  
void PassString3([MarshalAs(UnmanagedType.LPStr)]String s);  
void PassString4([MarshalAs(UnmanagedType.LPWStr)]String s);  
void PassStringRef1(ref String s);  
void PassStringRef2([MarshalAs(UnmanagedType.BStr)]ref String s);  
void PassStringRef3([MarshalAs(UnmanagedType.LPStr)]ref String s);  
void PassStringRef4([MarshalAs(UnmanagedType.LPWStr)]ref String s);  
);  
```  
  
 以下示例演示类型库中描述的相应接口。  
  
```  
[…]  
interface IStringWorker : IDispatch {  
HRESULT PassString1([in] BSTR s);  
HRESULT PassString2([in] BSTR s);  
HRESULT PassString3([in] LPStr s);  
HRESULT PassString4([in] LPWStr s);  
HRESULT PassStringRef1([in, out] BSTR *s);  
HRESULT PassStringRef2([in, out] BSTR *s);  
HRESULT PassStringRef3([in, out] LPStr *s);  
HRESULT PassStringRef4([in, out] LPWStr *s);  
);  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor5"></a>   
## <a name="strings-used-in-platform-invoke"></a>在平台调用中使用的字符串  
 平台调用复制字符串参数，将其从.NET Framework 格式 (Unicode) 转换为平台非托管格式。 当调用返回时，字符串固定不变，且不会从非托管内存复制回托管内存。  
  
 下表列出以平台调用的方法参数封送字符串时的封送处理选项。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性向封送字符串提供若干个 <xref:System.Runtime.InteropServices.UnmanagedType> 枚举值。  
  
|枚举类型|非托管格式说明|  
|----------------------|-------------------------------------|  
|`UnmanagedType.AnsiBStr`|具有预先固定长度和 ANSI 字符的 COM 样式 `BSTR`。|  
|`UnmanagedType.BStr`|具有预先固定长度和 Unicode 字符的 COM 样式 `BSTR`。|  
|`UnmanagedType.LPStr`|指向以 null 终止的 ANSI 字符数组的指针。|  
|`UnmanagedType.LPTStr`|指向以 null 终止的平台相关字符数组的指针。|  
|`UnmanagedType.LPWStr`|指向以 null 终止的 Unicode 字符数组的指针。|  
|`UnmanagedType.TBStr`|具有预先固定长度和平台相关字符的 COM 样式 `BSTR`。|  
|`VBByRefStr`|使 Visual Basic .NET 能够在非托管代码中更改字符串，并在托管代码中反映出结果的值。 此值仅支持用于平台调用。 这是 `ByVal` 字符串在 Visual Basic 中的默认值。|  
  
 此表适用于字符串。 但是，对于 <xref:System.Text.StringBuilder>，仅允许 `LPStr`、`LPTStr` 和 `LPWStr` 三个选项。  
  
 以下类型定义演示 `MarshalAsAttribute` 平台调用的正确用法。  
  
```vb  
Class StringLibAPI      
Public Declare Auto Sub PassLPStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPStr)> s As String)      
Public Declare Auto Sub PassLPWStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPWStr)> s As String)      
Public Declare Auto Sub PassLPTStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPTStr)> s As String)      
Public Declare Auto Sub PassBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.BStr)> s As String)      
Public Declare Auto Sub PassAnsiBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.AnsiBStr)> s As String)      
Public Declare Auto Sub PassTBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.TBStr)> s As String)  
End Class  
```  
  
```csharp  
class StringLibAPI {  
[DllImport("StringLib.Dll")]  
public static extern void PassLPStr([MarshalAs(UnmanagedType.LPStr)]  
String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassLPWStr([MarshalAs(UnmanagedType.LPWStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassLPTStr([MarshalAs(UnmanagedType.LPTStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void PassBStr([MarshalAs(UnmanagedType.BStr)]  
String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassAnsiBStr([MarshalAs(UnmanagedType.AnsiBStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void PassTBStr([MarshalAs(UnmanagedType.TBStr)]  
String s);  
}  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor2"></a>   
## <a name="strings-used-in-structures"></a>在结构中使用的字符串  
 字符串是结构的有效成员，但是 <xref:System.Text.StringBuilder> 缓冲区在结构中无效。 下表显示以字段封送字符串数据类型时的封送处理选项。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性向字段的封送字符串提供若干个 <xref:System.Runtime.InteropServices.UnmanagedType> 枚举值。  
  
|枚举类型|非托管格式说明|  
|----------------------|-------------------------------------|  
|`UnmanagedType.BStr`|具有预先固定长度和 Unicode 字符的 COM 样式 `BSTR`。|  
|`UnmanagedType.LPStr`|指向以 null 终止的 ANSI 字符数组的指针。|  
|`UnmanagedType.LPTStr`|指向以 null 终止的平台相关字符数组的指针。|  
|`UnmanagedType.LPWStr`|指向以 null 终止的 Unicode 字符数组的指针。|  
|`UnmanagedType.ByValTStr`|定长字符数组；数组的类型由包含结构的字符集确定。|  
  
 `ByValTStr` 类型用于结构中出现的内联定长字符数组。 其他类型适用于包含指向字符串的指针的结构中包含的字符串引用。  
  
 应用于包含结构的 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性的 `CharSet` 参数确定结构中字符串的字符格式。 以下示例结构包含字符串引用和内联字符串，以及 ANSI、Unicode 和平台相关字符。  
  
### <a name="type-library-representation"></a>类型库表示形式  
  
```  
struct StringInfoA {  
   char *    f1;  
   char      f2[256];  
};  
struct StringInfoW {  
   WCHAR *   f1;  
   WCHAR     f2[256];  
   BSTR      f3;  
};  
struct StringInfoT {  
   TCHAR *   f1;  
   TCHAR     f2[256];  
};  
```  
  
 以下代码示例演示如何使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性以不同的格式定义相同的结构。  
  
```vb  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Ansi)> _  
Structure StringInfoA  
<MarshalAs(UnmanagedType.LPStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
End Structure  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Unicode)> _  
Structure StringInfoW  
<MarshalAs(UnmanagedType.LPWStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
<MarshalAs(UnmanagedType.BStr)> Public f3 As String  
End Structure  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Auto)> _  
Structure StringInfoT  
<MarshalAs(UnmanagedType.LPTStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
End Structure  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]  
struct StringInfoA {  
   [MarshalAs(UnmanagedType.LPStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
}  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]  
struct StringInfoW {  
   [MarshalAs(UnmanagedType.LPWStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
   [MarshalAs(UnmanagedType.BStr)] public String f3;  
}  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]  
struct StringInfoT {  
   [MarshalAs(UnmanagedType.LPTStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
}  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor3"></a>   
## <a name="fixed-length-string-buffers"></a>定长字符串缓冲区  
 在某些情况下，必须将定长字符缓冲区传递到要操作的非托管代码中。 在这种情况下，只传递字符串将不起作用，因为被调用方不能修改所传递缓冲区的内容。 即使通过引用传递字符串，仍无法将缓冲区初始化为给定大小。  
  
 解决方法是将 <xref:System.Text.StringBuilder> 缓冲区作为参数而非字符串进行传递。 被调用方可以取消引用和修改 `StringBuilder`，前提是不超过 `StringBuilder` 的容量。 还可以初始化为固定长度。 例如，如果将 `StringBuilder` 缓冲区初始化为 `N` 容量，则封送处理程序提供大小为 (`N`+ 1) 个字符的缓冲区。 +1 解释了非托管字符串具有 null 终止符而帐户 `StringBuilder` 却不具有这一事实。  
  
 例如，Microsoft Win32 API `GetWindowText` 函数（在 Windows.h 中定义）是一个定长字符缓冲区，必须传递到要操作的非托管代码中。 `LpString` 指向调用方分配的大小为 `nMaxCount` 的缓冲区。 调用方应分配缓冲区，并将 `nMaxCount` 参数设置为已分配缓冲区的大小。 以下代码演示 `GetWindowText` 函数声明，如 Windows.h 中所定义。  
  
```  
int GetWindowText(  
HWND hWnd,        // Handle to window or control.  
LPTStr lpString,  // Text buffer.  
int nMaxCount     // Maximum number of characters to copy.  
);  
```  
  
 被调用方可以取消引用和修改 `StringBuilder`，前提是不超过 `StringBuilder` 的容量。 下面的代码示例演示如何将 `StringBuilder` 初始化为固定长度。  
  
```vb  
Public Class Win32API  
Public Declare Auto Sub GetWindowText Lib "User32.Dll" _  
(h As Integer, s As StringBuilder, nMaxCount As Integer)  
End Class  
Public Class Window  
   Friend h As Integer ' Friend handle to Window.  
   Public Function GetText() As String  
      Dim sb As New StringBuilder(256)  
      Win32API.GetWindowText(h, sb, sb.Capacity + 1)  
   Return sb.ToString()  
   End Function  
End Class  
```  
  
```csharp  
public class Win32API {  
[DllImport("User32.Dll")]  
public static extern void GetWindowText(int h, StringBuilder s,   
int nMaxCount);  
}  
public class Window {  
   internal int h;        // Internal handle to Window.  
   public String GetText() {  
      StringBuilder sb = new StringBuilder(256);  
      Win32API.GetWindowText(h, sb, sb.Capacity + 1);  
   return sb.ToString();  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [默认的封送行为](../../../docs/framework/interop/default-marshaling-behavior.md)   
 [Blittable 和非 Blittable 类型](../../../docs/framework/interop/blittable-and-non-blittable-types.md)   
 [方向特性](http://msdn.microsoft.com/en-us/241ac5b5-928e-4969-8f58-1dbc048f9ea2)   
 [复制和锁定](../../../docs/framework/interop/copying-and-pinning.md)

