---
title: 'Nasıl yapılır: PLINQ ile Dosya Dizinlerini Yineleme'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ queries, how to iterate directories
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
ms.openlocfilehash: 208076cb9b7b56ab13458fa0dd4d92f2023106b9
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635841"
---
# <a name="how-to-iterate-file-directories-with-plinq"></a>Nasıl yapılır: PLINQ ile Dosya Dizinlerini Yineleme

Bu makalede, dosya dizinleri işlemleri paralelleştirmek için iki yol gösterir. İlk sorgu, <xref:System.IO.Directory.GetFiles%2A> bir dizi dosya adını bir dizi dizin ve tüm alt dizinleri doldurmak için yöntemi kullanır. Bu yöntem, tüm dizi doldurulana kadar geri dönmüyor, çünkü işlemin başında gecikme sokulması tanıtabilir. Ancak, dizi doldurulur sonra, PLINQ hızlı bir şekilde paralel olarak işleyebilir.  
  
İkinci sorgu, sonuçları <xref:System.IO.Directory.EnumerateDirectories%2A> <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> hemen döndürmeye başlayan statik ve yöntemleri kullanır. Büyük dizin ağaçları üzerinde yinelenirken bu yaklaşım daha hızlı olabilir, ancak ilk örneğe kıyasla işlem süresi birçok etkene bağlıdır.  
  
> [!NOTE]
> Bu örnekler kullanımı göstermek için tasarlanmıştır ve Nesneler sorgusuna eşdeğer ardışık LINQ'dan daha hızlı çalışmayabilir. Hız hakkında daha fazla bilgi için [PLINQ'da Hızları Anlama'ya](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)bakın.  
  
## <a name="getfiles-example"></a>Dosyaları Al örneği

 Bu örnek, ağaçtaki tüm dizinlere erişiminiz olduğunda, dosya boyutları büyük olmadığında ve erişim süreleri önemli olmadığında, basit senaryolarda dosya dizinleri üzerinde nasıl yinelenirsiniz gösterilmektedir. Bu yaklaşım, dosya adları dizisi oluşturulurken başlangıçta bir gecikme dönemi içerir.  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## <a name="enumeratefiles-example"></a>Sayısal Dosyalar örneği

 Bu örnek, ağaçtaki tüm dizinlere erişiminiz olduğunda, dosya boyutları büyük olmadığında ve erişim süreleri önemli olmadığında, basit senaryolarda dosya dizinleri üzerinde nasıl yinelenirsiniz gösterilmektedir. Bu yaklaşım, önceki örnekten daha hızlı sonuç üretmeye başlar.  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 Kullanırken, <xref:System.IO.Directory.GetFiles%2A>ağaçtaki tüm dizinler üzerinde yeterli izinlere sahip olduğunuzdan emin olun. Aksi takdirde, bir özel durum atılır ve hiçbir sonuç döndürülür. PLINQ <xref:System.IO.Directory.EnumerateDirectories%2A> sorgusunda bunu kullanırken, G/Ç özel durumlarını, yinelemeye devam etmenizi sağlayacak zarif bir şekilde işlemek sorunludur. Kodunuz G/Ç veya yetkisiz erişim özel durumlarını işlemesi gerekiyorsa, [Nasıl Yapılır: Paralel Sınıf dosya dizinlerini nasıl yinele'](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-the-parallel-class.md)de açıklanan yaklaşımı göz önünde bulundurmalısınız.  
  
 G/Ç gecikmesi bir sorunsa, örneğin ağ üzerinden dosya G/Ç'de, [TPL ve Traditional .NET Framework Asynchronous Programming'de ve](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md) bu [blog gönderisinde](https://devblogs.microsoft.com/pfxteam/parallel-extensions-and-io/)açıklanan eşzamanlı G/Ç tekniklerinden birini kullanmayı düşünün.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Paralel LINQ (PLINQ)](../../../docs/standard/parallel-programming/introduction-to-plinq.md)
