---
title: <httpTransport>
ms.date: 03/30/2017
ms.assetid: 8b30c065-b32a-4fa3-8eb4-5537a9c6b897
ms.openlocfilehash: b3558db6018d79f0fad27ff28657bfadb5637467
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73736770"
---
# <a name="httptransport"></a>\<httpTransport >
Özel bağlama için SOAP iletileri iletmek üzere bir HTTP aktarımı belirtir.  
  
[ **\<configuration >** ](../configuration-element.md) \
&nbsp; &nbsp;[ **\<system. serviceModel >** ](system-servicemodel.md) \
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<bağlamaları >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<bağlama >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<httpTransport >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<httpTransport allowCookies="Boolean"
               authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"
               bypassProxyOnLocal="Boolean"
               hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"
               keepAliveEnabled="Boolean"
               maxBufferSize="Integer"
               proxyAddress="Uri"
               proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"
               realm="String"
               transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
               unsafeConnectionNtlmAuthentication="Boolean"
               useDefaultWebProxy="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Öznitelikler, alt ve üst öğeler aşağıdaki bölümlerde açıklanmaktadır.  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|  
|---------------|-----------------|  
|allowCookies|İstemcinin tanımlama bilgilerini kabul edip etmediğini ve gelecekteki isteklere yayıp yaymayacağını belirten bir Boole değeri. Varsayılan, `false` değeridir.<br /><br /> Tanımlama bilgilerini kullanan ASMX Web hizmetleriyle etkileşim kurarken bu özniteliği kullanabilirsiniz. Bu şekilde, sunucudan döndürülen tanımlama bilgilerinin, bu hizmet için gelecekteki tüm istemci isteklerine otomatik olarak kopyalandığından emin olabilirsiniz.|  
|authenticationScheme|HTTP dinleyicisi tarafından işlenen istemci isteklerinin kimliğini doğrulamak için kullanılan protokolü belirtir. Geçerli değerler şunlardır:<br /><br /> -Digest: Özet kimlik doğrulamasını belirtir.<br />-Anlaş: kimlik doğrulama düzenini belirlemek için istemcisiyle görüşürler. Hem istemci hem de sunucu Kerberos 'u destekliyorsa, kullanılır; Aksi halde, NTLM kullanılır.<br />-NTLM: NTLM kimlik doğrulamasını belirtir.<br />-Temel: temel kimlik doğrulamasını belirtir.<br />-Anonim: anonim kimlik doğrulamasını belirtir.<br /><br /> Varsayılan değer anonimdir. Bu öznitelik <xref:System.Net.AuthenticationSchemes>türündedir. Bu öznitelik yalnızca bir kez ayarlanabilir.|  
|bypassProxyOnLocal|Yerel adresler için proxy sunucusunun atlanıp atlanmayacağını belirten bir Boole değeri. Varsayılan, `false` değeridir.<br /><br /> Yerel LAN veya intranette olan yerel bir adres.<br /><br /> Hizmet adresi `http://localhost`ile başlıyorsa Windows Communication Foundation (WCF) her zaman proxy 'yi yoksayar.<br /><br /> İstemcilerin aynı makinede hizmetlerle görüşülürken bir proxy üzerinden gitmesini istiyorsanız, localhost yerine ana bilgisayar adını kullanmanız gerekir.|  
|hostnameComparisonMode|URI 'Leri ayrıştırmak için kullanılan HTTP ana bilgisayar adını karşılaştırma modunu belirtir. Geçerli değerler şunlardır<br /><br /> -StrongWildcard: ("+") belirtilen şema, bağlantı noktası ve göreli URI bağlamında tüm olası ana bilgisayar adları ile eşleşir.<br />-Tam: joker karakter yok<br />-WeakWildcard: ("\*"), açıkça veya güçlü joker karakter mekanizması aracılığıyla eşleşmeyen belirtilen şema, bağlantı noktası ve göreli UıR bağlamındaki tüm olası ana bilgisayar adı ile eşleşir.<br /><br /> Bu öznitelik <xref:System.ServiceModel.HostNameComparisonMode>türündedir. Varsayılan, <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard> değeridir.|  
|keepAliveEnabled|Internet kaynağına kalıcı bir bağlantı yapılıp yapılmayacağını belirten Boolean bir değer.|  
|maxBufferSize|Arabelleğin en büyük boyutunu belirten pozitif bir tamsayı. Varsayılan değer 524288 ' dir|  
|proxyAddress|HTTP proxy adresini belirten bir URI. `useSystemWebProxy` `true`, bu ayar `null`olmalıdır. Varsayılan, `null` değeridir.|  
|proxyAuthenticationScheme|HTTP proxy tarafından işlenen istemci isteklerinin kimliğini doğrulamak için kullanılan protokolü belirtir. Geçerli değerler şunlardır:<br /><br /> -None: kimlik doğrulaması gerçekleştirilmez.<br />-Digest: Özet kimlik doğrulamasını belirtir.<br />-Anlaş: kimlik doğrulama düzenini belirlemek için istemcisiyle görüşürler. Hem istemci hem de sunucu Kerberos 'u destekliyorsa, kullanılır; Aksi halde, NTLM kullanılır.<br />-NTLM: NTLM kimlik doğrulamasını belirtir.<br />-Temel: temel kimlik doğrulamasını belirtir.<br />-Anonim: anonim kimlik doğrulamasını belirtir.<br /><br /> Varsayılan değer anonimdir. Bu öznitelik <xref:System.Net.AuthenticationSchemes>türündedir. <xref:System.Net.AuthenticationSchemes.IntegratedWindowsAuthentication?displayProperty=nameWithType> desteklenmediğini unutmayın.|  
|bölgesindeki|Proxy/sunucu üzerinde kullanılacak bölgeyi belirten bir dize. Varsayılan değer boş bir dizedir.<br /><br /> Sunucular, korumalı kaynakları bölümlemek için alanları kullanır. Her bölüm kendi kimlik doğrulama düzenine ve/veya yetkilendirme veritabanına sahip olabilir. Bölgeler yalnızca temel ve Özet kimlik doğrulaması için kullanılır. İstemci başarıyla kimlik doğrulamasından geçtikten sonra, kimlik doğrulaması belirli bir bölgedeki tüm kaynaklar için geçerli olur. Bölge ayrıntılı açıklaması için, [IETF Web SITESINDE](https://www.ietf.org)rfc 2617 ' a bakın.|  
|transferMode|İletilerin arabelleğe alınıp alınmayacağını veya bir istek ya da yanıt olduğunu belirtir. Geçerli değerler şunlardır:<br /><br /> -Arabelleğe alınmış: istek ve yanıt iletilerinin ara belleğe alınır.<br />-Akışla: istek ve yanıt iletileri akışlardır.<br />-StreamedRequest: istek iletisi akışla yanıt iletisi arabelleğe alındı.<br />-Streammedresponse: istek iletisi arabelleğe alındı ve yanıt iletisi akışla.<br /><br /> Varsayılan değer arabelleğe alındı. Bu öznitelik <xref:System.ServiceModel.TransferMode> türündedir.|  
|unsafeConnectionNtlmAuthentication|Sunucuda güvensiz bağlantı paylaşımının etkin olup olmadığını belirten bir Boolean değer. Varsayılan, `false` değeridir. Etkinleştirilirse, NTLM kimlik doğrulaması her TCP bağlantısında bir kez gerçekleştirilir.|  
|useDefaultWebProxy|Kullanıcıya özel ayarlar yerine makine genelindeki proxy ayarlarının kullanılıp kullanılmayacağını belirten bir Boole değeri. Varsayılan, `true` değeridir.|  
  
### <a name="child-elements"></a>Alt Öğeler  
 Yok.  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\< bağlama >](bindings.md)|Özel bağlamanın tüm bağlama yeteneklerini tanımlar.|  
  
## <a name="remarks"></a>Açıklamalar  
 `httpTransport` öğesi, HTTP aktarım protokolünü uygulayan özel bir bağlama oluşturmak için başlangıç noktasıdır. HTTP, birlikte çalışabilirlik amacıyla kullanılan birincil aktarımdır. Bu taşıma, diğer WCF olmayan Web Hizmetleri yığınlarıyla birlikte çalışabilirliği sağlamak için Windows Communication Foundation (WCF) tarafından desteklenir.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Configuration.HttpTransportElement>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Taşımalar](../../../wcf/feature-details/transports.md)
- [Taşıma Seçme](../../../wcf/feature-details/choosing-a-transport.md)
- [Bağlamalar](../../../wcf/bindings.md)
- [Bağlamaları Genişletme](../../../wcf/extending/extending-bindings.md)
- [Özel Bağlamalar](../../../wcf/extending/custom-bindings.md)
- [\<customBinding >](custombinding.md)
