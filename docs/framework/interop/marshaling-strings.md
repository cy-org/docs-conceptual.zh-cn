---
title: "封送处理字符串"
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
- marshaling, samples
- platform invoke, marshaling data
- data marshaling, strings
- data marshaling, samples
- data marshaling, platform invoke
- marshaling. strings
- marshaling, platform invoke
- sample applications [.NET Framework], marshaling strings
ms.assetid: e21b078b-70fb-4905-be26-c097ab2433ff
caps.latest.revision: 9
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8d8455d4f1b4dbb463176c06d680b2bd0b1ff9d9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="marshaling-strings"></a>封送处理字符串
平台调用复制字符串参数，根据需要将其从 .NET Framework 格式 (Unicode) 转换为非托管格式 (ANSI)。 由于托管的字符串不可变，在函数返回时，平台调用并不将它们从非托管内存复制回托管内存。  
  
 下表列出了字符串的封送处理选项，描述了它们的用法，并提供了指向相应 .NET Framework 示例的链接。  
  
|String|描述|示例|  
|------------|-----------------|------------|  
|按值。|将字符串作为 In 参数传递。|[MsgBox](../../../docs/framework/interop/msgbox-sample.md)|  
|作为结果。|从非托管代码返回字符串。|[字符串](http://msdn.microsoft.com/en-us/be9e82a3-dc95-4aaa-9396-61b66e467e02)|  
|按引用。|使用 <xref:System.Text.StringBuilder> 将字符串作为 In/Out 参数传递。|[缓冲区](http://msdn.microsoft.com/en-us/e30d36e8-d7c4-4936-916a-8fdbe4d9ffd5)|  
|结构中按值。|在作为 In 参数的结构中传递字符串。|[结构](http://msdn.microsoft.com/en-us/96a62265-dcf9-4608-bc0a-1f762ab9f48e)|  
|结构中按引用 (char\*)。|在作为 In/Out 参数的结构中传递字符串。 非托管函数需要指向字符缓冲区的指针，并且该缓冲区大小是结构的成员。|[字符串](http://msdn.microsoft.com/en-us/be9e82a3-dc95-4aaa-9396-61b66e467e02)|  
|结构中按引用 (char[])。|在作为 In/Out 参数的结构中传递字符串。 非托管函数需要嵌入字符缓冲区。|[OSInfo](http://msdn.microsoft.com/en-us/69d89067-507b-41fe-859d-30bf3ff29455)|  
|类中按值 (char\*)。|在类（类是 In/Out 参数）中传递字符串。 非托管函数需要指向字符缓冲区的指针。|[OpenFileDlg](http://msdn.microsoft.com/en-us/b7dea792-cb92-4baf-ac7b-6a24803e6c75)|  
|类中按值 (char[])。|在类（类是 In/Out 参数）中传递字符串。 非托管函数需要嵌入字符缓冲区。|[OSInfo](http://msdn.microsoft.com/en-us/69d89067-507b-41fe-859d-30bf3ff29455)|  
|作为字符串数组按值。|创建按值传递的字符串数组。|[阵列](../../../docs/framework/interop/marshaling-different-types-of-arrays.md)|  
|作为包含字符串的结构数组按值。|创建包含字符串的结构数组，且该数组是按值传递的。|[阵列](../../../docs/framework/interop/marshaling-different-types-of-arrays.md)|  
  
## <a name="see-also"></a>另请参阅  
 [使用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)   
 [平台调用数据类型](http://msdn.microsoft.com/en-us/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [封送类、结构和联合](../../../docs/framework/interop/marshaling-classes-structures-and-unions.md)   
 [封送类型数组](http://msdn.microsoft.com/en-us/049b1c1b-228f-4445-88ec-91bc7fd4b1e8)   
 [其他封送处理示例](http://msdn.microsoft.com/en-us/a915c948-54e9-4d0f-a525-95a77fd8ed70)

