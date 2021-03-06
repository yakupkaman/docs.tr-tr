---
title: 108 - CustomTrackingRecordInfo
ms.date: 03/30/2017
ms.assetid: 5bee501e-4e00-42cd-b949-e88009c3d4e8
ms.openlocfilehash: 7398693208ca09aa1f9f56ef5354b86bb67f26a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052813"
---
# <a name="108---customtrackingrecordinfo"></a>108 - CustomTrackingRecordInfo
## <a name="properties"></a>Özellikler  
  
|||  
|-|-|  
|Kimliği|108|  
|anahtar sözcükler|Sorun giderme, ögesi, WFTracking UserEvents, EndToEndMonitoring,|  
|Düzey|Bilgiler|  
|Kanal|Microsoft Windows uygulama sunucusu-uygulamalar/analitik|  
  
## <a name="description"></a>Açıklama  
 İş akışı örneği içinde bir etkinlik düzeyi bilgileri ile CustomTrackingRecord içerilip bu olay tarafından ETW İzleme katılımcı yayılır.  
  
## <a name="message"></a>İleti  
 TrackRecord CustomTrackingRecord, InstanceId = = %1, RecordNumber = %2, EventTime = %3, ad = %4, ActivityName = %5, etkinlik kimliği = %6, ActivityInstanceId = %7, ActivityTypeName = %8, veri = %9, ek açıklamalar = % 10, ProfileName = % 11  
  
## <a name="details"></a>Ayrıntılar  
  
|Veri öğesi adı|Veri öğesi türü|Açıklama|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|İş akışı örnek kimliği|  
|Kayıt numarası|xs:long|Yayılan kaydın sıra numarası|  
|eventTime|xs:dateTime|Olay gösteriliyordu, UTC zamanı|  
|Ad|xs:string|CustomTrackingRecord adı|  
|activityName|xs:string|CustomTrackingRecord yayılan etkinlik adı|  
|Etkinlik Kimliği|xs:string|CustomTrackingRecord yayılan etkinliğin kimliği|  
|ActivityInstanceId|xs:string|Örnek kimliği CustomTrackingRecord yayılan etkinliği|  
|ActivityTypeName|xs:string|CustomTrackingRecord yayılan etkinlik adı|  
|Veri|xs:string|Bu olay ile izlenen verileri.  Değerlerini bir xml öğesi biçiminde depolanır \<öğeleri >\< öğe adı "dataName" type="System.String =" > dataValue\</item > \< /öğeler >.  Veri izlenecek sonra dizesini içeren \<öğeler / >. ETW olay boyutu ETW arabellek boyutu veya ETW olayı için en fazla yükü sınırlıdır. Olay boyutu ETW limitlerini sonra olay ek açıklamalar bırakarak ve veri değeri ile değiştirerek kesilmiş \<öğeleri >...  \< /öğeler >.  Aşağıdaki türleri ToString() tarafından döndürülen şekilde, değer olarak depolanır; String,char,bool,int,short,Long,uint,ushort,ulong,System.Single,float,Double,System.Guid,System.DateTimeOffset,System.DateTime.  Diğer tüm türlerin System.Runtime.Serialization.NetDataContractSerializer kullanarak serileştirilir.|  
|Ek Açıklamalar|xs:string|Bu olay için eklenen ek açıklamalar.  Değerlerini bir xml öğesi biçiminde depolanır \<öğeleri >\< öğe adı "annotationName" type="System.String =" > annotationValue\</item > \< /öğeler >.  Dize içeriyorsa hiçbir ek açıklama belirtilirse \<öğeler / >. ETW olay boyutu ETW arabellek boyutu veya ETW olayı için en fazla yükü sınırlıdır. Olay boyutu ETW limitlerini sonra olayı bırakarak ek açıklamalar ve ek açıklama değeri ile değiştirerek kesilmiş \<öğeleri >...  \< /öğeler >.|  
|profileName|xs:string|Adı veya yayılan bu olay ile sonuçlanan bir izleme profili|  
|HostReference|xs:string|Bu alan, barındırılan web hizmetleri için hizmet web hiyerarşideki benzersiz olarak tanımlar.  Biçimi olarak tanımlanan ' Web sitesi adı uygulamanın sanal yolu&#124;hizmet sanal yolu&#124;HizmetAdı ' örnek: ' Varsayılan Web sitesi/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName tarafından döndürülen dize.|
