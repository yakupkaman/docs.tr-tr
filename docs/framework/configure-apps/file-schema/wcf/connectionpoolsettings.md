---
title: <connectionPoolSettings>
ms.date: 03/30/2017
ms.assetid: 6fa7fa65-2c6e-4eab-b8cf-7690112c0be5
ms.openlocfilehash: 842173c7bd9673a1e08c93d5ed650a42b9d979e5
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400476"
---
# <a name="connectionpoolsettings"></a>\<connectionPoolSettings >
Adlandırılmış kanal bağlama için ek bağlantı havuzu ayarlarını belirtir.  
  
[ **\<Yapılandırma >** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<bağlama >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<bağlama >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<namedPipeTransport >** ](namedpipetransport.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<connectionPoolSettings >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<connectionPoolSettings groupName="String"
                        idleTimeout="TimeSpan"
                        maxOutboundConnectionsPerEndpoint="Integer" />
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Öznitelikler, alt ve üst öğeler aşağıdaki bölümlerde açıklanmaktadır.  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|  
|---------------|-----------------|  
|`groupName`|Giden kanallar için kullanılan bağlantı havuzu adını tanımlayan bir dize. Akışlı modda bağlantılar paylaşılmaz, yani bağlantı havuzunun devre dışı bırakıldığı anlamına gelir. Varsayılan değer "default" dizesidir. Belirli bir istemcinin bağlantılarını ayrı gruplar halinde yalıtmak için bu değeri değiştirebilirsiniz.|  
|`idleTimeout`|Bağlantı kesilmeden <xref:System.TimeSpan> önce bağlantının boşta kalabileceği en uzun süreyi belirten pozitif bir değer. Varsayılan değer 00:02:00 ' dir.|  
|`maxOutboundConnectionsPerEndpoint`|Hizmet tarafından başlatılan bir uzak uç noktaya bağlantı sayısını belirten pozitif bir tamsayı. Sınırın üzerindeki bağlantılar, sınırın altındaki bir boşluk kullanılabilir olana kadar sıraya alınır. Bir özel durum oluşturulmadan önce bağlantıların sırada kalacağı süreyi sınırlandırır.`idleTimeout` Varsayılan değer 10 ' dur.<br /><br /> Bu öznitelik, eşzamanlı etkin bağlantı sayısını istemciden belirli bir hizmet uç noktasına sınırlandırır. Bu değer, daha etkin istemci bağlantılarına sahip olacak şekilde aşılırsa, hizmet istemciye yanıt vermemeye başlayabilir. Bu durumda, bu değerin belirli bir uç nokta ile beklenen eşzamanlı istemci bağlantısı sayısı üst sınırını aşmayacak şekilde ayarlanması gerekir.|  
  
### <a name="child-elements"></a>Alt Öğeler  
 Yok.  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<namedPipeTransport >](namedpipetransport.md)|Bir kanalın adlandırılmış kanallar kullanarak ileti aktarmasına neden olan bir taşıma tanımlar.|  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Configuration.NamedPipeConnectionPoolSettingsElement>
- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement.ConnectionPoolSettings%2A>
- <xref:System.ServiceModel.Channels.NamedPipeConnectionPoolSettings>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Taşımalar](../../../wcf/feature-details/transports.md)
- [Taşıma Seçme](../../../wcf/feature-details/choosing-a-transport.md)
- [Bağlamalar](../../../wcf/bindings.md)
- [Bağlamaları Genişletme](../../../wcf/extending/extending-bindings.md)
- [Özel Bağlamalar](../../../wcf/extending/custom-bindings.md)
- [\<customBinding >](custombinding.md)
