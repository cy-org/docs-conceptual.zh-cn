---
title: "&lt;属性&gt;无法应用，因为 GUID 的格式&lt;数&gt;不正确 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc32500
- bc32500
dev_langs:
- VB
helpviewer_keywords:
- BC32500
ms.assetid: 6fa34c55-368e-4d7d-b488-07a3fffe045f
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f22f9ecd63582e2a346702919cf9154819b8eb0e
ms.lasthandoff: 03/13/2017

---
# <a name="39ltattributegt39-cannot-be-applied-because-the-format-of-the-guid-39ltnumbergt39-is-not-correct"></a>&lt;属性&gt;无法应用，因为 GUID 的格式&lt;数&gt;不正确
一个`COMClassAttribute`特性块指定不符合正确的格式生成 guid 全局唯一标识符 (GUID)。 `COMClassAttribute`使用 Guid 来唯一地标识类、 接口和创建事件。  
  
 一个 GUID 由 16 个字节组成，其中前八个是数值，而后八个为二进制形式。 它由 Microsoft 的实用工具，例如 uuidgen.exe 并保证在空间和时间是唯一的。  
  
 **错误 ID:** BC32500  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  确定正确的 GUID 或标识的 COM 对象所需的 Guid。  
  
2.  确保正确复制提供给 `COMClassAttribute` 特性块的 GUID 字符串。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Guid></xref:System.Guid>   
[属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)


