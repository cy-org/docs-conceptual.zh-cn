---
title: "可直接复制到本机结构中的类型和非直接复制到本机结构中的类型"
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
- interop marshaling, blittable types
- blittable types, interop marshaling
ms.assetid: d03b050e-2916-49a0-99ba-f19316e5c1b3
caps.latest.revision: 23
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3fa97ee1df14b5e08faa944265675264c0b6d95a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="blittable-and-non-blittable-types"></a>可直接复制到本机结构中的类型和非直接复制到本机结构中的类型
大多数数据类型在托管和非托管内存中具有共同的表示形式，而且不需要互操作封送处理程序进行特殊处理。 这些类型称为 blittable 类型，因为它们在托管和非托管代码之间传递时不需要进行转换。  
  
 从平台调用返回的结构必须是 blittable 类型。 平台调用不支持返回类型为 non-blittable 结构。  
  
 以下 <xref:System> 命名空间中的类型即是 blittable 类型：  
  
-   <xref:System.Byte?displayProperty=nameWithType>  
  
-   <xref:System.SByte?displayProperty=nameWithType>  
  
-   <xref:System.Int16?displayProperty=nameWithType>  
  
-   <xref:System.UInt16?displayProperty=nameWithType>  
  
-   <xref:System.Int32?displayProperty=nameWithType>  
  
-   <xref:System.UInt32?displayProperty=nameWithType>  
  
-   <xref:System.Int64?displayProperty=nameWithType>  
  
-   <xref:System.UInt64?displayProperty=nameWithType>  
  
-   <xref:System.IntPtr?displayProperty=nameWithType>  
  
-   <xref:System.UIntPtr?displayProperty=nameWithType>  
  
-   <xref:System.Single?displayProperty=nameWithType>  
  
-   <xref:System.Double?displayProperty=nameWithType>  
  
 下面的复杂类型也是 blittable 类型：  
  
-   所有 blittable 类型的一维数组，如整数数组。 但是，包含 blittable 类型变量数组的类型本身不是 blittable 类型。  
  
-   所有只包含 blittable 类型（和作为格式化类型进行封送的类）的格式化的值类型。 有关格式化的值类型的详细信息，请参阅[值类型的默认封送处理](http://msdn.microsoft.com/en-us/4d9a876c-e05a-40ba-bd85-bd22877f984a)。  
  
 对象引用不是 blittable 类型。 这包括本身是 blittable 的对象的引用数组。 例如，可以定义一个属于 blittable 类型的结构，但不能定义包含这些结构的引用数组的 blittable 类型。  
  
 作为一种优化方式，所有 blittable 类型数组和只包含 blittable 成员的类都是[固定的](../../../docs/framework/interop/copying-and-pinning.md)，因此无需在封送处理期间进行复制。 若调用方和被调用方位于同一单元中，这些类型会显示为作为 In/Out 参数被封送。 但是，这些类型实际上是作为 In 形参进行封送的，而且，如果要将实参作为 In/Out 形参进行封送，则必须应用 <xref:System.Runtime.InteropServices.InAttribute> 和 <xref:System.Runtime.InteropServices.OutAttribute> 属性。  
  
 在非托管环境中，某些托管数据类型要求具有不同的表示形式。 必须将这些 non-blittable 数据类型转换为可以封送的形式。 例如，托管字符串就是 non-blittable 类型，因为这些字符串必须转换为字符串对象后才能进行封送。  
  
 下表列出了 <xref:System> 命名空间中的 non-blittable 类型。 [委托](http://msdn.microsoft.com/en-us/d176ee76-f982-494b-b03d-92e4118896e2)是引用静态方法或类实例的数据结构，也是 non-blittable 类型。  
  
|Non-blittable 类型|描述|  
|-------------------------|-----------------|  
|[System.Array](../../../docs/framework/interop/default-marshaling-for-arrays.md)|转换为 C 样式数组或 `SAFEARRAY`。|  
|[System.Boolean](http://msdn.microsoft.com/en-us/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)|转换为 1、2 或 4 字节的值，`true` 表示 1 或 -1。|  
|[System.Char](http://msdn.microsoft.com/en-us/cecc87c1-075e-4cde-aa56-33d189f66feb)|转换为 Unicode 或 ANSI 字符。|  
|[System.Class](http://msdn.microsoft.com/en-us/fe334af5-0123-43d8-be84-26f6f023ddb6)|转换为类接口。|  
|[System.Object](../../../docs/framework/interop/default-marshaling-for-objects.md)|转换为变量或接口。|  
|[System.Mdarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|转换为 C 样式数组或 `SAFEARRAY`。|  
|[System.String](../../../docs/framework/interop/default-marshaling-for-strings.md)|转换为空引用中的终止字符串或转换为 BSTR。|  
|[System.Valuetype](http://msdn.microsoft.com/en-us/4d9a876c-e05a-40ba-bd85-bd22877f984a)|转换为具有固定内存布局的结构。|  
|[System.Szarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|转换为 C 样式数组或 `SAFEARRAY`。|  
  
 类和对象类型仅受 COM 互操作支持。 有关 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)]、C# 和 C++ 中的相应类型的信息，请参阅[类库概述](../../../docs/standard/class-library-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 [默认封送处理行为](../../../docs/framework/interop/default-marshaling-behavior.md)

