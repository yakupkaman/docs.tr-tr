---
title: 'Nasıl yapılır: GroupBox Şablonu Tanımlama'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], GroupBox
- GroupBox control [WPF], creating templates
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
ms.openlocfilehash: dd53af87ec2d12b2ed0dcf2b23374d76e8f631a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910526"
---
# <a name="how-to-define-a-groupbox-template"></a>Nasıl yapılır: GroupBox Şablonu Tanımlama
Bu örnek için bir şablonun nasıl oluşturulacağını gösterir. bir <xref:System.Windows.Controls.GroupBox> denetimi.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnekte tanımlayan bir <xref:System.Windows.Controls.GroupBox> denetim şablonu kullanarak bir <xref:System.Windows.Controls.Grid> denetim düzeni için. Şablonu kullanan bir <xref:System.Windows.Controls.BorderGapMaskConverter> kenarlığını tanımlamak için <xref:System.Windows.Controls.GroupBox> kenarlık getirmeyecek böylece <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> içeriği.  
  
 [!code-xaml[GroupBoxSnippet#GroupBoxTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Controls.GroupBox>
- [Nasıl yapılır: Bir grup oluşturun](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748321(v=vs.90))
