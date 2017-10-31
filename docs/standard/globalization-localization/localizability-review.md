---
title: "本地化评审 | Microsoft Docs"
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
  - "世界通用的应用程序，可本地化性"
  - "应用程序开发 [.NET Framework]，本地化"
  - "本地化能力 [.NET Framework]"
  - "国际应用程序 [.NET Framework]，可本地化性"
  - "全球化 [.NET Framework]，可本地化性"
  - "区域性，可本地化性"
  - "本地化 [.NET Framework]，可本地化性"
  - "全球应用程序，可本地化性"
  - "本地化资源"
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 本地化评审
本地化分析检查为全球通用应用程序的开发的一个中间步骤。  它验证一个全球化应用程序准备好进行本地化和识别所有代码或需要特别处理用户界面的任何特性。  这一步也执行本地化分析检查有助于确保本地化过程不会将任何功能上的缺陷引入应用程序。  当可本地化评审建议的所有问题解决时，应用程序就可以开始进行本地化。  如果评审可本地化详尽说明，不应开始进行本地化时才不能不修改任何源代码。  
  
 本地化分析检查包括以下三检查：  
  
-   [是实现全球化建议？](#global)  
  
-   [正确处理区分区域性的功能？](#culture)  
  
-   [使用国际数据的测试应用程序？](#test)  
  
<a name="global"></a>   
## 实现全球化建议  
 如果您的设计和开发应用程序时考虑了本地化，并且，如果您按照[全球化](../../../docs/standard/globalization-localization/globalization.md)文章介绍的建议，评审可本地化主要就是保证质量的关口。  否则，在此阶段您应检查并负责实现[globalization](../../../docs/standard/globalization-localization/globalization.md)的建议，并修复妨碍本地化的错误源代码。  
  
<a name="culture"></a>   
## 处理区分区域性的功能  
 .NET Framework 提供了区域性大不相同的区域的编程支持。  大多数情况下，您必须编写自定义代码来处理类似于的功能区域：  
  
-   地址  
  
-   电话号码。  
  
-   纸张大小。  
  
-   用于体重、长度、区域、音量和温度的度量单位。  虽然 .NET Framework 提供转换的内置支持在度量单位之间切换，您可以使用 <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=fullName>属性确定特定国家\/地区公制，是否使用，如下面的示例所阐释。  
  
     [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
     [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]  
  
<a name="test"></a>   
## 测试应用程序  
 在本地化应用程序之前，应当使用在操作系统的国际版本的国际数据测试它。  虽然大部分用户界面此时不本地化，可以检测问题例如：  
  
-   不保持操作系统版本之间正确执行的序列化数据。  
  
-   不反映当前区域性的约定的数字数据。  例如，数字可以显示与错误的组分隔符、小数分隔符或货币符号。  
  
-   不反映当前区域性的约定的日期和时间数据。  例如，表示月份和日的数字可能会以错误的顺序出现，日期分隔符可能不正确，或者该时区信息可能不正确。  
  
-   找不到的资源，因为尚未确定应用程序的默认区域性。  
  
-   以特定区域性中的异常顺序显示的字符串。  
  
-   返回意外的结果字符串比较或相等比较。  
  
 如果您遵循全球化建议，当开发应用程序，正确处理区域性敏感的功能以及确定和解决测试期间出现的本地化问题时，您可以执行下一步。[本地化](../../../docs/standard/globalization-localization/localization.md)。  
  
## 请参阅  
 [全球化和本地化](../../../docs/standard/globalization-localization/index.md)   
 [本地化](../../../docs/standard/globalization-localization/localization.md)   
 [全球化](../../../docs/standard/globalization-localization/globalization.md)   
 [桌面应用程序中的资源](../../../docs/framework/resources/index.md)