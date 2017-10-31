---
title: "如何：读取图像元数据 | Microsoft Docs"
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
  - "元数据, 属性项"
  - "元数据, 读取图像"
ms.assetid: 72ec0b31-0be7-444a-9575-1dbcb864e0be
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：读取图像元数据
一些图像文件中包含可供您读取以确定图像特征的元数据。  例如，数字照片中可能包含可供您读取以确定用于捕获该图像的照相机的品牌和型号的元数据。  利用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，可以读取现有的元数据，也可以将新的元数据写入图像文件中。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 将单独的元数据段存储在 <xref:System.Drawing.Imaging.PropertyItem> 对象中。  您可读取 <xref:System.Drawing.Image> 对象的 <xref:System.Drawing.Image.PropertyItems%2A> 属性以便从某个文件中检索所有的元数据。  <xref:System.Drawing.Image.PropertyItems%2A> 属性返回一个 <xref:System.Drawing.Imaging.PropertyItem> 对象的数组。  
  
 <xref:System.Drawing.Imaging.PropertyItem> 对象具有以下四个属性：`Id`、`Value`、`Len` 和 `Type`。  
  
## Id  
 用于标识元数据项的标记。  下表显示一些可赋予 <xref:System.Drawing.Imaging.PropertyItem.Id%2A> 的值。  
  
|十六进制数值|说明|  
|------------|--------|  
|0x0320<br /><br /> 0x010F<br /><br /> 0x0110<br /><br /> 0x9003<br /><br /> 0x829A<br /><br /> 0x5090<br /><br /> 0x5091|图像标题<br /><br /> 设备制造商<br /><br /> 设备型号<br /><br /> ExifDTOriginal<br /><br /> Exif 曝光时间<br /><br /> 亮度表<br /><br /> 色度表|  
  
## 值  
 值数组。  这些值的格式由 <xref:System.Drawing.Imaging.PropertyItem.Type%2A> 属性确定。  
  
## Len  
 <xref:System.Drawing.Imaging.PropertyItem.Value%2A> 属性指向的值的数组长度（以字节表示）。  
  
## 类型  
 `Value` 属性指向的数组中值的数据类型。  下表显示由 `Type` 属性值指示的格式  
  
|数值|说明|  
|--------|--------|  
|1|一个 `Byte`|  
|2|ASCII 编码的 `Byte` 对象的数组|  
|3|16 位整数|  
|4|32 位整数|  
|5|包含两个表示有理数的 `Byte` 对象的数组|  
|6|未使用|  
|7|未定义|  
|8|未使用|  
|9|`SLong`|  
|10|`SRational`|  
  
## 示例  
  
### 说明  
 下面的代码示例读取并显示 `FakePhoto.jpg` 文件中的七段元数据。  该列表中的第二个 \(index 1\) 属性项包含 <xref:System.Drawing.Imaging.PropertyItem.Id%2A> 0x010F（设备制造商）和 <xref:System.Drawing.Imaging.PropertyItem.Type%2A> 2（ASCII 编码的字节数组）。  代码示例显示该属性项的值。  
  
 该代码将生成类似以下内容的输出：  
  
 `Property Item 0`  
  
 `id: 0x320`  
  
 `type: 2`  
  
 `length: 16 bytes`  
  
 `Property Item 1`  
  
 `id: 0x10f`  
  
 `type: 2`  
  
 `length: 17 bytes`  
  
 `Property Item 2`  
  
 `id: 0x110`  
  
 `type: 2`  
  
 `length: 7 bytes`  
  
 `Property Item 3`  
  
 `id: 0x9003`  
  
 `type: 2`  
  
 `length: 20 bytes`  
  
 `Property Item 4`  
  
 `id: 0x829a`  
  
 `type: 5`  
  
 `length: 8 bytes`  
  
 `Property Item 5`  
  
 `id: 0x5090`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `Property Item 6`  
  
 `id: 0x5091`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `The equipment make is Northwind Camera.`  
  
### 代码  
 [!code-csharp[System.Drawing.WorkingWithImages#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.WorkingWithImages#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#51)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  处理该窗体的 <xref:System.Windows.Forms.Control.Paint> 事件，并将此代码粘贴到 paint 事件处理程序中。  必须用系统上有效的图像名和路径替换 `FakePhoto.jpg`，并导入 `System.Drawing.Imaging` 命名空间。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)