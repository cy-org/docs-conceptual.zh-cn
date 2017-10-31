---
title: "消息协议 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 消息协议
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 通道堆栈采用编码和传输通道将内部消息表示形式转换成其网络传输格式，并使用特定传输进行发送。用于 Web 服务互操作性的最常见传输是 HTTP，Web 服务使用的最常见编码是基于 XML 的 SOAP 1.1、SOAP 1.2 和消息传输优化机制 \(MTOM\)。  
  
 本主题讨论 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 所采用的以下协议的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现细节。  
  
|规范\/文档|链接|  
|------------|--------|  
|HTTP 1.1|http:\/\/www.ietf.org\/rfc\/rfc2616.txt|  
|SOAP 1.1 HTTP 绑定|http:\/\/www.w3.org\/TR\/2000\/NOTE\-SOAP\-20000508\/，第 7 节|  
|SOAP 1.2 HTTP 绑定|http:\/\/www.w3.org\/TR\/soap12\-part2\/，第 7 节|  
  
 本主题讨论 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 和 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 所采用的以下协议的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现细节。  
  
|规范\/文档|链接|  
|------------|--------|  
|XML|http:\/\/www.w3.org\/TR\/REC\-xml|  
|SOAP 1.1|http:\/\/www.w3.org\/TR\/2000\/NOTE\-SOAP\-20000508\/|  
|SOAP 1.2 核心|http:\/\/www.w3.org\/TR\/soap12\-part1\/|  
|WS\-Addressing 2004\/08|http:\/\/www.w3.org\/Submission\/2004\/SUBM\-ws\-addressing\-20040810\/|  
|W3C Web 服务寻址 1.0 \- 核心|http:\/\/www.w3.org\/TR\/2006\/REC\-ws\-addr\-core\-20060509|  
|W3C Web 服务寻址 1.0 \- SOAP 绑定|http:\/\/www.w3.org\/TR\/2006\/REC\-ws\-addr\-soap\-20060509|  
|W3C Web 服务寻址 1.0 \- WSDL 绑定|http:\/\/www.w3.org\/TR\/2006\/CR\-ws\-addr\-wsdl\-20060529\/|  
|W3C Web 服务寻址 1.0 \- 元数据|http:\/\/www.w3.org\/TR\/ws\-addr\-metadata\/|  
|WSDL SOAP1.1 绑定|http:\/\/www.w3.org\/TR\/wsdl\/|  
|WSDL SOAP1.2 绑定|http:\/\/www.w3.org\/Submission\/wsdl11soap12\/|  
  
 本主题讨论 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 所采用的以下协议的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现细节。  
  
|规范\/文档|链接|  
|------------|--------|  
|XOP|http:\/\/www.w3.org\/TR\/xop10\/|  
|MTOM \+ SOAP 1.2 绑定|http:\/\/www.w3.org\/TR\/soap12\-mtom\/|  
|MTOM SOAP 1.1 绑定|http:\/\/www.w3.org\/Submission\/soap11mtom10\/|  
|MTOM WS\-Policy 断言|http:\/\/www.w3.org\/Submission\/2006\/SUBM\-WS\-MTOMPolicy\-20061101\/。|  
  
 本主题通篇使用以下 XML 命名空间和关联的前缀。  
  
|前缀|命名空间统一资源标识符 \(URI\)|  
|--------|-------------------------|  
|s11|http:\/\/schemas.xmlsoap.org\/soap\/envelope|  
|s12|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/www.w3.org\/2004\/08\/addressing|  
|wsam|http:\/\/www.w3.org\/2007\/05\/addressing\/metadata|  
|wsap|http:\/\/schemas.xmlsoap.org\/ws\/2004\/09\/policy\/addressing|  
|wsa10|http:\/\/www.w3.org\/2005\/08\/addressing|  
|wsaw10|http:\/\/www.w3.org\/2006\/05\/addressing\/wsdl|  
|xop|http:\/\/www.w3.org\/2004\/08\/xop\/include|  
|xmime|http:\/\/www.w3.org\/2004\/06\/xmlmime<br /><br /> http:\/\/www.w3.org\/2005\/05\/xmlmime|  
|cdp|http:\/\/schemas.microsoft.com\/net\/2006\/06\/duplex|  
  
## SOAP 1.1 和 SOAP 1.2  
  
### 信封和处理模型  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现了遵循 Basic Profile 1.1 \(BP11\) 和 Basic Profile 1.0 \(SSBP10\) 的 SOAP 1.1 信封处理。SOAP 1.2 信封处理是遵循 SOAP12\-Part1 实现的。  
  
 本节说明 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在涉及 BP11 和 SOAP12\-Part1 时所采用的某些实现选项。  
  
#### 强制标头处理  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 遵循 SOAP 1.1 和 SOAP 1.2 规范中所述的规则来处理标有 `mustUnderstand` 的标头，但有以下变化。  
  
 进入 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道堆栈的消息由关联的绑定元素所配置的各个通道进行处理，例如，文本消息编码、安全、可靠消息传递和事务。每个通道都识别来自关联命名空间的标头，并将其标记为已理解。消息进入调度程序后，操作格式化程序读取相应消息\/操作协定所期望的标头，并将其标记为已理解。然后，调度程序验证是否还有任何标头未被理解，但仍标记为 `mustUnderstand`，如果是这样，则引发异常。包含 `mustUnderstand` 标头并且目标为接收方的消息不会由接收方应用程序代码进行处理。  
  
 这样的分层处理实现了 SOAP 节点的基础结构层和应用层之间的分离。  
  
-   B1111：未被理解的标头是在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构通道堆栈处理消息之后，应用程序处理该消息之前检测的。  
  
     在 SOAP 1.1 和 SOAP 1.2 中，`mustUnderstand` 标头值不相同。Basic Profile 1.1 要求，在 SOAP 1.1 消息中，`mustUnderstand` 值为 0 或 1。SOAP 1.2 可以使用 0、1、`false` 和 `true` 作为值，但建议使用 `xs:boolean` 值的规范表示形式（`false` 和 `true`）。  
  
-   B1112：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发出 `mustUnderstand` 值介于 0 和 1，针对 SOAP 信封 的 SOAP1.1 和 SOAP1.2 版本。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 接受 `mustUnderstand` 头 \(0, 1, `false`, `true`\) 的 `xs:boolean` 的整个值空间  
  
#### SOAP 错误  
 下面列出了特定于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 SOAP 错误实现。  
  
-   B2121：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 返回以下 SOAP 1.1 错误代码：`s11:mustUnderstand`、`s11:Client` 和 `s11:Server`。  
  
-   B2122：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 返回以下 SOAP 1.2 错误代码：`s12:MustUnderstand`、`s12:Sender` 和 `s12:Receiver`。  
  
### HTTP 绑定  
  
#### SOAP 1.1 HTTP 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 遵循 Basic Profile 1.1 规范第 3.4 节实现 SOAP1.1 HTTP 绑定，并提供如下说明：  
  
-   B2211：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务不实现 HTTP POST 请求的重定向。  
  
-   B2212：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端依据 3.4.8 支持 HTTP Cookie。  
  
#### SOAP 1.2 HTTP 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 按照 SOAP 1.2\-part 2 \(SOAP12Part2\) 规范实现 SOAP 1.2 HTTP 绑定，并提供如下说明。  
  
 SOAP 1.2 为 `application/soap+xml` 媒体类型提供了一个可选的操作参数。在未使用 WS\-Addressing 时，采用此参数优化消息调度很有用，这种情况下，不需要分析 SOAP 消息的正文。  
  
-   R2221：`application/soap+xml` 操作参数出现在 SOAP 1.2 请求中时，必须与相应 WSDL 绑定内的 `wsoap12:operation` 元素的 `soapAction` 属性匹配。  
  
-   R2222：如果使用 WS\-Addressing 2004\/08 或 WS\-Addressing 1.0，`application/soap+xml` 操作参数出现在 SOAP 1.2 消息中时，必须与 `wsa:Action` 匹配。  
  
 如果 WS\-Addressing 禁用，并且传入的请求不包含操作参数，则视为未指定消息 `Action`。  
  
## WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现了三个版本的 WS\-Addressing：  
  
-   WS\-Addressing 2004\/08  
  
-   W3C Web 服务寻址 1.0 核心 \(ADDR10\-CORE\) 和 SOAP 绑定 \(ADDR10\-SOAP\)  
  
-   WS\-Addressing 1.0 \- 元数据  
  
### 终结点引用  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现的所有 WS\-Addressing 版本都使用终结点引用来描述终结点。  
  
#### 终结点引用和 WS\-Addressing 版本  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]执行一些使用 WS 寻址的基础架构协议，尤其是 `EndpointReference`元素和 `W3C.WsAddressing.EndpointReferenceType`类（例如，WS ReliableMessaging、WS\-SecureConversation 和 WS\-Trust）。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]支持使用采用其他基础结构协议的 WS 寻址的任一版本。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]终结点支持每个终结点一个 WS 寻址版本。  
  
 对于 R3111，在与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点交换的消息中使用的 `EndpointReference` 元素或类型的命名空间必须与此终结点所实现的 WS\-Addressing 版本匹配。  
  
 例如，如果某个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点实现了 WS\-ReliableMessaging，由这样的终结点在 `CreateSequenceResponse` 内部返回的 `AcksTo` 标头使用 `EncodingBinding` 元素为此终结点指定的 WS\-Addressing 版本。  
  
#### 终结点引用和元数据  
 很多情况下，需要对给定终结点进行元数据或元数据引用通信。  
  
 B3121：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 采用 WS\-MetadataExchange \(MEX\) 规范第 6 节中描述的机制来按值或按引用包含终结点引用的元数据。  
  
 考虑这样一种情况，某个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务要求使用安全断言标记语言 \(SAML\) 令牌（由位于 http:\/\/sts.fabrikam123.com 的颁发机构颁发）进行身份验证。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点通过使用 `sp:IssuedToken` 断言（嵌套有指向令牌颁发机构的 `sp:Issuer` 断言）来描述这一身份验证要求。访问该 `sp:Issuer` 断言的客户端应用程序需要知道如何与令牌颁发机构终结点进行通信。客户端需要知道令牌颁发机构的有关元数据。通过使用 MEX 中定义的终结点引用元数据扩展，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了对令牌颁发机构元数据的引用。  
  
```  
<sp:IssuedToken>  
  <sp:Issuer>  
    <wsa10:Address>  
      http://sts.fabrikam123.com  
    </wsa10:Address>  
    <wsa10:Metadata>  
      <mex:Metadata>  
        <mex:MetadataSection>  
          <mex:MetadataReference>  
            <wsa10:Address>  
              http://sts.fabrikam123.com/mex  
            </wsa10:Address>  
          </mex:MetadataReference>  
        </mex:MetadataSection>  
      </mex:Metadata>  
    </wsa10:Metadata>  
  </sp:Issuer>  
</sp:IssuedToken>  
  
```  
  
### 消息寻址标头  
  
#### 消息头  
 对于两种 WS 寻址版本，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用这两个规范中规定的以下消息头：`wsa:To`、 `wsa:ReplyTo`、 `wsa:Action`、 `wsa:MessageID` 和  `wsa:RelatesTo`。  
  
 B3211：对于所有 WS\-Addressing 版本，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 承认但不现成生成 WS\-Addressing 消息头 `wsa:FaultTo` 和 `wsa:From`。  
  
 与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序交互的应用程序可添加这些消息头，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将对其进行相应处理。  
  
#### 引用参数和属性  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 根据相应的规范实现对终结点引用参数和引用属性的处  
  
 理。  
  
 B3221：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点在配置为使用 WS\-Addressing 2004\/08 时，对引用属性和引用参数的处理是没有区别的。  
  
### 消息交换模式  
 Web 服务操作调用所涉及的消息序列称为“消息交换模式”。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]支持单向模式、请求\-答复模式和双工消息交换模式。本节根据所用的消息交换模式说明 WS\-Addressing 对消息处理的要求。  
  
 本节通篇都是由请求方发送第一条消息，响应方接收第一条消息。  
  
#### 单向消息  
 当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点配置为支持带有给定 `Action` 的消息遵循单向模式时，该 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点将具有以下行为和要求。除非另有指定，否则这些行为和规则对于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中所支持的两种 WS\-Addressing 版本都适用：  
  
-   R3311：请求方必须包含 `wsa:To`、`wsa:Action` 以及表示终结点引用所指定的所有引用参数的标头。如果使用 WS\-Addressing 2004\/08 并且终结点引用指定了 \[reference properties\]，则对应的标头必须也添加到消息中。  
  
-   B3312：请求方可以包含 `MessageID`、`ReplyTo` 和 `FaultTo` 标头。接收方基础结构将忽略这些标头，并且这些标头将传给应用程序。  
  
-   R3313：在使用 HTTP 并且没有通过 HTTP 响应发送任何消息时，响应方必须发送一个正文为空且 HTTP 状态码为 202 的 HTTP 响应。  
  
     如果使用的是 HTTP 传输，并且操作协定声明消息是单向的，则 HTTP 响应仍可用于发送基础结构消息 — 例如，可靠消息传递可通过 HTTP 响应发送 `SequenceAcknowledgement` 消息。  
  
-   B3314：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方不发送错误消息来响应单向消息。  
  
#### 请求\-答复  
 当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点配置为支持带有给定 `Action` 的消息遵循请求\-答复模式时，该 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点将具有以下行为和要求。除非另有指定，否则这些行为和规则对于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中所支持的两种 WS\-Addressing 版本都适用：  
  
-   R3321：请求方必须在请求中包含 `wsa:To`、`wsa:Action`、`wsa:MessageID` 以及表示终结点引用所指定的所有 \[reference parameters\] 和\/或 \[reference properties\] 的标头。  
  
-   R3322：使用 WS\-Addressing 2004\/08 时，还必须在请求中包含 `ReplyTo`。  
  
-   R3323：如果使用 WS\-Addressing 1.0 并且请求中不存在 `ReplyTo`，则会使用 \[address\] 属性等于“http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous”的默认终结点引用。  
  
-   R3324：请求方必须在答复消息中包含 `wsa:To`、`wsa:Action` 和 `wsa:RelatesTo` 标头，并且必须在请求中包含表示由 `ReplyTo` 终结点引用所指定的所有 \[reference parameters\] 和\/或 \[reference properties\] 的标头。  
  
### Web 服务寻址错误  
 R3411：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成 WS\-Addressing 2004\/08 定义的以下错误。  
  
|代码|原因|  
|--------|--------|  
|wsa:DestinationUnreachable|到达的消息所带有的 `ReplyTo` 不同于为此通道建立的答复地址；在 To 标头中指定的地址上，没有终结点在进行侦听。|  
|wsa:ActionNotSupported|与终结点关联的基础结构通道或调度程序不能识别在 `Action` 标头中指定的操作。|  
  
 R3412：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成 WS\-Addressing 1.0 定义的以下错误。  
  
|代码|原因|  
|--------|--------|  
|wsa10:InvalidAddressingHeader|重复的 `wsa:To`、`wsa:ReplyTo`、`wsa:From` 或 `wsa:MessageID`。具有相同 `RelationshipType` 的重复的 `wsa:RelatesTo` 。|  
|wsa10:MessageAddressingHeaderRequired|缺少必需的 Addressing 标头。|  
|wsa10:DestinationUnreachable|到达的消息所带有的 `ReplyTo` 不同于为此通道建立的答复地址。在 To 标头中指定的地址上没有终结点在进行侦听。|  
|wsa10:ActionNotSupported|与终结点关联的基础结构通道或调度程序不能识别在 `Action` 标头中指定的操作。|  
|wsa10:EndpointUnavailable|RM 通道发送回此错误，指示终结点将不会根据对 `CreateSequence` 消息的寻址标头的检查结果来处理序列。|  
  
 上表中的代码对应于 SOAP 1.1 中的 `FaultCode` 和 SOAP 1.2 中的 `SubCode` \(Code\=Sender\)。  
  
### WSDL 1.1 绑定和 WS\-Policy 断言  
  
#### 指示使用 WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用策略断言来指示终结点对某个特定 WS\-Addressing 版本的支持。  
  
 下面的策略断言具有终结点策略主题 \[WS\-PA\]，并指示从终结点收发的消息必须使用 WS\-Addressing 2004\/08。  
  
```  
<wsap:UsingAddressing />  
```  
  
 此策略断言扩充了 WS\-Addressing 2004\/08 规范。  
  
 下面的策略断言指示发送\/接收的消息必须使用 WS\-Addressing 1.0。  
  
```vb  
<wsam:Addressing/>   
```  
  
 下面的策略断言具有终结点策略主题 \[WS\-PA\]，并指示从终结点收发的消息必须使用 WS\-Addressing 2004\/08。  
  
```  
<wsaw10:UsingAddressing />  
```  
  
 `wsaw10:UsingAddressing` 元素借自于 \[WS\-Addressing\-WSDL\]，并在符合该规范第 3.1.2 节的 WS\-Policy 的上下文中使用。  
  
 使用 Addressing 不会更改 WSDL 1.1、SOAP 1.1 和 SOAP 1.2 HTTP 绑定的语义。例如，如果某个请求发送到使用 Addressing 和 WSDL SOAP 1.x HTTP 绑定的终结点，并且该请求期望得到一个答复，则该答复必须用 HTTP 响应发送。  
  
 对于通过 http 响应发送的答复，WS\-AM 断言是：  
  
```xml  
<wsam:AnonymousResponses/>  
```  
  
 完整的策略断言可能类似于：  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
        <wsam:AnonymousResponses />   
    </wsp:Policy>  
</wsam:Addressing>  
```  
  
 但是，有些消息交换模式可以从在请求方和响应方之间建立两个独立的反向 HTTP 连接中获益，例如，由响应方发送的主动单向消息。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一个实用工具，通过它，两个基础传输通道可构成一个复合双工通道，其中一个通道用于输入消息，另一个用于输出消息。对于 HTTP 传输，复合双工提供了两个反向 HTTP 连接。请求方使用一个连接将消息发送到响应方，而响应方使用另一个连接将消息发送回请求方。  
  
 对于通过单独的 http 请求发送的答复，ws\-am 断言是：  
  
```xml  
<wsam:NonAnonymousResponses/>  
```  
  
 完整的策略断言可能类似于：  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
      <wsam:NonAnonymousResponses />   
   </wsp:Policy>  
  </wsam:Addressing>  
```  
  
 在使用 WSDL 1.1 SOAP 1.x HTTP 绑定的终结点上，如果要使用以下具有终结点策略主题 \[WS\-PA\] 的断言，要求将两个单独的反向 HTTP 连接分别用于从请求方到响应方以及从响应方到请求方传送消息。  
  
```  
<cdp:CompositeDuplex/>  
```  
  
 上面的陈述对于请求消息的 `wsa:ReplyTo` 标头提出了以下要求：  
  
-   R3514：如果终结点使用 WSDL 1.1 SOAP 1.x HTTP 绑定，并且有一个带有 `wsap10:UsingAddressing` 或 `wsap:UsingAddressing` 断言，且附加了 `cdp:CompositeDuplex` 的策略备选项，那么发送到该终结点的请求消息必须有一个 `[address]` 属性不等于“http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous”的 `ReplyTo` 标头。  
  
-   R3515：如果终结点使用 WSDL 1.1 SOAP 1.x HTTP 绑定，并且有一个带有 `wsap10:UsingAddressing` 断言的策略备选项，且未附加 `cdp:CompositeDuplex` 断言，那么发送到该终结点的请求消息必须有一个 `[address]` 属性等于“http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous”的 `ReplyTo` 标头，或者根本没有 `ReplyTo` 标头。  
  
-   R3516：如果终结点使用 WSDL 1.1 SOAP 1.x HTTP 绑定，并且有一个带有 `wsap:UsingAddressing` 断言的策略备选项，且未附加 `cdp:CompositeDuplex` 断言，那么发送到该终结点的请求消息必须有一个 `[address]` 属性等于“http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous”的 `ReplyTo` 标头。  
  
 WS\-addressing WSDL 规范力图描述类似协议绑定，它引入了一个带有 3 个文本值（required、optional 和 prohibited）的 `<wsaw:Anonymous/>` 元素来指示对 `wsa:ReplyTo` 标头的要求（第 3.2 节）。遗憾的是，在 WS\-Policy 的上下文中，这样的元素定义不特别适合用作断言，因为它要求使用特定于域的扩展来支持将此类元素用作断言的备选项的交集。这样的元素定义还指示 `ReplyTo` 标头的值在传输时与终结点行为相反，这使它只能特定于 HTTP 传输。  
  
#### 操作定义  
 WS\-Addressing 2004\/08 为 `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` 元素定义了一个 `wsa:Action` 属性。WS\-Addressing 1.0 WSDL 绑定 \(WS\-ADDR10\-WSDL\) 定义了一个类似属性 `wsaw10:Action`。  
  
 两者之间唯一的区别在于默认 Action 模式语义（分别在 WS\-ADDR 第 3.3.2 节和 WS\-ADDR10\-WSDL 第 4.4.4 节描述）。  
  
 两个终结点可以共享相同的 `portType`（即 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 术语中的协定）但使用不同 WS\-Addressing 版本。但是，如果 Action 是由 `portType` 定义的，并且在实现该 `portType` 的终结点之间不应更改，则不可能同时支持这两种默认操作模式。  
  
 为了解决这一矛盾，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 只支持 `Action` 属性的单个版本。  
  
 B3521：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` 元素的 `wsaw10:Action` 属性（在 WS\-ADDR10\-WSDL 中定义）来确定对应消息的 `Action` URI，而不考虑终结点所使用的 WS\-Addressing 版本。  
  
#### 在 WSDL 端口内使用终结点引用  
 WS\-ADDR10\-WSDL 4.1 节扩展了 `wsdl:port` 元素来包含 `<wsa10:EndpointReference…/>` 子元素来描述 WS 寻址中的终结点。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]扩展了 WS\-Addressing 2004\/08 中的这一实用工具，允许  `<wsa:EndpointReference…/>`允许`wsdl:port`的子元素出现。  
  
-   R3531：如果终结点有一个带有 `<wsaw10:UsingAddressing/>``wsdl:port 策略断言的附加策略备选项，则对应的` `<wsa10:EndpointReference  /> 元素可包含子元素` 。  
  
-   R3532：如果 `wsdl:port` 包含子元素 `<wsa10:EndpointReference  />`，则 `wsa10:EndpointReference/wsa10:Address` 子元素值必须与同级 `wsdl:port`\/`wsdl:location` 元素的 `@address` 属性的值匹配。  
  
-   R3533：如果终结点有一个带有 `<wsap:UsingAddressing/>``wsdl:port 策略断言的附加策略备选项，则对应的` `<wsa:EndpointReference  /> 元素可包含子元素` 。  
  
-   R3534：如果 `wsdl:port` 包含子元素 `<wsa:EndpointReference  />`，则 `wsa:EndpointReference/wsa:Address` 子元素值必须与同级 `wsdl:port`\/`wsdl:location` 元素的 `@address` 属性的值匹配。  
  
### 与 WS\-Security 的结合  
 根据 WS\-ADDR 和 WS\-ADDR10 中的安全注意事项章节，建议将所有寻址消息头和消息正文一起签名，以便将它们绑定在一起。  
  
 当 WS\-Security 用于消息完整性保护时，WS\-Addressing 消息头和从引用参数或\/和属性产生的标头必须与消息正文一起签名。  
  
### 示例  
  
#### 单向消息  
 在此方案中，发送方向接收方发出单向消息。使用 SOAP 1.2、HTTP 1.1 和 W3C WS\-Addressing 1.0。  
  
 请求消息结构：消息头包含 `wsa10:To` 和 `wsa10:Action` 元素。消息正文包含来自应用程序命名空间的一个特定 `<app:Ping>` 元素。  
  
 HTTP 标头：POST 中的目标与 `wsa10:To` 元素中的 URI 匹配。  
  
 按照 SOAP 1.2 的要求，Content\-Type 标头的值为 `application/soap+xml`。此外，还包含参数 `charset` 和 `action`。Content\-Type 标头的 `action` 参数与 `wsa10:Action` 消息头的值匹配。  
  
```  
POST http://fabrikam123.com/Service HTTP/1.1  
Content-Type: application/soap+xml; charset=utf-8;    
              action="http://fabrikam123.com/Service/OneWay"  
Host: 131.107.72.15  
Content-Length: 1501  
Expect: 100-continue  
Proxy-Connection: Keep-Alive  
<s12:Envelope>  
  <s12:Header>  
    <wsa10:To s12:mustUnderstand="1">  
        http://fabrikam123.com/Service  
    </wsa10:To>  
    <wsa10:Action s12:mustUnderstand="1">  
        http://fabrikam123.com/Service/OneWay   
    </wsa10:Action>  
  </s12:Header>  
  <s12:Body>  
    <Ping xmlns="http://fabrikam123.com/Service/">  
      <Text>Hello World</Text>  
    </Ping>  
  </s12:Body>  
</s12:Envelope>  
```  
  
 接收方以一个状态为 202 的空 HTTP 响应进行回应。HTTP 响应的一个示例为：  
  
```  
HTTP/1.1 202 Accepted  
Date: Fri, 15 Jul 2005 08:56:07 GMT  
Server: Microsoft-IIS/6.0  
MicrosoftOfficeWebServer: 5.0_Pub  
X-Powered-By: ASP.NET  
X-AspNet-Version: 2.0.50215  
Cache-Control: private  
Content-Length: 0  
```  
  
## SOAP 消息传输优化机制  
 本节介绍 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对 HTTP SOAP MTOM 的实现细节。MTOM 技术是与传统的文本\/XML 编码或 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 二进制编码同类的 SOAP 消息编码机制。MTOM 包括以下内容：  
  
-   \[XOP\] 描述的 XML 编码和打包机制，用于将包含 base64 编码的二进制数据的 XML 信息项优化为多个独立的二进制部分。  
  
-   XOP 包的 MIME 封装，用于将 XML Infoset 和 XOP 包的每一个二进制部分序列化为单独的 MIME 部分。  
  
-   应用于 SOAP 1.x 信封的 MIME XOP 编码。  
  
-   HTTP 传输绑定。  
  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，可以将 MTOM 用于非 HTTP 传输。不过，在本主题中，我们将着重讨论 HTTP 上的应用。  
  
 MTOM 格式利用了包含 MTOM 本身、XOP 以及 MIME 在内的大型规范集。在某种程度上，此规范集的模块性使得重新构造格式和处理语义的确切要求变得有点困难。本节介绍 MTOM HTTP 绑定的格式和处理要求。  
  
### MTOM 消息编码  
  
#### 生成 MTOM 消息  
 \[XOP\] 第 3.1 节描述了将具有元素信息项（包含 base64 值）的 XML 编码为抽象定义的 XOP 包的过程。  
  
 下面的一系列步骤描述了特定于 MTOM 的编码过程：  
  
1.  确保要编码的 SOAP 信封不包含 `[namespace name]` 为“http:\/\/www.w3.org\/2004\/08\/xop\/include”并且 `[local name]` 为 `Include` 的元素信息项。  
  
2.  创建一个空 MIME 包。  
  
3.  在原始 XML Infoset 中标识要优化的元素信息项。对于要优化的项，组成该元素信息项的 `[children]` 的字符必须是 `xs:base64Binary` 的规范形式（请参见 XSD\-2，3.2.16 base64Binary），在非空格内容前面、中间或后面，都不得包含任何空格字符。  
  
4.  创建一个是原始 SOAP 信封副本的 XOP SOAP 信封，但是，在上一步中标识的每个元素信息项的 children 都替换为如下构造的 `xop:Include` 元素信息项：  
  
    1.  通过将被替换字符处理为 base64 编码的数据，将其转换为二进制数据。  
  
    2.  生成一个符合 R3133 和 R3134 要求的唯一 Content\-ID 标头值。  
  
    3.  生成一个具有二进制值的 Content\-Transfer\-Encoding MIME 标头。  
  
    4.  如果要优化的元素信息项（新插入的 `xop:Include` 元素信息项的 \[parent\]）有一个 `xmime:contentType` 属性信息项，则生成一个带有 `xmime:contentType` 属性的值的 Content\-Type MIME 标头。  
  
    5.  生成一个新的二进制 MIME 部分，其内容由以下几项组成：从处理为 base64 的被替换数据解码的二进制数据、4b 中的 Content\-ID、4c 中的 Content\- Transfer\-Encoding 标头，以及 Content\-Type 标头（如果在步骤 4d 中生成）。  
  
    6.  将一个 `href` 属性添加到 `xop:Include` 元素，其值为从 Content\-ID 标头值（在步骤 4b 中生成）派生的 cid: uri。移除外层的“\<”和“\>”字符，对其余字符串进行 URL 转义，并添加前缀 `cid:`。以下最小字符集需要根据 RFC1738 和 RFC2396 进行转义。其他字符也可转义。  
  
        ```  
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">  
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"  
        ```  
  
5.  用步骤 4 中的 XOP SOAP 信封创建一个根 MIME 部分。  
  
6.  写入 HTTP 标头，包括 HTTP Content\-Type 标头。  
  
7.  写入 MIME 包。  
  
#### 处理 MTOM 消息  
 处理 MTOM 消息的过程与前面“生成 MTOM 消息”一节中所述的过程完全相反：  
  
1.  确保根 MIME 部分有 Content\-Type `application/xop+xml`。  
  
2.  通过将包的根 MIME 部分作为 XML 文档进行分析，构造一个 SOAP 信封。字符编码由根 MIME 部分的 Content\-Type 的 `charset` 参数确定。  
  
3.  对于构造的 SOAP 信封中的每个元素信息项（有一个 `xop:Include` 元素信息项作为其 \[children\] 属性的唯一成员）：  
  
    1.  移除 `cid:` 前缀，取消转义 `xop:Include` 元素的 `@href` 属性的值中所有 URI 转义序列 \(RFC 2396\)。将获得的字符串括在“\<”和“\>”中。  
  
    2.  找到 Content\-ID 标头值与步骤 3a 中派生的字符串匹配的 MIME 部分。  
  
    3.  将出现在每一项的 `children` 属性中的 `xop:Include` 元素信息项替换为字符信息项，这些字符信息项表示的是 MIME 部分（在步骤 3b 中标识）全部正文的规范 base64 编码（请参见 XSD\-2，3.2.16 base64Binary）（实际是将 `xop:Include` 元素信息项替换为从包部分重新构造的数据）。  
  
#### HTTP Content\-Type 标头  
 下面列出了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对 SOAP 1.x MTOM 编码消息（根据 MTOM 规范本身提出的要求，以及从 MTOM 和 RFC 2387 衍生的要求产生）的 HTTP Content\-Type 标头格式的说明。  
  
-   R4131：HTTP Content\-Type 标头必须具有值 multipart\/related（不区分大小写）及其参数。参数名不区分大小写。参数顺序并不重要。  
  
-   RFC 2045 第 5.1 节中列出了 MIME 消息 Content\-Type 标头的完全 Backus\-Naur 形式 \(BNF\)。  
  
-   R4132：HTTP Content\-Type 标头必须具有一个类型参数，并且值 `application/xop+xml` 括在双引号中。  
  
 尽管 RFC 2387 中未明确要求使用双引号，但是其文字提到所有 multipart\/related 媒体类型参数最有可能包含“@”或“\/”之类的保留字符，因此需要双引号。  
  
-   R4133：HTTP Content\-Type 标头应该有一个 start 参数，其值为包含 SOAP 1.x 信封的 MIME 部分的 Content\-ID 标头，并且括在双引号中。如果省略 start 参数，则第一个 MIME 部分必须包含 SOAP 1.x 信封。  
  
-   R4134：SOAP 1.1 MTOM 编码消息的 HTTP Content\-Type 标头必须包含值为 text\/xml（括在双引号中）的 start\-info 参数。  
  
-   R4135：SOAP 1.2 MTOM 编码消息的 HTTP Content\-Type 标头必须包含值为 `application/soap+xml`（括在双引号中）的 start\-info 参数。  
  
-   R4136：SOAP 1.x MTOM 编码消息的 HTTP Content\-Type 标头必须具有边界参数，其值（括在双引号中）与 RFC 2046 第 5.1.1 节中定义的 MIME 边界 BNF 匹配。  
  
    ```  
    boundary := 0*69<bchars> bcharsnospace   
    bchars := bcharsnospace / " "   
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"   
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"  
    ```  
  
     示例：  
  
     正确  
  
    ```  
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"  
  
    ```  
  
     正确  
  
    ```  
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
  
    ```  
  
     不正确  
  
    ```  
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"   
    ```  
  
#### Infoset MIME 部分  
 SOAP 1.x 信封封装为 XOP MIME 包的根部分，通常称为 `infoset` 部分。  
  
-   R4141：SOAP 1.x 信封必须封装为 XOP MIME 包的根部分，称为 `infoset` 部分，并从 HTTP Content\-Type 引用。  
  
-   R4142：SOAP `Infoset` 部分必须包含以下 MIME 标头：`Content-ID`、`Content-Transfer-Encoding` 和 `Content-Type`。  
  
 Content\-ID 标头的格式根据 RFC 2045 定义为  
  
```  
"Content-ID" ":" msg-id  
```  
  
 其中 `msg-id` 在 RFC 2822（取代 RFC 822，在 RFC 2045 中引用）定义：  
  
```  
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]  
```  
  
 并且实际上电子邮件地址括在“\<”与“\>”之间。RFC 2822 中增加了 `[CFWS]` 前缀和后缀，用于携带注释，不应用于保持互操作性。  
  
 R4143：Infoset MIME 部分的 Content\-ID 标头的值必须遵循 RFC 2822 中的 `msg-id` 结果，并省略 `[CFWS]` 前缀和后缀部分。  
  
 过去，很多 MIME 实现对括在“\<”和“\>”中的值应为电子邮件地址的要求很宽松，除了电子邮件地址之外，还使用括在“\<”、“\>”中的 `absoluteURI`。本版本的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用如下形式的 Content\-ID MIME 标头值：  
  
```  
Content-ID: <http://tempuri.org/0>   
```  
  
 R4144：MTOM 处理程序应接受符合以下宽松 `msg-id` 的 Content\-ID 标头值。  
  
```  
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]  
mail-address   =     id-left "@" id-right  
```  
  
 MIME \(RFC 2045\) 提供 Content\-Transfer\-Encoding 标头来传递 MIME 部分内容的编码。为 Content\-Transfer\-Encoding 定义的默认值为 7\-bit，它不适合于大多数 SOAP 消息，因此，需要使用 Content\-Transfer\-Encoding 标头以获得更好的互操作性：  
  
-   R4145：SOAP Infoset 部分必须包含 Content\-Transfer\-Encoding 标头。  
  
-   R4146：如果 SOAP 信封字符编码为 UTF\-8，则 Content\-Transfer\-Encoding 标头的值必须为 8\-bit。  
  
-   R4147：如果 SOAP 信封字符编码为 UTF\-16，则 Content\-Transfer\-Encoding 标头的值必须为 binary。  
  
-   根据 \[XOP\] 第 5 节，  
  
-   R4148：SOAP1.1 Infoset 部分必须包含媒体类型为 application\/xop\+xml 的 Content\-Type 标头，以及参数 type\=”text\/xml”和 charset  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="text/xml"  
    ```  
  
-   R4149：SOAP 1.2 Infoset 部分必须包含媒体类型为 `application/xop+xml` 的 Content\-Type 标头，以及参数 type\=”`application/soap+xml`”和 `charset`。  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="application/soap+xml"  
    ```  
  
     虽然 XOP 定义 `charset` 参数对于 `application/xop+xml` 是可选的，但是对于类似于 BP 1.1 对 `text/xml` 媒体类型要求有 `charset` 参数的互操作性，该参数仍然是需要的。  
  
-   R41410：`type` 和 `charset` 参数必须出现在 SOAP 1.x Infoset 部分的 Content\-Type 标头中。  
  
#### WCF 对 MTOM 的终结点支持  
 MTOM 的用途是对 SOAP 消息进行编码，以优化 base64 编码数据。下面列出了相关约束：  
  
-   R4151：任何包含 base64 编码数据的元素信息项都可以优化。  
  
-   B4152：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 优化包含 base64 编码数据并且长度超过 1024 字节的元素信息项。  
  
 配置为使用 MTOM 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点将始终发送 MTOM 编码消息。即使没有一个部分符合必需的标准，消息仍然是 MTOM 编码消息（序列化为一个 MIME 包，具有包含 SOAP 信封的单个 MIME 部分）。  
  
### MTOM 的 WS\-Policy 断言  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用以下策略断言来指示终结点对 MTOM 的使用：  
  
```  
<wsoma:OptimizedMimeSerialization ... />  
```  
  
-   R4211：上面的策略断言有一个终结点策略主题，并指定终结点收发的所有消息都必须使用 MTOM 进行优化。  
  
-   B4212：在配置为使用 MTOM 优化时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点将一个 MTOM 策略断言添加到对应 `wsdl:binding` 的附加策略中。  
  
### 与 WS\-Security 的结合  
 MTOM 是一种类似于 `text/xml` 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 二进制 XML 的编码机制。MTOM 可以与 WS\-Security 及其他 WS\-\* 协议自然结合：使用 WS\-Security 进行保护的消息可使用 MTOM 优化。  
  
### 示例  
  
#### 使用 MTOM 编码的 WCF SOAP 1.1 消息  
  
```  
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1  
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"  
Content-Type: multipart/related;type="application/xop+xml";  
              start="<http://tempuri.org/0>";start-info="text/xml";  
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
Host: 131.107.72.15  
Content-Length: 1501  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Body>  
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">  
      <array>  
        <xop:Include   
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"   
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </array>  
    </EchoBinaryAsString>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/1/632618206521093670>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
…Binary Content..  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
```  
  
#### 使用 MTOM 编码的 WCF 安全 SOAP 1.2 消息  
 此示例中，消息是使用 MTOM 以及采用 WS\-Security 进行保护的 SOAP 1.2 编码的。标识来进行编码的二进制部分为 `BinarySecurityToken` 的内容、对应于加密签名的 `EncryptedData` 的 `CipherValue`，以及经过加密的正文。请注意，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 未将 `EncryptedKey` 的 `CipherValue` 标识为进行优化，因为其长度小于 1024 个字节。  
  
```  
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1  
Content-Type: multipart/related; type="application/xop+xml";  
              start="<http://tempuri.org/0>";  
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";  
              start-info="application/soap+xml";   
              action="http://xmlsoap.org/echoBinaryAsString"  
Host: 131.107.72.15  
Content-Length: 1941  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
  <s:Header>  
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">  
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>  
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>  
      </u:Timestamp>  
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">  
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </o:BinarySecurityToken>  
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedKey>  
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">  
        <o:SecurityTokenReference>  
          <o:Reference URI="#_1"/>  
        </o:SecurityTokenReference>  
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>  
      </c:DerivedKeyToken>  
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:DataReference URI="#_3"/>  
        <e:DataReference URI="#_4"/>  
      </e:ReferenceList>  
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:Reference URI="#_2"/>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>  
          <e:CipherValue>  
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
          </e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedData>  
    </o:Security>  
  </s:Header>  
  <s:Body u:Id="_0">  
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
          <o:Reference URI="#_2"/>  
        </o:SecurityTokenReference>  
      </KeyInfo>  
      <e:CipherData>  
        <e:CipherValue>  
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
        </e:CipherValue>  
      </e:CipherData>  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/1/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary content of BinarySecurityToken - X509 Certificate...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/2/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted primary signature...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/3/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted Body...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--  
```