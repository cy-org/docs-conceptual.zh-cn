---
title: "IEnumRAWINPUTDEVIC:Skip | Microsoft Docs"
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
  - "Skip 方法"
ms.assetid: c967b0f8-1c6a-459c-8c16-d4f08918ab65
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# IEnumRAWINPUTDEVIC:Skip
指示枚举数跳过枚举中的后续 `celt` 元素，以便下次调用 [IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md) 时将不返回这些元素。  
  
## 语法  
  
```  
HRESULT Skip( [in] ULONG celt);  
```  
  
#### 参数  
 `celt`  
  
 \[in\] 要跳过的元素数。  
  
## 属性值\/返回值  
 HRESULT：如果提供的元素数目为 `celt`，则为 S\_OK；否则为 S\_FALSE。