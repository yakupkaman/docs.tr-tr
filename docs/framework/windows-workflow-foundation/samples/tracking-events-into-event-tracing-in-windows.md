---
title: Windows'ta Olay İzleme ile Olayları İzleme
ms.date: 03/30/2017
ms.assetid: f812659b-0943-45ff-9430-4defa733182b
ms.openlocfilehash: 2c397bcfa809a1306e9c31bf3f652b055d997f38
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/09/2020
ms.locfileid: "77094585"
---
# <a name="tracking-events-into-event-tracing-in-windows"></a>Windows'ta Olay İzleme ile Olayları İzleme

Bu örnek, bir iş akışı hizmetinde Windows Workflow Foundation (WF) izlemenin nasıl etkinleştirileceğini ve izleme olaylarının Windows için olay Izleme 'ye (ETW) nasıl görüntüleneceğini gösterir. İş akışı izleme kayıtlarını ETW 'ye yaymak için örnek ETW izleme katılımcısını (<xref:System.Activities.Tracking.EtwTrackingParticipant>) kullanır.

Örnekteki iş akışı bir istek alır, girdi verilerinin tersini giriş değişkenine atar ve istemciye geri dönüş döndürür. Giriş verileri 0 olduğunda, bu, iş akışının iptal edilmesine neden olan işlenmemiş bir sıfıra bölme özel durumu oluşur. İzleme etkinken, hata izleme kaydı ETW 'ye yayılır ve bu, daha sonra hatanın giderilmesine yardımcı olabilir. ETW izleme katılımcısı, kayıtları izlemeye abone olmak için bir izleme profili ile yapılandırılır. İzleme profili, Web. config dosyasında tanımlanır ve ETW izleme katılımcısı için bir yapılandırma parametresi olarak sağlanır. ETW izleme katılımcısı, iş akışı hizmetinin Web. config dosyasında yapılandırılır ve hizmet olarak hizmet davranışı olarak uygulanır. Bu örnekte, Olay Görüntüleyicisi kullanarak olay günlüğündeki izleme olaylarını görüntüleyebilirsiniz.

## <a name="workflow-tracking-details"></a>İş akışı Izleme ayrıntıları

Windows Workflow Foundation, bir iş akışı örneğinin yürütülmesini izlemek için bir izleme altyapısı sağlar. İzleme çalışma zamanı, iş akışı kullanım ömrü, iş akışı etkinliklerinin olayları ve özel etkinliklerle ilgili olayları göstermek için bir iş akışı örneği oluşturur. Aşağıdaki tabloda izleme altyapısının birincil bileşenleri ayrıntılı olarak verilmiştir.

|Bileşen|Açıklama|
|---------------|-----------------|
|Çalışma zamanını izleme|İzleme kayıtlarını yaymakta olan altyapıyı sağlar.|
|Katılımcıları izleme|İzleme kayıtlarına erişir. [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)], izleme kayıtlarını Windows için olay Izleme (ETW) olayları olarak yazan bir izleme katılımcılarıyla birlikte gelir.|
|İzleme profili|Bir iş akışı örneğinden yayılan izleme kayıtlarının bir alt kümesi için bir izleme katılımcısının abone olmasına izin veren bir filtreleme mekanizması.|

Aşağıdaki tabloda iş akışı çalışma zamanının yaydığı izleme kayıtlarının ayrıntıları verilmiştir.

|İzleme kaydı|Açıklama|
|---------------------|-----------------|
|İş akışı örneği izleme kayıtları.|İş akışı örneğinin yaşam döngüsünü açıklar. Örneğin, iş akışı başladığında veya tamamlandığında bir örnek kayıt yayınlanır.|
|Etkinlik durumu izleme kayıtları.|Ayrıntıları etkinlik yürütmesi. Bu kayıtlar, bir etkinliğin zamanlandığı veya etkinliğin ne zaman tamamlandığı ya da bir hata oluşturulduğu zaman gibi bir iş akışı etkinliğinin durumunu gösterir.|
|Bookmark sürdürme kaydı.|Bir iş akışı örneği içindeki bir yer işareti kaldığı zaman yayınlanır.|
|Özel izleme kayıtları.|Bir iş akışı yazarı özel izleme kayıtları oluşturabilir ve bunları özel etkinlik içinde yayabilir.|
|<xref:System.Activities.Tracking.ActivityScheduledRecord>|Bir etkinlik başka bir etkinliği zamanlıyor ise bu kayıt yayınlanır.|
|<xref:System.Activities.Tracking.FaultPropagationRecord>|Bu kayıt, bir etkinliğin bir hata yayıldığında yayılır.|
|<xref:System.Activities.Tracking.CancelRequestedRecord>|Bu kayıt, bir etkinlik başka bir etkinlik tarafından iptal edildiğinde yayınlanır.|

İzleme, izleme profilleri kullanılarak, yayılan izleme kayıtlarının bir alt kümesi için abone olur. Bir izleme profili, belirli bir izleme kayıt türü için abone 'e izin veren izleme sorguları içerir. İzleme profilleri kodda veya yapılandırmada belirtilebilir.

#### <a name="to-use-this-sample"></a>Bu örneği kullanmak için

1. Visual Studio 2010 kullanarak EtwTrackingParticipantSample. sln çözüm dosyasını açın.

2. Çözümü derlemek için CTRL + SHIFT + B tuşlarına basın.

3. Çözümü çalıştırmak için F5 'e basın.

    Hizmet, varsayılan olarak 53797 numaralı bağlantı noktasını (http://localhost:53797/SampleWorkflowService.xamlx)) dinler.

4. Dosya Gezgini 'ni kullanarak WCF test istemcisini açın.

    WCF Test istemcisi (WcfTestClient. exe) \<Visual Studio 2010 yükleme klasörü > \Common7\IDE\ klasöründe bulunur.

    Varsayılan Visual Studio 2010 yükleme klasörü C:\Program Files\Microsoft Visual Studio 10,0 ' dir.

5. WCF test istemcisinde **Dosya** menüsünden **Hizmet Ekle** ' yi seçin.

    Giriş kutusuna uç nokta adresini ekleyin. Varsayılan: `http://localhost:53797/SampleWorkflowService.xamlx`.

6. Olay Görüntüleyici uygulamasını açın.

    Hizmeti çağırmadan önce, **Başlat** menüsünden Olay Görüntüleyicisi başlatın, **Çalıştır** ' ı seçin ve `eventvwr.exe`yazın. Olay günlüğünün, iş akışı hizmetinden yayılan izleme olaylarını dinlediğinden emin olun.

7. Olay Görüntüleyicisi ağaç görünümünde **Olay Görüntüleyicisi**, **uygulamalar ve hizmet günlükleri**ve **Microsoft**' a gidin. Analitik ve hata ayıklama günlüklerini etkinleştirmek için **Microsoft** 'a sağ tıklayın ve **Görünüm** ' ü seçin ve ardından **analitik ve hata ayıklama günlüklerini göster**

    **Analitik ve hata ayıklama günlüklerini göster** seçeneğinin işaretli olduğundan emin olun.

8. Olay Görüntüleyicisi 'daki ağaç görünümünde **Olay Görüntüleyicisi**, **uygulamalar ve hizmetler günlükleri**, **Microsoft**, **Windows**, **uygulama sunucusu-uygulamalar**' a gidin. Analitik günlüğü etkinleştirmek için analiz ' e **sağ tıklayın ve** **günlüğü etkinleştir** ' i seçin.

9. `GetData`çift tıklayarak WCF test istemcisini kullanarak hizmeti test edin.

    Bu, `GetData` yöntemini açar. İstek bir parametre kabul eder ve değerin varsayılan değer olan 0 olmasını sağlar.

     **Çağır**' a tıklayın.

10. İş akışından yayılan olayları gözlemleyin.

    Olay Görüntüleyicisi dönün ve **Olay Görüntüleyicisi**, **uygulama ve hizmet günlükleri**, **Microsoft**, **Windows**, **uygulama sunucusu-uygulamalar**' a gidin. **Analitik** ' e sağ tıklayın ve **Yenile**' yi seçin.

    İş akışı olayları Olay Görüntüleyicisi 'nde görüntülenir. İş akışı yürütme olaylarının görüntülendiğini ve bunlardan birinin iş akışındaki hataya karşılık gelen işlenmemiş bir özel durum olduğunu unutmayın. Ayrıca, etkinliğin bir hata yaptığını gösteren bir uyarı olayı iş akışı etkinliğinden yayınlanır.

11. 9 ve 10 arasındaki adımları 0 dışında bir veri girişi ile tekrarlayın, böylece herhangi bir hata oluşturulmaz.

İzleme profilleri, iş akışı örneği durumu değiştiğinde çalışma zamanı tarafından yayılan olaylara abone olmanızı sağlar. İzleme gereksinimlerinize bağlı olarak, bir iş akışında küçük bir üst düzey durum değişikliği kümesine abone olan çok kaba bir profil oluşturabilirsiniz. Öte yandan, çıkış daha sonra yürütmeyi yeniden oluşturmak için yeterince zengin olan çok kesin bir profil oluşturabilirsiniz. Örnek, iş akışı çalışma zamanından, küçük bir olay kümesi gösteren `HealthMonitoring Tracking Profile`kullanarak ETW 'ye yayılan olayları gösterir. `Troubleshooting Tracking Profile`adlı Web. config dosyasında daha fazla iş akışı izleme olayı sağlayan farklı bir profil de sağlanır. [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] yüklendiğinde, Machine. config dosyasında boş ada sahip bir varsayılan profil yapılandırılır. Bu profil, hiçbir profil adı veya boş profil adı belirtilmediğinde ETW izleme davranışı yapılandırması tarafından kullanılır.

Sistem durumu izleme izleme profili, iş akışı örneği kayıtları ve etkinlik hatası yayma kayıtlarını yayar. Bu profil, bir Web. config yapılandırma dosyasına aşağıdaki izleme profili eklenerek oluşturulur.

```xml
<tracking>
  <profiles>
    <trackingProfile name="HealthMonitoring Tracking Profile">
      <workflow activityDefinitionId="*">
        <workflowInstanceQueries>
          <workflowInstanceQuery>
            <states>
              <state name="Started"/>
              <state name="Completed"/>
              <state name="Aborted"/>
              <state name="UnhandledException"/>
            </states>
          </workflowInstanceQuery>
        </workflowInstanceQueries>
        <faultPropagationQueries>
          <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>
        </faultPropagationQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```

 Profil, `EtwTrackingParticipant` yapılandırması aşağıdaki şekilde değiştirilerek değiştirilebilir.

```xml
<behaviors>
  <serviceBehaviors>
    <behavior>
      <etwTracking profileName="HealthMonitoring Tracking Profile"/>
    </behavior>
  </serviceBehaviors>
</behaviors>
```

#### <a name="to-clean-up-optional"></a>Temizlemek için (Isteğe bağlı)

1. Olay Görüntüleyicisi'ni açın.

2. **Olay Görüntüleyicisi**, **uygulama ve hizmet günlükleri**, **Microsoft**, **Windows**, **uygulama sunucusu-uygulamalar**' a gidin. **Analitik** öğesine sağ tıklayın ve **günlüğü devre dışı bırak**' ı seçin.

3. **Olay Görüntüleyicisi**, **uygulama ve hizmet günlükleri**, **Microsoft**, **Windows**, **uygulama sunucusu-uygulamalar**' a gidin. **Analitik** öğesine sağ tıklayın ve **Günlüğü Temizle**' yi seçin.

4. Olayları temizlemek için **Temizle** seçeneğini belirleyin.

## <a name="known-issue"></a>Bilinen sorun

> [!NOTE]
> Olay Görüntüleyicisi içinde, ETW olaylarının kodunu çözemediği bilinen bir sorun vardır. Aşağıdakine benzer bir hata iletisi görebilirsiniz.
>
> Kaynak Microsoft-Windows-uygulama sunucusu-uygulamalarından olay KIMLIĞI \<kimliği > açıklaması bulunamıyor. Bu olayı başlatan bileşen yerel bilgisayarınızda yüklü değil veya yükleme bozuk. Bileşeni yerel bilgisayara yükleyebilir veya onarabilirsiniz.
>
> Bu hatayla karşılaşırsanız, Eylemler bölmesinde Yenile ' ye tıklayın. Olay artık düzgün şekilde kod çözmelidir.

> [!IMPORTANT]
> Örnekler bilgisayarınızda zaten yüklü olabilir. Devam etmeden önce aşağıdaki (varsayılan) dizini denetleyin.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Bu dizin yoksa, tüm Windows Communication Foundation (WCF) ve [!INCLUDE[wf1](../../../../includes/wf1-md.md)] örneklerini indirmek üzere [.NET Framework 4 için Windows Communication Foundation (WCF) ve Windows Workflow Foundation (WF) örneklerine](https://www.microsoft.com/download/details.aspx?id=21459) gidin. Bu örnek, aşağıdaki dizinde bulunur.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\EtwTracking`

## <a name="see-also"></a>Ayrıca bkz.

- [AppFabric Izleme örnekleri](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))
