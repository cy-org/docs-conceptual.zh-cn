---
title: "系统信息和 Windows 窗体 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "域名, 检索"
  - "系统信息 [Windows 窗体]"
  - "SystemInformation 类 [Windows 窗体]"
  - "用户名, 检索"
ms.assetid: 30cf43a3-8cb2-4ff3-862b-6c34576616a8
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 系统信息和 Windows 窗体
有时，为了在编写代码时做出判断，必须收集有关运行应用程序的计算机的信息。  例如，您可能有一个仅当连接到特定的网络域时才适用的函数；这种情况下，您需要一种方法来确定该域，或者当该域不存在时禁用该函数。  
  
 Windows 窗体应用程序可使用 <xref:System.Windows.Forms.SystemInformation> 类，在运行时确定有关计算机的许多情况。  下面的示例演示了如何使用 <xref:System.Windows.Forms.SystemInformation> 类来检索 <xref:System.Windows.Forms.SystemInformation.UserName%2A> 和 <xref:System.Windows.Forms.SystemInformation.UserDomainName%2A>：  
  
```vb  
Dim User As String = Windows.Forms.SystemInformation.UserName  
Dim Domain As String = Windows.Forms.SystemInformation.UserDomainName  
  
MessageBox.Show("Good morning " & User & ". You are connected to " _  
& Domain)  
  
```  
  
```csharp  
string User = SystemInformation.UserName;  
string Domain = SystemInformation.UserDomainName;  
  
MessageBox.Show("Good morning " + User + ". You are connected to " _  
+ Domain)  
```  
  
 <xref:System.Windows.Forms.SystemInformation> 类的所有成员都是只读的；您无法修改用户的设置。  该类有 100 多个成员，用于返回各种信息，从连接到计算机上的监视器的数目 \(<xref:System.Windows.Forms.SystemInformation.MonitorCount%2A>\)，到 Windows 资源管理器中图标的间距（<xref:System.Windows.Forms.SystemInformation.IconHorizontalSpacing%2A> 和 <xref:System.Windows.Forms.SystemInformation.IconVerticalSpacing%2A>）等。  
  
 <xref:System.Windows.Forms.SystemInformation> 类的一些更有用的成员包括 <xref:System.Windows.Forms.SystemInformation.ComputerName%2A>、<xref:System.Windows.Forms.SystemInformation.DbcsEnabled%2A>、<xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> 和 <xref:System.Windows.Forms.SystemInformation.TerminalServerSession%2A>。  
  
## 请参阅  
 <xref:System.Windows.Forms.SystemInformation>   
 [Windows 窗体中的电源管理](../../../../docs/framework/winforms/advanced/power-management-in-windows-forms.md)