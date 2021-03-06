---
title: 'Nasıl yapılır: Paralel ve Sıralı LINQ Sorgularını Birleştirme'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
ms.openlocfilehash: 074714b1152c8804ee1e747104dbaf47f4645546
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635865"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>Nasıl yapılır: Paralel ve Sıralı LINQ Sorgularını Birleştirme

Bu örnek, PLINQ'a sorgudaki sonraki tüm işleçleri sırayla işlemesi için talimat vermek için <xref:System.Linq.ParallelEnumerable.AsSequential%2A> yöntemin nasıl kullanılacağını gösterir. Sıralı işleme genellikle paralelden daha yavaş olsa da, bazen doğru sonuçlar üretmek gerekir.  
  
> [!NOTE]
> Bu örnek, kullanımı göstermek için tasarlanmıştır ve Nesneler sorgusuna eşdeğer ardışık LINQ'dan daha hızlı çalışmayabilir. Hız hakkında daha fazla bilgi için [PLINQ'da Hızları Anlama'ya](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)bakın.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnekte, sorgunun <xref:System.Linq.ParallelEnumerable.AsSequential%2A> önceki bir yan tümcesinde oluşturulan sırayı korumak için gereken bir senaryo gösterilmektedir.  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>Kod Derleniyor  
 Bu kodu derlemek ve çalıştırmak için [PLINQ Veri Örneği](../../../docs/standard/parallel-programming/plinq-data-sample.md) projesine yapıştırın, `Main`yöntemi aramak için bir satır ekleyin ve **F5**tuşuna basın.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Paralel LINQ (PLINQ)](../../../docs/standard/parallel-programming/introduction-to-plinq.md)
