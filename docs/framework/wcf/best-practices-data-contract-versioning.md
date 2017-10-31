---
title: "最佳做法：数据协定版本管理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "最佳做法 [WCF], 数据协定版本管理"
  - "数据协定"
  - "服务协定"
  - "Windows Communication Foundation, 数据协定"
ms.assetid: bf0ab338-4d36-4e12-8002-8ebfdeb346cb
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# 最佳做法：数据协定版本管理
本主题列出了创建容易随时间而改变的数据协定的最佳做法。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]数据协定，请参见[使用数据协定](../../../docs/framework/wcf/feature-details/using-data-contracts.md)中的主题。  
  
## 有关架构验证的说明  
 讨论数据协定版本管理时，注意除非元素被默认标记为可选之外，由 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 导出的数据协定架构不具有任何版本管理支持，这很重要。  
  
 这意味着即使是最常用的版本管理方案（例如添加新的数据成员）也不能通过与给定架构无缝相关的方法实现。  较新版本的数据协定（例如新添数据成员）不会使用旧架构进行验证。  
  
 但是，有许多方案不需要严格遵从架构。  许多 Web 服务平台（包括 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 和使用 ASP.NET 创建的 XML Web services）默认不执行架构验证，因此允许使用架构未描述过的其他元素。  使用这样的平台工作时，许多版本管理方案更容易实现。  
  
 因此，存在两套数据协定版本管理准则：一套用于严格架构有效性十分重要的方案；另一套用于严格架构有效性不太重要的方案。  
  
## 需要进行架构验证时的版本管理  
 如果所有方向（从新到旧和从旧到新）都需要严格架构有效性，则应将数据协定视为不可变的。  如果需要进行版本管理，则应使用不同名称或命名空间创建新的数据协定，并且应相应地对使用该数据类型的服务协定进行版本管理。  
  
 例如，假设一个名为 `PoProcessing` 的采购订单处理服务协定具有 `PostPurchaseOrder` 操作，并采用一个符合 `PurchaseOrder` 数据协定的参数。  如果必须更改 `PurchaseOrder` 协定，则需要创建一个新数据协定，即包含更改的 `PurchaseOrder2`。  然后，必须在服务协定级别处理版本管理。  例如，可创建一个 `PostPurchaseOrder2` 操作，该操作采用 `PurchaseOrder2` 参数；也可创建一个 `PoProcessing2` 服务协定，其中 `PostPurchaseOrder` 操作采用 `PurchaseOrder2` 数据协定。  
  
 请注意，数据协定中由其他数据协定引用的更改也会扩展到服务模型层。  例如，在前面的方案中，不需要更改 `PurchaseOrder` 数据协定。  但是，该协定包含 `Customer` 数据协定的一个数据成员，而后者又包含了不需要更改的 `Address` 数据协定的一个数据成员。  在此情况下，需要创建一个包含所需更改的 `Address2` 数据协定、一个包含 `Address2` 数据成员的 `Customer2` 数据协定和一个包含 `Customer2` 数据成员的 `PurchaseOrder2` 数据协定。  与前面的情况一样，也必须对服务协定进行版本管理。  
  
 在这些示例中，虽然名称发生了改变（追加了一个“2”），但建议不要更改名称，而是通过对新命名空间追加版本号或日期来更改命名空间。  例如，`http://schemas.contoso.com/2005/05/21/PurchaseOrder` 数据协定应更改为 `http://schemas.contoso.com/2005/10/14/PurchaseOrder` 数据协定。  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)]最佳做法：[服务版本管理](../../../docs/framework/wcf/service-versioning.md)。  
  
 有时，您必须保证应用程序发送的消息严格遵从架构，但不能依赖要严格遵从架构的传入消息。  在这种情况下，存在传入消息中包含某些外来数据的危险。  这些外来值由 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 进行存储并返回，因此会导致发送对架构无效的消息。  若要避免此问题，应关闭往返功能。  有两种方法可以实现此目的。  
  
-   请勿在任何类型上实现 <xref:System.Runtime.Serialization.IExtensibleDataObject> 接口。  
  
-   对 <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> 属性 \(Property\) 设置为 `true` 的服务协定应用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性 \(Attribute\)。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]往返过程的更多信息，请参见[向前兼容的数据协定](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)。  
  
## 不要求进行架构验证时的版本管理  
 一般不要求严格遵从架构。  许多平台允许使用不是架构描述的其他元素。  只要允许这样，就可以使用[数据协定版本管理](../../../docs/framework/wcf/feature-details/data-contract-versioning.md)和[向前兼容的数据协定](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)中描述的功能全集。  下面是一些建议的准则。  
  
 必须严格遵守其中某些准则，以便能在接受类型的旧版本的地方发送类型的新版本，或在接受类型的新版本的地方发送类型的旧版本。  而其他准则，我们则不需要严格遵守，但此处也列出了，因为它们可能会受将来架构版本管理的影响。  
  
1.  不要尝试通过类型继承对数据协定进行版本管理。  若要创建较新的版本，可更改现有类型上的数据协定，也可创建新的不相关类型。  
  
2.  可以结合使用继承和数据协定，前提是不将继承用作版本管理机制，并且遵守某些规则。  如果某个类型派生于某个基类型，则在将来的版本中不要使它派生于其他基类型（除非版本具有相同的数据协定）。  其中存在一个例外，您可以将类型插入到数据协定类型及其基类型之间的层次结构中，但前提是该类型包含的数据成员名称与该层次结构中其他类型的任何可能版本中的其他成员名称不同。  通常情况下，在同一继承层次结构的不同级别使用具有相同名称的数据成员可导致严重的版本管理问题，因此应该避免。  
  
3.  从数据协定的第一个版本开始，始终实现 <xref:System.Runtime.Serialization.IExtensibleDataObject> 可启用往返。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [向前兼容的数据协定](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  如果已经释放了某个类型的一个或多个版本，而没有实现此接口，则在该类型的下一个版本中实现它。  
  
4.  在较新的版本中，不要更改数据协定名称或命名空间。  如果更改该类型在数据协定下的名称或命名空间，请确保使用适当的机制（例如 <xref:System.Runtime.Serialization.DataContractAttribute> 的 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 属性）保留数据协定名称和命名空间。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]命名的更多信息，请参见[数据协定名称](../../../docs/framework/wcf/feature-details/data-contract-names.md)。  
  
5.  在以后的版本中，不要更改任何数据成员的名称。  如果更改数据成员下的字段、属性或事件的名称，请使用 <xref:System.Runtime.Serialization.DataMemberAttribute> 的 `Name` 属性以保留现有数据成员名称。  
  
6.  在以后的版本中，不要更改数据成员下的任何字段、属性或事件的类型，否则该数据成员的结果数据协定会发生变化。  请记住，接口类型等效于 <xref:System.Object>，用于确定需要的数据协定。  
  
7.  在以后的版本中，不要通过调整 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(Attribute\) 的 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 属性 \(Property\) 来更改现有数据成员的顺序。  
  
8.  在以后的版本中，可以添加新的数据成员。  它们应始终遵循以下规则：  
  
    1.  <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 属性应始终保留其默认值 `false`。  
  
    2.  如果对于成员，默认值为 `null` 或零是不可接受的，则应使用 <xref:System.Runtime.Serialization.OnDeserializingAttribute> 提供一个回调方法，以便在传入流中不存在该成员时提供一个合理的默认值。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]回调，请参见[版本容错序列化回调](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)。  
  
    3.  应使用 `DataMemberAttribute` 上的 `Order` 属性，以确保所有新添加的数据成员显示在现有数据成员之后。  达到此目的的建议方法为：不应设置数据协定的第一个版本中的任何数据成员的 `Order` 属性。  应将添加到数据协定版本 2 中的所有数据成员的 `Order` 属性设置为 2。  将添加到数据协定版本 3 中的所有数据成员的 `Order` 设置为 3，依次类推。  允许将多个数据成员集设置为同一个 `Order` 编号。  
  
9. 在以后的版本中，不要移除数据成员，即使在以前的版本中 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 属性保留为其默认属性 `false`。  
  
10. 在各个版本中，不要更改任何现有数据成员上的 `IsRequired` 属性。  
  
11. 对于必需的数据成员（其中 `IsRequired` 为 `true`），不要更改各版本中的 `EmitDefaultValue` 属性。  
  
12. 不要尝试创建分支版本管理层次结构。  即，从任意版本到任何其他版本的至少一个方向上，应始终有一个路径仅使用这些准则允许的更改。  
  
     例如，如果 Person 数据协定的版本 1 仅包含 Name 数据成员，则不应创建仅添加 Age 成员的协定版本 2a，以及仅添加 Address 成员的版本 2b。  从 2a 到 2b 需要移除 Age 和添加 Address，从 2b 到 2a 需要移除 Address 和添加 Age。  这些准则不允许移除成员。  
  
13. 通常不应在您的应用程序的新版本中创建现有数据协定类型的新子类型。  同样，不应创建新的数据协定以代替声明为对象或接口类型的数据成员。  仅当您知道可以向旧应用程序的所有实例的已知类型列表中添加新类型时，才允许创建这些新类。  例如，在应用程序的版本 1 中，可能已为 LibraryItem 数据协定类型添加了 Book 和 Newspaper 数据协定子类型。  LibraryItem 随后应具有一个包含 Book 和 Newspaper 的已知类型列表。  假设您现在向版本 2 中添加一个 Magazine 类型，该类型是 LibraryItem 的一个子类型。  如果您从版本 2 向版本 1 发送一个 Magazine 实例，则在已知类型列表中找不到 Magazine 数据协定，因而会引发异常。  
  
14. 不应在版本间添加或移除枚举成员。  也不应重命名枚举成员，除非使用 `EnumMemberAttribute` 属性 \(Attribute\) 上的 Name 属性 \(Property\) 使这些成员在数据协定模型中的名称保持不变。  
  
15. 在数据协定模型中集合是可互换的，如[数据协定中的集合类型](../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)中所述。  这提供了极大的灵活性。  但是，请确保不会以不可互换的方式不慎更改版本间的集合类型。  例如，不要将非自定义集合（即没有 `CollectionDataContractAttribute` 属性的集合）更改为自定义集合，也不要将自定义集合更改为非自定义集合。  同样，不要更改不同版本间 `CollectionDataContractAttribute` 上的属性。  唯一允许更改的是添加一个 Name 或 Namespace 属性，前提是基础集合类型的名称或命名空间已更改，且需要使其数据协定名称和命名空间与以前版本中的相同。  
  
 在某些特殊的情况中，可以安全地忽略此处列出的某些准则。  确保在背离这些准则之前，已充分理解所涉及的序列化、反序列化和架构机制。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 <xref:System.ServiceModel.ServiceBehaviorAttribute>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>   
 <xref:System.Runtime.Serialization.ExtensionDataObject>   
 <xref:System.Runtime.Serialization.OnDeserializingAttribute>   
 [使用数据协定](../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [数据协定版本管理](../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [数据协定名称](../../../docs/framework/wcf/feature-details/data-contract-names.md)   
 [向前兼容的数据协定](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)   
 [版本容错序列化回调](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)