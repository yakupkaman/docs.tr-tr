---
title: statik değiştirici - C# Referans
ms.date: 01/22/2020
f1_keywords:
- static
- static_CSharpKeyword
helpviewer_keywords:
- static keyword [C#]
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
ms.openlocfilehash: e7671e9db488a7b50f4ed736864d6fa8d95eef1a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/14/2020
ms.locfileid: "76744666"
---
# <a name="static-c-reference"></a>static (C# Başvurusu)

`static` Belirli bir nesneye değil, türe ait statik bir üyeyi bildirmek için değiştirici'yi kullanın. `static` Değiştirici sınıfları bildirmek `static` için kullanılabilir. Sınıflarda, arabirimlerde ve yapılarda, değiştiriciyi `static` alanlara, yöntemlere, özelliklere, işleçlere, olaylara ve yapıcılara ekleyebilirsiniz. `static` Değiştirici dizinleyiciler veya sonlandırıcılar ile kullanılamaz. Daha fazla bilgi için Statik [Sınıflar ve Statik Sınıf Üyeleri'ne](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)bakın.

## <a name="example"></a>Örnek

Aşağıdaki sınıf olarak `static` bildirilir ve `static` yalnızca yöntemleri içerir:

[!code-csharp[csrefKeywordsModifiers#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#18)]

Sabit veya tür bildirimi dolaylı `static` olarak üyedir. Bir `static` üye bir örnek aracılığıyla başvurulamaz. Bunun yerine, tür adı ile başvurulan. Örneğin, aşağıdaki sınıfı göz önünde bulundurun:

[!code-csharp[csrefKeywordsModifiers#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#19)]

`static` Üyeye `x`başvurmak için, üyeaynı kapsamdaerişilebilir olmadığı sürece, `MyBaseC.MyStruct.x`tam nitelikli adı kullanın:

```csharp
Console.WriteLine(MyBaseC.MyStruct.x);
```

Bir sınıfın örneği sınıfın tüm örnek alanlarının ayrı bir kopyasını içerse de, her `static` alanın yalnızca bir kopyası vardır.

Başvuru `static` yöntemlerini veya [`this`](this.md) özellik erişimcilerini kullanmak mümkün değildir.

Anahtar `static` sözcük bir sınıfa uygulanırsa, sınıfın tüm `static`üyeleri .

Sınıflar, arabirimler `static` ve sınıflar `static` oluşturucuolabilir. Bir `static` oluşturucu program başladığında ve sınıf anında zaman arasında bir noktada denir.

> [!NOTE]
> Anahtar `static` kelimenin Kullanımı C++'a göre daha sınırlıdır. C++ anahtar sözcüğüyle karşılaştırmak için [bkz.](/cpp/cpp/storage-classes-cpp#static)

Üyeleri `static` göstermek için, bir şirket çalışanLarını temsil eden bir sınıfı düşünün. Sınıfın çalışanları saymak için bir yöntem ve çalışan sayısını depolamak için bir alan içerdiğini varsayalım. Hem yöntem hem de alan herhangi bir çalışan örneğine ait değildir. Bunun yerine, bir bütün olarak çalışanların sınıfına aittir. Sınıfın üyeleri olarak `static` ilan edilmelidirler.

## <a name="example"></a>Örnek

Bu örnek, yeni bir çalışanın adını ve kimliğini okur, çalışan sayacını bir er ler halinde arttırarak yeni çalışan ve yeni çalışan sayısına ait bilgileri görüntüler. Bu program klavyeden geçerli çalışan sayısını okur.

[!code-csharp[csrefKeywordsModifiers#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#20)]  

## <a name="example"></a>Örnek

Bu örnek, henüz bildirilmemiş `static` başka `static` bir alan kullanarak bir alanı başlatmanızı gösterilmektedir. `static` Alana açıkça bir değer atayana kadar sonuçlar tanımsız olacaktır.

[!code-csharp[csrefKeywordsModifiers#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#21)]  

## <a name="c-language-specification"></a>C# dili belirtimi

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Ayrıca bkz.

- [C# Referans](../index.md)
- [C# Programlama Kılavuzu](../../programming-guide/index.md)
- [C# Anahtar Kelimeler](index.md)
- [Değiştiriciler](index.md)
- [Statik Sınıflar ve Statik Sınıf Üyeleri](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
