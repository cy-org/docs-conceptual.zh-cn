---
title: "可靠消息传送协议版本 1.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5509a5c-de24-4bc2-9a48-19138055dcce
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 可靠消息传送协议版本 1.0
本主题讨论使用 HTTP 传输协议进行互操作所需的 WS\-Reliable Messaging February 2005（版本 1.0）的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 实现细节。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 遵循 WS Reliable Messaging 规范以及本主题中解释的约束和说明。请注意，WS\-ReliableMessaging 版本 1.0 协议是从 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 开始实现的。  
  
 通过 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中实现 WS\-Reliable Messaging February 2005 协议。  
  
 为方便起见，本主题使用以下角色：  
  
-   发起方：启动 WS\-Reliable Message 序列创建的客户端  
  
-   响应方：接收发起方的请求的服务  
  
 本文档使用下表中的前缀和命名空间。  
  
|前缀|命名空间|  
|--------|----------|  
|wsrm|http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm|  
|netrm|http:\/\/schemas.microsoft.com\/ws\/2006\/05\/rm|  
|s|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/schemas.xmlsoap.org\/ws\/2005\/08\/addressing|  
|wsse|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wssecurity\-secext\-1.0.xsd|  
  
## 消息传递  
  
### 序列建立消息  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 `CreateSequence` 和 `CreateSequenceResponse` 消息以建立可靠的消息序列。适用以下约束：  
  
-   B1101：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 `CreateSequence` 消息中或者在 `CreateSequence` 消息包含 `Offer` 元素（`Offer` 元素中的可选 `Expires` 元素）的情况下，不会生成可选的 Expires 元素。  
  
-   B1102：当访问 `CreateSequence` 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`Responder` 将发送和接收两个 `Expires` 元素（若存在），但不使用这两个元素的值。  
  
 WS\-Reliable Messaging 引入了 `Offer` 机制来建立两个形成会话的反向相关的序列。  
  
-   R1103：如果 `CreateSequence` 包含一个 `Offer` 元素，则可靠消息响应方要么必须接受序列并使用包含形成两个相关反向序列的 `wsrm:Accept` 元素的 `CreateSequenceResponse` 进行响应，要么必须拒绝 `CreateSequence` 请求。  
  
-   R1104：在反向序列上流动的 `SequenceAcknowledgement` 和应用程序消息必须发送到 `CreateSequence` 的 `ReplyTo` 终结点引用。  
  
-   R1105：`CreateSequence` 中的 `AcksTo` 和 `ReplyTo` 终结点引用必须具有与八进制识别匹配的地址值。  
  
     创建序列之前，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方验证 `AcksTo` 的 URI 部分与 `ReplyTo` EPR 是否相同。  
  
-   R1106：`CreateSequence` 中的 `AcksTo` 和 `ReplyTo` 终结点引用应具有相同的引用参数集。  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不强制但假定 `CreateSequence` 上的 `AcksTo` 和 `ReplyTo` 的 \[reference parameters\] 相同，并且从确认消息和反向序列消息的 `ReplyTo` 终结点引用中使用 \[reference parameters\]。  
  
-   R1107：在使用 `Offer` 机制建立两个反向序列时，在反向序列上流动的 `SequenceAcknowledgement` 和应用程序消息必须发送到 `CreateSequence` 的 `ReplyTo` 终结点引用。  
  
-   R1108：使用 Offer 机制建立两个反向序列时，`CreateSequenceResponse` 的 `wsrm:Accept` 元素的 `wsrm:AcksTo` 终结点引用子元素的 `[address]` 属性必须与 `CreateSequence` 的识别字节的目标 URI 相匹配。  
  
-   R1109：在使用 `Offer` 机制建立两个反向序列时，发起方发送的消息和响应方的消息确认必须发送到同一个终结点引用。  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-Reliable Messaging 在发起方和响应方之间建立可靠会话。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 WS\-Reliable Messaging 实现提供单向、请求\-答复和完全双工消息传递模式的可靠会话。`CreateSequence`\/`CreateSequenceResponse` 上的 WS\-Reliable Messaging `Offer` 机制使您可以建立两个相关的反向序列，并提供适合于所有消息终结点的会话协议。由于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为此类会话提供安全保证（包括端到端的会话完整性保护），因此确保发送到相同方的消息到达同一目标是可行的。这也允许在应用程序消息上捎带序列确认消息。因此，约束 R1104、R1105 和 R1108 适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
 `CreateSequence` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <a:Action s:mustUnderstand="1">  
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequence  
    </a:Action>  
    <a:ReplyTo>  
      <a:Address>          
         http://Business456.com/clientA        
      </a:Address>  
    </a:ReplyTo>  
    <a:MessageID>  
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
    </a:MessageID>  
    <a:To s:mustUnderstand="1">  
      http://Business456.com/clientA  
    </a:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequence>  
      <wsrm:AcksTo>  
       <wsa:Address>  
         http://Business456.com/clientA  
       </wsa:Address>  
     </wsrm:AcksTo>  
     <wsrm:Offer>  
      <wsrm:Identifier>  
        urn:uuid:0afb8d36-bf26-4776-b8cf-8c91fddb5496  
      </wsrm:Identifier>  
     </wsrm:Offer>  
   </wsrm:CreateSequence>  
  </s:Body>  
</s:Envelope>  
```  
  
 `CreateSequenceResponse` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <a:Action s:mustUnderstand="1">  
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequenceResponse  
    </a:Action>  
    <a:RelatesTo>  
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
    </a:RelatesTo>  
    <a:To s:mustUnderstand="1">  
      http://Business456.com/clientA  
    </a:To>  
  </s:Header>  
  <s:Body>  
   <wsrm:CreateSequenceResponse>  
    <Identifier>  
     urn:uuid:eea0a36c-b38a-43e8-8c76-2fabe2d76386  
    </Identifier>  
    <Accept>  
    <AcksTo>  
      <a:Address>  
        http://BusinessABC.com/serviceA  
      </a:Address>  
    </AcksTo>  
    </Accept>  
   </wsrm:CreateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### 序列  
 以下是适用于序列的约束的列表：  
  
-   B1201：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成并访问不大于 `xs:long` 的最大包含值 9223372036854775807 的序列号。  
  
-   B1202：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 总是使用 http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage 的操作 URI 生成正文空白的最后一条消息。  
  
-   B1203：只要操作 URI 不是 http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 就会接收和传送一条带有包含 `LastMessage` 元素的序列标头的消息。  
  
 Sequence 标头的一个示例。  
  
```  
<wsrm:Sequence>  
  <wsrm:Identifier>  
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
  </wsrm:Identifier>  
  <wsrm:MessageNumber>  
    10  
  </wsrm:MessageNumber>  
  <wsrm:LastMessage/>  
 </wsrm:Sequence>  
```  
  
### AckRequested 标头  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `AckRequested` 标头作为一种“保持活动状态”机制。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成可选的 `MessageNumber` 元素。在接收到带有包含 `MessageNumber` 元素的 `AckRequested` 标头的消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将忽略 `MessageNumber` 元素的值，如下面的示例所示。  
  
```  
<wsrm:AckRequested>  
  <wsrm:Identifier>  
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
  </wsrm:Identifier>  
</wsrm:AckRequested>  
```  
  
### SequenceAcknowledgement 标头  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将“非法携带”机制用于在 WS\-Reliable Messaging 中提供的序列确认。  
  
-   R1401：使用 `Offer` 机制建立两个相反序列时，`SequenceAcknowledgement` 头可能包括在传输到预期接收方的任何应用程序消息中。  
  
-   B1402：当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 必须在接收任何序列消息之前生成确认消息时（例如，满足 `AckRequested` 消息），[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将生成包含 0\-0 范围的 `SequenceAcknowledgement` 标头，如下面的示例所示。  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>  
        urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
      </wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="0" Lower="0"/>  
    </wsrm:SequenceAcknowledgement>  
    ```  
  
-   B1403：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成包含 `Nack` 元素的 `SequenceAcknowledgement` 标头，但支持 `Nack` 元素。  
  
### WS\-ReliableMessaging 错误  
 下面列出了适用于 WS\-Reliable Messaging 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现错误的约束：  
  
-   B1501：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成 `MessageNumberRollover` 错误。  
  
-   B1502：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点可能生成 `CreateSequenceRefused` 错误，如规范中所述。  
  
-   B1503：当服务终结点达到其连接限制并无法处理新连接时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成一个附加的 `CreateSequenceRefused` 错误子代码 `netrm:ConnectionLimitReached`，如下面的示例所示。  
  
    ```  
    <s:Envelope>  
      <s:Header>  
        <wsa:Action>  
          http://schemas.xmlsoap.org/ws/2005/08/addressing/fault  
        </wsa:Action>  
      </s:Header>  
      <s:Body>  
        <s:Fault>  
          <s:Code>  
            <s:Value>  
              s:Receiver  
            </s:Value>  
            <s:Subcode>  
              <s:Value>  
                wsrm:CreateSequenceRefused  
              </s:Value>  
              <s:Subcode>  
                <s:Value>  
                  netrm:ConnectionLimitReached  
                </s:Value>  
              </s:Subcode>  
            </s:Subcode>  
          </s:Code>  
          <s:Reason>  
            <s:Text xml:lang="en">  
              [Reason]  
            </s:Text>  
          </s:Reason>  
        </s:Fault>  
      </s:Body>  
    </s:Envelope>  
    ```  
  
### WS\-Addressing 错误  
 因为 WS\-Reliable Messaging 使用 WS\-Addressing，所以 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WS\-Reliable Messaging 实现可能生成 WS\-Addressing 错误。本节介绍了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在 WS\-Reliable Messaging 层显式生成的 WS\-Addressing 错误。  
  
-   B1601：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在满足以下条件之一时生成“要求消息寻址标头”：  
  
    -   消息缺少 `Sequence` 标头和 `Action` 标头。  
  
    -   `CreateSequence` 消息缺少 `MessageId` 标头。  
  
    -   `CreateSequence` 消息缺少 `ReplyTo` 标头。  
  
-   B1602：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在响应缺少 `Sequence` 标头并包含 WS\-Reliable Messaging 规范不能识别的 `Action` 标头的消息时，将生成“操作不支持”错误。  
  
-   B1603：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成“终结点不可用”错误以指示终结点将不会根据对 `CreateSequence` 消息的寻址标头的检查来处理序列。  
  
## 协议组合  
  
### 与 WS\-Addressing 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 WS\-Addressing 的两种版本：WS\-Addressing 2004\/08 \[WS\-ADDR\] 以及 W3C WS\-Addressing 1.0 建议 \[WS\-ADDR\-CORE\] 和 \[WS\-ADDR\-SOAP\]。  
  
 尽管 WS\-Reliable Messaging 规范只提及 WS\-Addressing 2004\/08，它并未限制要使用的 WS\-Addressing 版本。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   R2101：WS\-Addressing 2004\/08 和 WS\-Addressing 1.0 都可以与 WS\-Reliable Messaging 一起使用。  
  
-   R2102：必须在整个给定的 WS\-Reliable Messaging 序列或一对通过使用 `wsrm:Offer` 机制相关的反向序列上使用 WS\-Addressing 的单一版本。  
  
### 与 SOAP 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持将 SOAP 1.1 和 SOAP 1.2 与 WS\-Reliable Messaging 组合使用。  
  
### 与 WS\-Security 和 WS\-SecureConversation 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通过使用安全传输协议 \(HTTPS\)、与 WS\-Security 的组合以及与 WS\-Secure Conversation 的组合，为 WS\-Reliable Messaging 序列提供保护。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   R2301：为了在保护单个消息的完整性和机密性的同时保护 WS\-Reliable Messaging 序列的完整性，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 要求必须使用 WS\-Secure Conversation。  
  
-   R2302：WS\-Secure Conversation 会话必须在建立 WS\-Reliable Messaging 序列之前建立。  
  
-   R2303：如果 WS\-Reliable Messaging 序列生存期超过了 WS\-Secure Conversation 会话的生存期，则通过使用 WS\-Secure Conversation 建立的 `SecurityContextToken` 必须通过使用相应的 WS\-Secure Conversation 续订绑定来进行续订。  
  
-   B2304：WS\-Reliable Messaging 序列或一对相关的反向序列总是绑定到单一的 WS\-SecureConversation 会话。  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 源在 `CreateSequence` 消息的元素扩展性节中生成 `wsse:SecurityTokenReference` 元素。  
  
-   R2305：在与 WS\-Secure Conversation 组合时，`CreateSequence` 消息必须包含 `wsse:SecurityTokenReference` 元素。  
  
## WS\-Reliable Messaging WS\-Policy 断言  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-Reliable Messaging WS\-Policy 断言 `wsrm:RMAssertion` 来描述终结点功能。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   B3001：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `wsrm:RMAssertion` WS\-Policy 断言附加到 `wsdl:binding` 元素。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 `wsdl:binding` 和  `wsdl:port` 元素的附件。  
  
-   B3002：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 WS\-Reliable Messaging 断言的以下可选属性，并在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`ReliableMessagingBindingElement` 上提供对这些属性的控制：  
  
    -   `wsrm:InactivityTimeout`  
  
    -   `wsrm:AcknowledgementInterval`  
  
     下面是一个示例。  
  
    ```  
    <wsrm:RMAssertion>  
      <wsrm:InactivityTimeout Milliseconds="600000" />  
      <wsrm:AcknowledgementInterval Milliseconds="200" />  
    </wsrm:RMAssertion>  
    ```  
  
## 流控制 WS\-Reliable Messaging 扩展  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-Reliable Messaging 扩展性提供对序列消息流的其他可选的更紧密控制。  
  
 通过将 `ReliableSessionBindingElement` 的 `FlowControlEnabled``bool` 属性设置为 `true` 可启用流控制。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   B4001：在启用可靠消息传递流控制时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在 `SequenceAcknowledgement` 标头的元素扩展性中生成 `netrm:BufferRemaining` 元素。  
  
-   B4002：在启用可靠消息传递流控制时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不要求 `SequenceAcknowledgement` 标头中存在 `netrm:BufferRemaining` 元素，如下面的示例所示。  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>  
        http://fabrikam123.com/abc  
      </wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="1" Lower="1"/>             
      <netrm:BufferRemaining>  
        8  
      </netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
  
    ```  
  
-   B4003：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 `netrm:BufferRemaining` 来指示可靠消息传递目标可以缓冲多少条新消息。  
  
-   B4004：当可靠消息传递目标应用程序不能快速接收消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息传递服务将控制传输的消息的数目。可靠消息传递目标将缓冲消息，而该元素的值将下降为 0。  
  
-   B4005：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成介于 0 和 4096（包括这两个值）之间的 `netrm:BufferRemaining` 整数值，并读取介于 0 和 `xs:int` 的 `maxInclusive` 值 214748364（包括这两个值）之间的整数值。  
  
## 消息交换模式  
 本节描述了将 WS\-Reliable Messaging 用于不同的消息交换模式时的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的行为。对于每个消息交换模式，可以考虑下面的两个部署方案：  
  
-   不可寻址发起方：发起方位于防火墙后面；响应方仅可以通过 HTTP 响应向发起方传递消息。  
  
-   可寻址的发起方：发起方和响应方都可以发送 HTTP 请求；换句话说，可以建立两个相反的 HTTP 连接。  
  
### 单向、不可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过一个 HTTP 通道使用一个序列的单向消息交换模式。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求将所有消息从 RMS 传输到 RMD，并使用 HTTP 响应将所有消息从 RMD 传输到 RMS。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方生成未包含提议的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保在创建序列之前 `CreateSequence` 不包含提议。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方使用 `CreateSequenceResponse` 消息答复 `CreateSequence` 请求。  
  
#### SequenceAcknowledgement  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方处理除 `CreateSequence` 消息和错误消息之外的所有消息答复的确认消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方总是在对序列消息和 `AckRequested` 消息的响应中生成一个独立的确认消息。  
  
#### TerminateSequence 消息  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `TerminateSequence` 视为单向操作，这意味着，HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
### 单向、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种单向的消息交换模式，这种模式在入站和出站 Http 通道上使用一个序列。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求传输所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方生成未包含提议的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保在创建序列之前 `CreateSequence` 不包含提议。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在使用 `ReplyTo` 终结点引用寻址的 HTTP 请求上传输 `CreateSequenceResponse` 消息。  
  
### 双工、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种完全异步的双向消息交换模式，这种模式在入站和出站 HTTP 通道上使用两个序列。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求传输所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方生成包含提议的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保在创建序列之前 `CreateSequence` 包含提议。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在寻址到 `CreateSequence`的 `ReplyTo` 终结点引用的 HTTP 请求上发送 `CreateSequenceResponse`。  
  
#### 序列生存期  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将两个序列视为一个全双工会话。  
  
 生成使一个序列出错的错误时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 期望远程终结点使这两个序列出错。读取使一个序列出错的错误时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会使这两个序列出错。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以关闭其出站序列并继续处理其入站序列上的消息。相反，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以处理入站序列的关闭，并在其出站序列上继续发送消息。  
  
### 请求\-答复、不可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种单向的请求\-答复消息交换模式，这种模式在一个 HTTP 通道上使用两个序列。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求来传输请求序列的消息，并使用 HTTP 响应传输答复序列的消息。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方生成包含提议的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保在创建序列之前 `CreateSequence` 包含提议。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方使用 `CreateSequenceResponse` 消息答复 `CreateSequence` 请求。  
  
#### 单向消息  
 为了成功地完成单向消息交换协议，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列消息，并在 HTTP 响应上接收独立的 `SequenceAcknowledgement` 消息。`SequenceAcknowledgement` 必须确认已传输的消息。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方可以使用确认消息、错误或正文为空且具有 HTTP 202 状态代码的响应来答复请求。  
  
#### 双向消息  
 为了成功地完成双向消息交换协议，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列消息，并在 HTTP 响应上接收答复序列消息。响应必须包含一个确认已传输的请求序列消息的 `SequenceAcknowledgement`。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方可以使用应用程序答复、错误或正文为空且具有 HTTP 202 状态代码的响应来答复请求。  
  
 由于存在单向消息和应用程序答复的计时，因此请求序列消息的序列号与响应消息的序列号不相关联。  
  
#### 重试答复  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 依赖于 HTTP 请求\-答复关联来进行双向消息交换协议关联。因此，在确认请求序列消息时（而不是在 HTTP 响应携带确认消息、用户消息或错误时），[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方不会停止重试请求序列消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方重试次数依赖于与答复相关联的请求的 HTTP 请求路线。  
  
#### LastMessage 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求路线上生成并传输正文为空的最后一条消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 需要一个响应，但忽略实际响应消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方使用答复序列的正文为空的最后一条消息答复请求序列的正文为空的最后一条消息。  
  
 如果 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方接收到最后一条消息并且其中的操作 URI 不为 http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage 中，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用最后一条消息进行答复。在双向消息交换协议中，最后一条消息携带应用程序消息；在单向消息交换协议中，最后一条消息为空。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方不要求确认答复序列的正文为空的最后一条消息。  
  
#### TerminateSequence 交换  
 在所有请求已接收一个有效答复时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求路线上生成并传输请求序列的 `TerminateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 需要一个响应，但忽略实际响应消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方使用答复序列的 `TerminateSequence` 消息答复请求序列的 `TerminateSequence` 消息。  
  
 在正常的关闭序列中，两个 `TerminateSequence` 消息都携带一个完整范围的 `SequenceAcknowledgement`。  
  
### 请求\/答复、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种请求\-答复消息交换模式，这种模式在入站和出站 HTTP 通道上使用两个序列。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求传输所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方生成包含提议的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保在创建序列之前 `CreateSequence` 包含提议。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在寻址到 `CreateSequence`的 `ReplyTo` 终结点引用的 HTTP 请求上发送 `CreateSequenceResponse`。  
  
#### 请求\/答复关联  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方确保所有应用程序请求消息都具有一个 `MessageId` 和一个 `ReplyTo` 终结点引用。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在每个应用程序请求消息上应用 `CreateSequence` 消息的 `ReplyTo` 终结点引用。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方要求传入的请求消息具有一个 `MessageId` 和一个 `ReplyTo`。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保两个 `CreateSequence` 的终结点引用的 URI 与所有应用程序请求消息相同。