---
title: "GetCustomUI | Microsoft Docs"
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
  - "自定义错误消息 [WPF]"
  - "GetCustomUI 方法"
ms.assetid: e55180fc-35bb-4f80-a136-772b5eb3e4e5
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# GetCustomUI
在实现了 GetCustomUI 的情况下，PresentationHost.exe 会通过调用它来从主机获取自定义的进度和错误消息。  
  
## 语法  
  
```  
HRESULT GetCustomUI( [out] BSTR* pwzProgressAssemblyName, [out] BSTR* pwzProgressClassName, [out] BSTR* pwzErrorAssemblyName, [out] BSTR* pwzErrorClassName );  
```  
  
#### 参数  
 `pwzProgressAssemblyName`  
  
 \[out\] 指向某个程序集的指针，该程序集包含由主机提供的进度用户界面。  
  
 `pwzProgressClassName`  
  
 \[out\] 作为主机所提供的进度用户界面的类的名称，最好是一个 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 文件而且 <xref:System.Windows.Controls.Page> 是其顶级元素。  该类驻留在由 `pwzProgressAssemblyName` 指定的程序集内。  
  
 `pwzErrorAssemblyName`  
  
 \[out\] 指向某个程序集的指针，该程序集包含由主机提供的错误用户界面。  
  
 `pwzErrorClassName`  
  
 \[out\] 作为主机所提供的错误用户界面的类的名称，最好是一个 XAML 文件而且 <xref:System.Windows.Controls.Page> 是其顶级元素。  该类驻留在由 `pwzErrorAssemblyName` 指定的程序集内。  
  
## 属性值\/返回值  
 HRESULT：忽略。  
  
## 备注  
 主机应用程序可能具有一个无法由 PresentationHost.exe 的默认用户界面遵循的特定主题。  如果是这样，则主机应用程序可以实现 [GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md) 来向 PresentationHost.exe 返回进度和错误用户界面。  PresentationHost.exe 将总是在使用其默认用户界面之前调用 [GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md)。  
  
 此函数会在 PresentationHost 初始化过程中被调用一次。  
  
## 请参阅  
 [IWpfHostSupport](../../../../docs/framework/wpf/app-development/iwpfhostsupport.md)