---
title: "IEnumRAWINPUTDEVIC:Next | Microsoft Docs"
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
  - "Next 方法"
ms.assetid: 3698b44d-510e-4d18-b32b-85f17188ee26
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# IEnumRAWINPUTDEVIC:Next
枚举位于枚举器列表中的下一个 `celt` [RAWINPUTDEVICE](http://msdn.microsoft.com/library/default.asp?url=/%20library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputstructures/rawinputdevice.asp) 结构，并在 `rgelt` 将它们与 `pceltFetched` 中枚举元素的实际数量一起返回。  
  
## 语法  
  
```  
HRESULT Next(  
      [in] ULONG celt,  
      [out, size_is(celt), length_is(*pceltFetched)] RAWINPUTDEVICE *rgelt,  
      [out] ULONG *pceltFetched);  
```  
  
#### 参数  
 `celt`  
  
 \[in\] `rgelt` 中返回的 [RAWINPUTDEVICE](http://msdn.microsoft.com/library/default.asp?url=/%20library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputstructures/rawinputdevice.asp) 结构的数量。  
  
 `rgelt`  
  
 \[out\] celt 大小（或更大）的数组，用于接收枚举的 RAWINPUTDEVICE 结构。  
  
 `pceltFetched`  
  
 \[out\] 指向 `rgelt` 中实际提供的元素数量的指针。  如果 `rgelt` 为一，则调用方可传入 `NULL`。  
  
## 属性值\/返回值  
 HRESULT：如果提供的元素数量为 `celt`，则值为 S\_OK；否则为 S\_FALSE。