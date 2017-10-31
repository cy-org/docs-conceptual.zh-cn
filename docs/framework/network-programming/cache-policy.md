---
title: "缓存策略"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- time-based cache policies
- location-based cache policies
- cache [.NET Framework], policies
- request cache policies
- freshness of cached resources
- content cache policies
- expired content
ms.assetid: 1a7e04ec-7872-41c2-96c6-52566dcb412b
caps.latest.revision: 11
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7323c93ef89e340595f6b62947ea45867e651425
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="cache-policy"></a>缓存策略
缓存策略定义规则，这些规则用于确定使用已请求资源的缓存副本是否可以满足请求。 尽管应用程序为新鲜度指定客户端缓存要求，但有效的缓存策略是由客户端缓存要求、服务器的内容有效期限要求以及服务器的重新验证要求确定的。 客户端缓存策略和服务器要求的交互始终会造成最保守的缓存策略，有助于确保将最新鲜的内容返回给客户端应用程序。  
  
 缓存策略是基于位置或基于时间的。 基于位置的缓存策略根据可从中获取已请求资源的位置定义缓存条目的新鲜度。 基于时间的缓存策略使用检索资源的时间、随资源返回的标头和当前时间来定义缓存条目的新鲜度。 大多数应用程序可以使用基于默认时间的缓存策略，这可在 [http://www.ietf.org](http://www.ietf.org/) 上实现 RFC 2616 中指定的缓存策略。  
  
 下表中所述的类用于指定缓存策略。  
  
|类名|描述|  
|----------------|-----------------|  
|<xref:System.Net.Cache.HttpRequestCachePolicy>|表示使用 <xref:System.Net.HttpWebRequest> 对象请求的资源的基于位置和基于时间的缓存策略。|  
|<xref:System.Net.Cache.RequestCachePolicy>|表示使用 <xref:System.Net.WebRequest> 对象请求的资源的基于位置的缓存策略或基于 <xref:System.Net.Cache.RequestCacheLevel.Default> 时间的缓存策略。|  
|<xref:System.Net.Cache.HttpCacheAgeControl>|指定用于创建基于时间的 <xref:System.Net.Cache.HttpRequestCachePolicy> 对象的值。|  
|<xref:System.Net.Cache.HttpRequestCacheLevel>|指定用于创建基于位置和基于时间的 <xref:System.Net.Cache.HttpRequestCachePolicy> 对象的值。|  
|<xref:System.Net.Cache.RequestCacheLevel>|指定用于创建基于位置或基于 <xref:System.Net.Cache.RequestCacheLevel.Default> 时间的 <xref:System.Net.Cache.RequestCachePolicy> 对象的值。|  
  
 可以为应用程序发出的所有请求或为各个单独的请求定义一个缓存策略。 在同时指定应用程序级缓存策略和请求级缓存策略的情况下，会使用请求级策略。 通过以编程方式或通过使用应用程序或计算机配置文件，以指定应用程序级缓存策略。 有关详细信息，请参阅 [\<requestCaching> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)。  
  
 若要创建缓存策略，必须通过创建 <xref:System.Net.Cache.RequestCachePolicy> 或 <xref:System.Net.Cache.HttpRequestCachePolicy> 类的实例来创建策略对象。 若要针对某个请求指定策略，请将此请求的 <xref:System.Net.WebRequest.CachePolicy%2A> 属性设置为策略对象。 在以编程方式设置应用程序级策略时，请将 <xref:System.Net.HttpWebRequest.DefaultCachePolicy%2A> 属性设置为策略对象。  
  
 有关演示如何创建和使用缓存策略的代码示例，请参阅[在网络应用程序中配置缓存](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)。  
  
## <a name="see-also"></a>另请参阅  
 [网络应用程序的缓存管理](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [基于位置的缓存策略](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [基于时间的缓存策略](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [在网络应用程序中配置缓存](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)

