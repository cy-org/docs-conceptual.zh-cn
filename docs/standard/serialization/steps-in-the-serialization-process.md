---
title: "序列化过程中的步骤"
ms.date: 08/07/2017
ms.prod: .net
ms.topic: article
helpviewer_keywords:
- binary serialization, steps
- serialization, steps
ms.assetid: 4bcbc883-2a91-418f-b968-6c86a25e9737
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: a4c125493e1b59d329bf4626c45f48b2b222d308
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="steps-in-the-serialization-process"></a>序列化过程中的步骤
对[格式化程序](xref:System.Runtime.Serialization.Formatter)调用 <xref:System.Runtime.Serialization.Formatter.Serialize*> 方法时，将按照以下规则顺序进行对象序列化：

- 进行检查以确定格式化程序是否具有代理项选择器。 如果有，则检查代理项选择器是否处理给定类型的对象。 如果选择器处理该对象类型，则在代理项选择器上调用 <xref:System.Runtime.Serialization.ISerializable.GetObjectData*?displayProperty=fullName>。

- 如果没有代理项选择器，或者代理项选择器不处理该对象类型，则进行检查以确定是否用 [Serializable](xref:System.SerializableAttribute) 属性标记了该对象。 如果未标记该对象，则会引发 <xref:System.Runtime.Serialization.SerializationException>。

- 如果已相应地标记了对象，则检查该对象是否实现 <xref:System.Runtime.Serialization.ISerializable> 接口。 如果对象实现接口，则对该对象调用 <xref:System.Runtime.Serialization.ISerializable.GetObjectData*>。
  
- 如果对象未实现 <xref:System.Runtime.Serialization.ISerializable>，则使用默认序列化策略，从而序列化所有未标记为 [NonSerialized](xref:System.NonSerializedAttribute) 的字段。

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
## <a name="see-also"></a>另请参阅  
 [二进制序列化](binary-serialization.md)   
 [XML 和 SOAP 序列化](xml-and-soap-serialization.md)
