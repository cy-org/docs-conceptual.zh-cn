---
title: "JSON 和 XML 之间的映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22ee1f52-c708-4024-bbf0-572e0dae64af
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# JSON 和 XML 之间的映射
读取器和编写器生成的<xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>通过 JavaScript 对象表示法 (JSON) 内容提供 XML API。 JSON 使用 JavaScript 的对象文字子集对数据进行编码。 JSON 内容时也使用读取器和编写器，此工厂生成发送或接收的[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]使用的应用程序<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>或<xref:System.ServiceModel.WebHttpBinding>。  
  
 使用 JSON 内容进行初始化时，JSON 读取器的行为方式与文本 XML 读取器通过 XML 实例执行的方式相同。 对文本 XML 读取器的调用序列生成某个 XML 实例时，JSON 编写器写出 JSON 内容。 本主题中描述此 XML 实例和 JSON 内容之间的映射以供在高级方案中使用。  
  
 在内部，由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 处理时，JSON 表示为 XML infoset。 通常，无须关注此内部表示，因为该映射仅仅是逻辑映射：JSON 通常并不物理转换为内存中的 XML 或从 XML 转换为 JSON。 该映射意味着 XML API 用于访问 JSON 内容。  
  
 当[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用 JSON 时，通常的方案是<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>由自动插入<xref:System.ServiceModel.Description.WebScriptEnablingBehavior>行为，或由<xref:System.ServiceModel.Description.WebHttpBehavior>行为在适当的时候。 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>了解 JSON 和 XML infoset 之间的映射和行为就像它直接处理 json。 (可以使用<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>与任何 XML 读取器或编写器，并了解 XML 符合下面的映射。)  
  
 在高级方案中，可能需要直接访问下面的映射。 当您想要序列化和反序列化 JSON 自定义方式，而不依赖于时，会出现这些情况<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>，或在处理时<xref:System.ServiceModel.Channels.Message>直接为包含 JSON 消息的类型。 JSON-XML 映射也用于消息日志记录。 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中使用消息日志记录功能时，按照下一节中描述的映射，将 JSON 消息记录为 XML。  
  
 为阐明映射的概念，下面的示例采用一个 JSON 文档。  
  
```  
{"product":"pencil","price":12}  
```  
  
 若要读取此 JSON 文档，使用前面提到的读取器之一，请使用相同的序列<xref:System.Xml.XmlDictionaryReader>调用，就像要阅读下面的 XML 文档。  
  
```  
<root type="object">  
    <product type="string">pencil</product>  
    <price type="number">12</price>  
</root>  
```  
  
 此外，如果示例中的 JSON 消息由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 接收并记录，则在前面的日志中会看到 XML 片段。  
  
## <a name="mapping-between-json-and-the-xml-infoset"></a>JSON 和 XML Infoset 之间的映射  
 正式情况下，映射是 JSON 之间中所述[RFC 4627](http://go.microsoft.com/fwlink/?LinkId=98808) （除非在某些限制宽松和某些添加其他限制） 和 XML 信息集 （以及不是文本 XML） 中所述[XML 信息集](http://go.microsoft.com/fwlink/?LinkId=98809)。 请参阅本主题有关的定义*信息项*和 [方括号] 中的字段。  
  
 空 JSON 文档映射到空 XML 文档，而空 XML 文档映射到空 JSON 文档。 在 XML 到 JSON 的映射上，文档之后不允许有前导空白和尾随空白。  
  
 映射是在文档信息项 (DII) 或元素信息项 (EII) 和 JSON 之间定义的。 EII 或 DII 的 [文档元素] 属性称为根 JSON 元素。 请注意此映射不支持文档片段（具有多个根元素的 XML）。  
  
 示例：下面的文档：  
  
 `<?xml version="1.0"?>`  
  
 `<root type="number">42</root>`  
  
 和下面的元素：  
  
 `<root type="number">42</root>`  
  
 都具有到 JSON 的映射。 `root`1> 元素是根 JSON 元素，这两种情况。  
  
 此外，在使用 DII 的情况下，应该考虑以下内容：  
  
-   [子级] 列表中的某些项不得存在。 读取从 JSON 映射的 XML 时，不要依赖于此事实。  
  
-   [子级] 列表不包含注释信息项。  
  
-   [子级] 列表不包含 DTD 信息项。  
  
-   [子级] 列表不包含个人信息 (PI) 信息项（不将 \<?xml…> 声明视为 PI 信息项）  
  
-   [符号] 集为空。  
  
-   [未分析的实体] 集为空。  
  
 示例：下面的文档没有到 JSON 的映射，因为 [子级] 包含 PI 和注释。  
  
 `<?xml version="1.0"?>`  
  
 `<!--comment--><?pi?>`  
  
 `<root type="number">42</root>`  
  
 根 JSON 元素的 EII 具有以下特征：  
  
-   [本地名称] 具有值“root”。  
  
-   [命名空间名称] 没有值。  
  
-   [前缀] 没有值。  
  
-   [子级] 可能包含 EII（表示内部元素，将进一步描述）或 CII（字符信息项，将进一步描述）或这两者都不包含，但不能同时包含这两者。  
  
-   [属性] 可能包含以下可选的属性信息项 (AII)  
  
-   JSON 类型属性（“type”），将进一步描述。 此属性用于保留已映射 XML 中的 JSON 类型（字符串、数字、boolean、对象、数组或 null）。  
  
-   数据协定名称属性（“__type”），将进一步描述。 仅当 JSON 类型属性也存在且其 [正常化值] 为“object”时，此属性才能存在。 此属性由 `DataContractJsonSerializer` 用来保留数据协定类型信息 - 例如，在序列化派生类型和期望基类型的多态情况下。 如果未使用 `DataContractJsonSerializer`，则大多数情况下忽略此属性。  
  
-   [范围内命名空间] 包含“xml”到“http://www.w3.org/XML/1998/namespace”的绑定，如 infoset 规范要求的那样。  
  
-   [子级]、[属性] 和 [范围内命名空间] 不得具有除前面指定的之外的任何项，[命名空间属性] 不得具有成员，但是在读取从 JSON 映射的 XML 时不依赖于这些事实。  
  
 示例：下面的文档没有到 JSON 的映射，因为 [命名空间属性] 不为空。  
  
 `<?xml version="1.0"?>`  
  
 `<root  xmlns:a="myattributevalue">42</root>`  
  
 JSON 类型属性的 AII 具有以下特征：  
  
-   [命名空间名称] 没有值。  
  
-   [前缀] 没有值。  
  
-   [本地名称] 为“type”。  
  
-   [正常化值] 是下面部分中描述的可能类型值之一。  
  
-   [已指定] 为 `true`。  
  
-   [属性类型] 没有值。  
  
-   [引用] 没有值。  
  
 数据协定名称属性的 AII 具有以下特征：  
  
-   [命名空间名称] 没有值。  
  
-   [前缀] 没有值。  
  
-   [本地名称] 为“__type”（双下划线后跟“type”）。  
  
-   [正常化值] 是任何有效的 Unicode 字符串 – 此字符串到 JSON 的映射将在下面的部分中进行描述。  
  
-   [已指定] 为 `true`。  
  
-   [属性类型] 没有值。  
  
-   [引用] 没有值。  
  
 根 JSON 元素中包含的内部元素或其他内部元素具有以下特征：  
  
-   [本地名称] 可能具有任何值，将进一步描述  
  
-   [命名空间名称]、[前缀]、[子级]、[属性]、[命名空间属性] 和 [范围内命名空间] 遵循与根 JSON 元素相同的规则。  
  
 在根 JSON 元素和内部元素中，JSON 类型属性定义到 JSON 的映射和可能的 [子级] 及其解释。 属性的 [正常化值] 区分大小写，必须为小写，且不能包含空白。  
  
|`JSON Type Attribute` 的 AII 的 [正常化值]|对应 EII 的已允许 [子级]|映射到 JSON|  
|---------------------------------------------------------|---------------------------------------------------|---------------------|  
|`string`（或缺少 JSON 类型 AII）<br /><br /> `string` 与缺少 JSON 类型 AII 相同，使 `string` 成为默认值。<br /><br /> 因此，`<root> string1</root>` 映射到 JSON `string`“string1”。|0 个或多个 Cii|JSON `string`（JSON RFC，第 2.5 节）。 每个 `char` 是对应于来自 CII 的 [字符代码] 的字符。 如果没有 CII，则它映射到空 JSON `string`。<br /><br /> 示例：下面的元素映射到 JSON 片段：<br /><br /> `<root type="string">42</root>`<br /><br /> JSON 片段是“42”。<br /><br /> 在 XML 到 JSON 的映射上，必须转义的字符映射到转义符，所有其他字符都映射到未转义的字符。 "/"字符是特殊字符 – 即使它不一定要经过转义 (写出为"\\/")。<br /><br /> 示例：下面的元素映射到 JSON 片段。<br /><br /> `<root type="string">the "da/ta"</root>`<br /><br /> JSON 片段是" \\"da\\/ta\\""。<br /><br /> 在 JSON 到 XML 的映射上，任何转义符和未转义的字符都正确映射到对应的 [字符代码]。<br /><br /> 示例：JSON 片段“\u0041BC”映射到下面的 XML 元素。<br /><br /> `<root type="string">ABC</root>`<br /><br /> 字符串可以由未映射到 XML 的空白（JSON RFC 第 2 节中的“ws”）围绕。<br /><br /> 示例：JSON 片段           "ABC"（在第一个双引号之前存在空格）映射到下面的 XML 元素。<br /><br /> `<root type="string">ABC</root>`<br /><br /> XML 中的任何空白都映射到 JSON 中的空白。<br /><br /> 示例：下面的 XML 元素映射到 JSON 片段。<br /><br /> `<root type="string">  A BC      </root>`<br /><br /> JSON 片段是“ A BC ”。|  
|`number`|1 个或多个 CII|可能由空白围绕的 JSON `number`（JSON RFC，第 2.4 节）。 数字/空白组合中的每个字符都是对应于 CII 中 [字符代码] 的字符。<br /><br /> 示例：下面的元素映射到 JSON 片段。<br /><br /> `<root type="number">    42</root>`<br /><br /> JSON 片段是    42<br /><br /> （保留空白）。|  
|`boolean`|4 个或 5 个 CII（对应于 `true` 或 `false`），可能由其他空白 CII 围绕。|对应于字符串“true”的 CII 序列被映射到文字 `true`，而对应于字符串“false”的 CII 序列被映射到文字 `false`。 保留了围绕的空白。<br /><br /> 示例：下面的元素映射到 JSON 片段。<br /><br /> `<root type="boolean"> false</root>`<br /><br /> JSON 片段是 `false`。|  
|`null`|都不允许。|文字 `null`。 在 JSON 到 XML 的映射上，`null` 可能由未映射到 XML 的空白（第 2 节中的“ws”）围绕。<br /><br /> 示例：下面的元素映射到 JSON 片段。<br /><br /> `<root type="null"/>`<br /><br /> 或<br /><br /> `<root type="null"></root>`<br /><br /> :<br /><br /> 在这两种情况下 JSON 片段都是 `Null`。|  
|`object`|0 个或多个 EII。|如 JSON RFC 第 2.2 节中的 `begin-object`（左花括号），后跟每个 EII 的成员记录，将进一步说明。 如果存在多个 EII，则在成员记录之间存在值分隔符（逗号）。 所有这一切后跟 end-object（右花括号）。<br /><br /> 示例：下面的元素映射到 JSON 片段。<br /><br /> <root type="object"></root>\><br /><br /> <type1 type="string"></type1>\>aaa\><br /><br /> <type2 type="string"></type2>\>bbb\><br /><br /> \><br /><br /> JSON 片段是 {"type1":"aaa","type2":"bbb"}。<br /><br /> 如果在 XML 到 JSON 的映射上存在数据协定类型属性，则在开头插入其他成员记录。 其名称是数据协定类型属性（“__type”）的 [本地名称]，其值是该属性的 [正常化值]。 相反，在 JSON 到 XML 的映射，如果第一个成员记录的名称是数据协定类型属性的 [本地名称] (即，"\_（_t)")，对应的数据协定类型属性是映射 XML 中存在但不存在对应的 EII。 请注意，此成员记录必须首先出现在 JSON 对象中才能应用此特殊映射。 这与通常的 JSON 处理（成员记录的顺序是不重要的）相背离。<br /><br /> 示例:<br /><br /> 下面的 JSON 片段映射到 XML。<br /><br /> `{"__type":"Person","name":"John"}`<br /><br /> XML 是下面的代码。<br /><br /> `<root type="object" __type="Person">   <name type="string">John</name> </root>`<br /><br /> 请注意， \_（_t） AII 存在，但没有任何\_（_t) EII。<br /><br /> 但是，如果保留 JSON 中的顺序，如下面的示例所示。<br /><br /> {"name":"John"，"\_（_t)":"Person"}<br /><br /> 则显示对应的 XML。<br /><br /> `<root type="object">   <name type="string">John</name>   <__type type="string">Person</__type> </root>`<br /><br /> 也就是说， \_（_t） 不再具有特殊含义，映射到 EII 同往常一样，不是 AII。<br /><br /> 映射到 JSON 值时，AII 的 [正常化值] 的转义/未转义规则与在此表的“string”行中指定的 JSON 字符串的相同。<br /><br /> 示例:<br /><br /> `<root type="object" __type="\abc" />`<br /><br /> 前面的示例可以映射到下面的 JSON。<br /><br /> `{"__type":"\\abc"}`<br /><br /> 在 XML 到 JSON 的映射上，第一个 EII 的 [本地名称] 不得是"\_（_t)"。<br /><br /> 在对象的 XML 到 JSON 的映射上从不生成空白 (`ws`)，且在 JSON 到 XML 的映射上忽略空白。<br /><br /> 示例：下面的 JSON 片段映射到 XML 元素。<br /><br /> {   "ccc"   :  "aaa",   "ddd"    :"bbb"}<br /><br /> 在下面的代码中显示了 XML 元素。<br /><br /> `<root type="object">    <ccc type="string">aaa</ccc>    <ddd type="string">bbb</bar> </root >`|  
ray'|0 个或多个 EII|如 JSON RFC 第 2.3 节中的 begin-array（左花括号），后跟每个 EII 的数组记录，将进一步描述。 如果存在多个 EII，则在数组记录之间存在值分隔符（逗号）。 所有这一切后跟 end-array。<br /><br /> 示例：下面的 XML 元素映射到 JSON 片段。<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`<br /><br /> JSON 片段是 ["aaa","bbb"]<br /><br /> 在数组的 XML 到 JSON 的映射上从不生成空白 (`ws`)，且在 JSON 到 XML 的映射上忽略空白。<br /><br /> 示例：AJSON 片段。<br /><br /> [     "aaa",     "bbb"]<br /><br /> 它映射到的 XML 元素。<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`|  
  
 成员记录的工作原理如下：  
  
-   内部元素的 [本地名称] 映射到 `string` 的 `member` 部分，如 JSON RFC 第 2.2 节所定义。  
  
 示例：下面的元素映射到 JSON 片段。  
  
 `<root type="object"/>`  
  
 `<myLocalName type="string">aaa</myLocalName>`  
  
 `</root >`  
  
 将显示下面的 JSON 片段。  
  
 `{"myLocalName":"aaa"}`  
  
-   在 XML 到 JSON 的映射上，对必须在 JSON 中转义的字符进行转义，而不对其他字符进行转义。 但是，对“/”字符进行转义，尽管它不是必须转义的字符（在 JSON 到 XML 的映射上不必对它进行转义）。 这是支持 JSON 中 `DateTime` 数据的 ASP.NET AJAX 格式所必需的。  
  
-   在 JSON 到 XML 的映射上，提取所有字符（如有必要，则包括未转义的字符）以构成一个生成 [本地名称] 的 `string`。  
  
-   按照 `JSON Type Attribute`，内部元素 [子级] 映射到第 2.2 节中的值，就像 `Root JSON Element` 那样。 允许 EII 的多级嵌套（包括数组中的嵌套）。  
  
 示例：下面的元素映射到 JSON 片段。  
  
 `<root type="object">`  
  
 `<myLocalName1 type="string">myValue1</myLocalName1>`  
  
 `<myLocalName2 type="number">2</myLocalName2>`  
  
 `<myLocalName3 type="object">`  
  
 `<myNestedName1 type="boolean">true</myNestedName1>`  
  
 `<myNestedName2 type="null"/>`  
  
 `</myLocalName3>`  
  
 `</root >`  
  
 下面的 JSON 片段是它映射到的内容。  
  
 `{"myLocalName1":"myValue1","myLocalName2":2,"myLocalName3":{"myNestedName1":true,"myNestedName2":null}}`  
  
> [!NOTE]
>  在前面的映射中没有 XML 编码步骤。 因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 仅支持其中密钥名称包含的所有字符都是 XML 元素名称中的有效字符的 JSON 文档。 例如，不支持 JSON 文档 {"<":"a"}，因为 < 不是 XML 元素的有效名称。  
  
 相反的情况（字符在 XML 中有效而在 JSON 中无效）不会导致任何问题，因为上述映射包括 JSON 转义/取消转义步骤。  
  
 数组记录的工作原理如下：  
  
-   内部元素的 [本地名称] 是“item”。  
  
-   按照 JSON 类型属性，内部元素的 [子级] 映射到第 2.3 节中的值，Root JSON 元素也是这样。 允许 EII 的多级嵌套（包括对象内的嵌套）。  
  
 示例：下面的元素映射到 JSON 片段。  
  
 `<root type="array"/>`  
  
 `<item type="string">myValue1</item>`  
  
 `<item type="number">2</item>`  
  
 `<item type="array">`  
  
 `<item type="boolean">true</item>`  
  
 `<item type="null"/>`  
  
 `</item>`  
  
 `</root >`  
  
 下面是 JSON 片段。  
  
 `["myValue1",2,[true,null]]`  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>   
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>   
 [独立 JSON 序列化](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)