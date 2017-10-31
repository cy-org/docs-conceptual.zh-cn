---
title: "使用 Message 类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d62bfb-2aa3-4170-b6f8-c93d3afdbbed
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 使用 Message 类
<xref:System.ServiceModel.Channels.Message>类是至关重要的[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]。 客户端和服务之间的所有通信最终会都导致<xref:System.ServiceModel.Channels.Message>实例正在发送和接收。  
  
 您将不通常与交互<xref:System.ServiceModel.Channels.Message>直接类。 相反，您需要使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务模型构造（如数据协定、消息协定和操作协定）来描述传入消息和传出消息。 但是，在某些高级的方案使用编程<xref:System.ServiceModel.Channels.Message>直接类。 例如，您可能想要使用<xref:System.ServiceModel.Channels.Message>类︰  
  
-   需要一种替代方式来创建传出的消息内容（例如，从磁盘上的文件直接创建消息），而不是序列化 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 对象。  
  
-   需要一种替代方式来使用传入的消息内容（例如，需要将 XSLT 转换应用于原始 XML 内容），而不是反序列化为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 对象。  
  
-   无论消息内容怎样都需要使用常规方式来处理消息（例如，在生成路由器、负载平衡器或发布-订阅系统时对消息进行路由或转发）。  
  
 在使用之前<xref:System.ServiceModel.Channels.Message>类中，自己应熟悉[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]数据传输中的体系结构[数据传输体系结构概述](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)。  
  
 一个<xref:System.ServiceModel.Channels.Message>是通用的数据容器，但其设计严格遵循 SOAP 协议中消息的设计方式。 就像 SOAP 中一样，消息同时具有消息正文和标头。 消息正文包含实际负载数据，而标头包含其他已命名的数据容器。 用于读取和写入消息正文与标头的规则是不同的，例如，标头总是在内存中进行缓冲，并且可以按任意顺序访问任意次，而正文仅能读取一次且可以进行流式处理。 通常，使用 SOAP 时，消息正文被映射到 SOAP 正文，而消息头被映射到 SOAP 标头。  
  
## <a name="using-the-message-class-in-operations"></a>在操作中使用 Message 类  
 您可以使用<xref:System.ServiceModel.Channels.Message>作为输入参数的操作、 和 / 或操作的返回值的类。 如果<xref:System.ServiceModel.Channels.Message>使用任意位置在操作中，以下限制适用︰  
  
-   操作不能具有任何 `out` 或 `ref` 参数。  
  
-   不能有一个以上的 `input` 参数。 如果该参数存在，其类型必须为 Message 或消息协定。  
  
-   返回类型必须为 `void`、`Message` 或消息协定类型。  
  
 下面的代码示例包含一个有效的操作协定。  
  
 [!code-csharp[C_UsingTheMessageClass#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#1)]
 [!code-vb[C_UsingTheMessageClass#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#1)]  
  
## <a name="creating-basic-messages"></a>创建基本消息  
 <xref:System.ServiceModel.Channels.Message>类提供了静态`CreateMessage`工厂方法可用于创建基本消息。  
  
 所有`CreateMessage`重载都采用类型的版本参数<xref:System.ServiceModel.Channels.MessageVersion> ，该值指示要用于消息的 SOAP 和 Ws-addressing 版本。 如果您想要使用相同的协议版本与传入消息，则可以使用<xref:System.ServiceModel.OperationContext.IncomingMessageVersion%2A>属性<xref:System.ServiceModel.OperationContext>实例获取的从<xref:System.ServiceModel.OperationContext.Current%2A>属性。 大多数 `CreateMessage` 重载还具有一个字符串参数，该参数指示要用于消息的 SOAP 操作。 可以将版本设置为 `None` 以禁用 SOAP 信封生成；消息仅包含正文。  
  
## <a name="creating-messages-from-objects"></a>从对象创建消息  
 仅采用一个版本和一个操作作为参数的最基本的 `CreateMessage` 重载可创建一条正文为空的消息。 另一个重载采用一个附加<xref:System.Object>参数; 这将创建一条消息的正文是给定对象的序列化的表示。 使用<xref:System.Runtime.Serialization.DataContractSerializer>使用序列化的默认设置。 如果要使用其他序列化程序，或者希望对 `DataContractSerializer` 进行不同配置，请使用也采用一个 `CreateMessage` 参数的 `XmlObjectSerializer` 重载。  
  
 例如，若要在消息中返回一个对象，可以使用下面的代码。  
  
 [!code-csharp[C_UsingTheMessageClass#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#2)]
 [!code-vb[C_UsingTheMessageClass#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#2)]  
  
## <a name="creating-messages-from-xml-readers"></a>从 XML 读取器创建消息  
 有`CreateMessage`重载采用<xref:System.Xml.XmlReader>或<xref:System.Xml.XmlDictionaryReader>正文而不是对象。 在这种情况下，消息的正文会包含从传递的 XML 读取器中进行读取而产生的 XML。 例如，下面的代码会返回一条消息，该消息的正文内容是从一个 XML 文件中读取的。  
  
 [!code-csharp[C_UsingTheMessageClass#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#3)]
 [!code-vb[C_UsingTheMessageClass#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#3)]  
  
 此外，还有一些`CreateMessage`重载采用<xref:System.Xml.XmlReader>或<xref:System.Xml.XmlDictionaryReader> ，表示整个消息，而不仅仅是正文。 这些重载还采用一个整型 `maxSizeOfHeaders` 参数。 一旦创建了消息，标头就总是在内存中进行缓冲，而此参数用于限制发生的缓冲数量。 如果 XML 来自不受信任的源，那么为了降低发生拒绝服务攻击的可能性，将此参数设置为安全值就变得十分重要。 XML 读取器表示的消息的 SOAP 和 WS-Addressing 版本必须与使用版本参数指示的版本相匹配。  
  
## <a name="creating-messages-with-bodywriter"></a>使用 BodyWriter 创建消息  
 有一种 `CreateMessage` 重载采用一个 `BodyWriter` 实例来描述消息的正文。 `BodyWriter` 是一个抽象类，可以从该类派生以自定义创建消息正文的方式。 您可以创建自己的 `BodyWriter` 派生类，以便按照自定义方式来描述消息正文。 必须重写`BodyWriter.OnWriteBodyContents`采用的方法<xref:System.Xml.XmlDictionaryWriter>; 此方法负责写出正文。  
  
 正文编写器可以是缓冲式的，也可以是非缓冲式的（流式）。 缓冲式正文编写器可以任意次写出其内容，而流式正文编写器只能写出其内容一次。 `IsBuffered` 属性指示正文编写器是否为缓冲式的。 通过调用受保护的 `BodyWriter` 构造函数（该构造函数采用一个 `isBuffered` 布尔参数），可以设置正文编写器的这一属性。 正文编写器支持从非缓冲式正文编写器创建缓冲式正文编写器。 可以重写 `OnCreateBufferedCopy` 方法以自定义此过程。 默认情况下，使用包含由 `OnWriteBodyContents` 返回的 XML 的内存中缓冲区。 `OnCreateBufferedCopy` 采用一个 `maxBufferSize` 整型参数；如果重写此方法，则不得创建大于此最大大小的缓冲区。  
  
 `BodyWriter` 类提供了 `WriteBodyContents` 和 `CreateBufferedCopy` 方法，这两个方法实质上分别是 `OnWriteBodyContents` 和 `OnCreateBufferedCopy` 方法的瘦包装。 这些方法执行状态检查，以确保访问非缓冲式正文编写器的次数不会超过一次。 仅当基于 `Message` 创建自定义 `BodyWriters` 派生类时才直接调用这些方法。  
  
## <a name="creating-fault-messages"></a>创建错误消息  
 可以使用某些 `CreateMessage` 重载创建 SOAP 错误消息。 最基本的这些重载采用<xref:System.ServiceModel.Channels.MessageFault>描述错误的对象。 其他重载是为方便起见而提供的。 第一个这样的重载采用一个 `FaultCode` 和一个原因字符串作为参数，并使用 `MessageFault`（该方法使用这些信息）创建一个 `MessageFault.CreateFault`。 另一个重载采用一个详细信息对象作为参数，并将该对象与错误代码和原因一起传递给 `CreateFault`。 例如，下面的操作会返回一个错误。  
  
 [!code-csharp[C_UsingTheMessageClass#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#4)]
 [!code-vb[C_UsingTheMessageClass#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#4)]  
  
## <a name="extracting-message-body-data"></a>提取消息正文数据  
 `Message` 类支持多种从其正文提取信息的方式。 它们可分为以下几类：  
  
-   将整个消息正文一次性写出到 XML 编写器。 这被称为*写完邮件*。  
  
-   将 XML 读取器放在消息正文上。 这使您可以在以后根据需要逐段访问消息正文。 这被称为*读取一条消息*。  
  
-   可以将整个消息，包括其正文复制到内存中缓冲区的<xref:System.ServiceModel.Channels.MessageBuffer>类型。 这被称为*将消息复制*。  
  
 无论使用哪种访问方式，都只能访问 `Message` 的正文一次。 消息对象具有 `State` 属性，该属性最初设置为 Created。 前面列表中描述的三种访问方法分别将状态设置为 Written、Read 和 Copied。 此外，`Close` 方法可以在不再需要消息正文内容时将状态设置为 Closed。 只有当消息正文处于 Created 状态时，才能对其进行访问，并且在状态已更改后，无法返回到 Created 状态。  
  
## <a name="writing-messages"></a>写入消息  
 <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29>方法写出正文内容的给定`Message`实例与给定的 XML 编写器。 <xref:System.ServiceModel.Channels.Message.WriteBody%2A>方法也是如此，只不过它将正文内容封装在适当的包装元素 (例如， `soap:body`1>)。 最后， <xref:System.ServiceModel.Channels.Message.WriteMessage%2A>写出整个消息，包括包装 SOAP 信封和标头。 如果禁用 SOAP（Version 为 `MessageVersion.None`），则所有这三个方法都执行相同的操作：写出消息正文内容。  
  
 例如，下面的代码将一个传入消息的正文写出到一个文件中。  
  
 [!code-csharp[C_UsingTheMessageClass#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#5)]
 [!code-vb[C_UsingTheMessageClass#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#5)]  
  
 另有两个帮助器方法可写出某些 SOAP 开始元素标记。 这些方法不访问消息正文，因而不会更改消息状态。 其中包括:  
  
-   <xref:System.ServiceModel.Channels.Message.WriteStartBody%2A>写入开始正文元素，如`<soap:Body>`。  
  
-   <xref:System.ServiceModel.Channels.Message.WriteStartEnvelope%2A>写入开始信封元素，如`<soap:Envelope>`。  
  
 若要写入相应的结束元素标记，请对相应的 XML 编写器调用 `WriteEndElement`。 直接调用这些方法的情况极少。  
  
## <a name="reading-messages"></a>读取消息  
 读取消息正文的主要方法是调用<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>。 您得到<xref:System.Xml.XmlDictionaryReader>可用于读取消息正文。 请注意，<xref:System.ServiceModel.Channels.Message>转换到 Read 状态就立即<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>调用时，而不在您使用返回的 XML 读取器时发生。  
  
 <xref:System.ServiceModel.Channels.Message.GetBody%2A>方法还使您可以访问消息正文作为类型化对象。 在内部，此方法使用`GetReaderAtBodyContents`，因而也会转换到的消息状态<xref:System.ServiceModel.Channels.MessageState>状态 (请参阅<xref:System.ServiceModel.Channels.Message.State%2A>属性)。  
  
 很好的做法检查<xref:System.ServiceModel.Channels.Message.IsEmpty%2A>属性，在这种情况下消息正文为空并<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>引发<xref:System.InvalidOperationException>。 此外，如果是接收的消息 （例如，答复），可能还想要检查<xref:System.ServiceModel.Channels.Message.IsFault%2A>，该属性指示消息是否包含一个错误。  
  
 最基本的重载<xref:System.ServiceModel.Channels.Message.GetBody%2A>消息正文反序列化为的类型 （由泛型参数指示） 使用实例<xref:System.Runtime.Serialization.DataContractSerializer>配置为使用默认设置以及<xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A>禁用配额。 如果您想要使用不同的序列化引擎，或配置`DataContractSerializer`非默认方式，使用<xref:System.ServiceModel.Channels.Message.GetBody%2A>重载， <xref:System.Runtime.Serialization.XmlObjectSerializer>。  
  
 例如，下面的代码从包含一个序列化 `Person` 对象的消息正文中提取数据，然后输出人员的姓名。  
  
 [!code-csharp[C_UsingTheMessageClass#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#6)]
 [!code-vb[C_UsingTheMessageClass#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#6)]  
  
## <a name="copying-a-message-into-a-buffer"></a>将消息复制到缓冲区中  
 有时需要不只一次地访问消息正文，例如，作为发行者-订户系统的一部分而将同一消息转发给多个目标。 在这种情况下，需要在内存中缓冲整个消息（包括正文）。 你可以通过调用<xref:System.ServiceModel.Channels.Message.CreateBufferedCopy%28System.Int32%29>。 此方法采用一个表示最大缓冲区大小的整型参数，且创建一个不大于此大小的缓冲区。 如果消息来自不受信任的源，则将此参数设置为安全值是十分重要的。  
  
 作为返回缓冲区<xref:System.ServiceModel.Channels.MessageBuffer>实例。 可以通过几种方式访问缓冲区中的数据。 主要方法是调用<xref:System.ServiceModel.Channels.Message.CreateMessage%2A>创建`Message`从缓冲区的实例。  
  
 若要访问缓冲区中的数据的另一种方法是实现<xref:System.Xml.XPath.IXPathNavigable>接口<xref:System.ServiceModel.Channels.MessageBuffer>类直接访问基础 XML 的实现。 某些<xref:System.ServiceModel.Channels.MessageBuffer.CreateNavigator%2A>重载允许您创建<xref:System.Xml.XPath>导航器保护的节点配额，限制可以访问的 XML 节点的数目。 这有助于防止通过占用大量处理时间而实施的拒绝服务攻击。 默认情况下禁用此配额。 某些`CreateNavigator`重载允许您指定的空白区域应如何处理在 XML 中使用<xref:System.Xml.XmlSpace>枚举，具有默认值为`XmlSpace.None`。  
  
 最后一种方式访问消息缓冲区的内容是为流使用的内容写出<xref:System.ServiceModel.Channels.Message.WriteMessage%2A>。  
  
 下面的示例演示使用 `MessageBuffer` 的过程：将一个传入消息转发给多个接收方，然后将其记录到一个文件中。 如果不进行缓冲，这将是不可能的，因为消息正文只能被访问一次。  
  
 [!code-csharp[C_UsingTheMessageClass#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#7)]
 [!code-vb[C_UsingTheMessageClass#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#7)]  
  
 `MessageBuffer` 类还有其他值得注意的成员。 <xref:System.ServiceModel.Channels.MessageBuffer.Close%2A>不再需要缓冲区内容时可以来释放资源调用方法。 <xref:System.ServiceModel.Channels.MessageBuffer.BufferSize%2A>属性返回的已分配的缓冲区的大小。 <xref:System.ServiceModel.Channels.MessageBuffer.MessageContentType%2A>属性返回的消息的 MIME 内容类型。  
  
## <a name="accessing-the-message-body-for-debugging"></a>访问消息正文以进行调试  
 出于调试目的，您可以调用<xref:System.ServiceModel.Channels.Message.ToString%2A>方法以获取消息的表示形式作为字符串。 如果消息由文本编码器进行编码，则此表示通常与该消息在网络上的表示方式相匹配，只不过 XML 会以更好的格式表示以方便人们阅读。 一个例外的情况是消息正文。 正文只能被读取一次，且 `ToString` 不会更改消息状态。 因此，`ToString`方法可能会无法访问正文，并可能用占位符 （例如，"..." 替换消息正文。 因此，如果消息的正文内容很重要，则不要使用 `ToString` 来记录消息。  
  
## <a name="accessing-other-message-parts"></a>访问其他消息部分  
 该类提供了各种属性，以便访问除正文内容之外的其他与消息有关的信息。 但是，一旦关闭了消息，将无法调用这些属性：  
  
-   <xref:System.ServiceModel.Channels.Message.Headers%2A>属性表示消息头。 请参见本主题稍后关于“使用标头”的部分。  
  
-   <xref:System.ServiceModel.Channels.Message.Properties%2A>属性表示邮件属性，它是已命名的数据附加到消息，执行通常不会发出时将消息发送的片段。 请参见本主题稍后关于“使用属性”的部分。  
  
-   <xref:System.ServiceModel.Channels.Message.Version%2A>属性指示与消息关联的 SOAP 和 Ws-addressing 版本或`None`如果禁用了 SOAP。  
  
-   <xref:System.ServiceModel.Channels.Message.IsFault%2A>属性将返回`true`如果消息是 SOAP 错误消息。  
  
-   <xref:System.ServiceModel.Channels.Message.IsEmpty%2A>属性将返回`true`消息是否为空。  
  
 您可以使用<xref:System.ServiceModel.Channels.Message.GetBodyAttribute%28System.String%2CSystem.String%29>方法访问正文包装元素上的特定特性 (例如， `<soap:Body>`) 由特定名称和命名空间。 如果未找到这样一个属性，则返回 `null`。 仅当 `Message` 处于 Created 状态时（即尚未访问消息正文时），才能调用此方法。  
  
## <a name="working-with-headers"></a>使用标头  
 一个`Message`可以包含任意数量的已命名 XML 片断，这些片断称为*标头*。 每个片断通常都映射到一个 SOAP 标头。 通过访问标头`Headers`类型的属性<xref:System.ServiceModel.Channels.MessageHeaders>。 <xref:System.ServiceModel.Channels.MessageHeaders>是一套<xref:System.ServiceModel.Channels.MessageHeaderInfo>对象以及各个标头可通过访问其<xref:System.Collections.IEnumerable>接口或通过其索引器。 例如，下面的代码列出了某个 `Message` 中的所有标头的名称。  
  
 [!code-csharp[C_UsingTheMessageClass#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#8)]
 [!code-vb[C_UsingTheMessageClass#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#8)]  
  
#### <a name="adding-removing-finding-headers"></a>添加、删除、查找标头  
 可以使用的所有现有标头的末尾添加新的标头<xref:System.ServiceModel.Channels.MessageHeaders.Add%2A>方法。 您可以使用<xref:System.ServiceModel.Channels.MessageHeaders.Insert%2A>方法的特定索引处插入标头。 现有标头会发生位移，以便为插入的项腾出位置。 标头按照其索引进行排序，并且第一个可用索引为 0。 您可以使用各种<xref:System.ServiceModel.Channels.MessageHeaders.CopyHeadersFrom%2A>方法重载，可添加其他标头`Message`或`MessageHeaders`实例。 某些重载复制单个标头，而其他重载则复制所有标头。 <xref:System.ServiceModel.Channels.MessageHeaders.Clear%2A>方法移除所有标头。 <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAt%2A>方法删除 （移位在它后面的所有标头） 的特定索引处的标头。 <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAll%2A>方法删除具有特定名称和命名空间的所有标头。  
  
 检索特定标头使用<xref:System.ServiceModel.Channels.MessageHeaders.FindHeader%2A>方法。 此方法采用要查找的标头的名称和命名空间作为参数，并返回该标头的索引。 如果该标头出现了多次，则引发异常。 如果未找到该标头，则返回 –1。  
  
 在 SOAP 标头模型中，标头可以具有一个 `Actor` 值，该值指定标头的预期接收方。 最基本的 `FindHeader` 重载仅搜索准备发送给消息的最终接收方的标头。 但是，使用另一个重载可以指定搜索中包括哪些 `Actor` 值。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] SOAP 规范。  
  
 一个[CopyTo (MessageHeaderInfo\<xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29>方法可用于复制中的标头<xref:System.ServiceModel.Channels.MessageHeaders>集合到一个数组<xref:System.ServiceModel.Channels.MessageHeaderInfo>对象。  
  
 若要访问标头中的 XML 数据，您可以调用<xref:System.ServiceModel.Channels.MessageHeaders.GetReaderAtHeader%2A>并返回 XML 读取器为特定的标头索引。 如果您想要将标头内容反序列化为对象，使用<xref:System.ServiceModel.Channels.MessageHeaders.GetHeader%60%601%28System.Int32%29>或其他重载之一。 最基本的重载反序列化标头使用<xref:System.Runtime.Serialization.DataContractSerializer>在默认的配置方式。 如果您希望使用其他序列化程序或 `DataContractSerializer` 的其他配置，请使用采用一个 `XmlObjectSerializer` 作为参数的重载之一。 还有一些重载采用标头名称、命名空间作为参数，还可能采用一个 `Actor` 值列表而不是一个索引作为参数；这种重载是 `FindHeader` 和 `GetHeader` 的组合。  
  
## <a name="working-with-properties"></a>使用属性  
 一个 `Message` 实例可以包含任意多个具有任意类型的命名对象。 此集合可以通过类型为 `Properties` 的 `MessageProperties` 属性访问。 此集合实现<xref:System.Collections.Generic.IDictionary%602>接口，并充当从映射<xref:System.String>到<xref:System.Object>。\</TKey, TValue> 通常情况下，属性值不直接对应消息在网络上的任何部分，但而是提供对中的各个通道的各种消息处理提示[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]信道堆栈或[CopyTo (MessageHeaderInfo\<xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29>服务框架。 有关示例，请参阅[数据传输体系结构概述](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)。  
  
## <a name="inheriting-from-the-message-class"></a>从 Message 类继承  
 如果使用 `CreateMessage` 创建的内置消息类型不能满足您的要求，请创建一个从 `Message` 类派生的类。  
  
### <a name="defining-the-message-body-contents"></a>定义消息正文内容  
 用于访问消息正文中的数据的技术主要有三种：写入、读取消息正文以及将其复制到缓冲区。 这些操作最终导致<xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A>， <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents%2A>，和<xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A>所调用方法，分别在你的派生类上`Message`。 `Message` 基类保证对于每个 `Message` 实例仅调用这些方法中的一个，并保证每个方法的调用不会超过一次。 该基类还确保不会对已关闭的消息调用这些方法。 在您的实现中，无需跟踪消息状态。  
  
 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A>是一个抽象方法，必须加以实现。 定义消息正文内容的最基本的方式是使用此方法执行写入操作。 例如，下面的消息包含 100,000 个介于 1 到 20 之间的随机数。  
  
 [!code-csharp[C_UsingTheMessageClass#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#9)]
 [!code-vb[C_UsingTheMessageClass#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#9)]  
  
 
          `OnGetReaderAtBodyContents` 和 `OnCreateBufferedCopy` 方法具有适用于大多数情况的默认实现。 这些默认实现调用 `OnWriteBodyContents`，对结果进行缓冲，并且使用得到的缓冲区。 但是，在某些情况下，这可能还无法满足需要。 在前面的示例中，读取消息会导致 100,000 个 XML 元素被缓冲，这可能并不是理想的结果。 您可能希望重写 `OnGetReaderAtBodyContents` 以返回能够提供随机数的自定义 `XmlDictionaryReader` 派生类。 然后，您可以重写 `OnWriteBodyContents` 以使用 `OnGetReaderAtBodyContents` 属性返回的读取器，如下面的示例所示。  
  
 [!code-csharp[C_UsingTheMessageClass#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#10)]
 [!code-vb[C_UsingTheMessageClass#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#10)]  
  
 与此类似，您可能希望重写 `OnCreateBufferedCopy` 以返回您自己的 `MessageBuffer` 派生类。  
  
 除了提供消息正文内容以外，您的消息派生类还必须重写 `Version`、`Headers` 和 `Properties` 属性。  
  
 请注意，如果您创建消息的副本，则该副本将使用原始消息中的消息头。  
  
### <a name="other-members-that-can-be-overridden"></a>其他可以重写的成员  
 您可以重写<xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A>， <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A>，和<xref:System.ServiceModel.Channels.Message.OnWriteStartBody%2A>方法，以指定如何 SOAP 信封、 SOAP 标头和 SOAP 正文元素开始标记中写出。 这些方法通常对应于 `<soap:Envelope>`、`<soap:Header>` 和 `<soap:Body>`。 如果 `Version` 属性返回 `MessageVersion.None`，则这些方法通常不应该写出任何内容。  
  
> [!NOTE]
>  `OnGetReaderAtBodyContents` 的默认实现在调用 `OnWriteStartEnvelope` 以及缓冲结果之前调用 `OnWriteStartBody` 和 `OnWriteBodyContents`。 标头不会写出。  
  
 重写<xref:System.ServiceModel.Channels.Message.OnWriteMessage%2A>方法，以更改中的各个片段构造整个消息的方式。 `OnWriteMessage`从调用<xref:System.ServiceModel.Channels.Message.WriteMessage%2A>以及默认<xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A>实现。 请注意，重写<xref:System.ServiceModel.Channels.Message.WriteMessage%2A>并不是最佳做法。 它是更好一些，重写适当`On`方法 (例如， <xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A>， <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A>，和<xref:System.ServiceModel.Channels.BodyWriter.OnWriteBodyContents%2A>。  
  
 重写<xref:System.ServiceModel.Channels.Message.OnBodyToString%2A>来重写在调试期间表示消息正文的方式。 默认方式是将消息正文表示为三个点（“…”）。 请注意，当消息处于除 Closed 之外的任何状态时，可以多次调用此方法。 此方法的实现在任何情况下都不应产生必须仅执行一次的操作（如从只进的流中读取）。  
  
 重写<xref:System.ServiceModel.Channels.Message.OnGetBodyAttribute%2A>方法，以允许访问 SOAP 正文元素上的属性。 此方法可以调用任意次，但 `Message` 基类型保证仅当消息处于 Created 状态时才调用此方法。 在实现中不需要检查状态。 默认实现始终返回 `null`，这指示正文元素上不存在任何属性。  
  
 如果您`Message`对象必须执行任何特殊的清理操作不再需要消息正文时，可以重写<xref:System.ServiceModel.Channels.Message.OnClose%2A>。 默认实现不执行任何操作。  
  
 `IsEmpty` 和 `IsFault` 属性可以重写。 默认情况下，这两个属性都返回 `false`。