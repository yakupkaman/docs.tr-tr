---
title: '@ServiceHost'
ms.date: 03/30/2017
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
ms.openlocfilehash: fdd6d83836c4ef31a4d7c8e68cb0cc050ac6bea4
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76787797"
---
# <a name="servicehost"></a>\@ServiceHost

Barındırılan hizmet ile hizmet ana bilgisayarını oluşturmak için kullanılan fabrikası ve. svc dosyasında belirtilen barındırma koduna erişmek veya derlemek için gereken diğer programlama yönlerini ilişkilendirir.

## <a name="syntax"></a>Sözdizimi

```xml
<% @ServiceHost
Service = "Service, ServiceNamespace"
Factory = "Factory, FactoryNamespace"
Debug = "Debug"
Language = "Language"
CodeBehind = "CodeBehind"
%>
```

## <a name="attributes"></a>{1&gt;{2&gt;Öznitelikler&lt;2}&lt;1}

### <a name="service"></a>Hizmet

Barındırılan hizmetin CLR türü adı. Bu, bir veya daha fazla hizmet kişilerini uygulayan bir türün tam adı olmalıdır.

### <a name="factory"></a>Çar

Hizmet ana bilgisayarının örneğini oluşturmak için kullanılan hizmet ana bilgisayar fabrikasının CLR tür adı. Bu öznitelik isteğe bağlıdır. Belirtilmemişse, varsayılan <xref:System.ServiceModel.Activation.ServiceHostFactory> kullanılır ve bu bir <xref:System.ServiceModel.ServiceHost>örneğini döndürür.

### <a name="debug"></a>Hata ayıklama

Windows Communication Foundation (WCF) hizmetinin hata ayıklama sembolleriyle derlenmesi gerekip gerekmediğini belirtir. WCF hizmetinin hata ayıklama simgeleriyle derlenmesi gerekiyorsa `true`; Aksi takdirde, `false`.

### <a name="language"></a>Dil

Dosya (. svc) içindeki tüm satır içi kodları derlerken kullanılan dili belirtir. Değerler herhangi birini temsil edebilir. Sırasıyla, Visual Basic ve JScript .NET 'e C#başvuran `C#`, `VB`ve `JS`dahil olmak üzere net destekli dil. Bu öznitelik isteğe bağlıdır.

### <a name="codebehind"></a>CodeBehind

XML Web hizmetini uygulayan sınıf aynı dosyada yer almıyor ve bir derlemeye derlenmediği ve *\Bin* dizinine YERLEŞTIRILEBILECEK olan XML Web hizmetini uygulayan kaynak dosyayı belirtir.

## <a name="remarks"></a>Açıklamalar

Hizmeti barındırmak için kullanılan <xref:System.ServiceModel.ServiceHost>, Windows Communication Foundation (WCF) programlama modeli içindeki bir genişletilebilirlik noktasıdır. Bir fabrika deseninin, büyük olasılıkla barındırma ortamının doğrudan örneği bulunmayan çok biçimli bir tür olduğu için <xref:System.ServiceModel.ServiceHost> örneğini oluşturmak için kullanılır.

Varsayılan uygulama, <xref:System.ServiceModel.ServiceHost>örneğini oluşturmak için <xref:System.ServiceModel.Activation.ServiceHostFactory> kullanır. Ancak, `@ServiceHost` yönergesinde fabrika uygulamanızın CLR türü adını belirterek kendi fabrikanızı (türetilmiş ana bilgisayarınızı döndüren bir tane) sağlayabilirsiniz.

Varsayılan fabrika yerine kendi özel hizmet ana bilgisayar fabrikasını kullanmak için, tür adını `@ServiceHost` yönergesinde aşağıdaki gibi sağlamanız yeterlidir.

```xml
<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>
```

Fabrika uygulamalarını mümkün olduğunca ışık olarak tutun. Çok sayıda özel mantığa sahipseniz, bu mantığı fabrika yerine ana bilgisayarınıza yerleştirirseniz, kodunuz daha yeniden kullanılabilir.

Örneğin, `MyService`için AJAX özellikli bir uç noktayı etkinleştirmek üzere, aşağıdaki örnekte gösterildiği gibi, `@ServiceHost` yönergesinde varsayılan <xref:System.ServiceModel.Activation.ServiceHostFactory>yerine `Factory` özniteliğinin değeri için <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> belirtin:

```xml
<% @ServiceHost
Service="MyService"
Language="C#"
Debug="true"
Factory="WebScriptServiceHostFactory"
%>
```

## <a name="see-also"></a>Ayrıca bkz.

- [Özel Hizmet Konağı](../../../wcf/samples/custom-service-host.md)
