---
title: "在 .NET Framework 中构建控制台应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework, building console applications
- application development [.NET Framework], console
- console applications
ms.assetid: c21fb997-9f0e-40a5-8741-f73bba376bd8
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: bba3cde0d4e1c15ea764322b8ab0ef1501e53739
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="building-console-applications-in-the-net-framework"></a>在 .NET Framework 中构建控制台应用程序
.NET Framework 中的应用程序可以使用 <xref:System.Console?displayProperty=fullName> 类在控制台中读取和写入字符。 读取自控制台的数据是从标准输入流读取的，而写入到控制台的数据将写入标准输出流，并且写入控制台的错误数据将写入标准错误输出流。 应用程序启动时，这些数据流会自动与控制台关联，并分别表示为 <xref:System.Console.In%2A>、<xref:System.Console.Out%2A> 和 <xref:System.Console.Error%2A> 属性。  
  
 <xref:System.Console.In%2A?displayProperty=fullName> 属性的值是 <xref:System.IO.TextReader?displayProperty=fullName> 对象，而 <xref:System.Console.Out%2A?displayProperty=fullName> 和 <xref:System.Console.Error%2A?displayProperty=fullName> 属性的值都是 <xref:System.IO.TextWriter?displayProperty=fullName> 对象。 你可以将这些属性与不表示控制台的流关联，以便可以将该流指向不同的输入位置或输出位置。 例如，你可以通过将 <xref:System.Console.Out%2A?displayProperty=fullName> 属性设置为 <xref:System.IO.StreamWriter?displayProperty=fullName> 将输出重定向到一个文件，这将通过 <xref:System.Console.SetOut%2A?displayProperty=fullName> 方法封装 <xref:System.IO.FileStream?displayProperty=fullName>。 <xref:System.Console.In%2A?displayProperty=fullName> 和 <xref:System.Console.Out%2A?displayProperty=fullName> 属性不需要引用相同流。  
  
> [!NOTE]
>  有关生成控制台应用程序（包括 C#、Visual Basic 和 C++ 中的示例）的详细信息，请参阅 <xref:System.Console> 类文档。  
  
 如果不存在控制台（比如在基于 Windows 的应用程序中），写入标准输出流的输出将不可见，因为没有可以将信息写入的控制台。 将信息写入不可访问的控制台不会引发异常。  
  
 此外，若要使控制台在使用 Visual Studio 开发的基于 Windows 的应用程序内进行读取和写入，请打开项目的“属性”对话框，单击“应用程序”选项卡，并将“应用程序类型”设置为“控制台应用程序”。  
  
 控制台应用程序缺少在默认情况下启动的消息泵。 因此，控制台调用 Microsoft Win32 计时器时可能会失败。  
  
 System.Console 类具有从控制台读取单独的字符或整行的方法。 其他方法转换数据和格式字符串，然后将设置了格式的字符串写入控制台。 有关设置字符串格式的详细信息，请参阅[格式设置类型](../../docs/standard/base-types/formatting-types.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Console?displayProperty=fullName>   
 [格式设置类型](../../docs/standard/base-types/formatting-types.md)

