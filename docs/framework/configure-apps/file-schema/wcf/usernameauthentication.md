---
title: <userNameAuthentication>
ms.date: 03/30/2017
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
ms.openlocfilehash: dc5c00a2204646863ae2570bb97b8d70e22a72d4
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399183"
---
# <a name="usernameauthentication"></a>\<userNameAuthentication >
Hizmetin kimlik bilgilerini Kullanıcı adı ve parolaya göre belirtir.  
  
[ **\<Yapılandırma >** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<davranışlar >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Servicedavranışlar >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<davranış >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCredentials >** ](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<userNameAuthentication >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<userNameAuthentication cacheLogonTokenLifetime="TimeSpan"
                        cacheLogonTokens="Boolean"
                        customUserNamePasswordValidatorType="String"
                        includeWindowsGroups="Boolean"
                        maxCacheLogonTokens="Integer"
                        membershipProviderName="String"
                        userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Öznitelikler, alt ve üst öğeler aşağıdaki bölümlerde açıklanmaktadır.  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|Bir <xref:System.TimeSpan> belirtecin önbelleğe alındığı sürenin en uzun uzunluğunu belirten bir. Varsayılan değer 00:15:00 ' dir.|  
|`cacheLogonTokens`|Oturum açma belirteçlerinin önbelleğe alınıp alınmayacağını belirten bir Boole değeri. Varsayılan, `false` değeridir.|  
|`customUserNamePasswordValidatorType`|Kullanılacak özel Kullanıcı adı parola Doğrulayıcı türünü belirten bir dize. Varsayılan değer boş bir dizedir.|  
|`includeWindowsGroups`|Windows gruplarının güvenlik bağlamına dahil edilip edilmeyeceğini belirten bir Boole değeri. Varsayılan, `true` değeridir.<br /><br /> Bu özniteliğin olarak `true` ayarlanması, tam grup genişlemesiyle sonuçlandığından performans etkisine sahiptir. Bir kullanıcının ait olduğu `false` grupların listesini oluşturmanız gerekmiyorsa bu özelliği olarak ayarlayın.|  
|`maxCacheLogonTokens`|Önbelleğe eklenecek en fazla oturum açma belirteçleri sayısını belirten bir tamsayı. Bu değer sıfırdan büyük olmalıdır. Varsayılan değer 128 ' dir.|  
|`membershipProviderName`|Bir bağlamanın `username`özniteliği olarak ayarlandığında, Kullanıcı adı Windows hesaplarına eşlenir. `clientCredentialType` İlgili parola doğrulama mekanizmasını sağlayan <xref:System.Web.Security.MembershipProvider> değerin adını içeren bir dize olan bu özniteliği kullanarak bu davranışı geçersiz kılabilirsiniz.|  
|`userNamePasswordValidationMode`|Kullanıcı adı parolasının doğrulanma şeklini belirtir. Geçerli değerler şunlardır:<br /><br /> -Windows<br />-MembershipProvider<br />-Özel<br /><br /> Varsayılan olarak Windows. Bu öznitelik türü <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>.|  
  
### <a name="child-elements"></a>Alt Öğeler  
 Yok.  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<serviceCredentials >](servicecredentials.md)|Hizmetin kimliğini doğrulamak için kullanılacak kimlik bilgisini ve istemci kimlik bilgileri doğrulaması ile ilgili ayarları belirtir.|  
  
## <a name="remarks"></a>Açıklamalar  
 Bir hizmet tarafından kullanılan bağlamalardan hiçbiri Kullanıcı adı/parola tabanlı kimlik doğrulaması için yapılandırılmamışsa, bu öğenin öznitelikleri yok sayılır. Bunlar, `customUserNamePasswordValidatorType`, ve `membershipProviderName` `includeWindowsGroups` içerir`userNamePasswordValidationMode`.  
  
 Bir hizmet tarafından kullanılan bağlamalardan hiçbiri Kullanıcı adı/parola için Windows kimlik doğrulaması kullanmak üzere yapılandırılmamışsa, oturum açma belirteçlerini önbelleğe alma ile ilgili ayarlar yoksayılır. Bunlar, ve `cacheLogonTokenLifetime` `cacheLogonTokens`içerir. `maxCacheLogonTokens`  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Configuration.UserNameServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>
