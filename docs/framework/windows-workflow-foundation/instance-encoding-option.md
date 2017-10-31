---
title: "实例编码选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 实例编码选项
SQL 工作流实例存储的**实例编码选项**属性，允许您指定 SQL 持久性提供程序是否应在将工作流实例状态信息保存到持久性数据库中之前使用 GZip 算法压缩该信息。此属性的允许值为 GZip 和 None。默认值为 None。以下列表对这两个选项进行了说明。  
  
1.  **GZip**。在将状态信息持久保存到持久性数据库中之前，持久性提供程序使用 GZip 算法对该状态信息进行编码。  
  
2.  **None**。在将状态信息保存到持久性数据库中之前，持久性提供程序不会对该状态信息进行编码。  
  
 使用 GZip 对工作流实例状态信息进行编码可减少 SQL 数据库中的内存消耗，并且还可减少网络消耗（如果数据库位于网络上的另一台计算机上，而不是位于运行工作流服务宿主的计算机上）。一般原则是将**实例编码选项**属性设置为 **None**（如果工作流实例状态很小）。