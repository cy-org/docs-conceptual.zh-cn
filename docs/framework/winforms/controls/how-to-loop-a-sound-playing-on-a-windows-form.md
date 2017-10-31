---
title: "如何：在 Windows 窗体上循环播放声音 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "播放声音, 循环"
  - "声音循环"
  - "SoundPlayer 类, 循环播放"
  - "声音, 循环"
ms.assetid: ea95dd46-10a3-46c0-8263-4b205f00df7f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：在 Windows 窗体上循环播放声音
以下代码示例重复播放声音。  当 `stopPlayingButton_Click` 事件处理程序中的代码运行时，当前播放的所有声音都将停止。  如果未播放任何声音，则无任何操作。  
  
## 示例  
 [!code-csharp[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/VB/Form1.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
-   即，使用有效的文件名替换文件名 `"c:\Windows\Media\chimes.wav"`。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 可靠编程  
 文件操作应包含在相应的异常处理块内。  
  
 以下情况可能会导致异常：  
  
-   路径名称格式不正确。  例如，它包含无效字符或仅为空白（<xref:System.ArgumentException> 类）。  
  
-   此路径为只读路径（<xref:System.IO.IOException> 类）。  
  
-   此路径名为 `Nothing`（<xref:System.ArgumentNullException> 类）。  
  
-   此路径名过长（<xref:System.IO.PathTooLongException> 类）。  
  
-   路径无效（<xref:System.IO.DirectoryNotFoundException> 类）。  
  
-   此路径仅为冒号“:”（<xref:System.NotSupportedException> 类）。  
  
## .NET Framework 安全性  
 不要根据文件的名称来判断文件的内容。  例如，文件 Form1.vb 可能不是 Visual Basic 源文件。  在应用程序中使用输入的数据之前，需验证所有的输入内容。  
  
## 请参阅  
 <xref:System.Media.SoundPlayer.PlayLooping%2A>   
 [如何：在 Windows 窗体上播放声音](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)   
 [SoundPlayer 类概述](../../../../docs/framework/winforms/controls/soundplayer-class-overview.md)