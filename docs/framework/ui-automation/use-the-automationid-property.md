---
title: AutomationID Özelliğini Kullanma
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutomationId property
- UI Automation, AutomationId property
- properties, AutomationId
ms.assetid: a24e807b-d7c3-4e93-ac48-80094c4e1c90
ms.openlocfilehash: a07a9c9bf6b0bf1e2f8ce56653a90a3aad3c4b2f
ms.sourcegitcommit: 9a97c76e141333394676bc5d264c6624b6f45bcf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75741383"
---
# <a name="use-the-automationid-property"></a>AutomationID Özelliğini Kullanma
> [!NOTE]
> Bu belge, <xref:System.Windows.Automation> ad alanında tanımlanan yönetilen [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sınıflarını kullanmak isteyen .NET Framework geliştiricilere yöneliktir. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]hakkında en son bilgiler için bkz. [Windows Otomasyonu API: UI Otomasyonu](/windows/win32/winauto/entry-uiauto-win32).  
  
 Bu konu, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ağaç içindeki bir öğeyi bulmak için <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> nasıl ve ne zaman kullanılabileceğini gösteren senaryolar ve örnek kod içerir.  
  
 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>, bir UI Otomasyon öğesini eşlerinden bağımsız olarak tanımlar. Denetim kimliğiyle ilgili özellik tanımlayıcıları hakkında daha fazla bilgi için bkz. [UI Automation özelliklerine genel bakış](ui-automation-properties-overview.md).  
  
> [!NOTE]
> <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> ağaç genelinde benzersiz bir kimliği garanti etmez; genellikle kapsayıcı ve kapsam bilgilerinin yararlı olması gerekir. Örneğin, bir uygulama birden çok üst düzey menü öğesi olan bir menü denetimi içerebilir, buna karşılık birden çok alt menü öğesi vardır. Bu ikincil menü öğeleri, "Item1", "Item 2" gibi genel bir düzen tarafından tanımlanabilir ve üst düzey menü öğelerinde alt öğeler için yinelenen tanımlayıcılara izin verebilir.  
  
## <a name="scenarios"></a>Senaryolar  
 Öğeleri ararken doğru ve tutarlı sonuçlar elde etmek için <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> kullanımını gerektiren üç birincil UI Otomasyonu istemci uygulama senaryosu belirlenmiştir.  
  
> [!NOTE]
> <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>, en üst düzey uygulama pencereleri hariç denetim görünümündeki tüm UI Otomasyon öğeleri, bir ID veya x:Uid olmayan [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] denetimlerinden türetilmiş Kullanıcı Arabirimi Otomasyonu öğeleri ve bir denetim KIMLIĞINE sahip olmayan Win32 denetimlerinden türetilmiş UI Otomasyonu öğeleri tarafından desteklenir.  
  
#### <a name="use-a-unique-and-discoverable-automationid-to-locate-a-specific-element-in-the-ui-automation-tree"></a>UI Otomasyon ağacındaki belirli bir öğeyi bulmak için benzersiz ve bulunabilir bir AutomationId kullanın  
  
- İlgilendiğiniz bir [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] öğesinin <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> raporlamak için UI Spy gibi bir araç kullanın. Bu değer daha sonra, sonraki otomatikleştirilmiş test için test betiği gibi bir istemci uygulamasına kopyalanabilir ve yapıştırılabilir. Bu yaklaşım, çalışma zamanında bir öğeyi tanımlamak ve bulmak için gereken kodu azaltır ve basitleştirir.  
  
> [!CAUTION]
> Genel olarak, <xref:System.Windows.Automation.AutomationElement.RootElement%2A>yalnızca doğrudan alt öğelerini almaya çalışırsınız. Alt öğeler için arama yüzlerce veya hatta binlerce öğe aracılığıyla yineleyebilir ve muhtemelen yığın taşmasına neden olabilir. Daha düşük bir düzeyde belirli bir öğe edinmeye çalışıyorsanız, aramanızı uygulama penceresinden veya bir kapsayıcıdan daha düşük bir düzeyde başlatmanız gerekir.  
  
 [!code-csharp[UIAAutomationID_snip#100](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#100)]
 [!code-vb[UIAAutomationID_snip#100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#100)]  
  
#### <a name="use-a-persistent-path-to-return-to-a-previously-identified-automationelement"></a>Daha önce tanımlanan bir AutomationElement öğesine dönmek için kalıcı bir yol kullanın  
  
- Basit test betiklerinden güçlü kayıt ve kayıttan yürütme yardımcı programlarına istemci uygulamaları, dosya açma iletişim kutusu veya menü öğesi gibi şu anda örneği bulunmayan öğelere erişim gerektirebilir ve bu nedenle UI Otomasyon ağacında yok. Bu öğeler yalnızca bir çoğaltma veya "kayıttan yürütme" ile örnek olarak, AutomationId, Denetim desenleri ve olay dinleyicileri gibi UI Otomasyon özelliklerinin kullanımı aracılığıyla belirli bir Kullanıcı Arabirimi eylemleri dizisi aracılığıyla oluşturulabilir.
  
 [!code-csharp[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#uiaworkerthread)]
 [!code-vb[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#uiaworkerthread)]  
[!code-csharp[UIAAutomationID_snip#Playback](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#playback)]
[!code-vb[UIAAutomationID_snip#Playback](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#playback)]  
  
#### <a name="use-a-relative-path-to-return-to-a-previously-identified-automationelement"></a>Daha önce tanımlanan bir AutomationElement öğesine dönmek için göreli yol kullanın  
  
- Bazı durumlarda, AutomationId yalnızca eşdüzey öğeler arasında benzersiz olduğundan garantilenmiş olduğundan, UI Otomasyon ağacındaki birden çok öğe aynı AutomationId özellik değerlerine sahip olabilir. Bu durumlarda, öğeler bir üst öğeye göre benzersiz şekilde tanımlanabilir ve gerekirse, bir üst öğe. Örneğin, bir geliştirici birden çok alt menü öğesi olan, her biri "Item1", "Item2" gibi sıralı AutomationId ile tanımlanmış olan birden çok menü öğesiyle bir menü çubuğu sağlayabilir. Daha sonra her menü öğesi, kendi AutomationId 'si ile birlikte kendi üst öğesinin AutomationId 'si ile ve gerekirse kendi üst öğesi ile benzersiz şekilde tanımlanabilir.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>
- [UI Otomasyon Ağacına Genel Bakış](ui-automation-tree-overview.md)
- [Özellik Koşulunu Temel Alan UI Otomasyonu Öğesi Bulma](find-a-ui-automation-element-based-on-a-property-condition.md)
