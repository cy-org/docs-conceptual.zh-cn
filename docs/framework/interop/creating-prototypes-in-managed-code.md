---
title: "在托管代码中创建原型"
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
- prototypes in managed code
- COM interop, DLL functions
- unmanaged functions
- platform invoke, creating prototypes
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, object fields
- DLL functions
- object fields in platform invoke
ms.assetid: ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9a3dcc625a838dc8823930e31541543b9c4c7f8f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="creating-prototypes-in-managed-code"></a>在托管代码中创建原型
本主题介绍了如何访问非托管函数，并介绍了在托管代码中批注方法定义的若干属性字段。 有关演示如何构造要用于平台调用、基于 .NET 的声明的示例，请参阅[用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)。  
  
 在从托管代码访问非托管 DLL 函数之前，需要知道函数的名称以及将其导出的 DLL 的名称。 使用此信息，可开始为 DLL 中实现的非托管函数编写托管定义。 此外，可调整平台调用创建函数以及将数据封送到函数和从中封送数据的方法。  
  
> [!NOTE]
>  借助分配字符串的 Win32 API 函数，你可以使用 `LocalFree` 等方法释放字符串。 平台调用以不同方式处理此类参数。 为了调用平台调用，将参数设为 `IntPtr` 类型，而不是 `String` 类型。 使用 <xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName> 类提供的方法手动将类型转换为字符串，并将其手动释放。  
  
## <a name="declaration-basics"></a>声明基本知识  
 如以下示例所示，非托管函数的托管定义依赖于语言。 有关更完整的代码示例，请参阅[平台调用示例](../../../docs/framework/interop/platform-invoke-examples.md)。  
  
```vb  
Imports System.Runtime.InteropServices  
Public Class Win32  
    Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, _  
        ByVal txt As String, ByVal caption As String, _  
        ByVal Typ As Integer) As IntPtr  
End Class  
```  
  
 若要将 <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>、<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>、<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>、<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>、<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError> 或 <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar> 字段应用到 [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)] 声明，必须使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 属性，而不是 `Declare` 语句。  
  
```vb  
Imports System.Runtime.InteropServices  
Public Class Win32  
   <DllImport ("user32.dll", CharSet := CharSet.Auto)> _  
   Public Shared Function MessageBox (ByVal hWnd As Integer, _  
        ByVal txt As String, ByVal caption As String, _  
        ByVal Typ As Integer) As IntPtr  
   End Function  
End Class  
```  
  
```csharp  
using System.Runtime.InteropServices;  
[DllImport("user32.dll")]  
    public static extern IntPtr MessageBox(int hWnd, String text,   
                                       String caption, uint type);  
```  
  
```cpp  
using namespace System::Runtime::InteropServices;  
[DllImport("user32.dll")]  
    extern "C" IntPtr MessageBox(int hWnd, String* pText,  
    String* pCaption unsigned int uType);  
```  
  
## <a name="adjusting-the-definition"></a>调整定义  
 无论是否设置为显式，属性字段都将定义托管代码的行为。 平台调用根据程序集中作为元数据存在的各个字段上设置的默认值进行操作。 可通过调整一个或多个字段的值来更改此默认行为。 在很多情况下，使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 设置值。  
  
 下表列出了与平台调用相关的完整的属性字段集。 对于每个字段，此表包括了默认值以及有关如何使用这些字段来定义非托管 DLL 函数的信息的链接。  
  
|字段|描述|  
|-----------|-----------------|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>|启用或禁用最佳映射。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>|指定要用于传递方法自变量的调用约定。 默认值是 `WinAPI`，此值对应于 32 位基于 Intel 的平台的 `__stdcall`。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>|控件名称重整以及应将字符串自变量封送到函数的方法。 默认值为 `CharSet.Ansi`。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>|指定要调用的 DLL 入口点。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>|控制是否应修改入口点以对应字符集。 默认值因编程语言而异。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>|控制是否应将托管方法签名转换为返回 HRESULT 并具有返回值的附加 [out，retval] 自变量的非托管签名。<br /><br /> 默认值为 `true`（不应转换签名）。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError>|允许调用方使用 `Marshal.GetLastWin32Error` API 函数确定执行此方法时是否发生了错误。 在 Visual Basic 中，默认值为 `true`；在 C# 和 C++ 中，默认值为 `false`。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar>|控制在转换为 ANSI "?" 字符的非托管 Unicode 字符上引发的异常。|  
  
 详细的引用信息，请参阅 <xref:System.Runtime.InteropServices.DllImportAttribute>。  
  
## <a name="platform-invoke-security-considerations"></a>平台调用安全注意事项  
 <xref:System.Security.Permissions.SecurityAction> 枚举的 `Assert`、`Deny` 和 `PermitOnly` 成员被称为堆栈审核修饰符。 如果将这些成员用作平台调用声明和 COM 接口定义语言 (IDL) 语句上的声明性属性，则会被忽略。  
  
### <a name="platform-invoke-examples"></a>平台调用示例  
 本节中的平台调用示例阐明了如何将 `RegistryPermission` 属性和堆栈审核修饰符一起使用。  
  
 在以下代码示例中，将忽略 <xref:System.Security.Permissions.SecurityAction>`Assert`、`Deny` 和 `PermitOnly` 修饰符。  
  
```  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionAssert();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 但是，以下示例接受 `Demand` 修饰符。  
  
```  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 如果将 <xref:System.Security.Permissions.SecurityAction> 修饰符放置在包含（包装）平台调用的类中，则无法正常运行。  
  
```cpp  
      [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
public ref class PInvokeWrapper  
{  
public:  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
};  
```  
  
```csharp  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
class PInvokeWrapper  
{  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
}  
```  
  
 如果 <xref:System.Security.Permissions.SecurityAction> 修饰符位于嵌套方案中平台调用的调用方上，则也可在此方案中正常运行：  
  
```cpp  
      {  
public ref class PInvokeWrapper  
public:  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
  
    [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
};  
```  
  
```csharp  
class PInvokeScenario  
{  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionInternal();  
  
    [RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
}  
```  
  
#### <a name="com-interop-examples"></a>COM 互操作示例  
 本节中的 COM 互操作示例阐明了如何将 `RegistryPermission` 属性和堆栈审核修饰符一起使用。  
  
 与上节中的平台调用示例相似，以下 COM 互操作接口声明也会忽略 `Assert`、`Deny` 和 `PermitOnly` 修饰符。  
  
```  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDenyStubsItf  
{  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
 此外，COM 互操作接口声明方案不接受 `Demand` 修饰符，如以下示例所示。  
  
```  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDemandStubsItf  
{  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用非托管 DLL 函数](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)   
 [指定入口点](../../../docs/framework/interop/specifying-an-entry-point.md)   
 [指定字符集](../../../docs/framework/interop/specifying-a-character-set.md)   
 [平台调用示例](../../../docs/framework/interop/platform-invoke-examples.md)   
 [平台调用安全注意事项](http://msdn.microsoft.com/en-us/bbcc67f7-50b5-4917-88ed-cb15470409fb)   
 [标识 DLL 中的函数](../../../docs/framework/interop/identifying-functions-in-dlls.md)   
 [创建用于容纳 DLL 函数的类](../../../docs/framework/interop/creating-a-class-to-hold-dll-functions.md)   
 [调用 DLL 函数](../../../docs/framework/interop/calling-a-dll-function.md)

