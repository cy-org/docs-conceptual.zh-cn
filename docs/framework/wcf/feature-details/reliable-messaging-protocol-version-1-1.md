---
title: "可靠消息协议版本 1.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 可靠消息协议版本 1.1
本主题介绍了 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] WS\-ReliableMessaging 执行细节 2007 年 2 月 （版本1.1）协议所需的互操作使用 HTTP 传输。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 遵循的 WS ReliableMessaging 规范与约束和解释本主题中的说明。请注意，WS\-ReliableMessaging 版本 1.1 协议是从 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 开始实现的。  
  
 2007 年 2 月发布的 WS\-ReliableMessaging 协议是在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中由 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> 实现的。  
  
 为方便起见，本主题使用以下角色：  
  
-   发起方：启动 WS\-Reliable Message 序列创建的客户端。  
  
-   响应方：接收发起方请求的服务。  
  
 本文档使用下表中的前缀和命名空间。  
  
|||  
|-|-|  
|前缀|命名空间|  
|wsrm|http:\/\/docs.oasis\-open.org\/ws\-rx\/wsrm\/200702|  
|netrm|http:\/\/schemas.microsoft.com\/ws\/2006\/05\/rm|  
|s|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/schemas.xmlsoap.org\/ws\/2005\/08\/addressing|  
|wsse|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wssecurity\-secext\-1.0.xsd|  
|wsrmp|http:\/\/docs.oasis\-open.org\/ws\-rx\/wsrmp\/200702|  
|netrmp|http:\/\/schemas.microsoft.com\/ws\-rx\/wsrmp\/200702|  
|wsp|（WS\-Policy 1.2 或 WS\-Policy 1.5）|  
  
## 消息传递  
  
### 序列创建  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现 `CreateSequence` 和 `CreateSequenceResponse` 消息以建立可靠消息序列。适用以下约束：  
  
-   B1101：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方与 `CreateSequence` 消息的 `ReplyTo`、`AcksTo` 和 `Offer/Endpoint` 使用相同的终结点引用。  
  
-   R1102：`CreateSequence` 消息中的 `AcksTo`、`ReplyTo` 和 `Offer/Endpoint` 终结点引用必须具有包含相同字符串表示的地址值，以便它们与八进制形式匹配。  
  
    -   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在创建序列之前验证 `AcksTo`、`ReplyTo` 和 `Endpoint` 终结点引用的 URI 部分是否相同。  
  
-   R1103：`CreateSequence` 消息中的 `AcksTo`、`ReplyTo` 和 `Offer/Endpoint` 终结点引用应该具有一组相同的引用参数。  
  
    -   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不强制而是假定 `CreateSequence` 上的 `AcksTo`、`ReplyTo` 和 `Offer/Endpoint` 终结点引用的引用参数是相同的，并将来自 `ReplyTo` 终结点应用的引用参数用于确认和相反序列消息。  
  
-   B1104：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方不在 `CreateSequence` 消息中生成可选的 `Expires` 或 `Offer/Expires` 元素。  
  
-   B1105：访问 `CreateSequence` 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方将 `CreateSequence` 元素中的 `Expires` 值用作 `CreateSequenceResponse` 元素中的 `Expires` 值。否则，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方读取并忽略 `Expires` 和 `Offer/Expires` 值。  
  
-   B1106：访问 `CreateSequenceResponse` 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方读取可选的 `Expires` 值但不使用它。  
  
-   B1107：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方和响应方始终在 `CreateSequence/Offer` 和 `CreateSequenceResponse` 元素中生成可选的 `IncompleteSequenceBehavior` 元素。  
  
-   B1108：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 仅使用 `IncompleteSequenceBehavior` 元素中的 `DiscardFollowingFirstGap` 和 `NoDiscard` 值。  
  
    -   WS\-ReliableMessaging 利用 `Offer` 机制建立构成会话的两个相反的相关序列。  
  
-   B1109：如果 `CreateSequence` 包含 `Offer` 元素，则单向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方通过没有 `Accept` 元素的 `CreateSequenceResponse` 进行响应来拒绝所提供的序列。  
  
-   B1110：如果可靠消息响应方拒绝所提供的序列，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方查找新建立的序列中的错误。  
  
-   B1111：如果 `CreateSequence` 不包含 `Offer` 元素，则双向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方通过 `CreateSequenceRefused` 错误进行响应来拒绝所提供的序列。  
  
-   R1112：使用 `Offer` 机制建立两个相反序列时，`CreateSequenceResponse/Accept/AcksTo` 终结点引用的 `[address]` 属性必须与 `CreateSequence` 消息的目标 URI 逐字节匹配。  
  
-   R1113：使用 `Offer` 机制建立两个相反序列时，从发起方流向响应方的两个序列上的所有消息都必须发送到同一终结点引用。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-ReliableMessaging 在发起方和响应方之间建立可靠的会话。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WS\-ReliableMessaging 实现为单向、请求\-答复和全双工消息模式提供了可靠的会话。`CreateSequence` 和 `CreateSequenceResponse` 上的 WS\-ReliableMessaging `Offer` 机制允许您建立两个相关的相反序列，并提供适合于所有消息终结点的会话协议。由于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为这样的会话提供了安全保证（包括会话完整性的端到端保护），因此确保发往同一方的消息到达同一目标是很实用的。这还允许应用程序消息上序列确认的“非法携带”。因此，约束 R1102、R1112 和 R1113 适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
 `CreateSequence` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>  
    <wsa:ReplyTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>   
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequence>  
      <wsrm:AcksTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>  
      </wsrm:AcksTo>  
      <wsrm:Offer>  
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>  
        <wsrm:Endpoint>  
          <wsa:Address>http://Business456.com/clientA</wsa:Address>  
        </wsrm:Endpoint>  
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      </wsrm:Offer>  
    </wsrm:CreateSequence>  
  </s:Body>  
</s:Envelope>  
```  
  
 `CreateSequenceResponse` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      <wsrm:Accept>  
        <wsrm:AcksTo>  
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>  
        </wsrm:AcksTo>  
      </wsrm:Accept>  
    </wsrm:CreateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### 关闭序列  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `CloseSequence` 和 `CloseSequenceResponse` 消息用于可靠消息源启动的关闭。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息目标不会启动关闭，且 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息源不支持可靠消息目标启动的关闭。适用以下约束：  
  
-   B1201：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息源始终发送 `CloseSequence` 消息以关闭序列。  
  
-   B1202：可靠消息源在发送 `CloseSequence` 消息之前，等待确认全部的序列消息。  
  
-   B1203：除非序列不包含消息，否则可靠消息源始终包括可选的 `LastMsgNumber` 元素。  
  
-   R1204：可靠消息目标不得通过发送 `CloseSequence` 消息启动关闭。  
  
-   B1205：接收到 `CloseSequence` 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息源认为序列不完整并发送错误。  
  
 `CloseSequence` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
    </wsrm:CloseSequence>  
  </s:Body>  
</s:Envelope>  
Example CloseSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:CloseSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### 序列终止  
 在完成 `CloseSequence/CloseSequenceResponse` 握手后 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 主要使用 `TerminateSequence/TerminateSequenceResponse` 握手。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息目标不启动终止，且可靠消息源不支持可靠消息目标启动的终止。适用以下约束：  
  
-   B1301：在成功完成 `CloseSequence/CloseSequenceResponse` 握手后，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方仅发送 `TerminateSequence` 消息。  
  
-   R1302：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 验证 `LastMsgNumber` 元素在给定序列的所有 `CloseSequence` 和 `TerminateSequence` 消息中是否一致。这意味着 `LastMsgNumber` 并不存在于所有 `CloseSequence` 和 `TerminateSequence` 消息上，或者它存在于所有 `CloseSequence` 和 `TerminateSequence` 消息上且完全相同。  
  
-   B1303：在 `CloseSequence/CloseSequenceResponse` 握手后收到 `TerminateSequence` 消息时，可靠消息目标通过 `TerminateSequenceResponse` 消息进行响应。由于可靠消息源在发送 `TerminateSequence` 消息之前具有最终确认，因此可靠消息目标可毫无疑问地知道序列将结束，并立即回收资源。  
  
-   B1304：在 `CloseSequence/CloseSequenceResponse` 握手之前收到 `TerminateSequence` 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息目标通过 `TerminateSequenceResponse` 消息进行响应。如果可靠消息目标确定序列中没有不一致之处，则可靠消息目标将在回收资源之前等待应用程序目标指定的时间，以便客户端有机会接收最终确认。否则，可靠消息目标立即回收资源，并通过引发 `Faulted` 事件向应用程序目标指出序列结束但存有疑问。  
  
 `TerminateSequence` 消息的一个示例。  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
      </wsrm:TerminateSequence>  
  </s:Body>  
</s:Envelope>  
Example TerminateSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:TerminateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### 序列  
 以下是适用于序列的约束的列表：  
  
-   B1401：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成并访问不大于 `xs:long` 的最大包含值 9223372036854775807 的序列号。  
  
 `Sequence` 标头的一个示例。  
  
```  
<wsrm:Sequence s:mustUnderstand="1">  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:MessageNumber>1</wsrm:MessageNumber>  
</wsrm:Sequence>  
```  
  
### 请求确认  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `AckRequested` 头用作“保持活动状态”机制。  
  
 `AckRequested` 标头的一个示例。  
  
```  
<wsrm:AckRequested>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
</wsrm:AckRequested>  
```  
  
### SequenceAcknowledgement  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将“非法携带”机制用于在 WS\-Reliable Messaging 中提供的序列确认。适用以下约束：  
  
-   R1601：使用 `Offer` 机制建立两个相反序列时，`SequenceAcknowledgement` 头可能包括在传输到预期接收方的任何应用程序消息中。远程终结点必须能够访问非法携带的 `SequenceAcknowledgement` 标头。  
  
-   B1602: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成包含 `SequenceAcknowledgement` 标题 `Nack` 元素。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成包含 `Nack` 元素序列号，如果不包含序列号，则忽略 `Nack` 元素和值。  
  
 `SequenceAcknowledgement` 标头的一个示例。  
  
```  
<wsrm:SequenceAcknowledgement>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>  
</wsrm:SequenceAcknowledgement>  
```  
  
### WS\-ReliableMessaging 错误  
 下面列出了适用 WS\-ReliableMessaging 错误的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 实现的约束。适用以下约束：  
  
-   B1701：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成 `MessageNumberRollover` 错误。  
  
-   B1702：对于 SOAP 1.2，当服务终结点达到其连接限制而无法处理新连接时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成嵌套的 `CreateSequenceRefused` 错误子代码 `netrm:ConnectionLimitReached`，如以下示例所示。  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>  
  </s:Header>  
  <s:Body>  
    <s:Fault>  
      <s:Code>  
        <s:Value>s:Receiver</s:Value>  
        <s:Subcode>  
          <s:Value>wsrm:CreateSequenceRefused</s:Value>  
          <s:Subcode>  
            <s:Value>netrm:ConnectionLimitReached</s:Value>  
          </s:Subcode>  
        </s:Subcode>  
      </s:Code>  
      <s:Reason>  
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>  
      </s:Reason>  
    </s:Fault>  
  </s:Body>  
</s:Envelope>  
```  
  
### WS\-Addressing 错误  
 由于 WS\-ReliableMessaging 使用 WS\-Addressing，因此 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WS\-ReliableMessaging 实现可能会生成并传输 WS\-Addressing 错误。本节介绍 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在 WS\-ReliableMessaging 层上显式生成并传输的 WS\-Addressing 错误：  
  
-   B1801：当以下条件之一为真时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成并传输 `Message Addressing Header Required` 错误：  
  
    -   `CreateSequence`、`CloseSequence` 或 `TerminateSequence` 消息缺少 `MessageId` 头。  
  
    -   `CreateSequence` `CloseSequence` 或 `TerminateSequence` 消息缺少 `ReplyTo` 头。  
  
    -   `CreateSequenceResponse`、`CloseSequenceResponse` 或 `TerminateSequenceResponse` 消息缺少 `RelatesTo` 头。  
  
-   B1802：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成并传输 `Endpoint Unavailable` 错误，以指示不存在可以基于 `CreateSequence` 消息中寻址头的检查处理序列的终结点侦听。  
  
## 协议组合  
  
### 与 WS\-Addressing 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 WS\-Addressing 的两种版本：WS\-Addressing 2004\/08 \[WS\-ADDR\] 以及 W3C WS\-Addressing 1.0 建议 \[WS\-ADDR\-CORE\] 和 \[WS\-ADDR\-SOAP\]。  
  
 尽管 WS\-ReliableMessaging 规范仅提及 WS\-Addressing 2004\/08，但是它不限制要使用的 WS\-Addressing 版本。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   R2101：WS\-Addressing 2004\/08 和 WS\-Addressing 1.0 都可以与 WS\-Reliable Messaging 一起使用。  
  
-   R2102：在整个的给定 WS\-ReliableMessaging 序列或通过使用 `Offer` 机制关联的一对相反序列中，必须使用 WS\-Addressing 的单个版本。  
  
### 与 SOAP 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持将 SOAP 1.1 和 SOAP 1.2 与 WS\-Reliable Messaging 一起使用。  
  
### 与 WS\-Security 和 WS\-SecureConversation 组合  
 通过使用安全传输 \(HTTPS\)、与 WS\-Security 的组合以及与 WS\-Secure Conversation 的组合，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了对 WS\-ReliableMessaging 序列的保护。WS\-ReliableMessaging 1.1 协议、WS\-Security 1.1 和 WS\-Secure Conversation 1.3 协议应该一起使用。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   R2301：为了保护单个消息的完整性和机密性以及 WS\-ReliableMessaging 序列的完整性，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 要求必须使用 WS\-Secure Conversation。  
  
-   R2302：必须在建立 WS\-ReliableMessaging 序列之前建立 WS\-Secure Conversation 会话。  
  
-   R2303：如果 WS\-ReliableMessaging 序列生存期超过了 WS\-Secure Conversation 会话的生存期，则必须通过使用对应的 WS\-Secure Conversation 续订绑定来续订通过使用 WS\-Secure Conversation 建立的 `SecurityContextToken`。  
  
-   B2304：WS\-ReliableMessaging 序列或一对相关的相反序列始终绑定到单个 WS\-SecureConversation 会话。  
  
-   R2305：与 WS\-Secure Conversation 组合时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方要求 `CreateSequence` 消息包含 `wsse:SecurityTokenReference` 元素和 `wsrm:UsesSequenceSTR` 头。  
  
 `UsesSequenceSTR` 标头的一个示例。  
  
```  
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>  
```  
  
### 与 SSL\/TLS 会话组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不支持与 SSL\/TLS 会话组合：  
  
-   B2401：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不生成 `wsrm:UsesSequenceSSL` 头。  
  
-   R2402：可靠消息发起方不得将包含 `wsrm:UsesSequenceSSL` 头的 `CreateSequence` 消息发送到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方。  
  
### 与 WS\-Policy 组合  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 WS\-Policy 的两种版本：WS\-Policy 1.2 和 WS\-Policy 1.5。  
  
## WS\-ReliableMessaging WS\-Policy 断言  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-ReliableMessaging WS\-Policy 断言 `wsrm:RMAssertion` 描述终结点功能。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   B3001： [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 附加 `wsrmn:RMAssertion` WS\-Policy 断言  `wsdl:binding` 元素。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持两个附件 `wsdl:binding` 和  `wsdl:port` 元素。  
  
-   B3002：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 从不生成 `wsp:Optional` 标记。  
  
-   B3003：访问 `wsrmp:RMAssertion` WS\-Policy 断言时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 忽略 `wsp:Optional` 标记并将 WS\-RM 策略视为强制。  
  
-   R3004：由于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不与 SSL\/TLS 会话组合，因此 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不接受指定 `wsrmp:SequenceTransportSecurity` 的策略。  
  
-   B3005：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 始终生成 `wsrmp:DeliveryAssurance` 元素。  
  
-   B3006：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 始终指定 `wsrmp:ExactlyOnce` 传递确定性。  
  
-   B3007：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成并读取 WS\-ReliableMessaging 断言的以下属性，以及在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`ReliableSessionBindingElement` 上提供对它们的控制：  
  
    -   `netrmp:InactivityTimeout`  
  
    -   `netrmp:AcknowledgementInterval`  
  
     `RMAssertion` 的一个示例。  
  
    ```  
    <wsrmp:RMAssertion>  
      <wsp:Policy>  
        <wsrmp:SequenceSTR/>  
        <wsrmp:DeliveryAssurance>  
          <wsp:Policy>  
            <wsrmp:ExactlyOnce/>  
            <wsrmp:InOrder/>  
          </wsp:Policy>  
        </wsrmp:DeliveryAssurance>  
      </wsp:Policy>  
      <netrmp:InactivityTimeout Milliseconds="600000"/>  
      <netrmp:AcknowledgementInterval Milliseconds="200"/>  
    </wsrmp:RMAssertion>  
    ```  
  
## 流控制 WS\-ReliableMessaging 扩展  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 WS\-ReliableMessaging 扩展性提供对序列消息流的其他可选的更紧密控制。  
  
 通过将 `ReliableSessionBindingElement` 的 `FlowControlEnabled``boolean` 属性设置为 `true` 可启用流控制。下面列出了适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的约束：  
  
-   B4001：启用可靠消息流控制时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在 `SequenceAcknowledgement` 头的元素扩展性中生成 `netrm:BufferRemaining` 元素，如下面的示例所示。  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="1" Lower="1"/>             
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    ```  
  
-   B4002：甚至在启用可靠消息流控制时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 也不要求 `SequenceAcknowledgement` 标头中包含 `netrm:BufferRemaining` 元素。  
  
-   B4003：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息目标使用 `netrm:BufferRemaining` 指示它可以缓冲多少条新消息。  
  
-   B4004：启用可靠消息流控制时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠消息源使用 `netrm:BufferRemaining` 的值遏制消息传输。  
  
-   B4005：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成介于 0 和 4096（包括这两个值）之间的 `netrm:BufferRemaining` 整数值，并读取介于 0 和 `xs:int` 的 `maxInclusive` 值 214748364（包括这两个值）之间的整数值。  
  
## 消息交换模式  
 本节介绍 WS\-ReliableMessaging 用于不同消息交换模式时 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的行为。对于每个消息交换模式，可以考虑下面的两个部署方案：  
  
-   不可寻址的发起方：发起方位于防火墙背后；响应方只能在 HTTP 响应上将消息传递到发起方。  
  
-   可寻址的发起方：发起方和响应方都可以发送 HTTP 请求；换句话说，可以建立两个相反的 HTTP 连接。  
  
### 单向、不可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用一个序列的单向消息交换模式提供 HTTP 信道。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过一个 HTTP 通道使用一个序列的单向消息交换模式。使用 HTTP 请求将所有消息从发起方传输到响应方，并使用 HTTP 响应将所有消息从响应方传输到发起方。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输没有 `Offer` 元素的 `CreateSequence` 消息，并在 HTTP 响应上期望 `CreateSequenceResponse` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方创建一个序列，并在 HTTP 响应上传输没有 `Accept` 元素的 `CreateSequenceResponse` 消息。  
  
#### SequenceAcknowledgement  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方处理除 `CreateSequence` 消息和错误消息之外的所有消息答复的确认消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方始终将 HTTP 响应上的独立确认传输到所有序列和 `AckRequested` 消息。  
  
#### CloseSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输 `CloseSequence` 消息，并在 HTTP 响应上期望 `CreateSequenceResponse` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在 HTTP 响应上传输 `CloseSequenceResponse` 消息。  
  
#### TerminateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输 `TerminateSequence` 消息，并在 HTTP 响应上期望 `TerminateSequenceResponse` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在 HTTP 响应上传输 `TerminateSequenceResponse` 消息。  
  
### 单向、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种单向的消息交换模式，这种模式在入站和出站 Http 通道上使用一个序列。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用 HTTP 请求传输的所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输没有 `Offer` 元素的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方创建一个序列，并在 HTTP 请求上传输没有 `Accept` 元素的 `CreateSequenceResponse` 消息。  
  
### 双工、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过一个入站和一个出站 HTTP 通道使用两个序列的完全异步的双向消息交换模式。此消息交换模式可以与 `Request/Reply`、`Addressable` 发起方消息交换模式有限地混合使用。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 HTTP 请求传输的所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输具有 `Offer` 元素的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保 `CreateSequence` 具有 `Offer` 元素，然后创建一个序列并传输具有 `Accept` 元素的 `CreateSequenceResponse` 消息。  
  
#### 序列生存期  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将两个序列视为一个全双工会话。  
  
 生成使一个序列出错的错误时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 期望远程终结点使这两个序列出错。读取使一个序列出错的错误时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会使这两个序列出错。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以关闭其出站序列并继续处理其入站序列上的消息。相反，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以处理入站序列的关闭，并在其出站序列上继续发送消息。  
  
### 请求\-答复和单向、不可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过 HTTP 通道使用两个序列的请求\-答复消息交换模式。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过一个 HTTP 通道使用一个序列的单向消息交换模式。使用 HTTP 请求将所有消息从发起方传输到响应方，并使用 HTTP 响应将所有消息从响应方传输到发起方。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输具有 `Offer` 元素的 `CreateSequence` 消息，并在 HTTP 响应上期望 `CreateSequenceResponse` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方创建一个序列，并在 HTTP 响应上传输具有 `Accept` 元素的 `CreateSequenceResponse` 消息。  
  
#### 单向消息  
 为成功完成单向消息交换，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列消息，并在 HTTP 响应上接收独立的 `SequenceAcknowledgement` 消息。`SequenceAcknowledgement` 必须确认已传输的消息。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方可能通过确认、错误或正文为空且具有 HTTP 202 状态代码的响应来答复请求。  
  
#### 双向消息  
 为了成功地完成双向消息交换协议，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列消息，并在 HTTP 响应上接收答复序列消息。响应必须包含一个确认已传输的请求序列消息的 `SequenceAcknowledgement`。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方可以使用应用程序答复、错误或正文为空且具有 HTTP 202 状态代码的响应来答复请求。  
  
 由于存在单向消息和应用程序答复的计时，因此请求序列消息的序列号与响应消息的序列号不相关联。  
  
#### 重试答复  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 依赖于 HTTP 请求\-答复关联来进行双向消息交换协议关联。由于这一原因，在已确认请求序列消息时而不是在 HTTP 响应包含 `SequenceAcknowledgement`、应用程序答复或错误时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方不停止重试请求序列消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在答复与其相关的请求的 HTTP 响应上重试答复。  
  
#### CloseSequence 交换  
 收到所有单向请求序列消息的所有答复序列消息和确认后，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列的 `CloseSequence` 消息，并在 HTTP 响应上期望 `CloseSequenceResponse`。  
  
 关闭请求序列将隐式关闭答复序列。这意味着 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 `CloseSequence` 消息上包括答复序列的最终 `SequenceAcknowledgement`，且答复序列没有 `CloseSequence` 交换。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保已确认所有答复并在 HTTP 响应上传输 `CloseSequenceResponse` 消息。  
  
#### TerminateSequence 交换  
 收到 `CloseSequenceResponse` 消息后，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输请求序列的 `TerminateSequence` 消息，并在 HTTP 响应上期望 `TerminateSequenceResponse`。  
  
 与 `CloseSequence` 交换一样，终止请求序列将隐式终止答复序列。这意味着 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 `TerminateSequence` 消息上包括答复序列的最终 `SequenceAcknowledgement`，且答复序列没有 `TerminateSequence` 交换。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方在 HTTP 响应上传输 `TerminateSequenceResponse` 消息。  
  
### 请求\/答复、可寻址的发起方  
  
#### 绑定  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了通过一个入站和一个出站 HTTP 通道使用两个序列的请求\-答复消息交换模式。此消息交换模式可以与 `Duplex, Addressable` 发起方消息交换模式有限地混合使用。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用 HTTP 请求传输的所有消息。所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### CreateSequence 交换  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 发起方在 HTTP 请求上传输具有 `Offer` 元素的 `CreateSequence` 消息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 响应方确保 `CreateSequence` 具有 `Offer` 元素，然后创建一个序列并传输具有 `Accept` 元素的 `CreateSequenceResponse` 消息。  
  
#### 请求\/答复关联  
 以下内容适用于所有关联的请求和答复：  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 确保所有应用程序请求消息都具有 `ReplyTo` 终结点引用和 `MessageId`。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将本地终结点引用作为每个应用程序请求消息的 `ReplyTo` 应用。本地终结点引用是发起方的 `CreateSequence` 消息的 `ReplyTo` 和响应方的 `CreateSequence` 消息的 `To`。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 确保传入请求消息具有 `MessageId` 和 `ReplyTo`。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 确保所有应用程序请求消息的 `ReplyTo` 终结点引用的 URI 都与前面定义的本地终结点引用匹配。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 确保所有答复都具有遵循 `wsa` 请求\/答复关联规则的正确 `RelatesTo` 和 `To` 头。