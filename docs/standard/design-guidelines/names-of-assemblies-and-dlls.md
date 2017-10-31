---
title: "程序集和 Dll 的名称 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Dll 的名称 [.NET Framework]"
  - "程序集的名称 [.NET Framework]"
  - "程序集 [.NET Framework] 名称"
  - "Dll 名称"
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 程序集和 Dll 的名称
程序集是部署和托管的代码程序标识的单元。 尽管程序集可以跨一个或多个文件，通常程序集一对一映射的 DLL。 因此，本部分介绍唯一 DLL 命名约定，然后可以映射到程序集的命名约定。  
  
 **✓ 执行** 选择建议的功能，例如 System.Data 大块的 Dll 程序集的名称。  
  
 程序集和 DLL 的名称不一定非得对应于命名空间名称，但可以合理地命名程序集时，请遵循命名空间名称。 好的经验法则是名称的公共前缀的程序集中包含的程序集所基于的 DLL。 例如，具有两个命名空间中的程序集 `MyCompany.MyTechnology.FirstFeature` 和 `MyCompany.MyTechnology.SecondFeature`, ，可以调用 `MyCompany.MyTechnology.dll`。  
  
 **✓ 请考虑** 按照下面的模式命名 Dll:  
  
 `<Company>.<Component>.dll`  
  
 其中 `<Component>` 包含一个或多个圆点分隔的子句。 例如：  
  
 `Litware.Controls.dll`。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)