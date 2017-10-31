---
title: "不区分区域性的字符串操作 | Microsoft Docs"
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
  - "区分大小写的比较"
  - "区域性, 不区分区域性的字符串操作"
  - "不区分区域性的字符串操作"
  - "区分区域性的字符串操作"
  - "全球化 [.NET Framework], 不区分区域性的字符串操作"
  - "本地化 [.NET Framework], 不区分区域性的字符串操作"
  - "字符串 [.NET Framework], 不区分区域性的字符串操作"
  - "世界通用的应用程序, 不区分区域性的字符串操作"
ms.assetid: e6e2bb94-a95d-44e2-b68c-cfdd1db77784
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 不区分区域性的字符串操作
如果要创建旨在按区域性向用户显示结果的应用程序，则区分区域性的字符串操作无疑是一个有利条件。  默认情况下，区分区域性的方法从当前线程的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> 属性中获得要使用的区域性。  
  
 请注意，并非在所有场合都需要执行区分区域性的字符串操作。  当结果不应依赖于区域性时，使用区分区域性的操作可能会导致应用程序代码在遇到自定义事例映射和排序规则的区域性时失败。  例如，参阅 [针对使用字符串的最佳做法](../../../docs/standard/base-types/best-practices-strings.md)一文中的“使用当前区域性的字符串比较”一节。  
  
 字符串操作是否应该区分区域性取决于应用程序使用结果的方式。  向用户显示结果的字符串操作通常应是区分区域性的。  例如，如果应用程序在列表框中显示本地化字符串的排序列表，则应用程序应执行区分区域性的排序操作。  
  
 内部使用的字符串操作的结果通常应该是不区分区域性的。  一般而言，如果应用程序使用的是不向用户显示的文件名、持久性格式或符号信息，则字符串操作的结果不应因区域性而异。  例如，如果应用程序比较字符串以确定它是否是可识别的 XML 标记，则这种比较不应是区分区域性的。  此外，如果安全决策基于字符串比较或大小写更改操作的结果，则操作应该不区分区域性，以确保结果不受 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> 值的影响。  
  
 无论要开发的应用程序是否包含用来处理本地化和全球化问题的代码，你都应该对默认情况下检索区分区域性的结果的 .NET Framework 方法有所了解。  本主题旨在阐释应用程序如何正确地使用这些方法来获得不区分区域性的结果。  
  
## 请参阅  
 [全球化和本地化](../../../docs/standard/globalization-localization/index.md)