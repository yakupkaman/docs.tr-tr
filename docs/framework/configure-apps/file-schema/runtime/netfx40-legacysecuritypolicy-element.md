---
title: <NetFx40_LegacySecurityPolicy> Öğesi
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_LegacySecurityPolicy> element
- NetFx40_LegacySecurityPolicy element
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
ms.openlocfilehash: d5192eb56bb8b640544bdc52a0bb9d8a5277efef
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73116247"
---
# <a name="netfx40_legacysecuritypolicy-element"></a>\<NetFx40_LegacySecurityPolicy > öğesi

Çalışma zamanının eski kod erişim güvenliği (CAS) ilkesi kullanıp kullanmadığını belirtir.

[ **\<configuration >** ](../configuration-element.md) \
&nbsp; &nbsp;[ **\<runtime >** ](runtime-element.md) \
&nbsp;&nbsp;&nbsp;&nbsp; **\<NetFx40_LegacySecurityPolicy >**  

## <a name="syntax"></a>Sözdizimi

```xml
<NetFx40_LegacySecurityPolicy
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler

Öznitelikler, alt ve üst öğeler aşağıdaki bölümlerde açıklanmaktadır.

### <a name="attributes"></a>Öznitelikler

|Öznitelik|Açıklama|
|---------------|-----------------|
|`enabled`|Gerekli öznitelik.<br /><br /> Çalışma zamanının eski CAS ilkesini kullanıp kullanmadığını belirtir.|

## <a name="enabled-attribute"></a>etkin Öznitelik

|Değer|Açıklama|
|-----------|-----------------|
|`false`|Çalışma zamanı eski CAS ilkesini kullanmaz. Bu varsayılandır.|
|`true`|Çalışma zamanı eski CAS ilkesini kullanır.|

### <a name="child-elements"></a>Alt Öğeler

Yok.

### <a name="parent-elements"></a>Üst Öğeler

|Öğe|Açıklama|
|-------------|-----------------|
|`configuration`|Her yapılandırma dosyasında yer alan ve ortak dil çalışma zamanı ve .NET Framework uygulamaları tarafından kullanılan kök öğe.|
|`runtime`|Çalışma zamanı başlatma seçenekleri hakkında bilgi içerir.|

## <a name="remarks"></a>Açıklamalar

.NET Framework sürüm 3,5 ve önceki sürümlerde CAS ilkesi her zaman etkindir. .NET Framework 4 ' te CAS ilkesinin etkinleştirilmiş olması gerekir.

CAS ilkesi sürüme özgüdür. .NET Framework önceki sürümlerinde bulunan özel CA ilkelerinin .NET Framework 4 ' te önceden belirtilmesi gerekir.

`<NetFx40_LegacySecurityPolicy>` öğesinin bir .NET Framework 4 derlemesine uygulanması, [güvenlik açısından saydam kodu](../../../misc/security-transparent-code.md)etkilemez; Saydamlık kuralları hala geçerlidir.

> [!IMPORTANT]
> `<NetFx40_LegacySecurityPolicy>` öğesinin uygulanması, [genel derleme önbelleğinde](../../../app-domains/gac.md)yüklü olmayan [Yerel Görüntü Oluşturucu (Ngen. exe)](../../../tools/ngen-exe-native-image-generator.md) tarafından oluşturulan yerel görüntü derlemeleri için önemli performans cezalarıyla sonuçlanabilir. Performans düşüşü, çalışma zamanının öznitelik uygulandığında derlemeleri yerel görüntü olarak yüklemesi nedeniyle oluşur ve bu, tam zamanında derlemeler olarak yüklenmekte olur.

> [!NOTE]
> Visual Studio projeniz için proje ayarları içindeki .NET Framework 4 ' ten daha eski bir hedef .NET Framework sürümünü belirtirseniz, bu sürüm için belirttiğiniz özel CAS ilkeleri de dahil olmak üzere CAS ilkesi etkinleştirilir. Ancak, yeni .NET Framework 4 türlerini ve üyelerini kullanamazsınız. Ayrıca, [uygulama yapılandırma dosyanızdaki](../../index.md)başlangıç ayarları şemasında [\<supportedRuntime > öğesini](../startup/supportedruntime-element.md) kullanarak .NET Framework önceki bir sürümünü de belirtebilirsiniz.

> [!NOTE]
> Yapılandırma dosyası söz dizimi büyük/küçük harfe duyarlıdır. Söz dizimini sözdizimi ve örnek bölümlerinde belirtilen şekilde kullanmanız gerekir.

## <a name="configuration-file"></a>Yapılandırma Dosyası

Bu öğe yalnızca uygulama yapılandırma dosyasında kullanılabilir.

## <a name="example"></a>Örnek

Aşağıdaki örnekte, bir uygulama için eski CAS ilkesinin nasıl etkinleştirileceği gösterilmektedir.

```xml
<configuration>
   <runtime>
      <NetFx40_LegacySecurityPolicy enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>Ayrıca bkz.

- [Çalışma Zamanı Ayarları Şeması](index.md)
- [Yapılandırma Dosyası Şeması](../index.md)
