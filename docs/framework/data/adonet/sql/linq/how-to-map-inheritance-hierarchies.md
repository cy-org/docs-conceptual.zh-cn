---
title: "如何：映射继承层次结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b27c779b-9355-4dc7-b95f-7dfd504b6e48
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 如何：映射继承层次结构
若要在 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 中执行继承映射，您必须按以下步骤中的说明在继承层次结构的根类中指定属性 \(Attribute\) 和属性 \(Attribute\) 的属性 \(Property\)。  使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的开发人员可以使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来映射继承层次结构。  请参阅[如何：使用 O\/R 设计器配置继承](../Topic/How%20to:%20Configure%20inheritance%20by%20using%20the%20O-R%20Designer.md)。  
  
> [!NOTE]
>  子类中不需要具有特殊属性 \(Attribute\) 或属性 \(Property\)。  请特别注意，子类不具有 <xref:System.Data.Linq.Mapping.TableAttribute> 属性。  
  
### 映射继承层次结构  
  
1.  向根类添加 <xref:System.Data.Linq.Mapping.TableAttribute> 属性。  
  
2.  为层次结构中的每个类添加 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute> 属性，同样是添加到根类中。  
  
3.  为每个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute> 属性 \(Attribute\)，定义一个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A> 属性 \(Property\)。  
  
     此属性 \(Property\) 保存一个值，该值显示在数据库表的 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDiscriminator%2A> 列中，用来指示该行数据所属的类或子类。  
  
4.  为每个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute> 属性 \(Attribute\)，也添加一个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Type%2A> 属性 \(Property\)。  
  
     此属性 \(Property\) 保存一个值，此值指定键值所表示的类或子类。  
  
5.  仅在其中一个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute> 属性 \(Attribute\) 上，添加一个 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.IsDefault%2A> 属性 \(Property\)。  
  
     此属性 \(Property\) 用来在数据库表中的鉴别器值在继承映射中不与任何  值匹配时指定回退<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A>映射。  
  
6.  为 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDiscriminator%2A> 属性 \(Attribute\) 添加一个 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性 \(Property\)。  
  
     此属性 \(Property\) 表示这是保存 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A> 值的列。  
  
## 示例  
  
> [!NOTE]
>  如果您使用的是 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]，则可以使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 来配置继承。  请参阅[如何：使用 O\/R 设计器配置继承](../Topic/How%20to:%20Configure%20inheritance%20by%20using%20the%20O-R%20Designer.md)  
  
 在下面的代码示例中，`Vehicle` 定义为根类，并且已执行前面的步骤来说明 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 的层次结构。  
  
 [!code-csharp[DLinqCustomize#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#4)]
 [!code-vb[DLinqCustomize#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#4)]  
  
## 请参阅  
 [继承支持](../../../../../../docs/framework/data/adonet/sql/linq/inheritance-support.md)   
 [如何：使用代码编辑器自定义实体类](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)