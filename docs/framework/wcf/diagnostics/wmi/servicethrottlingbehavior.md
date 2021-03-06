---
title: ServiceThrottlingBehavior
ms.date: 03/30/2017
ms.assetid: 37b9e517-1f1f-4ec4-9fcb-2b8016794f5b
ms.openlocfilehash: 572e458f08c4717207667db9940296c4a957199a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956877"
---
# <a name="servicethrottlingbehavior"></a>ServiceThrottlingBehavior
ServiceThrottlingBehavior  
  
## <a name="syntax"></a>Sözdizimi  
  
```csharp  
class ServiceThrottlingBehavior : Behavior  
{  
  sint32 MaxConcurrentCalls;  
  sint32 MaxConcurrentInstances;  
  sint32 MaxConcurrentSessions;  
};  
```  
  
## <a name="methods"></a>Yöntemler  
 Denetlemek ServiceThrottlingBehavior sınıf herhangi bir yöntemi tanımlamaz.  
  
## <a name="properties"></a>Özellikler  
 Denetlemek ServiceThrottlingBehavior sınıfı aşağıdaki özelliklere sahiptir:  
  
### <a name="maxconcurrentcalls"></a>maxConcurrentCalls  
 Veri türü: SINT32  
  
 Erişim türü: salt okunur  
  
 Bir ServiceHost tüm dağıtıcı nesneler arasında etkin bir şekilde işlenen ileti sayısı.  
  
### <a name="maxconcurrentinstances"></a>MaxConcurrentInstances  
 Veri türü: SINT32  
  
 Erişim türü: salt okunur  
  
 Aynı anda çalışabilecek hizmet nesneleri sayısı.  
  
### <a name="maxconcurrentsessions"></a>MaxConcurrentSessions  
 Veri türü: SINT32  
  
 Erişim türü: salt okunur  
  
 En fazla bir konak aynı anda kabul edebileceği oturum sayısını.  
  
## <a name="requirements"></a>Gereksinimler  
  
|MOF|Bildirilmiş Servicemodel.mof.|  
|---------|-----------------------------------|  
|Ad Alanı|İçinde tanımlı root\ServiceModel|  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
