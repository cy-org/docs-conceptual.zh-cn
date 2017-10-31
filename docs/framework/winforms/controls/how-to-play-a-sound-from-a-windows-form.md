---
title: "如何：在 Windows 窗体上播放声音 | Microsoft Docs"
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
  - "播放声音，Windows 窗体"
  - "播放声音"
  - "SoundPlayer 类"
  - "声音"
  - "My.Computer.Audio 对象，播放声音"
  - "示例 [Windows 窗体] 声音"
ms.assetid: 3d3350b7-1ebd-4e05-a738-48ca1160a19d
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 Windows 窗体上播放声音
此示例在运行时位于给定路径中播放声音。  
  
## <a name="example"></a>示例  
  
```vb  
Sub PlaySimpleSound()  
    My.Computer.Audio.Play("c:\Windows\Media\chimes.wav")  
End Sub  
```  
  
```csharp  
private void playSimpleSound()  
{  
    SoundPlayer simpleSound = new SoundPlayer(@"c:\Windows\Media\chimes.wav");  
    simpleSound.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   即，使用有效的文件名替换文件名 `"c:\Windows\Media\chimes.wav"`。  
  
-   (C#)对引用<xref:System.Media?displayProperty=fullName>命名空间。  
  
## <a name="robust-programming"></a>可靠编程  
 文件操作应包含在相应的结构化异常处理块内。  
  
 以下情况可能会导致异常：  
  
-   路径名称格式不正确。 例如，它包含非法字符或仅为空白 (<xref:System.ArgumentException>类)。  
  
-   该路径是只读的 (<xref:System.IO.IOException>类)。  
  
-   路径名称格式不`null`(<xref:System.ArgumentNullException>类)。  
  
-   路径名称格式不太长 (<xref:System.IO.PathTooLongException>类)。  
  
-   路径无效 (<xref:System.IO.DirectoryNotFoundException>类)。  
  
-   该路径是仅为冒号":"(<xref:System.NotSupportedException>类)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 不要根据文件的名称来判断文件的内容。 例如，文件 `Form1.vb` 可能不是 Visual Basic 源文件。 在应用程序中使用输入的数据之前，需验证所有的输入内容。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Media.SoundPlayer>   
 [如何︰ 在 Windows 窗体异步加载声音](../../../../docs/framework/winforms/controls/how-to-load-a-sound-asynchronously-within-a-windows-form.md)   
 