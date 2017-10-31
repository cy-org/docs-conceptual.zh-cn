---
title: "如何：显示日期和时间值中的毫秒 | Microsoft Docs"
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
  - "日期 [.NET Framework], 毫秒"
  - "DateTime.ToString 方法"
  - "显示日期和时间数据"
  - "毫秒 [.NET Framework]"
  - "时间 [.NET Framework], 毫秒"
ms.assetid: ae1a0610-90b9-4877-8eb6-4e30bc5e00cf
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：显示日期和时间值中的毫秒
默认的日期和时间格式化方法（例如 <xref:System.DateTime.ToString?displayProperty=fullName>）包括时间值的小时、分钟和秒钟，但不包括它的毫秒部分。  本主题演示如何在格式化的日期和时间字符串中包含日期和时间的毫秒部分。  
  
### 显示 DateTime 值的毫秒部分  
  
1.  如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime.Parse%28System.String%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=fullName> 方法将其转换为 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 值。  
  
2.  若要从时间中提取毫秒部分的字符串表示形式，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.ToString%2A> 方法，并以 `format` 参数形式传递 `fff` 或 `FFF` 自定义格式模式（单独传递或与其他自定义格式说明符一起传递）。  
  
## 示例  
 该示例将在控制台中显示 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值的毫秒部分（单独显示及包括在更长的日期和时间字符串中）。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#1)]
 [!code-vb[Formatting.HowTo.Millisecond#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#1)]  
  
 `fff` 格式模式包括毫秒值中的任何尾随零。  `FFF` 格式模式则禁止显示它们。  下面的示例中阐释了这种差异。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#2)]
 [!code-vb[Formatting.HowTo.Millisecond#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#2)]  
  
 在定义包括日期和时间的毫秒部分的完整自定义格式说明符时，会产生以下问题：定义的硬编码格式可能无法与应用程序当前区域性中的时间元素排列方式相对应。  更好的替代方法是检索由当前区域性的 <xref:System.Globalization.DateTimeFormatInfo> 对象定义的某个日期和时间显示模式，并将其修改为包括毫秒部分。  该示例也阐释了这种方法。  它从 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=fullName> 属性中检索当前区域性的完整日期和时间模式，然后在其秒钟模式后面插入自定义模式 `.ffff`。  请注意，该示例使用正则表达式在单个方法调用中执行此操作。  
  
 另外，还可以使用自定义格式说明符显示秒钟的小数（而非毫秒）部分。  例如，`f` 或 `F` 自定义格式说明符显示十分之一秒，`ff` 或 `FF` 自定义格式说明符显示百分之一秒，`ffff` 或 `FFFF` 自定义格式说明符显示万分之一秒。  在返回的字符串中，毫秒的小数部分将被截断，而不是进行舍入。  下面的示例中使用了这些格式说明符。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#3)]
 [!code-vb[Formatting.HowTo.Millisecond#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#3)]  
  
> [!NOTE]
>  可以为秒钟显示非常微小的部分，例如万分之一秒或十万分之一秒。  但是，这些值可能并没有意义。  日期和时间值的精度取决于系统时钟的分辨率。  在 Windows NT 3.5 和更高版本以及 [!INCLUDE[windowsver](../../../includes/windowsver-md.md)] 操作系统中，时钟的分辨率大约为 10\-15 毫秒。  
  
## 编译代码  
 在命令行处使用 csc.exe 或 vb.exe 编译代码。  若要在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中编译代码，请将代码置于控制台应用程序项目模板中。  
  
## 请参阅  
 <xref:System.Globalization.DateTimeFormatInfo>   
 [自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)