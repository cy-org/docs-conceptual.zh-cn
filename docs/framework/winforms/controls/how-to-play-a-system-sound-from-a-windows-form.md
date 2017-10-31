---
title: "如何：从 Windows 窗体中播放系统声音 | Microsoft Docs"
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
  - "为系统事件播放的声音"
  - "播放声音，Windows 窗体"
  - "从 Windows 窗体播放系统声音"
  - "播放声音，系统"
  - "SoundPlayer 类，系统声音"
  - "播放声音"
  - "示例 [Windows 窗体] 声音"
ms.assetid: afb206ff-4824-4804-a8d4-185bf5ad8e7c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：从 Windows 窗体中播放系统声音
下面的代码示例中起`Exclamation`在运行时的系统声音。 有关系统声音的详细信息，请参阅<xref:System.Media.SystemSounds>。  
  
## <a name="example"></a>示例  
  
```vb  
Public Sub PlayExclamation()  
    SystemSounds.Exclamation.Play()  
End Sub  
  
```  
  
```csharp  
public void playExclamation()  
{  
    SystemSounds.Exclamation.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对引用<xref:System.Media?displayProperty=fullName>命名空间。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Media.SoundPlayer>   
 <xref:System.Media.SystemSounds>   
 [如何︰ 在 Windows 窗体播放提示音](../../../../docs/framework/winforms/controls/how-to-play-a-beep-from-a-windows-form.md)   
 [如何︰ 从 Windows 窗体播放声音](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)