---
title: "对象的默认封送处理"
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
- objects, interop marshaling
- interop marshaling, objects
ms.assetid: c2ef0284-b061-4e12-b6d3-6a502b9cc558
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 67d05a21d537bfca92bc76473fb6f6048865ef8c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="default-marshaling-for-objects"></a>对象的默认封送处理
可将类型化为 <xref:System.Object?displayProperty=fullName> 的参数和字段作为下列任一类型向非托管代码公开：  
  
-   对象为参数时，作为变体。  
  
-   对象为结构字段时，作为接口。  
  
 仅 COM 互操作支持对象类型的封送处理。 默认行为是将对象封送到 COM 变体。 这些规则只适用于 Object 类型，不适用于从 Object 类派生的强类型对象。  
  
 本主题提供有关封送对象类型的以下附加信息：  
  
-   [封送选项](#cpcondefaultmarshalingforobjectsanchor7)  
  
-   [将对象封送到接口](#cpcondefaultmarshalingforobjectsanchor2)  
  
-   [将对象封送到变体](#cpcondefaultmarshalingforobjectsanchor3)  
  
-   [将变体封送到对象](#cpcondefaultmarshalingforobjectsanchor4)  
  
-   [封送 ByRef 变体](#cpcondefaultmarshalingforobjectsanchor6)  
  
<a name="cpcondefaultmarshalingforobjectsanchor7"></a>   
## <a name="marshaling-options"></a>封送处理选项  
 下表显示 Object 数据类型的封送处理选项。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 属性提供若干个 <xref:System.Runtime.InteropServices.UnmanagedType> 枚举值来封送对象。  
  
|枚举类型|非托管格式说明|  
|----------------------|-------------------------------------|  
|UnmanagedType.Struct<br /><br /> （参数默认值）|COM 样式的变体。|  
|UnmanagedType.Interface|如果可能，为 IDispatch 接口；否则为 IUnknown 接口。|  
|UnmanagedType.IUnknown<br /><br /> （字段默认值）|IUnknown 接口。|  
|UnmanagedType.IDispatch|IDispatch 接口。|  
  
 以下示例显示了 `MarshalObject` 的托管接口定义。  
  
```vb  
Interface MarshalObject  
   Sub SetVariant(o As Object)  
   Sub SetVariantRef(ByRef o As Object)  
   Function GetVariant() As Object  
  
   Sub SetIDispatch( <MarshalAs(UnmanagedType.IDispatch)> o As Object)  
   Sub SetIDispatchRef(ByRef <MarshalAs(UnmanagedType.IDispatch)> o _  
      As Object)  
   Function GetIDispatch() As <MarshalAs(UnmanagedType.IDispatch)> Object  
   Sub SetIUnknown( <MarshalAs(UnmanagedType.IUnknown)> o As Object)  
   Sub SetIUnknownRef(ByRef <MarshalAs(UnmanagedType.IUnknown)> o _  
      As Object)  
   Function GetIUnknown() As <MarshalAs(UnmanagedType.IUnknown)> Object  
End Interface  
```  
  
```csharp  
interface MarshalObject {  
   void SetVariant(Object o);  
   void SetVariantRef(ref Object o);  
   Object GetVariant();  
  
   void SetIDispatch ([MarshalAs(UnmanagedType.IDispatch)]Object o);  
   void SetIDispatchRef([MarshalAs(UnmanagedType.IDispatch)]ref Object o);  
   [MarshalAs(UnmanagedType.IDispatch)] Object GetIDispatch();  
   void SetIUnknown ([MarshalAs(UnmanagedType.IUnknown)]Object o);  
   void SetIUnknownRef([MarshalAs(UnmanagedType.IUnknown)]ref Object o);  
   [MarshalAs(UnmanagedType.IUnknown)] Object GetIUnknown();  
}  
```  
  
 以下代码将 `MarshalObject` 接口导出到类型库。  
  
```  
interface MarshalObject {  
   HRESULT SetVariant([in] VARIANT o);  
   HRESULT SetVariantRef([in,out] VARIANT *o);  
   HRESULT GetVariant([out,retval] VARIANT *o)   
   HRESULT SetIDispatch([in] IDispatch *o);  
   HRESULT SetIDispatchRef([in,out] IDispatch **o);  
   HRESULT GetIDispatch([out,retval] IDispatch **o)   
   HRESULT SetIUnknown([in] IUnknown *o);  
   HRESULT SetIUnknownRef([in,out] IUnknown **o);  
   HRESULT GetIUnknown([out,retval] IUnknown **o)   
}  
```  
  
> [!NOTE]
>  互操作封送拆收器在调用后自动释放变体内所有已分配的对象。  
  
 以下示例显示已设置格式的值类型。  
  
```vb  
Public Structure ObjectHolder  
   Dim o1 As Object  
   <MarshalAs(UnmanagedType.IDispatch)> Public o2 As Object  
End Structure  
```  
  
```csharp  
public struct ObjectHolder {  
   Object o1;  
   [MarshalAs(UnmanagedType.IDispatch)]public Object o2;  
}  
```  
  
 以下代码将已设置格式的类型导出到类型库。  
  
```  
struct ObjectHolder {  
   VARIANT o1;  
   IDispatch *o2;  
}  
```  
  
<a name="cpcondefaultmarshalingforobjectsanchor2"></a>   
## <a name="marshaling-object-to-interface"></a>将对象封送到接口  
 将对象作为接口向 COM 公开时，该接口是托管类型 <xref:System.Object> 的类接口（即 _Object 接口）。 该接口被类型化为 IDispatch (<xref:System.Runtime.InteropServices.UnmanagedType>) 或所得类型库中的 IUnknown (UnmanagedType.IUnknown)。 通过 _Object 接口，COM 客户端可动态调用托管类的成员或由该托管类的派生类实现的任何成员。 客户端还可调用 QueryInterface 获取由托管类型显式实现的任何其他接口。  
  
<a name="cpcondefaultmarshalingforobjectsanchor3"></a>   
## <a name="marshaling-object-to-variant"></a>将对象封送到变体  
 将对象封送到变体时，在运行时根据以下规则确定内部变体类型：  
  
-   如果对象引用为 null（Visual Basic 中为 Nothing），则将对象封送到 VT_EMPTY 类型的变体。  
  
-   如果对象是下表中列出的任何类型的实例，则得到的变体类型由封送拆收器内置的规则确定，并且显示在下表中。  
  
-   需要显式控制封送行为的其他对象可实现 <xref:System.IConvertible> 接口。 在这种情况下，变体类型由从 <xref:System.IConvertible.GetTypeCode%2A?displayProperty=fullName> 方法返回的类型代码确定。 否则，将对象作为 VT_UNKNOWN 类型的变体封送。  
  
### <a name="marshaling-system-types-to-variant"></a>将系统类型封送到变体  
 下表显示托管对象类型及其相应的 COM 变体类型。 仅当所调用方法的签名属于 <xref:System.Object?displayProperty=fullName> 类型时，才转换这些类型。  
  
|对象类型|COM 变体类型|  
|-----------------|----------------------|  
|Null 对象引用（在 Visual Basic 中为 Nothing）。|VT_EMPTY|  
|<xref:System.DBNull?displayProperty=fullName>|VT_NULL|  
|<xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=fullName>|VT_ERROR|  
|<xref:System.Reflection.Missing?displayProperty=fullName>|带 E_PARAMNOTFOUND 的 VT_ERROR|  
|<xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=fullName>|VT_DISPATCH|  
|<xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=fullName>|VT_UNKNOWN|  
|<xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=fullName>|VT_CY|  
|<xref:System.Boolean?displayProperty=fullName>|VT_BOOL|  
|<xref:System.SByte?displayProperty=fullName>|VT_I1|  
|<xref:System.Byte?displayProperty=fullName>|VT_UI1|  
|<xref:System.Int16?displayProperty=fullName>|VT_I2|  
|<xref:System.UInt16?displayProperty=fullName>|VT_UI2|  
|<xref:System.Int32?displayProperty=fullName>|VT_I4|  
|<xref:System.UInt32?displayProperty=fullName>|VT_UI4|  
|<xref:System.Int64?displayProperty=fullName>|VT_I8|  
|<xref:System.UInt64?displayProperty=fullName>|VT_UI8|  
|<xref:System.Single?displayProperty=fullName>|VT_R4|  
|<xref:System.Double?displayProperty=fullName>|VT_R8|  
|<xref:System.Decimal?displayProperty=fullName>|VT_DECIMAL|  
|<xref:System.DateTime?displayProperty=fullName>|VT_DATE|  
|<xref:System.String?displayProperty=fullName>|VT_BSTR|  
|<xref:System.IntPtr?displayProperty=fullName>|VT_INT|  
|<xref:System.UIntPtr?displayProperty=fullName>|VT_UINT|  
|<xref:System.Array?displayProperty=fullName>|VT_ARRAY|  
  
 以下代码示例使用前一示例中定义的 `MarshalObject` 接口，演示如何将各种类型的变体传递给 COM 服务器。  
  
```vb  
Dim mo As New MarshalObject()  
mo.SetVariant(Nothing)         ' Marshal as variant of type VT_EMPTY.  
mo.SetVariant(System.DBNull.Value) ' Marshal as variant of type VT_NULL.  
mo.SetVariant(CInt(27))        ' Marshal as variant of type VT_I2.  
mo.SetVariant(CLng(27))        ' Marshal as variant of type VT_I4.  
mo.SetVariant(CSng(27.0))      ' Marshal as variant of type VT_R4.  
mo.SetVariant(CDbl(27.0))      ' Marshal as variant of type VT_R8.  
```  
  
```csharp  
MarshalObject mo = new MarshalObject();  
mo.SetVariant(null);            // Marshal as variant of type VT_EMPTY.  
mo.SetVariant(System.DBNull.Value); // Marshal as variant of type VT_NULL.  
mo.SetVariant((int)27);          // Marshal as variant of type VT_I2.  
mo.SetVariant((long)27);          // Marshal as variant of type VT_I4.  
mo.SetVariant((single)27.0);   // Marshal as variant of type VT_R4.  
mo.SetVariant((double)27.0);   // Marshal as variant of type VT_R8.  
```  
  
 可使用 <xref:System.Runtime.InteropServices.ErrorWrapper>、<xref:System.Runtime.InteropServices.DispatchWrapper>、<xref:System.Runtime.InteropServices.UnknownWrapper> 和 <xref:System.Runtime.InteropServices.CurrencyWrapper> 等包装类封送不具有相应托管类型的 COM 类型。 以下代码示例演示如何使用这些包装类将各种类型的变体传递给 COM 服务器。  
  
```vb  
Imports System.Runtime.InteropServices  
' Pass inew as a variant of type VT_UNKNOWN interface.  
mo.SetVariant(New UnknownWrapper(inew))  
' Pass inew as a variant of type VT_DISPATCH interface.  
mo.SetVariant(New DispatchWrapper(inew))  
' Pass a value as a variant of type VT_ERROR interface.  
mo.SetVariant(New ErrorWrapper(&H80054002))  
' Pass a value as a variant of type VT_CURRENCY interface.  
mo.SetVariant(New CurrencyWrapper(New Decimal(5.25)))  
```  
  
```csharp  
using System.Runtime.InteropServices;  
// Pass inew as a variant of type VT_UNKNOWN interface.  
mo.SetVariant(new UnknownWrapper(inew));  
// Pass inew as a variant of type VT_DISPATCH interface.  
mo.SetVariant(new DispatchWrapper(inew));  
// Pass a value as a variant of type VT_ERROR interface.  
mo.SetVariant(new ErrorWrapper(0x80054002));  
// Pass a value as a variant of type VT_CURRENCY interface.  
mo.SetVariant(new CurrencyWrapper(new Decimal(5.25)));  
```  
  
 包装类在 <xref:System.Runtime.InteropServices> 命名空间中定义。  
  
### <a name="marshaling-the-iconvertible-interface-to-variant"></a>将 IConvertible 接口封送到变体  
 类型（上一节中列出的类型除外）可通过实现 <xref:System.IConvertible> 接口来控制封送处理它们的方式。 如果对象实现 IConvertible 接口，则 COM 变体类型将在运行时由从 <xref:System.IConvertible.GetTypeCode%2A?displayProperty=fullName> 方法返回的 <xref:System.TypeCode> 枚举值确定。  
  
 下表显示 TypeCode 枚举可能的值以及每个值相应的 COM 变体类型。  
  
|TypeCode|COM 变体类型|  
|--------------|----------------------|  
|TypeCode.Empty|VT_EMPTY|  
|TypeCode.Object|VT_UNKNOWN|  
|TypeCode.DBNull|VT_NULL|  
|TypeCode.Boolean|VT_BOOL|  
|TypeCode.Char|VT_UI2|  
|TypeCode.Sbyte|VT_I1|  
|TypeCode.Byte|VT_UI1|  
|TypeCode.Int16|VT_I2|  
|TypeCode.UInt16|VT_UI2|  
|TypeCode.Int32|VT_I4|  
|TypeCode.UInt32|VT_UI4|  
|TypeCode.Int64|VT_I8|  
|TypeCode.UInt64|VT_UI8|  
|TypeCode.Single|VT_R4|  
|TypeCode.Double|VT_R8|  
|TypeCode.Decimal|VT_DECIMAL|  
|TypeCode.DateTime|VT_DATE|  
|TypeCode.String|VT_BSTR|  
|不支持。|VT_INT|  
|不支持。|VT_UINT|  
|不支持。|VT_ARRAY|  
|不支持。|VT_RECORD|  
|不支持。|VT_CY|  
|不支持。|VT_VARIANT|  
  
 通过调用 IConvertible.To Type 接口确定 COM 变体的值，其中 To Type 是转换例程，它对应于从 IConvertible.GetTypeCode 返回的类型。 例如，将从 IConvertible.GetTypeCode 返回 TypeCode.Double 的对象作为 VT_R8 类型的 COM 变体封送。 通过强制转换为 IConvertible 接口并调用 <xref:System.IConvertible.ToDouble%2A> 方法，可获取变体值（存储在 COM 变体的 dblVal 字段中）。  
  
<a name="cpcondefaultmarshalingforobjectsanchor4"></a>   
## <a name="marshaling-variant-to-object"></a>将变体封送到对象  
 将变体封送到对象时，所封送变体的类型（有时是值）确定生成的对象类型。 下表标识每个变体类型以及变体从 COM 传递给 .NET Framework 时封送拆收器所创建的相应对象类型。  
  
|COM 变体类型|对象类型|  
|----------------------|-----------------|  
|VT_EMPTY|Null 对象引用（在 Visual Basic 中为 Nothing）。|  
|VT_NULL|<xref:System.DBNull?displayProperty=fullName>|  
|VT_DISPATCH|System.__ComObject；如果 (pdispVal == null)，则为 null|  
|VT_UNKNOWN|System.__ComObject；如果 (punkVal == null)，则为 null|  
|VT_ERROR|<xref:System.UInt32?displayProperty=fullName>|  
|VT_BOOL|<xref:System.Boolean?displayProperty=fullName>|  
|VT_I1|<xref:System.SByte?displayProperty=fullName>|  
|VT_UI1|<xref:System.Byte?displayProperty=fullName>|  
|VT_I2|<xref:System.Int16?displayProperty=fullName>|  
|VT_UI2|<xref:System.UInt16?displayProperty=fullName>|  
|VT_I4|<xref:System.Int32?displayProperty=fullName>|  
|VT_UI4|<xref:System.UInt32?displayProperty=fullName>|  
|VT_I8|<xref:System.Int64?displayProperty=fullName>|  
|VT_UI8|<xref:System.UInt64?displayProperty=fullName>|  
|VT_R4|<xref:System.Single?displayProperty=fullName>|  
|VT_R8|<xref:System.Double?displayProperty=fullName>|  
|VT_DECIMAL|<xref:System.Decimal?displayProperty=fullName>|  
|VT_DATE|<xref:System.DateTime?displayProperty=fullName>|  
|VT_BSTR|<xref:System.String?displayProperty=fullName>|  
|VT_INT|<xref:System.Int32?displayProperty=fullName>|  
|VT_UINT|<xref:System.UInt32?displayProperty=fullName>|  
|VT_ARRAY | VT_\*|<xref:System.Array?displayProperty=fullName>|  
|VT_CY|<xref:System.Decimal?displayProperty=fullName>|  
|VT_RECORD|对应装箱的值类型。|  
|VT_VARIANT|不支持。|  
  
 变体类型从 COM 传递给托管代码、再传回 COM，这样的变体类型在调用期间可能不会保留同一变体类型。 请考虑将 VT_DISPATCH 类型的变体从 COM 传递到 .NET Framework 时会发生的情况。 在封送处理期间，变体转换为 <xref:System.Object?displayProperty=fullName>。 如果随后对象传回 COM，则将它封送回 VT_UNKNOWN 类型的变体。 将对象从托管代码封送到 COM 时，无法保证产生的变体与最初用于产生该对象的变体为同一类型。  
  
<a name="cpcondefaultmarshalingforobjectsanchor6"></a>   
## <a name="marshaling-byref-variants"></a>封送 ByRef 变体  
 虽然变体本身可以按值或按引用传递，但 VT_BYREF 标志也可用于任何变体类型，指示变体的内容按引用传递，而不是按值传递。 对于按引用封送变体与使用设置的 VT_BYREF 标志封送变体，人们容易混淆这二者之间的差异。 下图阐明了这些差异。  
  
 ![堆栈上传递的变体](../../../docs/framework/interop/media/interopvariant.gif "interopvariant")  
按值和按引用传递的变体  
  
 **值封送对象和变体的默认行为**  
  
-   将对象从托管代码传递给 COM 时，使用在[将对象封送到变体](#cpcondefaultmarshalingforobjectsanchor3)中定义的规则，将对象内容复制到封送拆收器创建的新变体中。 对非托管端的变体所做的更改不会在从调用返回时传回起始对象。  
  
-   将变体从 COM 传递给托管代码时，使用[将变体封送到对象](#cpcondefaultmarshalingforobjectsanchor4)中定义的规则，将变体内容复制到新创建的对象。 对托管端的对象所做的更改不会在从调用返回时传回起始变体。  
  
 **按引用封送对象和变体的默认行为**  
  
 要将更改传回调用方，必须按引用传递参数。 例如，可使用 C# 中的 ref 关键字（或 Visual Basic 托管代码中的 ByRef），按引用传递参数。 在 COM 中，使用指针（例如 variant \*）传递引用参数。  
  
-   将对象按引用传递给 COM 时，封送拆收器创建一个新变体，并在调用前将对象引用内容复制到变体中。 变体被传递给未托管的函数，用户可在其中随意更改变体的内容。 从调用返回时，对非托管端的变体所做的更改会传回起始对象。 如果变体类型与传递给调用的变体类型不同，则更改会传回另一类型的对象。 也就是说，传递给调用的对象类型可以不同于从调用返回的对象类型。  
  
-   按引用将变体传递给托管代码时，封送拆收器创建一个新对象，并在调用前将变体内容复制到对象中。 对对象的引用被传递给托管函数，用户可在其中随意更改该对象。 从调用返回时，对引用的对象所做的任何更改都将传回起始变体。 如果对象类型与传入调用的对象类型不同，则起始变体的类型发生更改，值传回变体中。 同样，传入调用的变体类型可以不同于从调用返回的变体类型。  
  
 **使用设置的 VT_BYREF 标志封送变体的默认行为**  
  
-   按值传递给托管代码的变体可设置 VT_BYREF 标志，用于指示该变体包含引用而不是值。 在这种情况下，仍会将变体封送到对象，因为变体是按值传递的。 封送拆收器自动取消对变体内容的引用，并在调用前将其复制到新创建的对象中。 然后，将对象传入托管函数中；但是，在从调用返回时，不会将该对象传回起始变体中。 对托管对象所做的更改丢失。  
  
    > [!CAUTION]
    >  即使变体设置了 VT_BYREF 标志，也无法更改按值传递的变体的值。  
  
-   按引用传递给托管代码的变体也可设置 VT_BYREF 标志，用于指示该变体包含另一个引用。 如果采用此做法，则会将该变体封送到 ref 对象，因为变体是按引用传递的。 封送拆收器自动取消对变体内容的引用，并在调用前将其复制到新创建的对象中。 从调用返回时，仅当对象与传入的对象是同一类型时，才会将对象的值传回起始变体内的引用。 也就是说，传播不会更改设置了 VT_BYREF 标志的变体的类型。 如果在调用期间对象类型发生变化，则在从调用返回时将发生 <xref:System.InvalidCastException>。  
  
 下表总结了变体和对象的传播规则。  
  
|From|到|传回的更改|  
|----------|--------|-----------------------------|  
|变体 v|对象 o|Never|  
|对象 o|变体 v|Never|  
|变体 \* pv|Ref 对象 o|Always|  
|Ref 对象 o|变体 \* pv|Always|  
|变体  v (VT_BYREF | VT_)**\***|对象 o|Never|  
|变体 v (VT_BYREF | VT_)|Ref 对象 o|仅类型未发生更改时。|  
  
## <a name="see-also"></a>另请参阅  
 [默认的封送行为](../../../docs/framework/interop/default-marshaling-behavior.md)   
 [Blittable 和非 Blittable 类型](../../../docs/framework/interop/blittable-and-non-blittable-types.md)   
 [方向特性](http://msdn.microsoft.com/en-us/241ac5b5-928e-4969-8f58-1dbc048f9ea2)   
 [复制和锁定](../../../docs/framework/interop/copying-and-pinning.md)

