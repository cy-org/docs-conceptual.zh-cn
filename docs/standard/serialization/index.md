---
title: ".NET 中的序列化"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XML serialization, defined
- binary serialization
- serializing objects
- serialization
- objects, serializing
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 4aaef3337c9ee2464925ed4dc31c075a4e68a9dc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="serialization-in-net"></a>.NET 中的序列化
序列化是将对象状态转换为可保持或传输的形式的过程。 序列化的补集是反序列化，后者将流转换为对象。 这两个过程一起保证数据易于存储和传输。  
  
.NET 具有两种序列化技术：  
  
-   二进制序列化保持类型保真，这对于多次调用应用程序时保持对象状态非常有用。 例如，通过将对象序列化到剪贴板，可在不同的应用程序之间共享对象。 您可以将对象序列化到流、磁盘、内存和网络等。 远程处理使用序列化，“按值”在计算机或应用程序域之间传递对象。  
  
-   XML 序列化只序列化公共属性和字段，并且不保持类型保真。 当您希望提供或使用数据而不限制使用该数据的应用程序时，这一点非常有用。 由于 XML 是开放式的标准，因此它对于通过 Web 共享数据来说是一个理想选择。 SOAP 同样是开放式的标准，这使它也成为一个理想选择。  
  
## <a name="in-this-section"></a>本节内容  
[序列化帮助主题](../../../docs/standard/serialization/serialization-how-to-topics.md)  
列出指向此节中包含的“如何”主题的链接。
  
[二进制序列化](../../../docs/standard/serialization/binary-serialization.md)  
描述随公共语言运行库一起提供的二进制序列化机制。

[XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)  
描述随公共语言运行库一起提供的 XML 和 SOAP 序列化机制。

[序列化工具](../../../docs/standard/serialization/serialization-tools.md)  
这些工具可帮助开发序列化代码。

[序列化示例](../../../docs/standard/serialization/serialization-samples.md)  
这些示例演示了如何进行序列化。

## <a name="reference"></a>参考
<xref:System.Runtime.Serialization> 包含可用于序列化和反序列化对象的类。
  
<xref:System.Xml.Serialization>  
包含可用于将对象序列化为 XML 格式的文档或流的类。
