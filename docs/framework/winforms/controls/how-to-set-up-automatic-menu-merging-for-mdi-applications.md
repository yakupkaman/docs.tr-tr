---
title: 'Nasıl yapılır: MDI Uygulamaları için Otomatik Menü Birleştirmeyi Ayarlama'
ms.date: 03/30/2017
helpviewer_keywords:
- MenuStrip [Windows Forms], merging
- Merging [Windows Forms], automatic menu
ms.assetid: 55e32cad-1141-4a56-aa33-d9543ca3d393
ms.openlocfilehash: 33e07bb655d81c6a802ebdce871a2fed845a5c96
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013029"
---
# <a name="how-to-set-up-automatic-menu-merging-for-mdi-applications"></a>Nasıl yapılır: MDI Uygulamaları için Otomatik Menü Birleştirmeyi Ayarlama
Otomatik ile Çok Belgeli Arabirim (MDI) uygulamasında birleştirmeyi ayarlamak için aşağıdaki yordamı temel adımları sunar <xref:System.Windows.Forms.MenuStrip>.  
  
### <a name="to-set-up-automatic-menu-merging"></a>Otomatik menü birleştirmeyi ayarlama  
  
1. MDI üst formunun oluşturabilmek, <xref:System.Windows.Forms.Form.IsMdiContainer%2A> özelliğini `true`.  
  
2. Ekleme bir <xref:System.Windows.Forms.MenuStrip> ayarlama MDI için kendi <xref:System.Windows.Forms.Form.MainMenuStrip%2A> özelliğini <xref:System.Windows.Forms.MenuStrip>.  
  
3. MDI alt formu oluşturun ve ayarlayın, <xref:System.Windows.Forms.Form.MdiParent%2A> özelliğini üst formun adı.  
  
4. Ekleme bir <xref:System.Windows.Forms.MenuStrip> MDI alt formu.  
  
5. Alt formunda <xref:System.Windows.Forms.ToolStripItem.Visible%2A> özelliği <xref:System.Windows.Forms.MenuStrip> için `false`.  
  
6. Alt formun menü öğeleri ekleme <xref:System.Windows.Forms.MenuStrip> üst form birleştirmek istediğiniz <xref:System.Windows.Forms.MenuStrip> alt formun zaman etkinleştirilir.  
  
7. Kullanım <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> özelliği menüsündeki öğeler alt formu <xref:System.Windows.Forms.MenuStrip> üst formun nasıl birleştirecek denetlemek için.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip Denetimine Genel Bakış](menustrip-control-overview-windows-forms.md)
