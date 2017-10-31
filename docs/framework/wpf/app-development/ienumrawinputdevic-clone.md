---
title: "IEnumRAWINPUTDEVIC:Clone | Microsoft Docs"
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
  - "Clone 方法"
ms.assetid: 2a6a1900-aa55-45fa-9382-241d569a2dc4
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# IEnumRAWINPUTDEVIC:Clone
创建与当前枚举数的状态相同的另一个原始输入设备枚举数，以循环访问同一列表。  
  
## 语法  
  
```  
HRESULT Clone( [out] IEnumRAWINPUTDEVICE **ppenum);  
```  
  
#### 参数  
 `ppenum`  
  
 \[out\] 接收 [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md) 接口指针的输出变量的地址。  如果此方法失败，则未定义此输出变量的值。  
  
## 属性值\/返回值  
 HRESULT：此方法支持标准返回值 E\_INVALIDARG、E\_OUTOFMEMORY 和 E\_UNEXPECTED。  
  
## 备注  
 使用此方法，可以记录枚举序列中之后要返回到的点。  调用方必须独立于第一个枚举数来发布这一新的枚举数。