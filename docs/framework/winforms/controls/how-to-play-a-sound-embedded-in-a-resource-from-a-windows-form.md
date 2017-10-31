---
title: "如何：从 Windows 窗体播放资源中嵌入的声音 | Microsoft Docs"
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
  - "从资源播放声音"
  - "播放声音的资源 [Windows 窗体]"
  - "从资源播放声音"
  - "SoundPlayer 类，从资源播放声音"
ms.assetid: 7d148bb6-8a1e-47d7-a08d-35828d2e688f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：从 Windows 窗体播放资源中嵌入的声音
您可以使用<xref:System.Media.SoundPlayer>类，以从嵌入的资源播放声音。  
  
## <a name="example"></a>示例  
 [!code-csharp[System.Windows.Forms.Sound#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Sound/CS/soundtestform.cs#10)]
 [!code-vb[System.Windows.Forms.Sound#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Sound/VB/soundtestform.vb#10)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
 导入<xref:System.Media?displayProperty=fullName>命名空间。  
  
 为您的项目中嵌入的资源包括声音文件。  
  
 替换"<>\>"替换为在其中嵌入的声音文件的程序集的名称。 不包括".dll"后缀。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Media.SoundPlayer>   
 [如何︰ 从 Windows 窗体播放声音](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)   
 [如何︰ 循环 Windows 窗体上播放声音](../../../../docs/framework/winforms/controls/how-to-loop-a-sound-playing-on-a-windows-form.md)