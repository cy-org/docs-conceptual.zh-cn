---
title: '&lt;webMessageEncoding&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 892ca485-e21a-4a44-8e40-633161ef6796
caps.latest.revision: 7
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 06920c0ebce33d7e55bc56ddb29843bba43de7a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="ltwebmessageencodinggt"></a>&lt;webMessageEncoding&gt;
在 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 绑定中使用纯文本 XML 与 JavaScript 对象表示法 (JSON) 消息编码以及“原始”二进制内容时，能够对其进行读写。  
  
 \<system.serviceModel >  
\<绑定 >  
\<customBinding >  
\<绑定 >  
\<webMessageEncoding >  
  
## <a name="syntax"></a>语法  
  
```xml  
<webMessageEncoding   
      maxReadPoolSize="Integer"  
   maxWritePoolSize="Integer"  
  
writeEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`maxReadPoolSize`|无需分配新的读取器便可同时读取的消息数。 池越大，系统允许的活动峰值就越大，但工作集也会随之增大。 默认情况下将为每个内部编码器（文本、JSON 和“原始”）分配 64 个读取器。<br /><br /> 增大此数字将会增加内存消耗，但能够让编码器处理传入消息的突现高峰，因为编码器可以使用池中已创建的读取器，而不必创建新的读取器。|  
|`maxWritePoolSize`|无需分配新的编写器便可同时发送的消息数。 池越大，系统允许的活动峰值就越大，但工作集也会随之增大。 默认情况下将为每个内部编码器（文本、JSON 和“原始”）分配 16 个编写器。<br /><br /> 增大此数字将会增加内存消耗，但能够让编码器处理传出消息的突现高峰，因为编码器可以使用池中已创建的编写器，而不必创建新的编写器。|  
|`writeEncoding`|指定要用来在绑定上发出消息的字符集编码。 有效值为：<br /><br /> -UnicodeFffeTextEncoding: Unicode Big Endian 编码。<br />-Utf16TextEncoding: Unicode 编码。<br />-Utf8TextEncoding: 8 位编码。<br /><br /> 默认值为 Utf8TextEncoding。 此属性的类型为 <xref:System.Text.Encoding>。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<readerQuotas >](http://msdn.microsoft.com/library/3e5e42ff-cef8-478f-bf14-034449239bfd)|定义可由采用此绑定配置的终结点进行处理的 SOAP 消息的复杂性约束。 此元素的类型为 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<绑定 >](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## <a name="remarks"></a>备注  
 编码是将消息转换为一个字节序列的过程。 解码是反向过程。 这些过程都需要字符编码规范。  
  
 `webMessageEncoding` 元素的工作方式是委托一系列内部编码器对纯文本 XML 与 JSON 编码以及“原始”二进制数据进行处理。 委托由复合消息编码器来完成。  
  
 在不使用 SOAP 消息（由 `webHttpBinding` 元素使用）的方案中，用该绑定元素及其复合编码器控制编码。 这些方案包括“纯旧式 XML”(POX)、具象状态传输 (REST)、真正简单的整合 (RSS) 与 Atom 整合以及异步 JavaScript 和 XML (AJAX)。 复合消息编码器不支持 SOAP 或 WS-Addressing。  
  
 可以使用 `writeEncoding` 属性通过写字符编码来配置绑定元素。 所提供的 <xref:System.Text.Encoding> 值指定 JSON 与文本 XML 情况的编写行为。 在读取时，将理解任何有效的消息编码与文本编码。  
  
 属性 `maxReadPoolSize` 与 `maxWritePoolSize` 也可以分别用来设置要分配的读取器和编写器最大数目。 默认情况下，将分配 64 个读取器和 16 个编写器。  
  
 默认复杂性约束也都设置使用[ \<readerQuotas >](http://msdn.microsoft.com/library/3e5e42ff-cef8-478f-bf14-034449239bfd)企图利用消息复杂性来占用终结点处理的元素，以防止某种类型的拒绝服务 (DOS) 攻击资源。  
  
## <a name="example"></a>示例  
  
```xml  
<webMessageEncoding   
    maxReadPoolSize="256"  
    maxWritePoolSize="128"  
    messageVersion="None"  
    textEncoding="utf-8"   
/>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Configuration.WebMessageEncodingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>   
 [消息编码](../../../../../docs/framework/configure-apps/file-schema/wcf/message-encoding.md)   
 [选择消息编码器](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

