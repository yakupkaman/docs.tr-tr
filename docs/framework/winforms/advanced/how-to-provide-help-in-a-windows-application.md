---
title: 'Nasıl yapılır: Bir Windows Uygulamasında Yardım Sağlama'
ms.date: 03/30/2017
helpviewer_keywords:
- Help [Windows Forms], Windows applications
- HTML Help [Windows Forms], Windows Forms
- Windows applications [Windows Forms], providing Help
- HelpProvider component [Windows Forms]
- forms [Windows Forms], providing Help
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
ms.openlocfilehash: 2f9c0a9791db28cebd055ca446fdff16b9e276a4
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959616"
---
# <a name="how-to-provide-help-in-a-windows-application"></a>Nasıl yapılır: Bir Windows Uygulamasında Yardım Sağlama

Yapabileceğiniz kullanım <xref:System.Windows.Forms.HelpProvider> Yardım konuları için bir Yardım dosyası içinde Windows Forms özel denetimlerinde eklemeye bileşeni. Yardım dosyasında, HTML veya HTMLHelp olabilir 1.x veya büyük biçimi.

## <a name="provide-help"></a>Yardım sağlama

1. Visual Studio'da gelen **araç kutusu**, sürükleyin bir <xref:System.Windows.Forms.HelpProvider> formunuza bileşen.

     Bileşen Tepsisi Windows Form Tasarımcısı'nın altındaki yer alacaktır.

2. İçinde **özellikleri** penceresinde <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> özelliğini .chm, .col veya .htm Yardım dosya.

3. Formunuzda kullandığınız ve buna başka bir denetim seçin **özellikleri** penceresinde <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> özelliği.

     Geçirilen dize budur <xref:System.Windows.Forms.HelpProvider> Yardım dosyanıza uygun bir Yardım konusuna Göndereceğim bileşen.

4. İçinde **özellikleri** penceresinde <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> bir değere <xref:System.Windows.Forms.HelpNavigator> sabit listesi.

     Bu yolla belirler **HelpKeyword** özelliği Yardım sistemine geçirilir. Aşağıdaki tabloda, olası ayarlar ve açıklamalarının gösterir.

    |Üye Adı|Açıklama|
    |-----------------|-----------------|
    |AssociateIndex|Belirtilen bir konu için bir dizin belirtilen URL'de yapılacağını belirtir.|
    |Bul|Belirtilen URL'nin arama sayfası görüntüleneceğini belirtir.|
    |Dizin|Belirtilen URL dizinini görüntüleneceğini belirtir.|
    |KeywordIndex|Aramak için bir anahtar sözcüğü ve belirtilen URL'de gerçekleştirilecek eylemi belirtir.|
    |TableOfContents|1.0 HTML Yardım dosyasının İçindekiler görüntüleneceğini belirtir.|
    |Konu|Belirtilen URL tarafından başvurulan konu görüntüleneceğini belirtir.|

 F1 tuşuna basarak çalışma zamanında olduğunda denetimi — hangi ayarladığınız için **HelpKeyword** ve **HelpNavigator** özellikleri — sahip odak ile ilişkili Yardım dosyasını açtığınızda <xref:System.Windows.Forms.HelpProvider> bileşeni.

 Şu anda **HelpNamespace** özelliği Yardım dosyalarını aşağıdaki üç formatta destekler: HTMLHelp 1.x HTMLHelp 2.0 ve HTML. Bu nedenle, ayarlayabileceğiniz **HelpNamespace** özelliği için bir Web sayfası gibi bir http:// adresi. Bu yapıldığında, içinde belirtilen dize ile Web sayfası için varsayılan tarayıcı açılır **HelpKeyword** yer işareti kullanılan özellik. Bağlantı, belirli bir parçası için bir HTML sayfasına atlamak için kullanılır.

> [!IMPORTANT]
> Uygulamanızda kullanmadan önce bir istemciden gönderilen herhangi bir bilgi denetlemek dikkatli olun. Kötü amaçlı kullanıcılara veya yürütülebilir komut dosyası, SQL deyimleri ya da diğer kod ekleme göndermeye. Bir kullanıcının giriş görüntülemek, bir veritabanında saklamak veya onunla çalışan önce olmayabilecek bilgi içermiyor denetleyin. Bir normal bir şekilde denetlemek için anahtar sözcükler "BETİK" gibi bir kullanıcıdan giriş aldığınızda aramak için normal bir ifade kullanmaktır.

Ayrıca <xref:System.Windows.Forms.HelpProvider> açılır Yardım, Yardım dosyaları, Windows Forms'da denetimleri için görüntüleyecek şekilde yapılandırılmış olsa bile göstermek için bileşeni. Daha fazla bilgi için [nasıl yapılır: Açılır Yardımı görüntüleme](how-to-display-pop-up-help.md).

## <a name="see-also"></a>Ayrıca bkz.

- [Nasıl yapılır: Açılır Yardımı görüntüleme](how-to-display-pop-up-help.md)
- [ToolTips Kullanarak Denetim Yardımı](control-help-using-tooltips.md)
- [Windows Forms'ta Kullanıcı Yardımını Tümleştirme](integrating-user-help-in-windows-forms.md)
- [Windows Forms](../index.md)
