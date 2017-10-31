---
title: "如何：使用 Windows 窗体 ImageList 组件添加或移除图像 | Microsoft Docs"
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
  - "ImageList 组件 [Windows 窗体], 添加图像"
  - "ImageList 组件 [Windows 窗体], 移除图像"
  - "图像 [Windows 窗体], 添加到 ImageList 组件"
  - "图像 [Windows 窗体], 通过控件显示"
  - "图像 [Windows 窗体], 从 ImageList 组件中移除"
  - "图像 [Windows 窗体], 为控件存储"
ms.assetid: c5eacc56-f769-4e2e-bfb7-f756620913db
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 Windows 窗体 ImageList 组件添加或移除图像
通常，Windows 窗体 <xref:System.Windows.Forms.ImageList> 组件在与控件关联之前，先用图像填充。  不过，可以在将图像列表与控件关联之后添加和移除图像。  
  
> [!NOTE]
>  在移除图像时，请验证任何关联控件的 <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> 属性仍然有效。  
  
### 以编程方式添加图像  
  
-   使用图像列表的 <xref:System.Windows.Forms.ImageList.Images%2A> 属性的 <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> 方法。  
  
     在下面的代码示例中，图标位置的路径设置是**“My Documents”**文件夹。  使用此位置是因为可假定大多数运行 Windows 操作系统的计算机都包含该文件夹。  选择此位置还能让具有最低系统访问级别的用户更安全地运行应用程序。  下面的代码示例需要您有一个已添加了 <xref:System.Windows.Forms.ImageList> 控件的窗体。  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void addImage()  
    {  
    // Be sure that you use an appropriate escape sequence (such as the   
    // @) when specifying the location of the file.  
       System.Drawing.Image myImage =   
         Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void addImage()  
       {  
       // Replace the bold image in the following sample   
       // with your own icon.  
       // Be sure that you use an appropriate escape sequence (such as   
       // \\) when specifying the location of the file.  
          System::Drawing::Image ^ myImage =   
             Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
       }  
    ```  
  
### 用键值添加图像  
  
-   使用接受键值的图像列表的 <xref:System.Windows.Forms.ImageList.Images%2A> 属性的 <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> 方法之一。  
  
     在下面的代码示例中，图标位置的路径设置是**“My Documents”**文件夹。  使用此位置是因为可假定大多数运行 Windows 操作系统的计算机都包含该文件夹。  选择此位置还能让具有最低系统访问级别的用户更安全地运行应用程序。  下面的代码示例需要您有一个已添加了 <xref:System.Windows.Forms.ImageList> 控件的窗体。  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add("myPhoto", myImage)  
    End Sub  
  
    ```  
  
```csharp  
public void addImage()  
{  
// Be sure that you use an appropriate escape sequence (such as the   
// @) when specifying the location of the file.  
   System.Drawing.Image myImage =   
     Image.FromFile  
   (System.Environment.GetFolderPath  
   (System.Environment.SpecialFolder.Personal)  
   + @"\Image.gif");  
   imageList1.Images.Add("myPhoto", myImage);  
}  
  
```  
  
### 以编程方式移除所有图像  
  
-   可以使用 <xref:System.Windows.Forms.ImageList.ImageCollection.Remove%2A> 方法移除单个图像  
  
     \- 或 \-  
  
     可以使用 <xref:System.Windows.Forms.ImageList.ImageCollection.Clear%2A> 方法清除图像列表中的所有图像。  
  
    ```vb  
    ' Removes the first image in the image list  
    ImageList1.Images.Remove(myImage)  
    ' Clears all images in the image list  
    ImageList1.Images.Clear()  
  
    ```  
  
```csharp  
// Removes the first image in the image list.  
imageList1.Images.Remove(myImage);  
// Clears all images in the image list.  
imageList1.Images.Clear();  
  
```  
  
### 通过键移除图像  
  
-   使用 <xref:System.Windows.Forms.ImageList.ImageCollection.RemoveByKey%2A> 方法可以按图像的键移除单个图像。  
  
    ```vb  
    ' Removes the image named "myPhoto" from the list.  
    ImageList1.Images.RemoveByKey("myPhoto")  
  
    ```  
  
```csharp  
// Removes the image named "myPhoto" from the list.  
imageList1.Images.RemoveByKey("myPhoto");  
  
```  
  
## 请参阅  
 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)   
 [ImageList 组件概述](../../../../docs/framework/winforms/controls/imagelist-component-overview-windows-forms.md)   
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)