---
title: 'Nasıl yapılır: Çok Satırlı TextBox Denetimi Oluşturma'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], multiple lines of text
ms.assetid: 05914a93-d0ea-4a9a-b693-09df7d4e2ac2
ms.openlocfilehash: 29fb4c9498fe163c36e71680242d3ef8cf98c089
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001279"
---
# <a name="how-to-create-a-multiline-textbox-control"></a>Nasıl yapılır: Çok Satırlı TextBox Denetimi Oluşturma
Bu örnek nasıl kullanılacağını gösterir [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] tanımlamak için bir <xref:System.Windows.Controls.TextBox> birden çok metin satırı uyum sağlayacak şekilde otomatik olarak genişletilecektir denetimi.  
  
## <a name="example"></a>Örnek  
 Ayarlama <xref:System.Windows.Controls.TextBox.TextWrapping%2A> özniteliğini **kaydırma** yeni bir kaydırılmasına neden olur ne zaman satır kenarı <xref:System.Windows.Controls.TextBox> denetim ulaşıldığında, otomatik olarak genişleyen <xref:System.Windows.Controls.TextBox> olursa yeni bir satır için yer dahil edilecek denetimi gerekli.  
  
 Ayarı <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> özniteliğini **true** RETURN tuşuna basıldığında, bir kez daha otomatik olarak eklenmesi için yeni bir satır neden <xref:System.Windows.Controls.TextBox> gerekirse yeni bir satır için yer eklenecek.  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> Özniteliği için bir kaydırma çubuğu ekler <xref:System.Windows.Controls.TextBox>, böylece içeriğini <xref:System.Windows.Controls.TextBox> değilse kaydırılabileceğini <xref:System.Windows.Controls.TextBox> veya kendisini kapsayan pencerenin boyutu genişletir.  
  
 [!code-xaml[TextBox_MiscCode#_MultilineTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.TextWrapping>
- [TextBox Genel Bakış](textbox-overview.md)
- [RichTextBox Genel Bakış](richtextbox-overview.md)
