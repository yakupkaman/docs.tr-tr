---
title: 'Nasıl yapılır: Windows Hizmetleri Oluşturma'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, creating
- templates, Windows Service
ms.assetid: 0f5e2cbb-d95d-477c-b2b5-4b990e6b86ff
author: ghogen
ms.openlocfilehash: 514675b3c3ce1f6701dff571361df672fb520c6a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053668"
---
# <a name="how-to-create-windows-services"></a>Nasıl yapılır: Windows Hizmetleri Oluşturma
Bir hizmet oluşturduğunuzda, **Windows hizmeti**adlı bir Visual Studio proje şablonu kullanabilirsiniz. Bu şablon uygun sınıflara ve ad alanlarına başvurarak, hizmetler için temel sınıftan devralmayı ayarlayarak ve büyük olasılıkla geçersiz kılmak istediğiniz yöntemlerin birkaçını geçersiz kılarak sizin için işin çoğunu otomatik olarak yapar.  
  
> [!WARNING]
> Windows Hizmetleri proje şablonu, Visual Studio 'nun Express sürümünde kullanılamaz.  
  
 Bir işlevsel hizmet oluşturmak için en azından şunları yapmanız gerekir:  
  
- <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> Özelliği ayarlayın.  
  
- Hizmet uygulamanız için gerekli yükleyicileri oluşturun.  
  
- Hizmetinizin davranışını özelleştirmek için <xref:System.ServiceProcess.ServiceBase.OnStart%2A> ve <xref:System.ServiceProcess.ServiceBase.OnStop%2A> yöntemlerinin kodunu geçersiz kılın ve belirtin.  
  
### <a name="to-create-a-windows-service-application"></a>Bir Windows hizmet uygulaması oluşturmak için  
  
1. Bir **Windows hizmeti** projesi oluşturun.  
  
    > [!NOTE]
    > Şablon kullanmadan bir hizmet yazma yönergeleri için bkz [. nasıl yapılır: Hizmetleri programlı olarak](how-to-write-services-programmatically.md)yazın.  
  
2. **Özellikler** penceresinde hizmetinizin <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> özelliğini ayarlayın.  
  
     ![ServiceName özelliğini ayarlayın.](./media/windowsservice-servicename.PNG "WindowsService_ServiceName")  
  
    > [!NOTE]
    > <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> Özelliğin değeri her zaman yükleyici sınıflarında kaydedilen adla eşleşmelidir. Bu özelliği değiştirirseniz, yükleyici sınıflarının <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> özelliğini de güncelleştirmeniz gerekir.  
  
3. Hizmetinizin nasıl çalışacağını öğrenmek için aşağıdaki özelliklerden herhangi birini ayarlayın.  
  
    |Özellik|Ayar|  
    |--------------|-------------|  
    |<xref:System.ServiceProcess.ServiceBase.CanStop%2A>|`True`hizmetin çalışmayı durdurmak için istekleri kabul edeceğini belirtmek için; `false` hizmetin durdurulmasını engellemek için.|  
    |<xref:System.ServiceProcess.ServiceBase.CanShutdown%2A>|`True`hizmetin, yaşadığı bilgisayar kapandığında bildirim almak istediğini göstermek için, <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> yordamı çağırabileceği şekilde etkinleştirir.|  
    |<xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A>|`True`hizmetin çalışmayı duraklatmak veya çalışmaya devam etmek için istekleri kabul edeceğini belirtmek için; `false` hizmetin duraklatılmasını ve devam ettirmasını engellemek için.|  
    |<xref:System.ServiceProcess.ServiceBase.CanHandlePowerEvent%2A>|`True`hizmetin bilgisayarın güç durumundaki değişikliklerin bildirimini işleyebileceğini belirtmek için; `false` hizmetin bu değişiklikler hakkında bildirilmesini engellemek için.|  
    |<xref:System.ServiceProcess.ServiceBase.AutoLog%2A>|`True`Hizmetiniz bir eylem gerçekleştirdiğinde Uygulama olay günlüğü 'ne bilgilendirici girişler yazmak için; `false` bu işlevi devre dışı bırakmak için. Daha fazla bilgi için [nasıl yapılır: Hizmetlerle](how-to-log-information-about-services.md)ilgili bilgileri günlüğe kaydedin. **Not:**  Varsayılan olarak, <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> olarak `true`ayarlanır.|  
  
    > [!NOTE]
    > Veya olarak ayarlandığında, **hizmet denetimi Yöneticisi** hizmeti durdurmak, duraklatmak veya devam ettirmek için ilgili menü seçeneklerini devre dışı bırakır. `false` <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> <xref:System.ServiceProcess.ServiceBase.CanStop%2A>  
  
4. Kod düzenleyicisine erişin ve <xref:System.ServiceProcess.ServiceBase.OnStart%2A> <xref:System.ServiceProcess.ServiceBase.OnStop%2A> yordamları için istediğiniz işlemeyi girin.  
  
5. İşlevselliği tanımlamak istediğiniz diğer yöntemleri geçersiz kılın.  
  
6. Hizmet uygulamanız için gerekli yükleyicileri ekleyin. Daha fazla bilgi için [nasıl yapılır: Hizmet uygulamanıza](how-to-add-installers-to-your-service-application.md)yükleyicileri ekleyin.  
  
7. **Build** menüsünden **Build Solution** ' i seçerek projenizi oluşturun.  
  
    > [!NOTE]
    > Projenizi çalıştırmak için F5 tuşuna basmayın; bir hizmet projesini bu şekilde çalıştıramazsınız.  
  
8. Hizmetini yükleyin. Daha fazla bilgi için [nasıl yapılır: Hizmetleri](how-to-install-and-uninstall-services.md)yükleme ve kaldırma.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Windows Hizmeti Uygulamalarına Giriş](introduction-to-windows-service-applications.md)
- [Nasıl yapılır: Hizmetleri programlı olarak yaz](how-to-write-services-programmatically.md)
- [Nasıl yapılır: Hizmet uygulamanıza yükleyiciler ekleme](how-to-add-installers-to-your-service-application.md)
- [Nasıl yapılır: Hizmetlerle Ilgili bilgileri günlüğe kaydet](how-to-log-information-about-services.md)
- [Nasıl yapılır: Hizmetleri Başlat](how-to-start-services.md)
- [Nasıl yapılır: Hizmetler için güvenlik bağlamını belirtin](how-to-specify-the-security-context-for-services.md)
- [Nasıl yapılır: Hizmetleri yükleme ve kaldırma](how-to-install-and-uninstall-services.md)
- [İzlenecek yol: Bileşen tasarımcısında bir Windows hizmeti uygulaması oluşturma](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
