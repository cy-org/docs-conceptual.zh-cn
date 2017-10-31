---
title: "空间函数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 90cb177d-88a0-45be-97e8-3b306283c6e0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 空间函数
空间类型没有文本格式。  但是，您可以使用规范实体实体框架函数，这些函数可使用已知文本格式的字符串来调用。  例如，以下函数调用会生成一个几何点：  
  
```  
GeometryFromText('POINT (43 -73)')  
```  
  
 [SpatialEdmFunctions 方法](http://msdn.microsoft.com/library/hh749531.aspx)页列出了 Entity Framework 的所有空间规范方法。  请单击相关方法以查看应向函数传递哪些参数。