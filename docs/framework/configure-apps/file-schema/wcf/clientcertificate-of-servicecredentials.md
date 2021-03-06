---
title: <clientCertificate> / <serviceCredentials>
ms.date: 03/30/2017
ms.assetid: 90ad03aa-2317-43dd-8a72-6d24cdcad15c
ms.openlocfilehash: a8a78bbfcd9dfbf6975503a845d5bb4e2d24b13d
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398133"
---
# <a name="clientcertificate-of-servicecredentials"></a>\<\<ServiceCredentials > ClientCertificate >
Bir çift yönlü iletişim düzeninde bir hizmet oluşturmak ve bir istemciye iletileri şifrelemek için kullanılan bir X. 509.440 sertifikası tanımlar.  
  
[ **\<Yapılandırma >** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<davranışlar >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Servicedavranışlar >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<davranış >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCredentials >** ](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<clientCertificate >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<clientCertificate>
  <certificate />
  <authentication />
</clientCertificate>
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Aşağıdaki bölümlerde öznitelikler, alt öğeler ve üst öğeler açıklanır  
  
### <a name="attributes"></a>Öznitelikler  
 Yok.  
  
### <a name="child-elements"></a>Alt Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<kimlik doğrulama >](authentication-of-clientcertificate-element.md)|İstemci sertifikası için kimlik doğrulama seçeneklerini belirtir.|  
|[\<Sertifika >](certificate-of-clientcertificate-element.md)|Kullanılacak sertifikayı belirtir.|  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<serviceCredentials >](servicecredentials.md)|Hizmetin kimliğini doğrulamak için kullanılacak kimlik bilgilerini ve istemci kimlik bilgileri doğrulaması ile ilgili ayarları belirtir.|  
  
## <a name="remarks"></a>Açıklamalar  
 Bu öğe, hizmetin istemci sertifikası ile güvenli bir şekilde iletişim kurmak için istemcinin sertifikasının önceden olması gerektiği durumlarda kullanılır. Bu, çift yönlü iletişim deseninin kullanıldığı durumlarda oluşur. Daha tipik istek/yanıt modelinde istemci, isteğin sertifikasını istemciye geri yanıtını şifrelemek ve imzalamak için kullandığı isteği içerir. Çift yönlü iletişim modelinde, hizmette istemciden bir istek yoktur ve bu nedenle iletinin istemciye güvenmesi için istemcinin sertifikasının önceden olması gerekir. Bu nedenle, istemcinin sertifikasını bant dışı bir anlaşmede edinmeniz ve bu öğeyi kullanarak sertifikayı belirtmeniz gerekir. Çift yönlü hizmetler hakkında daha fazla bilgi için [bkz. nasıl yapılır: Çift yönlü sözleşme](../../../wcf/feature-details/how-to-create-a-duplex-contract.md)oluşturun.  
  
 Bu öğedeki sertifika kümesi, iletileri yalnızca `MutualCertificateDuplex` ileti güvenliği kimlik doğrulama moduyla yapılandırılan bağlamalar için istemciye şifrelemek üzere kullanılır.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.ClientCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.ClientCertificate%2A>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>
- [Nasıl yapılır: Çift yönlü sözleşme oluşturma](../../../wcf/feature-details/how-to-create-a-duplex-contract.md)
- [Güvenlik Davranışları](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Sertifikalarla Çalışma](../../../wcf/feature-details/working-with-certificates.md)
