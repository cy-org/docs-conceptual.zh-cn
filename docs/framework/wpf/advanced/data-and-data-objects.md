---
title: "数据和数据对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据传输 [WPF], 拖放"
  - "DataFormats 类 [WPF]"
  - "DataObject 类 [WPF]"
ms.assetid: 5967d557-1867-420f-a524-ae3af78402da
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 数据和数据对象
在拖放操作中传输的数据存储在数据对象中。  概念上而言，数据对象包含一对或多对下列组件：  
  
-   一个包含实际数据的 <xref:System.Object>。  
  
-   一个对应的数据格式标识符。  
  
 数据本身可以包含作为基本 <xref:System.Object> 表示的任何内容。  对应的数据格式是提供有关数据格式的提示的字符串或 <xref:System.Type>。  数据对象支持承载多个“数据\/数据格式”对；这样，一个数据对象即可提供多种格式的数据。  
  
<a name="Data_and_Data_Objects"></a>   
## 数据对象  
 所有数据对象都必须实现 <xref:System.Windows.IDataObject> 接口，该接口提供以下标准方法集，以启用和便于数据传输。  
  
|方法|摘要|  
|--------|--------|  
|<xref:System.Windows.IDataObject.GetData%2A>|检索指定数据格式的数据对象。|  
|<xref:System.Windows.IDataObject.GetDataPresent%2A>|查看是否具有指定格式的数据，或者数据是否可以转换为指定格式。|  
|<xref:System.Windows.IDataObject.GetFormats%2A>|返回一个格式列表，此数据对象中的数据以这些格式存储，或可以转换为这些格式。|  
|<xref:System.Windows.IDataObject.SetData%2A>|在此数据对象中存储指定的数据。|  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供 <xref:System.Windows.DataObject> 类中的 <xref:System.Windows.IDataObject> 的基本实现。  对于许多常见数据传输方案，常用 <xref:System.Windows.DataObject> 类已足够满足要求。  
  
 有几种预定义格式，如位图、CSV、文件、HTML、RTF、字符串、文本和音频。  有关随 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的预定义数据格式的信息，请参见 <xref:System.Windows.DataFormats> 类参考主题。  
  
 数据对象通常包括在提取数据时将以一种格式存储的数据自动转换为另一种格式的功能，此功能称为自动转换。  当查询数据对象中的可用数据格式时，可以通过调用 <xref:System.Windows.DataObject.GetFormats%28System.Boolean%29> 或 <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> 方法并将 `autoConvert` 参数指定为 `false` 来从本机数据格式中筛选可自动转换的数据格式。  当使用 <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%2CSystem.Boolean%29> 方法将数据添加到数据对象中时，可以通过将 `autoConvert` 参数设置为 `false` 来禁止数据自动转换。  
  
<a name="Working_with_Data_Objects"></a>   
## 处理数据对象  
 本节介绍创建和处理数据对象的常见技术。  
  
### 创建新数据对象  
 <xref:System.Windows.DataObject> 类提供一些重载构造函数，以便于使用单一“数据\/数据格式”对来填充新的 <xref:System.Windows.DataObject> 实例。  
  
 下面的代码示例新建一个数据对象，并利用重载构造函数之一 <xref:System.Windows.DataObject.%23ctor%2A>\(<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%29>\)，使用一个字符串和指定的数据格式初始化该数据对象。  在这种情况下，数据格式由一个字符串指定；<xref:System.Windows.DataFormats> 类提供一组预定义的类型字符串。  默认情况下允许存储数据的自动转换。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
 有关创建数据对象的更多代码示例，请参见[创建数据对象](../../../../docs/framework/wpf/advanced/how-to-create-a-data-object.md)。  
  
### 存储多种格式的数据  
 一个数据对象能够存储多种格式的数据。  与只提供一种数据格式相比较，在一个数据对象中策略性地使用多种数据格式可以使该数据对象供更多种放置目标使用。  请注意，一般而言，拖动源一定不知道潜在放置目标可使用的数据格式。  
  
 下面的示例演示如何使用 <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> 方法将数据以多种格式添加到数据对象中。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
### 查询数据对象以获取可用格式  
 由于一个数据对象可包含任意数量的数据格式，数据对象包含用于检索可用数据格式列表的功能。  
  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetFormats%2A> 重载获取一个字符串数组，该数组用于表示某数据对象中可用的所有数据格式（包括本机和自动转换的格式）。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
 有关查询数据对象以获取可用数据格式的更多代码示例，请参见[列出数据对象中的数据格式](../../../../docs/framework/wpf/advanced/how-to-list-the-data-formats-in-a-data-object.md)。  有关查询数据对象以了解是否存在特定数据格式的示例，请参见[确定数据格式是否存在于数据对象中](../../../../docs/framework/wpf/advanced/how-to-determine-if-a-data-format-is-present-in-a-data-object.md)。  
  
### 从数据对象检索数据  
 从数据对象检索特定格式的数据只需调用 <xref:System.Windows.DataObject.GetData%2A> 方法之一并指定所需的数据格式。  可以使用 <xref:System.Windows.DataObject.GetDataPresent%2A> 方法之一来检查是否存在特定数据格式。  <xref:System.Windows.DataObject.GetData%2A> 返回 <xref:System.Object> 中的数据；根据数据格式，此对象可以强制转换为类型特定的容器。  
  
 下面的代码示例使用 <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> 重载首先检查是否存在指定的数据格式（本机或自动转换）。  如果存在指定的格式，则该示例使用 <xref:System.Windows.DataObject.GetData%28System.String%29> 方法检索数据。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
 有关从数据对象检索数据的更多代码示例，请参见[以特定数据格式检索数据](../../../../docs/framework/wpf/advanced/how-to-retrieve-data-in-a-particular-data-format.md)。  
  
### 从数据对象中移除数据  
 不能直接从数据对象中移除数据。  若要从数据对象中有效移除数据，请按照以下步骤操作：  
  
1.  新建一个只包含要保留的数据的数据对象。  
  
2.  将所需的数据从旧数据对象“复制”到新数据对象。  若要复制数据，请使用 <xref:System.Windows.DataObject.GetData%2A> 方法之一检索包含原始数据的 <xref:System.Object>，然后使用 <xref:System.Windows.DataObject.SetData%2A> 方法之一将数据添加到新数据对象中。  
  
3.  使用新数据对象替换旧数据对象。  
  
> [!NOTE]
>  即使数据和数据格式与以前的调用完全一样，<xref:System.Windows.DataObject.SetData%2A> 方法也只将数据添加到数据对象中，而并不替换数据。  对同一数据和数据格式调用 <xref:System.Windows.DataObject.SetData%2A> 两次会导致“数据\/数据格式”在数据对象中出现两次。