---
title: <configuration> öğesi
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration
helpviewer_keywords:
- <configuration> element
- configuration element
- container tags, <configuration> element
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
ms.openlocfilehash: 0e09ec49024b769c516fd97085904781f64b4486
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921243"
---
# <a name="configuration-element"></a>\<Yapılandırma > öğesi

Her yapılandırma dosyasında yer alan ve ortak dil çalışma zamanı ve .NET Framework uygulamaları tarafından kullanılan kök öğe.

**\<Yapılandırma >**

## <a name="syntax"></a>Sözdizimi

```xml
<configuration>
  <!-- Configuration settings -->
</configuration>
```

## <a name="attributes"></a>Öznitelikler

Yok.

## <a name="parent-element"></a>Üst öğe

Yok.

## <a name="child-elements"></a>Alt öğeleri

|     | Açıklama |
| --- | ----------- |
| [ **\<assemblyBinding >** ](assemblybinding-element-for-configuration.md) | Yapılandırma düzeyinde derleme bağlama ilkesini belirtir.|
| [Başlangıç > ayarları şeması  **\<** ](./startup/index.md) | Başlangıç ayarları şemasındaki tüm öğeler. |
| [çalışma zamanı > ayarları şeması  **\<** ](./runtime/index.md) | Çalışma zamanı ayarları şemasındaki tüm öğeler. |
| [**System. Runtime. Remoting > ayarları şeması \<** ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/z415cf9a(v=vs.100)) | Uzaktan iletişim ayarları şemasındaki tüm öğeler. |
| [sistem .net > ayarları şeması  **\<** ](./network/index.md) | Ağ ayarları şemasındaki tüm öğeler. |
| [cryptographyısettings > ayarları şeması  **\<** ](./cryptography/index.md) | Şifre ayarları şemasındaki tüm öğeler. |
| [Yapılandırma > bölümleri şeması  **\<** ](configuration-sections-schema.md) | Yapılandırma bölümü ayarları şemasında tüm öğeler. |
| [İzleme ve Hata Ayıklama Ayarları Şeması](./trace-debug/index.md) | İzleme ve hata ayıklama ayarları şemasındaki tüm öğeler. |
| [ASP.NET yapılandırma ayarları şeması](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100)) | ASP.NET yapılandırma şemasında, ASP.NET Web siteleri ve uygulamaları yapılandırma öğelerini içeren tüm öğeler. *Web. config* dosyalarında kullanılır. |
| [WebServices > ayarları şeması  **\<** ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cctwteet(v=vs.100)) | Web Hizmetleri ayarları şemasındaki tüm öğeler. |
| [Web Ayarları Şeması](./web/index.md) | Web ayarları şemasında, ASP.NET 'in IIS gibi bir konak uygulamasıyla nasıl çalıştığını yapılandırmaya yönelik öğeler içeren tüm öğeler. *Aspnet. config* dosyalarında kullanılır. |

## <a name="remarks"></a>Açıklamalar

Her yapılandırma dosyası tam olarak bir  **\<Yapılandırma >** öğesi içermelidir.

## <a name="see-also"></a>Ayrıca bkz.

- [.NET Framework için yapılandırma dosyası şeması](index.md)
