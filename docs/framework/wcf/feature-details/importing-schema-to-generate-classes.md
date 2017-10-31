---
title: "导入架构以生成类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, 架构导入和导出"
  - "XsdDataContractImporter 类"
ms.assetid: b9170583-8c34-43bd-97bb-6c0c8dddeee0
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 导入架构以生成类
若要从与可用架构中生成类[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]，使用<xref:System.Runtime.Serialization.XsdDataContractImporter>类。 本主题描述该过程和变体。  
  
## <a name="the-import-process"></a>导入过程  
 架构导入过程开头<xref:System.Xml.Schema.XmlSchemaSet> ，并生成<xref:System.CodeDom.CodeCompileUnit>。  
  
 `XmlSchemaSet` 是 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的架构对象模型 (SOM) 的一部分，SOM 表示 XML 架构定义语言 (XSD) 架构文档集。 若要创建`XmlSchemaSet`对象从 XSD 文档集，反序列化到每个文档<xref:System.Xml.Schema.XmlSchema>对象 (使用<xref:System.Xml.Serialization.XmlSerializer>) 并将这些对象添加到一个新`XmlSchemaSet`。  
  
 `CodeCompileUnit` 是 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的代码文档对象模型 (CodeDOM) 的一部分，CodeDOM 以抽象方式表示 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 代码。 若要生成实际代码从`CodeCompileUnit`，使用的子类<xref:System.CodeDom.Compiler.CodeDomProvider>类，如<xref:Microsoft.CSharp.CSharpCodeProvider>或<xref:Microsoft.VisualBasic.VBCodeProvider>类。  
  
#### <a name="to-import-a-schema"></a>导入架构  
  
1.  创建的实例<xref:System.Runtime.Serialization.XsdDataContractImporter>。  
  
2.  可选。 在构造函数中传递一个 `CodeCompileUnit`。 将在架构导入期间生成的类型添加到此 `CodeCompileUnit` 实例中，而不是以空白 `CodeCompileUnit` 开始。  
  
3.  可选。 通过调用某个<xref:System.Runtime.Serialization.XsdDataContractImporter.CanImport%2A>方法。 该方法确定给定架构是否为有效的数据协定架构，以及是否可以被导入。 `CanImport` 方法具有与下一步中的 `Import` 相同的重载。  
  
4.  调用某个重载`Import`方法，例如， <xref:System.Runtime.Serialization.XsdDataContractImporter.Import%28System.Xml.Schema.XmlSchemaSet%29>方法。  
  
     最简单的重载采用 `XmlSchemaSet` 并导入在架构集中找到的所有类型，包括匿名类型。 其他重载允许您指定要导入的 XSD 类型的列表 (形式<xref:System.Xml.XmlQualifiedName>或集合的`XmlQualifiedName`对象)。 在此情况下，仅导入指定的类型。 重载采用<xref:System.Xml.Schema.XmlSchemaElement>用于导入之外的特定元素`XmlSchemaSet`，以及与其关联的类型 （它是匿名还是不）。 该重载返回一个 `XmlQualifiedName`，表示为此元素生成的类型的数据协定名称。  
  
     多次调用 `Import` 方法会向同一个 `CodeCompileUnit` 添加多个项。 如果某个类型已经存在于 `CodeCompileUnit` 中，则不会再在其中生成该类型。 在同一个 `Import` 上多次调用 `XsdDataContractImporter`，而不是使用多个 `XsdDataContractImporter` 对象。 建议使用这种方法以避免生成重复的类型。  
  
    > [!NOTE]
    >  如果导入期间出现了故障，则 `CodeCompileUnit` 将处于不可预知的状态。 使用从失败的导入中产生的 `CodeCompileUnit` 可能会使您暴露出安全漏洞。  
  
5.  访问`CodeCompileUnit`通过<xref:System.Runtime.Serialization.XsdDataContractImporter.CodeCompileUnit%2A>属性。  
  
### <a name="import-options-customizing-the-generated-types"></a>导入选项：自定义生成的类型  
 您可以设置<xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A>属性<xref:System.Runtime.Serialization.XsdDataContractImporter>实例<xref:System.Runtime.Serialization.ImportOptions>类来控制导入过程的各个方面。 许多选项会直接影响生成的类型。  
  
#### <a name="controlling-the-access-level-generateinternal-or-the-internal-switch"></a>控制访问级别（GenerateInternal 或 /internal 开关）  
 这对应于**/ 内部**开关[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  
  
 通常情况下，公共类型是从架构生成的，具有私有字段和匹配的公共数据成员属性。 若要生成内部类型，将设置<xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A>属性设置为`true`。  
  
 下面的示例演示转换为内部的架构类时<xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A>属性设置为`true.`  
  
 [!code-csharp[c_SchemaImportExport#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#2)]
 [!code-vb[c_SchemaImportExport#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#2)]  
  
#### <a name="controlling-namespaces-namespaces-or-the-namespace-switch"></a>控制命名空间（Namespaces 或 /namespace 开关）  
 这对应于**/namespace**开关`Svcutil.exe`工具。  
  
 通常情况下，从架构生成类型都将生成到[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]对应于特定每个 XSD 命名空间具有命名空间[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]按照中所述映射的命名空间[数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)。 您可以自定义此映射通过<xref:System.Runtime.Serialization.ImportOptions.Namespaces%2A>属性设置为<xref:System.Collections.Generic.Dictionary%602>。\</TKey, TValue> 如果在字典中找到了给定的 XSD 命名空间，则也可从字典中获得匹配的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 命名空间。  
  
 例如，考虑下面的架构。  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#10](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#10)]  -->  
  
 下面的示例使用 `Namespaces` 属性将“http://schemas.contoso.com/carSchema”命名空间映射为“Contoso.Cars”。  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
#### <a name="adding-the-serializableattribute-generateserializable-or-the-serializable-switch"></a>添加 SerializableAttribute（GenerateSerializable 或 /serializable 开关）  
 这对应于**/ 可序列化**开关`Svcutil.exe`工具。  
  
 有时，对于从架构生成的类型，能够通过一定[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]运行时序列化引擎 (例如， <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName>和<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>类)。 这在使用这些类型进行 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 远程处理时很有用。 若要实现此目的，必须应用<xref:System.SerializableAttribute>属性设为生成的类型，除了常规<xref:System.Runtime.Serialization.DataContractAttribute>属性。 如果 `GenerateSerializable` 导入选项设置为 `true`，则将自动生成该属性。  
  
 下面的示例演示在 `Vehicle` 导入选项设置为 `GenerateSerializable` 时生成的 `true` 类。  
  
 [!code-csharp[c_SchemaImportExport#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#4)]
 [!code-vb[c_SchemaImportExport#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#4)]  
  
#### <a name="adding-data-binding-support-enabledatabinding-or-the-enabledatabinding-switch"></a>添加数据绑定支持（EnableDataBinding 或 /enableDataBinding 开关）  
 这对应于**/enableDataBinding**切换于 Svcutil.exe 工具。  
  
 有时，可能需要将从架构生成的类型绑定到图形用户界面组件，这样这些类型实例的任何更新都将自动更新 UI。 `XsdDataContractImporter`可以生成实现的类型<xref:System.ComponentModel.INotifyPropertyChanged>接口使任何属性更改都触发事件的方式。 如果您正在生成支持此接口的客户端 UI 编程环境一起使用的类型 (如[!INCLUDE[avalon1](../../../../includes/avalon1-md.md)])，请设置<xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A>属性设置为`true`要启用此功能。  
  
 下面的示例演示`Vehicle`类生成具有<xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A>设置为`true`。  
  
 [!code-csharp[C_SchemaImportExport#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#5)]
 [!code-vb[C_SchemaImportExport#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#5)]  
  
### <a name="import-options-choosing-collection-types"></a>导入选项：选择集合类型  
 XML 中存在两种特殊的模式，用于表示项集合：项列表和项与项之间的关联。 下面是一个字符串列表示例。  
  
 <!-- TODO: review snippet reference [!code[C_SchemaImportExport#11](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#11)]  -->  
  
 下面是一个字符串与整数（`city name` 和 `population`）之间的关联示例。  
  
 <!-- TODO: review snippet reference [!code[C_SchemaImportExport#12](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#12)]  -->  
  
> [!NOTE]
>  也可将任何关联视为列表。 例如，可以将上面的关联视为一个复杂的 `city` 对象列表，这些对象碰巧有两个字段（一个字符串字段和一个整数字段）。 这两种模式在 XSD 架构中都有一种表示形式。 由于无法区分列表和关联，因此始终将这种模式作为列表处理，架构中出现特定于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的特殊批注除外。 该批注指示给定模式表示一个关联。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)。  
  
 通常情况下，将列表作为派生自泛型列表的集合数据协定导入，或作为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数组导入，具体取决于架构是否遵循集合的标准命名模式。 此进行了更详细地描述[数据协定中的集合类型](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)。 关联是正常情况下为导入<xref:System.Collections.Generic.Dictionary%602>或派生自字典对象的集合数据协定。\</TKey, TValue> 例如，考虑下面的架构。  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#13](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#13)]  -->  
  
 这将按照下面的方式导入（出于可读性目的，显示的是字段而非属性）。  
  
 [!code-csharp[c_SchemaImportExport#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#6)]
 [!code-vb[c_SchemaImportExport#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#6)]  
  
 可以自定义为此类架构模式生成的集合类型。 例如，您可能需要生成派生自的集合<xref:System.ComponentModel.BindingList%601>而不是<xref:System.Collections.Generic.List%601>在集合中的内容更改时，会自动更新以便将类型绑定到列表框中，并让它的类。 若要执行此操作，将设置<xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>属性<xref:System.Runtime.Serialization.ImportOptions>类传递给列表集合类型，以用于 （以后称为引用的类型）。 导入任何集合时，将扫描引用的集合类型的列表，并使用最佳匹配集合（如果能够找到）。 关联只能与实现泛型或非泛型类型进行匹配<xref:System.Collections.IDictionary>接口，而列表可与任何受支持的集合类型相匹配。  
  
 例如，如果<xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>属性设置为<xref:System.ComponentModel.BindingList%601>、 `people` ，如下所示生成在上例中的类型。  
  
 [!code-csharp[C_SchemaImportExport#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#7)]
 [!code-vb[C_SchemaImportExport#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#7)]  
  
 将封闭式泛型视为最佳匹配。 例如，如果类型`BindingList(Of Integer)`和<xref:System.Collections.ArrayList>传递到引用的类型的集合，任何在架构中找到整数列表作为导入`BindingList(Of Integer)`。 将任何其他列表（例如 `List(Of String)`）作为 `ArrayList` 导入。  
  
 如果将实现泛型 `IDictionary` 接口的一个类型添加到引用的类型集合，则其类型参数必须完全打开或完全封闭。  
  
 不允许重复。 例如，不能同时向引用的类型添加 `List(Of Integer)` 和 `Collection(Of Integer)`。 这会使在架构中找到整数列表时无法确定应该使用哪一个整数。 仅当架构中的某个类型暴露出重复问题时才能检测到重复项。 例如，如果导入的架构中不包含整数列表，则允许引用的类型集合中同时具有 `List(Of Integer)` 和 `Collection(Of Integer)`，两者都不会产生任何影响。  
  
 引用的集合类型机制不仅适用于基元集合，也适用于复杂类型集合（包括其他集合的集合）。  
  
 `ReferencedCollectionTypes`属性对应于**/collectionType**切换于 SvcUtil.exe 工具。 请注意，若要引用多个集合类型， **/collectionType**交换机必须多次指定。 如果类型不在 MsCorLib.dll 中，还必须使用引用其程序集**/引用**切换。  
  
#### <a name="import-options-referencing-existing-types"></a>导入选项：引用现有类型  
 有时，架构中的类型对应于现有 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型，因此不需要从头开始生成这些类型。 （本节仅适用于非集合类型。 有关集合类型，请参见上一节。）  
  
 例如，您可能有一个标准公司范围内的“Person”数据协定类型，通常在表示人员时需要使用它。 每当某个服务利用该类型且其架构显示在该服务元数据中时，在导入此架构时您可能需要重用现有的 `Person` 类型，而不需要为每个服务生成新的类型。  
  
 若要执行此操作，将传递一份[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]您想要重用到集合的类型<xref:System.Runtime.Serialization.ImportOptions.ReferencedTypes%2A>属性返回<xref:System.Runtime.Serialization.ImportOptions>类。 如果任何这些类型的数据协定名称和命名空间与架构类型的名称和命名空间相匹配，则执行结构比较。 如果比较结果确定这些类型同时具有匹配的名称和匹配的构造，则重用现有的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型，而不生成新的类型。 如果仅名称匹配而构造不匹配，则引发异常。 请注意，引用类型（例如，添加新的可选数据成员）时不允许进行版本管理。 构造必须完全匹配。  
  
 向引用的类型集合添加多个具有相同数据协定名称和命名空间的类型是合法的，前提是不导入具有该名称和命名空间的架构类型。 这样您就可以轻松地将程序集中的所有类型添加到集合中，而无需担心在架构中并未实际出现的类型重复项。  
  
 `ReferencedTypes`属性对应于**/引用**切入特定的 Svcutil.exe 工具操作模式。  
  
> [!NOTE]
>  当使用 Svcutil.exe 或 (在[!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)])**添加服务引用**自动引用 MsCorLib.dll 中的类型的所有工具。  
  
#### <a name="import-options-importing-non-datacontract-schema-as-ixmlserializable-types"></a>导入选项：将 Non-DataContract 架构作为 IXmlSerializable 类型导入  
 <xref:System.Runtime.Serialization.XsdDataContractImporter>支持架构的有限的子集。 如果出现不受支持的架构构造（例如，XML 属性），导入尝试会失败并引发异常。 但是，将设置<xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>属性设置为`true`可扩展受支持架构的范围。 当设置为`true`、 <xref:System.Runtime.Serialization.XsdDataContractImporter>生成实现的类型<xref:System.Xml.Serialization.IXmlSerializable>接口。 这样可直接访问这些类型的 XML 表示形式。  
  
##### <a name="design-considerations"></a>设计注意事项  
  
-   直接使用弱类型 XML 表示形式可能有些困难。 请考虑使用其他序列化引擎，如<xref:System.Xml.Serialization.XmlSerializer>，以使用不兼容的数据协定架构的强类型化的方式。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][使用 XmlSerializer 类](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)。  
  
-   某些架构构造不能由导入<xref:System.Runtime.Serialization.XsdDataContractImporter>即使<xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>属性设置为`true`。 同样，请考虑使用<xref:System.Xml.Serialization.XmlSerializer>这种情况下。  
  
-   支持的确切架构构造，当<xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>是`true`或`false`中所述[数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)。  
  
-   架构生成<xref:System.Xml.Serialization.IXmlSerializable>类型不保留保真时导入和导出。 也就是说，从生成的类型导出架构或作为类导入时不返回原始架构。  
  
 则可以将组合<xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>选项与<xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A>前面所述的选项。 类型，该生成为<xref:System.Xml.Serialization.IXmlSerializable>时使用的实现中，结构检查将跳过<xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A>功能。  
  
 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>选项对应于**/importXmlTypes**切换于 Svcutil.exe 工具。  
  
##### <a name="working-with-generated-ixmlserializable-types"></a>使用生成的 IXmlSerializable 类型  
 生成`IXmlSerializable`类型包含一个名为"nodesField"的私有字段返回的数组<xref:System.Xml.XmlNode>对象。 反序列化此类的实例时，可以使用 XML 文档对象模型直接通过该字段访问 XML 数据。 序列化此类的实例时，可以将该字段设置为所需的 XML 数据，然后它将被序列化。  
  
 这是通过 `IXmlSerializable` 实现完成的。 在生成`IXmlSerializable`类型， <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A>实现调用<xref:System.Runtime.Serialization.XmlSerializableServices.ReadNodes%2A>方法<xref:System.Runtime.Serialization.XmlSerializableServices>类。 该方法是将通过提供的 XML 转换一个 helper 方法<xref:System.Xml.XmlReader>指向数组<xref:System.Xml.XmlNode>对象。 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>实现执行相反的操作，并将转换的数组`XmlNode`对象传递给一系列<xref:System.Xml.XmlWriter>调用。 这通过<xref:System.Runtime.Serialization.XmlSerializableServices.WriteNodes%2A>方法。  
  
 可以在生成的 `IXmlSerializable` 类上运行架构导出过程。 如上所述，您将不会重新获得原始架构。 相反，您将获得“anyType”的标准 XSD 类型，这是任何 XSD 类型的通配符。  
  
 这可以通过应用<xref:System.Xml.Serialization.XmlSchemaProviderAttribute>属性设为生成`IXmlSerializable`类并指定一个方法调用<xref:System.Runtime.Serialization.XmlSerializableServices.AddDefaultSchema%2A>方法以生成"anyType"类型。  
  
> [!NOTE]
>  <xref:System.Runtime.Serialization.XmlSerializableServices>存在只是为了支持此特定功能的类型。 建议不将其用于任何其他目的。  
  
#### <a name="import-options-advanced-options"></a>导入选项：高级选项  
 下面介绍高级导入选项：  
  
-   <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A>属性。 指定<xref:System.CodeDom.Compiler.CodeDomProvider>要用于为生成的类生成代码。 导入机制尝试避免功能<xref:System.CodeDom.Compiler.CodeDomProvider>不支持。 例如，J# 语言不支持泛型。 如果此属性中指定 J# 代码提供程序，以导入程序的生成没有通用类型<xref:System.CodeDom.CodeCompileUnit>。 如果<xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A>未设置，则完整的集[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]功能使用不带任何限制。  
  
-   <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A>属性。 <xref:System.Runtime.Serialization.IDataContractSurrogate>实现可以使用此属性指定。 <xref:System.Runtime.Serialization.IDataContractSurrogate>自定义导入过程。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][数据协定代理项](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)。 默认情况下，不使用代理项。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 <xref:System.Runtime.Serialization.ImportOptions>   
 [数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)   
 [数据协定代理项](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)   
 [架构导入和导出](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)   
 [从类导出架构](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)   
 [数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)