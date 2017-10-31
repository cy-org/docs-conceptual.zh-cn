---
title: "如何：枚举计算机上存在的时区 | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "枚举时区 [.NET Framework]"
  - "时区 [.NET Framework], 枚举"
ms.assetid: bb7a42ab-6bd9-4c5c-b734-5546d51f8669
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：枚举计算机上存在的时区
若要成功使用指定的时区，系统需要能获得有关该时区的信息。  Windows XP 和 Windows Vista 操作系统将此信息存储在注册表中。  不过，虽然世界上存在的时区总数很大，但注册表只包含有关它们中的一部分的信息。  此外，注册表本身是一个动态结构，其内容可能会被有意或无意更改。  因此，应用程序不能始终假定系统上已定义并存在某个特定的时区。  对于使用时区信息的很多应用程序，第一步都是要确定本地系统上是否存在所需的时区，或者是为用户提供一个时区列表以供其选择。  这都要求应用程序枚举本地系统上定义的时区。  
  
> [!NOTE]
>  如果应用程序依赖的特定时区可能没有在本地系统上定义，该应用程序可通过序列化和反序列化有关该时区的信息来确保存在该时区。  随后，可以将该时区添加到某个 List 控件中，以供应用程序用户选择。  有关详细信息，请参见[如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。  
  
### 枚举本地系统上存在的时区  
  
1.  调用 <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=fullName> 方法。  该方法返回 <xref:System.TimeZoneInfo> 对象的泛型集合 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>。  集合中的条目按其 <xref:System.TimeZoneInfo.DisplayName%2A> 属性排序。  例如：  
  
     [!code-csharp[System.TimeZone2.Concepts#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#1)]
     [!code-vb[System.TimeZone2.Concepts#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#1)]  
  
2.  使用 `foreach` 循环（在 C\# 中）或 `For Each`…`Next` 循环（在 Visual Basic 中）枚举集合中的各个 <xref:System.TimeZoneInfo> 对象，然后对每个对象执行任何必需的处理。  例如，下面的代码枚举步骤 1 中返回的 <xref:System.TimeZoneInfo> 对象的 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 集合，并在控制台上列出每个时区的显示名称。  
  
     [!code-csharp[System.TimeZone2.Concepts#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#12)]
     [!code-vb[System.TimeZone2.Concepts#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#12)]  
  
### 为用户提供本地系统上存在的时区的列表  
  
1.  调用 <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=fullName> 方法。  该方法返回 <xref:System.TimeZoneInfo> 对象的泛型集合 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>。  
  
2.  将步骤 1 中返回的集合分配给 Windows 窗体或 ASP.NET List 控件的 `DataSource` 属性。  
  
3.  检索用户选定的 <xref:System.TimeZoneInfo> 对象。  
  
 该示例演示一个 Windows 应用程序。  
  
## 示例  
 该示例首先启动一个在列表框中显示系统上定义的时区的 Windows 应用程序。  随后，该示例显示一个对话框，其中包含用户所选时区对象的 <xref:System.TimeZoneInfo.DisplayName%2A> 属性值。  
  
 [!code-csharp[System.TimeZone2.Concepts#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#2)]
 [!code-vb[System.TimeZone2.Concepts#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#2)]  
  
 大多数 List 控件（例如 <xref:System.Windows.Forms.ListBox?displayProperty=fullName> 或 <xref:System.Web.UI.WebControls.BulletedList?displayProperty=fullName> 控件）都允许将某个对象变量的集合分配给它们的 `DataSource` 属性，条件是该集合实现 <xref:System.Collections.IEnumerable> 接口（泛型类 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 可执行此操作）。为了显示集合中的单个对象，该控件会调用该对象的 `ToString` 方法以提取用于表示该对象的字符串。  对于 <xref:System.TimeZoneInfo> 对象，`ToString` 方法会返回 <xref:System.TimeZoneInfo> 对象的显示名称（其 <xref:System.TimeZoneInfo.DisplayName%2A> 属性值）。  
  
> [!NOTE]
>  由于 List 控件会调用对象的 `ToString` 方法，因此可以将 <xref:System.TimeZoneInfo> 对象的集合分配给该控件，以便让该控件为每个对象显示一个有意义的名称并检索用户选定的 <xref:System.TimeZoneInfo> 对象。  这样便不再需要执行如下过程：提取集合中每个对象的字符串，将该字符串分配给某个集合，然后又将该集合分配给控件的 `DataSource` 属性，检索用户选定的字符串，然后使用此字符串提取它所描述的对象。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   导入下列命名空间：  
  
     <xref:System>（在 C\# 代码中）  
  
     <xref:System.Collections.ObjectModel>  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)   
 [如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)