---
title: "如何：从 Windows 窗体中播放提示音 | Microsoft Docs"
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
  - "声音、 提示音"
  - "Windows 窗体声音"
  - "播放声音"
  - "窗体声音"
  - "示例 [Windows 窗体] 声音"
ms.assetid: 7ea5cded-4888-4f35-8f28-5cab1a55c973
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：从 Windows 窗体中播放提示音
此示例中播放提示音在运行时。  
  
## <a name="example"></a>示例  
  
```vb  
Public Sub OnePing()  
    Beep()  
End Sub  
```  
  
```csharp  
public void onePing()  
{  
    SystemSounds.Beep.Play();  
}  
```  
  
> [!NOTE]
>  C# 代码示例中播放的声音由<xref:System.Media.SystemSounds.Beep%2A>系统声音设置。 有关详细信息，请参阅<xref:System.Media.SystemSounds>。  
  
## <a name="compiling-the-code"></a>编译代码  
 对于 C# 中，此示例需要引用<xref:System.Media?displayProperty=fullName>命名空间。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Interaction.Beep%2A>   
 <xref:System.Media.SoundPlayer>   
 [如何︰ 在 Windows 窗体播放系统声音](../../../../docs/framework/winforms/controls/how-to-play-a-system-sound-from-a-windows-form.md)   
 [如何︰ 从 Windows 窗体播放声音](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)