---
title: "使用 My.Resources 和 My.Settings 快速开发应用程序 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Resources 对象, 开发应用程序"
  - "My.Settings 对象, 开发应用程序"
  - "快速应用程序开发 (RAD), My.Resources"
  - "快速应用程序开发 (RAD), My.Settings"
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 使用 My.Resources 和 My.Settings 快速开发应用程序 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`My.Resources` 对象提供对应用程序资源的访问，并允许您动态检索应用程序的资源。  
  
## 检索资源  
 通过 `My.Resources` 对象可检索多种资源（例如音频文件、图标、图像和字符串）。  例如，您可以访问应用程序中特定于区域性的资源文件。  下面的示例将窗体的图标设置为名为 `Form1Icon` 的图标，此图标存储于应用程序的资源文件中。  
  
 [!code-vb[VbVbcnMy#7](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/rapid-application-development-with-my-resources-and-my-settings_1.vb)]  
  
 `My.Resources` 对象仅公开全局资源。  它不提供对与窗体相关联的资源文件的访问。  必须从窗体中访问窗体资源。  有关更多信息，请参见 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/zh-cn/9a96220d-a19b-4de0-9f48-01e5d82679e5)。  
  
 同样，`My.Settings` 对象提供对应用程序设置的访问，并且允许您动态存储和检索应用程序的属性设置及其他信息。  有关更多信息，请参见 [My.Resources 对象](../../../visual-basic/language-reference/objects/my-resources-object.md) 和 [My.Settings 对象](../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
## 请参阅  
 [My.Resources 对象](../../../visual-basic/language-reference/objects/my-resources-object.md)   
 [My.Settings 对象](../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [访问应用程序的设置](../../../visual-basic/developing-apps/programming/app-settings/accessing-application-settings.md)