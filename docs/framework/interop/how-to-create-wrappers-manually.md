---
title: "如何：手动创建包装"
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
- wrappers, creating manually
ms.assetid: cc2a70d8-6a58-4071-a8cf-ce28c018c09b
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 218e92b379d562be66c72cb731654907766f2ec4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-create-wrappers-manually"></a>如何：手动创建包装
如果决定在托管源代码中手动声明 COM 类型，则最佳的着手点是现有的接口定义语言 (IDL) 文件或类型库。 不具备 IDL 文件或无法生成类型库文件时，可以通过创建托管的声明并将生成的程序集导出到类型库来模拟 COM 类型。  
  
### <a name="to-simulate-com-types-from-managed-source"></a>从托管源模拟 COM 类型  
  
1.  在符合公共语言规范 (CLS) 的语言中声明类型并编译文件。  
  
2.  使用[类型库导出程序 (Tlbexp.exe)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md) 导出包含类型的程序集。  
  
3.  将导出的 COM 类型库用作声明面向 COM 托管类型的基础。  
  
### <a name="to-create-a-runtime-callable-wrapper-rcw"></a>创建运行时可调用包装器 (RCW)  
  
1.  假设你有一个 IDL 文件或类型库文件，请决定要在自定义 RCW 中包含哪些类和接口。 可以排除不打算在应用程序中直接或间接使用的任何类型。  
  
2.  在符合 CLS 的语言中创建一个源文件，并声明类型。 有关导入转换过程的完整说明，请参阅[有关从类型库转换到程序集的摘要](http://msdn.microsoft.com/en-us/bf3f90c5-4770-4ab8-895c-3ba1055cc958)。 实际上，创建自定义 RCW 时，需要手动执行由[类型库导入程序 (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) 所提供的类型转换活动。 下一章节的示例显示 IDL 或类型库文件中的类型以及它们在 C# 代码中的对应类型。  
  
3.  完成声明后，请像编译任何其他托管源代码一样编译此文件。  
  
4.  与使用 Tlbimp.exe 导入的类型相同，某些类型需要其他信息，你可以将其直接添加到自己的代码中。 有关详细信息，请参阅[如何：编辑互操作程序集](http://msdn.microsoft.com/en-us/16aacb20-2269-42bf-a812-b6a7df17e277)。  
  
## <a name="example"></a>示例  
 以下代码演示了 IDL 中的 `ISATest` 接口和 `SATest` 类以及 C# 源代码中相应类型的示例。  
  
 **IDL 或类型库文件**  
  
```  
 [  
object,  
uuid(40A8C65D-2448-447A-B786-64682CBEF133),  
dual,  
helpstring("ISATest Interface"),  
pointer_default(unique)  
 ]  
interface ISATest : IDispatch  
 {  
[id(1), helpstring("method InSArray")]   
HRESULT InSArray([in] SAFEARRAY(int) *ppsa, [out,retval] int *pSum);  
 };  
 [  
uuid(116CCA1E-7E39-4515-9849-90790DA6431E),  
helpstring("SATest Class")  
 ]  
coclass SATest  
 {  
  [default] interface ISATest;  
 };  
```  
  
 **托管源代码的包装器**  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
using System.Runtime.CompilerServices;  
  
[assembly:Guid("E4A992B8-6F5C-442C-96E7-C4778924C753")]  
[assembly:ImportedFromTypeLib("SAServerLib")]  
namespace SAServer  
{  
 [ComImport]  
 [Guid("40A8C65D-2448-447A-B786-64682CBEF133")]  
 [TypeLibType(TypeLibTypeFlags.FLicensed)]  
 public interface ISATest  
 {  
  [DispId(1)]  
  //[MethodImpl(MethodImplOptions.InternalCall,  
  // MethodCodeType=MethodCodeType.Runtime)]  
  int InSArray( [MarshalAs(UnmanagedType.SafeArray,  
      SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }   
 [ComImport]  
 [Guid("116CCA1E-7E39-4515-9849-90790DA6431E")]  
 [ClassInterface(ClassInterfaceType.None)]   
 [TypeLibType(TypeLibTypeFlags.FCanCreate)]  
 public class SATest : ISATest   
 {  
  [DispId(1)]  
  [MethodImpl(MethodImplOptions.InternalCall,   
  MethodCodeType=MethodCodeType.Runtime)]  
  extern int ISATest.InSArray( [MarshalAs(UnmanagedType.SafeArray,   
  SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [自定义运行时可调用包装器](http://msdn.microsoft.com/en-us/4652beaf-77d0-4f37-9687-ca193288c0be)   
 [COM 数据类型](http://msdn.microsoft.com/en-us/f93ae35d-a416-4218-8700-c8218cc90061)   
 [如何：编辑互操作程序集](http://msdn.microsoft.com/en-us/16aacb20-2269-42bf-a812-b6a7df17e277)   
 [有关从类型库转换到程序集的摘要](http://msdn.microsoft.com/en-us/bf3f90c5-4770-4ab8-895c-3ba1055cc958)   
 [Tlbimp.exe（类型库导入程序）](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)   
 [Tlbexp.exe（类型库导出程序）](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)

