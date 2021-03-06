---
title: "Nasıl yapılır: Salt Okunur Freezable'ın Yazılabilir Kopyasını Edinme"
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cloning Freezable objects [WPF]
- Freezable objects [WPF], modifiable clones
ms.assetid: d028de61-bbe9-4d62-b656-8fe3b1b2ca24
ms.openlocfilehash: 910c5dada6ca82f68992722e4df6b35f9f7497c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942798"
---
# <a name="how-to-obtain-a-writable-copy-of-a-read-only-freezable"></a>Nasıl yapılır: Salt Okunur Freezable'ın Yazılabilir Kopyasını Edinme
Bu örnek nasıl kullanılacağını gösterir <xref:System.Windows.Freezable.Clone%2A> salt okunur'ın yazılabilir kopyasını oluşturmak için gereken yöntemini <xref:System.Windows.Freezable>.  
  
 Sonra bir <xref:System.Windows.Freezable> nesne işaretlenmiş salt okunur ("dondurulmuş"), onu değiştiremezsiniz. Ancak, kullanabileceğiniz <xref:System.Windows.Freezable.Clone%2A> donmuş nesnesi değiştirilebilir bir kopyasını oluşturmak için yöntemi.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, dondurulmuş değiştirilebilir kopyasını oluşturur. <xref:System.Windows.Media.SolidColorBrush> nesne.  
  
 [!code-csharp[freezablesample_procedural#CloneExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
 Hakkında daha fazla bilgi için <xref:System.Windows.Freezable> nesneleri bkz [Freezable nesnelerine genel bakış](freezable-objects-overview.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Freezable>
- <xref:System.Windows.Freezable.CloneCurrentValue%2A>
- [Freezable Nesnelerine Genel Bakış](freezable-objects-overview.md)
- [Nasıl Yapılır Konuları](base-elements-how-to-topics.md)
