---
title: 'Nasıl yapılır: Yönetilen HTML Belgesi Nesne Modeline Erişme'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- HTML DOM [Windows Forms], accessing
- managed HTML DOM [Windows Forms], accessing
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
ms.openlocfilehash: 2a195dc6583d5a0a72bd08b66f8933f4002e879a
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487268"
---
# <a name="how-to-access-the-managed-html-document-object-model"></a>Nasıl yapılır: Yönetilen HTML Belgesi Nesne Modeline Erişme
Yönetilen HTML belgesi nesne modeli (DOM) iki tür uygulamalar arasında erişebilirsiniz:  
  
- Barındırılan yönetilen bir Windows Forms uygulaması (.exe) <xref:System.Windows.Forms.WebBrowser> denetimi. Bu iki teknoloji, ile tamamlayıcı <xref:System.Windows.Forms.WebBrowser> denetimi için kullanıcı ve belgenin mantıksal yapısını temsil eden HTML DOM sayfa görüntüleme.  
  
- Bir Windows Forms <xref:System.Windows.Forms.UserControl> Internet Explorer içinde barındırılan. Sayfayı temsil eden HTML DOM erişebilir, <xref:System.Windows.Forms.UserControl> belgenin yapısını değiştirebilir veya diğer birçok olası arasında kalıcı iletişim kutuları açmak için barındırılır.  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>DOM bir Windows Forms uygulamasından erişmek için  
  
1. Konak bir <xref:System.Windows.Forms.WebBrowser> Windows Forms uygulamanızdaki denetlemek ve izlemek için <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> olay. Denetimleri barındırma ve olaylar için izleme hakkında daha fazla bilgi için bkz [olayları](../../../standard/events/index.md).  
  
2. Alma <xref:System.Windows.Forms.HtmlDocument> erişerek geçerli sayfa için <xref:System.Windows.Forms.WebBrowser.Document%2A> özelliği <xref:System.Windows.Forms.WebBrowser> denetimi.  

### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>Internet Explorer'da barındırılan bir UserControl DOM erişmek için  
  
1. Kendi özel bir türetilmiş sınıf, oluşturmak <xref:System.Windows.Forms.UserControl> sınıfı. Daha fazla bilgi için [nasıl yapılır: Bileşik denetimler yazma](how-to-author-composite-controls.md).  
  
2. Aşağıdaki kod, yük olay işleyicisi içine yerleştirin, <xref:System.Windows.Forms.UserControl>:  
  
 [!code-csharp[AccessHTMLDOMControl#1](~/samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>Güçlü Programlama  
  
1. DOM ile kullanıldığında <xref:System.Windows.Forms.WebBrowser> denetimi, her zaman beklemesi gereken kadar <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> olaylarının erişmeyi denemeden önce <xref:System.Windows.Forms.WebBrowser.Document%2A> özelliği <xref:System.Windows.Forms.WebBrowser> denetimi. <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> Tüm belgeyi yüklendikten sonra olayı oluşturulur; daha önce DOM kullanırsanız, uygulamanızda bir çalışma zamanı özel durumuna neden risk.  
  
## <a name="net-framework-security"></a>.NET Framework Güvenliği  
  
1. Uygulamanızı veya <xref:System.Windows.Forms.UserControl> yönetilen HTML DOM erişmek için tam güven gerektirir ClickOnce kullanarak bir Windows Forms uygulaması dağıtıyorsanız, tam güven izni yükseltme ya da güvenilir uygulama dağıtımı kullanarak talep edebilir; bkz: [ClickOnce uygulamalarının güvenliğini sağlama](/visualstudio/deployment/securing-clickonce-applications) Ayrıntılar için.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Yönetilen HTML Belgesi Nesne Modelini Kullanma](using-the-managed-html-document-object-model.md)
