---
title: 'Nasıl yapılır: Veritabanı Değerlerini Tutarak Çakışmaları Çözümleme'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b475cf72-9e64-4f6e-99c1-af7737bc85ef
ms.openlocfilehash: e42f48a188741c3ddff44f6444fa351192c8175f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793341"
---
# <a name="how-to-resolve-conflicts-by-retaining-database-values"></a>Nasıl yapılır: Veritabanı Değerlerini Tutarak Çakışmaları Çözümleme
Değişikliklerinizi yeniden göndermeye çalışmadan önce beklenen ve gerçek veritabanı değerleri arasındaki farkları mutabık kılmak için, veritabanında bulunan değerleri bekletmek için kullanabilirsiniz <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues> . Nesne modelindeki geçerli değerlerin üzerine yazılır. Daha fazla bilgi için bkz [. iyimser eşzamanlılık: Genel](optimistic-concurrency-overview.md)bakış.  
  
> [!NOTE]
> Her durumda, istemcideki kayıt, veritabanındaki güncelleştirilmiş verileri alarak yenilenir. Bu eylem, sonraki güncelleştirme denemasının aynı eşzamanlılık denetimlerinde başarısız olmasına neden olur.  
  
## <a name="example"></a>Örnek  
 Bu senaryoda, Kullanıcı1 değişiklikleri <xref:System.Data.Linq.ChangeConflictException> göndermeye çalıştığında bir özel durum oluşturulur, çünkü kullanıcı2 bu arada yardımcı ve departman sütunlarını değiştirdi. Aşağıdaki tabloda durum gösterilmektedir.  
  
||Yöneticisi|Yardımc|Bölüm|  
|------|-------------|---------------|----------------|  
|Kullanıcı1 ve kullanıcı2 tarafından sorgulandığında özgün veritabanı durumu.|Alfrelar|Maria|Satış|  
|Kullanıcı1 bu değişiklikleri göndermeye hazırlar.|Alfred||Pazarlama|  
|Kullanıcı2 bu değişiklikleri zaten gönderdi.||Mary|Hizmet|  
  
 Kullanıcı1, daha yeni veritabanı değerlerini nesne modelindeki geçerli değerlerin üzerine yazarak bu çakışmayı çözmeye karar verir.  
  
 Kullanıcı1 kullanarak <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues>çakışmayı çözdüğünde, veritabanındaki sonuç tabloda aşağıdaki gibidir:  
  
||Yöneticisi|Yardımc|Bölüm|  
|------|-------------|---------------|----------------|  
|Çakışma çözümünden sonra yeni durum.|Alfrelar<br /><br /> orijinale|Mary<br /><br /> (kullanıcı2 'ten)|Hizmet<br /><br /> (kullanıcı2 'ten)|  
  
 Aşağıdaki örnek kod, veritabanı değerleriyle nesne modelindeki geçerli değerlerin üzerine yazmayı gösterir. (Bireysel üye çakışmalarının denetimi veya özel işlenmesi gerçekleşmez.)  
  
 [!code-csharp[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Nasıl yapılır: Değişiklik çakışmalarını yönetme](how-to-manage-change-conflicts.md)
