---
title: "封送处理不同类型的数组"
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
- marshaling, Arrays sample
- data marshaling, Arrays sample
ms.assetid: c5ac9920-5b6e-4dc9-bf2d-1f6f8ad3b0bf
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3a91c74cf6734776fd6356c201e6754f34a8fbcf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="marshaling-different-types-of-arrays"></a>封送处理不同类型的数组
数组是包含有一个或多个相同类型的元素的托管代码中的引用类型。 尽管数组是引用类型，但它们却作为 In 参数传递到非托管函数。 此行为与托管数组传递到托管对象的方式不一致，数组作为 In/Out 参数进行传递。 有关其他详细信息，请参阅 [复制和锁定](../../../docs/framework/interop/copying-and-pinning.md)。  
  
 下表列出了数组的封送处理选项，并描述了它们的用法。  
  
|数组|描述|  
|-----------|-----------------|  
|通过值传递的整数。|将整数的数组作为 In 参数进行传递。|  
|通过引用传递的整数。|将整数的数组作为 In/Out 参数进行传递。|  
|通过值传递的整数（二维）。|将整数的矩阵作为 In 参数进行传递。|  
|通过值传递的字符串。|将字符串的数组作为 In 参数进行传递。|  
|传递具有整数的结构。|将包含整数的结构数组作为 In 参数进行传递。|  
|传递具有字符串的结构。|将仅包含整数的结构数组作为 In/Out 参数进行传递。 可以更改数组的成员。|  
  
## <a name="example"></a>示例  
 本示例演示如何传递以下类型的数组：  
  
-   通过值传递的整数数组。  
  
-   通过引用传递的整数数组（可以调整大小）。  
  
-   通过值传递的整数多维数组（矩阵）。  
  
-   通过值传递的字符串数组。  
  
-   传递具有整数的结构数组。  
  
-   传递具有字符串的结构数组。  
  
 除非数组由引用显式地进行封送处理，否则将以默认行为将数组封送为 In 参数。 通过显示应用 <xref:System.Runtime.InteropServices.InAttribute> 和 <xref:System.Runtime.InteropServices.OutAttribute> 属性，可以更改此行为。  
  
 数组示例使用以下非托管函数，这些函数与其原始函数声明一起显示：  
  
-   从 PinvokeLib.dll 导出的**TestArrayOfInts** 。  
  
    ```  
    int TestArrayOfInts(int* pArray, int pSize);  
    ```  
  
-   从 PinvokeLib.dll 导出的**TestRefArrayOfInts** 。  
  
    ```  
    int TestRefArrayOfInts(int** ppArray, int* pSize);  
    ```  
  
-   从 PinvokeLib.dll 导出的**TestMatrixOfInts** 。  
  
    ```  
    int TestMatrixOfInts(int pMatrix[][COL_DIM], int row);  
    ```  
  
-   从 PinvokeLib.dll 导出的**TestArrayOfStrings** 。  
  
    ```  
    int TestArrayOfStrings(char** ppStrArray, int size);  
    ```  
  
-   从 PinvokeLib.dll 导出的**TestArrayOfStructs** 。  
  
    ```  
    int TestArrayOfStructs(MYPOINT* pPointArray, int size);  
    ```  
  
-   从 PinvokeLib.dll 导出的**TestArrayOfStructs2** 。  
  
    ```  
    int TestArrayOfStructs2 (MYPERSON* pPersonArray, int size);  
    ```  
  
 [PinvokeLib.dll](http://msdn.microsoft.com/en-us/5d1438d7-9946-489d-8ede-6c694a08f614) 是一个自定义的非托管库，它包含之前列出的函数、两个结构变量（ **MYPOINT** 和 **MYPERSON**）的实现。 此结构包含以下元素：  
  
```  
typedef struct _MYPOINT  
{  
   int x;   
   int y;   
} MYPOINT;  
  
typedef struct _MYPERSON  
{  
   char* first;   
   char* last;   
} MYPERSON;  
```  
  
 在此示例中， `MyPoint` 和 `MyPerson` 结构包含嵌入类型。 设置 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性，以确保成员在内存中按照它们出现的顺序进行排列。  
  
 `LibWrap` 类包含一组 `App` 类调用的方法。 有关传递数组的特定详细信息，请参阅以下示例中的注释。 默认情况下，一个引用类型的数组将作为 In 参数进行传递。 为使调用方接收结果， **InAttribute** 和 **OutAttribute** 必须显式应用于包含该数组的参数。  
  
### <a name="declaring-prototypes"></a>声明原型  
 [!code-csharp[Conceptual.Interop.Marshaling#31](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/arrays.cs#31)] [!code-vb[Conceptual.Interop.Marshaling#31](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/arrays.vb#31)]  
  
### <a name="calling-functions"></a>调用函数  
 [!code-csharp[Conceptual.Interop.Marshaling#32](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/arrays.cs#32)] [!code-vb[Conceptual.Interop.Marshaling#32](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/arrays.vb#32)]  
  
## <a name="see-also"></a>另请参阅  
 [封送类型数组](http://msdn.microsoft.com/en-us/049b1c1b-228f-4445-88ec-91bc7fd4b1e8)   
 [平台调用数据类型](http://msdn.microsoft.com/en-us/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [在托管代码中创建原型](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)

