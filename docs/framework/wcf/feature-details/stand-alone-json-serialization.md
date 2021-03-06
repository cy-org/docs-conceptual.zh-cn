---
title: "独立 JSON 序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 312bd7b2-1300-4b12-801e-ebe742bd2287
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# 独立 JSON 序列化
JSON（JavaScript 对象表示法）是专门为浏览器中的网页上运行的 JavaScript 代码而设计的一种数据格式。它是在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中创建的 ASP.NET AJAX 服务所使用的默认数据格式。  
  
 在未与 ASP.NET 集成的情况下（在此情况下，XML 将是默认格式，但可以选择 JSON）创建 AJAX 服务时，也可以使用此格式。  
  
 最后，如果需要 JSON 支持但不创建 AJAX 服务，则可以使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>，以便将 .NET 对象直接序列化为 JSON 数据并将此类数据反序列化回 .NET 类型的实例。有关如何执行此操作的说明，请参见[如何：对 JSON 数据进行序列化和反序列化](../../../../docs/framework/wcf/feature-details/how-to-serialize-and-deserialize-json-data.md)。  
  
 使用 JSON 时，它支持的 .NET 类型与 <xref:System.Runtime.Serialization.DataContractSerializer> 支持的类型相同，但有少数例外。有关支持的类型的列表，请参见[数据协定序列化程序支持的类型](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)。支持的类型包括大多数基元类型、大多数数组和集合类型，以及使用 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 的复杂类型。  
  
## 将 .NET 类型映射到 JSON 类型  
 下表显示了 .NET 类型和 JSON\/JavaScript 类型在通过序列化和反序列化过程进行映射时的对应关系。  
  
|.NET 类型|JSON\/JavaScript|注释|  
|-------------|----------------------|--------|  
|所有数值类型，例如 <xref:System.Int32>、<xref:System.Decimal> 或 <xref:System.Double>|Number|不支持 `Double.NaN`、`Double.PositiveInfinity` 和 `Double.NegativeInfinity` 等特殊值，它们会导致无效的 JSON。|  
|<xref:System.Enum>|Number|请参见本主题中后面的“枚举和 JSON”。|  
|<xref:System.Boolean>|Boolean|\-\-|  
|<xref:System.String>,<xref:System.Char>|String|\-\-|  
|<xref:System.Timespan>, <xref:System.Guid>, <xref:System.Uri>|String|这些类型在 JSON 与 XML 中的格式相同（基本上，TimeSpan 采用 ISO 8601 持续时间格式，GUID 采用“12345678\-ABCD\-ABCD\-ABCD\-1234567890AB”格式，URI 则采用其本来的字符串形式，例如“http:\/\/www.example.com”）。有关精确的信息，请参见[数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)。|  
|<xref:System.Xml.XmlQualifiedName>|字符串|格式为“名称:命名空间”（第一个冒号之前的所有内容都是名称）。可以缺少名称或命名空间。如果没有命名空间，则也可以省略冒号。|  
|<xref:System.Array> 类型为  的 。<xref:System.Byte>|数字数组|每个数字都表示一个字节的值。|  
|<xref:System.Datetime>|DateTime 或 String|请参见本主题中后面的“日期\/时间和 JSON”。|  
|<xref:System.DatetimeOffset>|复杂类型|请参见本主题中后面的“日期\/时间和 JSON”。|  
|XML 和 ADO.NET 类型（<xref:System.Xml.XmlElement>、<br /><br /> <xref:System.Xml.Linq.XElement>.<xref:System.Xml.XmlNode>、<br /><br /> <xref:System.Runtime.Serialization.ISerializable>,<br /><br /> <xref:System.Data.DataSet>\).|String|请参见本主题的“XML 类型和 JSON”一节。|  
|<xref:System.DBNull>|空复杂类型|\-\-|  
|集合、字典和数组|数组|请参见本主题的“集合、字典和数组”一节。|  
|复杂类型（应用了 <xref:System.Runtime.Serialization.DataContractAttribute> 或 <xref:System.SerializableAttribute>）|复杂类型|数据成员变为 JavaScript 复杂类型的成员。|  
|实现 <xref:System.Runtime.Serialization.ISerializable> 接口的复杂类型|复杂类型|与其他复杂类型相同，但不支持某些 <xref:System.Runtime.Serialization.ISerializable> 类型（请参见本主题“高级信息”一节的“ISerializable 支持”部分）。|  
|任何类型的 `Null` 值|Null|也支持可以为 null 的类型，这些类型映射到 JSON 的方式与不可以为 null 的类型相同。|  
  
### 枚举和 JSON  
 在 JSON 中，枚举成员值被作为数字处理，这与数据协定中处理枚举成员值的方式不同。在数据协定中，枚举成员值被视为成员名称。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]数据协定处理的更多信息，请参见[数据协定中的枚举类型](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md)。  
  
-   例如，如果存在 `public enum Color {red, green, blue, yellow, pink}`，则序列化 `yellow` 将生成数字 3，而不是字符串“yellow”。  
  
-   所有 `enum` 成员都是可序列化的。如果使用了 <xref:System.Runtime.Serialization.EnumMemberAttribute> 和 <xref:System.NonSerializedAttribute> 属性，则忽略它们。  
  
-   可以反序列化不存在的 `enum` 值。例如，可以将值 87 反序列化为上面的颜色枚举，尽管并未定义相应的颜色名称。  
  
-   标志 `enum` 并不特殊，其处理方式与任何其他 `enum` 相同。  
  
### 日期\/时间和 JSON  
 JSON 格式不直接支持日期和时间。但是，由于这些类型十分常用，因此 ASP.NET AJAX 对它们提供了特殊的支持。使用 ASP.NET AJAX 代理时，.NET 中的 <xref:System.DateTime> 类型与 JavaScript 中的 `DateTime` 类型完全对应。  
  
-   当不使用 ASP.NET 时，<xref:System.DateTime> 类型在 JSON 中将表示为一个具有特殊格式的字符串。本主题的“高级信息”一节中对这种特殊格式进行了描述。  
  
-   <xref:System.DateTimeOffset> 在 JSON 中以复杂类型表示：{"DateTime":dateTime,"OffsetMinutes":offsetMinutes}。`offsetMinutes` 成员是与相关事件所在位置关联的本地时间与格林威治标准时间 \(GMT\)（现在也称为协调世界时 \(UTC\)）之间的偏移量。`dateTime` 成员表示发生相关事件时的时间实例（同样，当使用 ASP.NET AJAX 时，它将变为 JavaScript 中的 `DateTime`；不使用 ASP.NET AJAX 时，它将变为字符串）。`dateTime` 成员始终用 GMT 格式进行序列化。因此，如果描述纽约时间凌晨 3:00，`dateTime` 的时间部分将是上午 8:00，而 `offsetMinutes` 是 300（从 GMT 中减去 300 分钟或 5 个小时）。  
  
    > [!NOTE]
    >  在将 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 对象序列化为 JSON 时，它们保留的信息精度仅为毫秒。在序列化期间，次于毫秒的值（微秒\/毫微秒）将丢失。  
  
### XML 类型和 JSON  
 XML 类型成为 JSON 字符串。  
  
-   例如，如果 XElement 类型的数据成员“q”包含 \<abc\/\>，则 JSON 是 {"q":"\<abc\/\>"}。  
  
-   有一些特殊的规则来指定如何包装 XML。有关更多信息，请参见本主题后面的“高级信息”一节。  
  
-   使用 ASP.NET AJAX 时，如果不希望使用 JavaScript 中的字符串，而是想改用 XML DOM，请在 <xref:System.ServiceModel.Web.WebGetAttribute> 上将 <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> 属性设置为 XML，或者在 <xref:System.ServiceModel.Web.WebInvokeAttribute> 上将 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> 属性设置为 XML。  
  
### 集合、字典和数组  
 在 JSON 中，所有的集合、字典和数组都表示为数组。  
  
-   在 JSON 表示中，忽略使用 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 的任何自定义。  
  
-   词典不能直接用于 JSON。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，Dictionary\<string,object\> 可能并不像用于其他 JSON 技术时所期望的那样获得相同的支持。例如，在字典中，如果“abc”映射到“xyz”，且“def”映射到 42，则 JSON 表示形式不是 {"abc":"xyz","def":42}，而是 \[{"Key":"abc","Value":"xyz"},{"Key":"def","Value":42}\]。  
  
-   如果想要直接使用 JSON（动态访问键和值，而不预定义严格的协定），您有下面几个选择：  
  
    -   请考虑使用[弱类型 JSON 序列化 \(AJAX\)](../../../../docs/framework/wcf/samples/weakly-typed-json-serialization-sample.md) 示例。  
  
    -   请考虑使用 <xref:System.Runtime.Serialization.ISerializable> 接口和反序列化构造函数。这两个机制允许分别访问序列化和反序列化时的 JSON 键\/值对，但不能用于部分受信任的方案。  
  
    -   请考虑使用 [JSON 和 XML 之间的映射](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md)代替序列化程序。  
  
    -   在序列化的上下文中，“多态性”是指在需要基类型时序列化派生类型的能力。在以多态形式使用集合时（例如，在将集合分配给 <xref:System.Object> 时），有一些 JSON 特定的特殊规则。有关此问题的更多详细讨论，请参见本主题后面的“高级信息”一节。  
  
## 其他详细信息  
  
### 数据成员的顺序  
 使用 JSON 时数据成员的顺序并不重要。具体而言，即使设置了 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>，也仍然可以按任意顺序反序列化 JSON 数据。  
  
### JSON 类型  
 JSON 类型在反序列化时并不一定要与上面的表匹配。例如，`Int` 通常映射到 JSON 数字，但只要 JSON 字符串中包含有效的数字，就可以成功地从该字符串反序列化到此类型。即，如果存在名为“q”的 `Int` 数据成员，则 {"q":42} 和 {"q":"42"} 都是有效的。  
  
### 多态性  
 多态序列化具备在需要基类型时序列化派生类型的能力。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对 JSON 序列化的这种支持方式与对 XML 序列化的支持方式类似。例如，可以在需要 `MyBaseType` 时序列化 `MyDerivedType`，或者在需要 `Object` 时序列化 `Int`。  
  
 需要基类型时，反序列化派生类型可能会丢失类型信息，除非反序列化复杂类型。例如，如果在需要 <xref:System.Object> 时序列化 <xref:System.Uri>，将导致一个 JSON 字符串。如果随后将此字符串反序列化回 <xref:System.Object>，将返回一个 .NET <xref:System.String>。反序列化程序并不知道该字符串最初属于 <xref:System.Uri> 类型。通常情况下，在需要 <xref:System.Object> 时，所有的 JSON 字符串都将反序列化为 .NET 字符串，并且用于序列化 .NET 集合、字典和数组的所有 JSON 数组都将反序列化为 <xref:System.Object> 类型的 .NET <xref:System.Array>，而不考虑实际的原始类型。JSON 布尔值映射到 .NET <xref:System.Boolean>。但是，在需要 <xref:System.Object> 时，JSON 数字将反序列化为 .NET <xref:System.Int32>、<xref:System.Decimal> 或 <xref:System.Double>，将根据具体情况自动选择最适合的类型。  
  
 反序列化为接口类型时，<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 会将声明的类型作为对象进行反序列化。  
  
 在处理自己的基类型和派生类型时，通常需要使用 <xref:System.Runtime.Serialization.KnownTypeAttribute>、<xref:System.ServiceModel.ServiceKnownTypeAttribute> 或与之等效的机制。例如，如果返回值应为 `Animal` 的操作实际返回了 `Cat`（从 `Animal` 中派生）的实例，则应向 `Animal` 类型应用 <xref:System.Runtime.Serialization.KnownTypeAttribute> 或者向该操作应用 <xref:System.ServiceModel.ServiceKnownTypeAttribute>，并在这些属性中指定 `Cat` 类型。有关更多信息，请参见[数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。  
  
 有关多态序列化工作方式的详细信息，以及使用多态序列化时必须遵从的部分限制的讨论，请参见本主题后面的“高级信息”一节。  
  
### 版本管理  
 JSON 中完全支持数据协定版本管理功能，其中包括 <xref:System.Runtime.Serialization.IExtensibleDataObject> 接口。不仅如此，在多数情况下还可以将一种格式（例如 XML）的类型反序列化，然后再将其序列化为另一种格式（例如 JSON），同时仍然保留 <xref:System.Runtime.Serialization.IExtensibleDataObject> 中的数据。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][向前兼容的数据协定](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).请记住，JSON 不进行排序，因此所有顺序信息都将丢失。而且，JSON 不支持多个键\/值对使用同一键名。最后，对 <xref:System.Runtime.Serialization.IExtensibleDataObject> 执行的所有操作在本质上都是多态的，即它们的派生类型均被分配给所有类型的基类型 <xref:System.Object>。  
  
## URL 中的 JSON  
 在结合使用 ASP.NET AJAX 终结点与 HTTP GET 谓词（使用 <xref:System.ServiceModel.Web.WebGetAttribute> 属性）时，传入的参数将出现在请求 URL 而不是消息正文中。请求 URL 中甚至还支持 JSON。因此，如果某项操作采用一个名为“number”的 `Int` 以及一个名为“p”的 `Person` 复杂类型，则 URL 可能类似于下面的 URL。  
  
```  
http://example.com/myservice.svc/MyOperation?number=7&p={"name":"John","age":42}  
```  
  
 如果使用 ASP.NET AJAX 脚本管理器控件和代理调用服务，则此 URL 将由代理自动生成，而不会显示出来。JSON 不能用在非 ASP.NET AJAX 终结点上的 URL 中。  
  
## 高级信息  
  
### ISerializable 支持  
  
#### 受支持和不受支持的 ISerializable 类型  
 通常情况下，序列化\/反序列化 JSON 时完全支持实现 <xref:System.Runtime.Serialization.ISerializable> 接口的类型。但是，其中有些类型（包括一些 .NET Framework 类型）采用特殊的实现方式，以致以下 JSON 特定的序列化方面会导致它们不能正确地反序列化：  
  
-   使用 <xref:System.Runtime.Serialization.ISerializable> 时，各个数据成员的类型始终无法提前预知。这将导致与将类型反序列化为对象时类似的多态情况。正如前文所述，这在 JSON 中可能会导致类型信息丢失。例如，如果某类型在其 <xref:System.Runtime.Serialization.ISerializable> 实现中序列化一个 `enum`，则当其尝试直接反序列化回 `enum`（未执行正确的强制转换）时将失败。这是因为，`enum` 使用 JSON 中的数字进行序列化，而 JSON 数字却反序列化为内置的 .NET 数值类型（Int32、Decimal 或 Double）。因此，数字用于 `enum` 值的事实将丢失。  
  
-   在反序列化构造函数中依赖特定的反序列化顺序的 <xref:System.Runtime.Serialization.ISerializable> 类型可能也无法反序列化某些 JSON 数据，因为大多数 JSON 序列化程序并不能保证遵循任何特定的顺序。  
  
#### 工厂类型  
 虽然 JSON 中通常支持 <xref:System.Runtime.Serialization.IObjectReference> 接口，但它不支持需要“工厂类型”功能（从 <xref:System.Runtime.Serialization.IObjectReference.GetRealObject%28System.Runtime.Serialization.StreamingContext%29> 中返回与实现接口的类型不同的类型实例）的任何类型。  
  
### DateTime 连网格式  
 <xref:System.DateTime> 值显示为“\/Date\(700000\+0500\)\/”形式的 JSON 字符串，其中第一个数字（在提供的示例中为 700000）是 GMT 时区中自 1970 年 1 月 1 日午夜以来按正常时间（非夏令时）经过的毫秒数。该数字可以是负数，以表示之前的时间。示例中包括“\+0500”的部分可选，它指示该时间属于 <xref:System.DateTimeKind> 类型，即它在反序列化时应转换为本地时区。如果没有该部分，则会将时间反序列化为 <xref:System.DateTimeKind>。实际数字（本示例中为“0500”）及其符号（\+ 或 \-）将被忽略。  
  
 序列化 <xref:System.DateTime> 时，写入的 <xref:System.DateTimeKind> 和 <xref:System.DateTimeKind> 时间将带有偏移量，而写入的 <xref:System.DateTimeKind> 则不带偏移量。  
  
 ASP.NET AJAX 客户端 JavaScript 代码会自动将此类字符串转换为 JavaScript `DateTime` 实例。如果有其他字符串采用了类似的形式，则即使它们不属于 .NET 中的 <xref:System.DateTime> 类型，也会对它们执行转换。  
  
 只有“\/”字符为转义字符（即 JSON 的形式类似于“\\\/Date\(700000\+0500\)\\\/”）时，才会进行转换，因此 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 JSON 编码器（由 <xref:System.ServiceModel.WebHttpBinding> 启用）始终会对“\/”字符进行转义。  
  
### JSON 字符串中的 XML  
  
#### XmlElement  
 <xref:System.Xml.XmlElement> 按原样执行序列化，而不进行包装。例如，如果 <xref:System.Xml.XmlElement> 类型的数据成员“x”包含 \<abc\/\>，则表示为以下形式。  
  
```  
{"x":"<abc/>"}  
```  
  
#### XmlNode 数组  
 在 <xref:System.Xml.XmlNode> 类型的标准数据协定命名空间内，该类型的 <xref:System.Array> 对象被包装在一个称为 ArrayOfXmlNode 的元素中。如果“x”是一个数组，并包含命名空间“ns”中的属性节点“N”，且该属性节点又包含“value”和一个空元素节点“M”，则可以按以下方式表示该数组。  
  
```  
{"x":"<ArrayOfXmlNode xmlns=\"http://schemas.datacontract.org/2004/07/System.Xml\" a:N=\"value\" xmlns:a=\"ns\"><M/></ArrayOfXmlNode>"}  
```  
  
 XmlNode 数组的开头（在其他元素之前）不支持空命名空间中的属性。  
  
#### 包括 XElement 和 DataSet 的 IXmlSerializable 类型  
 <xref:System.Runtime.Serialization.ISerializable> 类型可分为“内容类型”、“数据集类型”和“元素类型”。有关这些类型的定义，请参见 [数据协定中的 XML 和 ADO.NET 类型](../../../../docs/framework/wcf/feature-details/xml-and-ado-net-types-in-data-contracts.md)。  
  
 “内容”和“数据集”类型类似，它们都会被序列化为上一节中所讨论的 <xref:System.Xml.XmlNode> 的 <xref:System.Array> 对象。它们的包装元素的名称和命名空间与数据协定的名称和相应类型的命名空间相对应。  
  
 “元素”类型（例如 <xref:System.Xml.Linq.XElement>）按原样序列化，这与本主题前面讨论的 <xref:System.Xml.XmlElement> 类似。  
  
### 多态性  
  
#### 保留类型信息  
 正如前文所述，JSON 中支持多态性，但有一些限制。JavaScript 是一种弱类型语言，类型标识通常并不会产生问题。但是，当使用 JSON 在强类型系统 \(.NET\) 与弱类型系统 \(JavaScript\) 之间进行通信时，保留类型标识将十分有用。例如，数据协定名称为“Square”和“Circle”的类型派生自数据协定名称为“Shape”的类型。如果将“Circle”从 .NET 发送至 JavaScript，随后又将其返回给某个需要“Shape”的 .NET 方法，则 .NET 端就需要知道该对象最初为“Circle”，否则所有特定于派生类型的信息（例如，“Circle”的“radius”数据成员）都可能丢失。  
  
 若要保留类型标识，可以在将复杂类型序列化为 JSON 时添加“类型提示”。这样，反序列化程序在识别该提示后，便可以执行相应的操作。“类型提示”是一个键名为“\_\_type”（两个下划线，后跟单词“type”）的 JSON 键\/值对。该值是一个 JSON 字符串，其形式为“数据协定名称:数据协定命名空间”（第一个冒号前的所有内容都是名称）。在前面的示例中，“Circle”可以按以下方式进行序列化。  
  
```  
{"__type":"Circle:http://example.com/myNamespace","x":50,"y":70,"radius":10}  
```  
  
 类型提示与 `xsi:type` 属性非常相似，此属性由 XML 架构实例标准定义，供序列化\/反序列化 XML 时使用。  
  
 禁止将数据成员命名为“\_\_type”，因为它可能与类型提示发生冲突。  
  
#### 减小类型提示的大小  
 为了减小 JSON 消息的大小，默认的数据协定命名空间前缀 \(http:\/\/schemas.datacontract.org\/2004\/07\/\) 已替换为“\#”字符。（为了使这一替换具备可逆性，此操作采用了一项转义规则：如果命名空间以“\#”或“\\”字符开头，将为它们追加另一个“\\”字符。）这样，如果“Circle”是 .NET 命名空间“MyApp.Shapes”中的一个类型，则其默认的数据协定命名空间将是 http:\/\/schemas.datacontract.org\/2004\/07\/MyApp。下面是 Shapes 及其 JSON 表示形式。  
  
```  
{"__type":"Circle:#MyApp.Shapes","x":50,"y":70,"radius":10}  
```  
  
 执行反序列化时，既能识别截断的名称 \(\#MyApp.Shapes\)，也能识别完整的名称 \(http:\/\/schemas.datacontract.org\/2004\/07\/MyApp.Shapes\)。  
  
#### JSON 对象中的类型提示位置  
 请注意，类型提示必须出现在 JSON 表示形式的开头。这是 JSON 处理中唯一一种重视键\/值对顺序的情况。例如，下面不是指定类型提示的有效方式。  
  
```  
{"x":50,"y":70,"radius":10,"__type":"Circle:#MyApp.Shapes"}  
```  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 ASP.NET AJAX 客户端页使用的 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 始终都会最先发出类型提示。  
  
#### 类型提示仅适用于复杂类型  
 对于非复杂类型，无法发出类型提示。例如，如果操作的返回类型为 <xref:System.Object>，但却返回了 Circle，则 JSON 表示形式可能像前面显示的那样保留了类型信息。但是，如果返回了 URI，则 JSON 表示形式将是一个字符串，而该字符串原来用于表示 URI 的事实将丢失。这不仅适用于基元类型，也适用于集合和数组。  
  
#### 发出类型提示的时机  
 类型提示可能会显著增大消息的大小（缓解此问题的一种方式是尽量使用较短的数据协定命名空间）。因此，在确定是否发出类型提示时，应循序下列规则：  
  
-   使用 ASP.NET AJAX 时，始终都应尽可能多地发出类型提示，即使不存在基分配\/派生分配（例如，将 Circle 分配给 Circle）也不例外。（这是完全实现从弱类型的 JSON 环境调入强类型的 .NET 环境，又不造成大量信息丢失所必需的。）  
  
-   如果在未与 ASP.NET 集成的情况下使用 AJAX 服务，则只有当存在基分配\/派生分配时才应发出类型提示，即在将 Circle 分配给 Shape 或 <xref:System.Object> 而不是分配给 Circle 时发出。这不仅满足了正确实现 JavaScript 客户端的需要，而且在最大程度上减少了发出的信息，从而提高了性能。但是，如果客户端的设计有误，则无法防止类型信息丢失。如果要避免处理此客户端问题，请同时避免服务器上的基分配\/派生分配。  
  
-   使用 <xref:System.Runtime.Serialization.DataContractSerializer> 类型时，`alwaysEmitTypeInformation` 构造函数参数允许您在前面两种模式之间进行选择，其默认值为“`false`”（仅在需要时才发出类型提示）。  
  
#### 重复的数据成员名称  
 派生类型信息和基类型信息共同存在于同一个 JSON 对象中，且可以按任意顺序出现。例如，`Shape` 可以表示为以下形式。  
  
```  
{"__type":"Shape:#MyApp.Shapes","x":50,"y":70}  
```  
  
 而 Circle 则可以表示为以下形式。  
  
```  
{"__type":"Circle:#MyApp.Shapes","x":50, "radius":10,"y":70}  
```  
  
 如果基类型 `Shape` 也包含一个名为“`radius`”的数据成员，则会在序列化和反序列化时导致冲突，前者是由于 JSON 对象不能具有重复的键名所致，后者是因为无法确定“radius”指的是 `Shape.radius` 还是 `Circle.radius` 所致。因此，虽然一般不建议在数据协定类中使用“属性隐藏”概念（基类和派生类中的数据成员同名），但 JSON 中实际上禁止这种情况。  
  
#### 多态性和 IXmlSerializable 类型  
 根据常规数据协定规则，只要满足已知类型要求，就可以用多态形式将 <xref:System.Xml.Serialization.IXmlSerializable> 类型正常分配给彼此。但是，如果用序列化 <xref:System.Xml.Serialization.IXmlSerializable> 类型代替序列化 <xref:System.Object>，则会像 JSON 字符串那样导致类型信息丢失。  
  
#### 多态性和某些接口类型  
 在需要非 <xref:System.Xml.Serialization.IXmlSerializable> 的非集合类型（<xref:System.Object> 除外）时，禁止序列化集合类型或实现 <xref:System.Xml.Serialization.IXmlSerializable> 的类型。例如，假设存在一个名为 `IMyInterface` 的自定义接口和一个 `MyType` 类型，这两者均实现 `int` 类型的 <xref:System.Collections.Generic.IEnumerable%601> 以及 `IMyInterface`。如果操作的返回类型为 `IMyInterface`，则禁止其返回 `MyType`。这是因为，`MyType` 必须序列化为 JSON 数组并需要类型提示，但如前所述，类型提示只能包括在复杂类型中，而不能包括在数组中。  
  
#### 已知类型和配置  
 <xref:System.Runtime.Serialization.DataContractSerializer> 使用的所有已知类型机制同样受 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 支持。这两个序列化程序都会在 [\<system.runtime.serialization\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md) 中读取同一配置元素 [\<dataContractSerializer\>](../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md)，以发现通过配置文件添加的已知类型。  
  
#### 分配给对象的集合  
 序列化分配给对象的集合时，会将它们视为实现 <xref:System.Collections.Generic.IEnumerable%601> 的集合：一个 JSON 数组，其中属于复杂类型的每一项都具有类型提示。例如，分配给 <xref:System.Object> 的 `Shape` 类型的 <xref:System.Collections.Generic.List%601> 将类似于以下形式。  
  
```  
[{"__type":"Shape:#MyApp.Shapes","x":50,"y":70},  
{"__type":"Shape:#MyApp.Shapes","x":58,"y":73},  
{"__type":"Shape:#MyApp.Shapes","x":41,"y":32}]  
```  
  
 当反序列化回 <xref:System.Object> 时：  
  
-   `Shape` 必须处于“已知类型”列表中。将 `Shape` 类型的 <xref:System.Collections.Generic.List%601> 添加到已知类型中没有任何影响。请注意，对于本示例，无需在序列化时将 `Shape` 添加到已知类型中，此操作是自动完成的。  
  
-   该集合将被反序列化为属于 <xref:System.Object> 类型且包含 `Shape` 实例的 <xref:System.Array>。  
  
#### 分配给基集合的派生集合  
 将派生集合分配给基集合时，通常会将该集合作为基类型的集合进行序列化。但是，如果派生集合的项类型不能分配给基集合的项类型，则会引发异常。  
  
#### 类型提示和字典  
 将字典分配给 <xref:System.Object> 时，字典中的每个键和值项都将被视为已分配给 <xref:System.Object> 并会获得类型提示。  
  
 序列化字典类型时，包含“Key”和“Value”成员的 JSON 对象不会受 `alwaysEmitTypeInformation` 设置的影响，并只有在前面的集合规则需要时才会包含类型提示。  
  
### 有效的 JSON 键名  
 序列化程序 XML 编码的键名不是有效的 XML 名称。例如，名为“123”的数据成员将具有诸如“\_x0031\_\_x0032\_\_x0033\_”之类的编码名称，这是因为“123”不是有效的 XML 元素名称（以数字开头）。在 XML 名称中，如果某些国际字符集无效，也会出现类似的情况。有关 XML 对 JSON 处理的这种影响的说明，请参见 [JSON 和 XML 之间的映射](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md)。  
  
## 请参阅  
 [对 JSON 和其他数据传输格式的支持](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)