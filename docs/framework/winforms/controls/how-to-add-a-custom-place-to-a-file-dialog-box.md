---
title: "如何：向文件对话框添加自定义区域 | Microsoft Docs"
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
  - "自定义区域到对话框"
  - "向对话框添加自定义区域"
  - "CustomPlaces 集合"
ms.assetid: 63f6469b-59cd-40f6-9e61-8b5831856780
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：向文件对话框添加自定义区域
默认打开和保存对话框中，位于[!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)]上标题为对话框中的左侧有一个区域**收藏夹链接**。 此区域称为自定义区域。 <xref:System.Windows.Forms.OpenFileDialog>和<xref:System.Windows.Forms.SaveFileDialog>类使您得以文件夹添加到<xref:System.Windows.Forms.FileDialog.CustomPlaces%2A>集合。  
  
> [!NOTE]
>  为了使才会显示在一个自定义空间<xref:System.Windows.Forms.OpenFileDialog>或<xref:System.Windows.Forms.SaveFileDialog>、 <xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A>属性必须设置为`true`（默认值）。  
  
### <a name="to-add-a-custom-place-to-a-file-dialog-box"></a>若要向文件对话框添加自定义区域  
  
-   添加路径时，已知文件夹 GUID，或<xref:System.Windows.Forms.FileDialogCustomPlace>对象传递给<xref:System.Windows.Forms.FileDialog.CustomPlaces%2A>对话框中的集合。  
  
     下面的代码示例演示如何添加路径︰  
  
    ```vb  
    OpenFileDialog1.CustomPlaces.Add("C:\MyCustomPlace")  
    ```  
  
    ```csharp  
    openFileDialog1.CustomPlaces.Add("C:\\MyCustomPlace");  
    ```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.FileDialog>   
 <xref:System.Windows.Forms.FileDialogCustomPlacesCollection.Add%2A?displayProperty=fullName>   
 [文件对话框自定义区域的已知文件夹 Guid](../../../../docs/framework/winforms/controls/known-folder-guids-for-file-dialog-custom-places.md)