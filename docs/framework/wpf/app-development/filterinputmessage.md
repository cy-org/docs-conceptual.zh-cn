---
title: "FilterInputMessage | Microsoft Docs"
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
  - "FilterInputMessage 方法"
  - "原始输入 [WPF]"
ms.assetid: 4d74c6cf-7d1d-49ff-96c1-231340ce54f5
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# FilterInputMessage
除非返回 E\_NOTIMP，否则每当收到一条消息时都会由 PresentationHost.exe 调用。  
  
## 语法  
  
```  
HRESULT FilterInputMessage( [in] MSG* pMsg ) ;  
```  
  
#### 参数  
 `pMsg`  
  
 \[in\] 发送给正在获得原始输入的窗口的 WM\_INPUT 消息。  
  
## 属性值\/返回值  
 HRESULT：  
  
 S\_OK \- 筛选器未处理该消息，且可能执行进一步处理。  
  
 S\_FALSE \- 筛选器已处理此消息，且应执行进一步处理。  
  
 E\_NOTIMPL – 如果返回此值，则不再调用 [FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md)。  这可能会从以下主机应用程序返回：仅对向 PresentationHost.exe 提供自定义进度和错误用户界面有兴趣且对从 PresentationHost.exe 向自身转发原始输入消息不感兴趣。  
  
## 备注  
 PresentationHost.exe 是各种原始输入设备（包括键盘、鼠标和远程控件）的目标。  有时，主机应用程序中的行为取决于输入，否则将由 PresentationHost.exe 消耗。  例如，主机应用程序可能依靠接收特定输入消息来确定是否显示特定的用户界面元素。  
  
 若要允许主机应用程序接收必要的输入消息以提供这些行为，PresentationHost.exe 会通过调用 [FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md) 将适当的原始输入消息转发给承载的应用程序。  
  
 承载的应用程序通过注册由 [GetRawInputDevices](../../../../docs/framework/wpf/app-development/getrawinputdevices.md) 返回的原始输入设备（人机接口设备）的设置来接收原始输入消息。  
  
## 请参阅  
 [WM\_INPUT 通知](http://msdn.microsoft.com/library/default.asp?url=/library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputmessages/wm_input.asp)