---
title: "Thread Local Storage: Thread-Relative Static Fields and Data Slots | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "threading [.NET Framework], local storage"
  - "threading [.NET Framework], thread-relative static fields"
  - "local thread storage"
  - "TLS"
ms.assetid: c633a4dc-a790-4ed1-96b5-f72bd968b284
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Thread Local Storage: Thread-Relative Static Fields and Data Slots
可以使用托管线程本地存储区 \(TLS\) 存储某一线程和应用程序域所独有的数据。  .NET Framework 提供了两种使用托管 TLS 的方式：线程相关的静态字段和数据槽。  
  
-   如果您可以在编译时预料到您的确切需要，请使用线程相关的静态字段（在 Visual Basic 中为线程相关的 `Shared` 字段）。  线程相关的静态字段可提供最佳性能。  它们还具备编译时类型检查的优点。  
  
-   如果只能在运行时发现您的实际需要，请使用数据槽。  数据槽比线程相关的静态字段慢一些且更加难于使用，并且数据存储为 <xref:System.Object> 类型，因此必须将其强制转换为正确的类型才能使用。  
  
 在非托管 C\+\+ 中，可以使用 `TlsAlloc` 来动态分配槽，使用 `__declspec(thread)` 来声明变量应在线程相关的存储区中进行分配。  线程相关的静态字段和数据槽提供了此行为的托管版本。  
  
 在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]中，可以使用 <xref:System.Threading.ThreadLocal%601?displayProperty=fullName> 类创建线程本地对象，在第一次使用该对象时它将惰式初始化。  有关详细信息，请参阅[延迟初始化](../../../docs/framework/performance/lazy-initialization.md)。  
  
## 托管 TLS 中数据的唯一性  
 无论是使用线程相关的静态字段还是使用数据槽，托管 TLS 中的数据都是线程和应用程序域组合所独有的。  
  
-   在应用程序域内部，一个线程不能修改另一个线程中的数据，即使这两个线程使用同一个字段或槽时也不能。  
  
-   当线程从多个应用程序域中访问同一个字段或槽时，会在每个应用程序域中维护一个单独的值。  
  
 例如，如果某个线程设置线程相关的静态字段的值，接着它进入另一个应用程序域，然后检索该字段的值，则在第二个应用程序域中检索的值将不同于第一个应用程序域中的值。  在第二个应用程序域中为该字段设置一个新值不会影响第一个应用程序域中该字段的值。  
  
 同样，当某个线程获取两个不同应用程序域中的同一命名数据槽时，第一个应用程序域中的数据将始终与第二个应用程序域中的数据无关。  
  
## 线程相关的静态字段  
 如果您知道一些数据总是某个线程和应用程序域组合所独有的，请向该静态字段应用 <xref:System.ThreadStaticAttribute> 特性。  与使用任何其他静态字段一样使用该字段。  该字段中的数据是每个使用它的线程所独有的。  
  
 线程相关的静态字段的性能优于数据槽，并且具有编译时类型检查的优点。  
  
 请注意，任何类构造函数代码都将在访问该字段的第一个上下文中的第一个线程上运行。  在同一应用程序域内的所有其他线程或上下文中，如果字段是引用类型，它们将被初始化为 `null`（在 Visual Basic 中为 `Nothing`）；如果字段是值类型，它们将被初始化为它们的默认值。  因此，您不应依赖于类构造函数来初始化线程相关的静态字段。  而应避免初始化线程相关的静态字段并假定它们初始化为 `null` \(`Nothing`\) 或它们的默认值。  
  
## 数据槽  
 .NET Framework 提供了线程和应用程序域组合所独有的动态数据槽。  数据槽包括两种类型：命名槽和未命名槽。  两者都是通过使用 <xref:System.LocalDataStoreSlot> 结构来实现的。  
  
-   若要创建命名数据槽，请使用 <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=fullName> 或 <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=fullName> 方法。  若要获取对某个现有命名槽的引用，请将其名称传递给 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 方法。  
  
-   若要创建未命名数据槽，请使用 <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=fullName> 方法。  
  
 对于命名槽和未命名槽，请使用 <xref:System.Threading.Thread.SetData%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.GetData%2A?displayProperty=fullName> 方法设置和检索槽中的信息。  这些都是静态方法，它们始终作用于当前正在执行它们的线程的数据。  
  
 命名槽可能很方便，因为您可以在需要它时通过将其名称传递给 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 方法来检索该槽，而不是维护对未命名槽的引用。  但是，如果另一个组件使用相同的名称来命名其线程相关的存储区，并且有一个线程同时执行来自您的组件和该组件的代码，则这两个组件可能会破坏彼此的数据。（本方案假定这两个组件在同一应用程序域内运行，并且它们并不用于共享相同数据。）  
  
## 请参阅  
 <xref:System.ContextStaticAttribute>   
 <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=fullName>   
 <xref:System.ThreadStaticAttribute>   
 <xref:System.Runtime.Remoting.Messaging.CallContext>   
 [Threading](../../../docs/standard/threading/index.md)