---
title: Tür Sağlayıcıları
description: Bir F# tür sağlayıcının, programlarınızda kullanılmak üzere türler, Özellikler ve yöntemler sağlayan bir bileşen olduğunu öğrenin.
ms.date: 04/02/2018
ms.openlocfilehash: 7fa0ff6b5f2b0bc978df2988f22b2042acc22320
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74552912"
---
# <a name="type-providers"></a>Tür Sağlayıcıları

Bir F# tür sağlayıcısı programınız içinde kullanmanız için türler, özellikler ve yöntemler sağlayan bir bileşendir. Tür sağlayıcıları, F# derleyici tarafından oluşturulan ve dış veri kaynağını temel alan, **sağlanmış türler**olarak bilinen öğeleri oluşturur.

Örneğin, SQL için F# bir tür sağlayıcısı ilişkisel bir veritabanındaki tabloları ve sütunları temsil eden türler oluşturabilir. Aslında, bu, [SqlProvider](https://fsprojects.github.io/SQLProvider/) tür sağlayıcısının yaptığı şeydir.

Sunulan türler, bir tür sağlayıcısına giriş parametrelerine bağımlıdır. Bu giriş bir örnek veri kaynağı (bir JSON şema dosyası gibi), doğrudan bir dış hizmete işaret eden bir URL veya bir veri kaynağına bağlantı dizesi olabilir. Bir tür sağlayıcısı ayrıca tür gruplarının isteğe bağlı olarak genişletildiğinden de emin olabilir; diğer bir deyişle, türlerine gerçekten programınızın başvurduğu durumlarda genişletilir. Bu çevrimiçi veri marketleri gibi büyük ölçekli bilgi uzaylarının doğrudan, istek anında bütünleştirmesini türü kesin belirlenmiş olarak sağlar.

## <a name="generative-and-erased-type-providers"></a>Genel ve silinmiş tür sağlayıcıları

Tür sağlayıcıları iki şekilde gelir: genel ve silinmiş.

Genel tür sağlayıcıları, üretildikleri derlemeye .NET türleri olarak yazılabilen türler üretir. Bu, diğer derlemelerdeki koddan tüketilebilmesi için izin verir. Bu, veri kaynağının türü belirlenmiş gösteriminin genellikle .NET türleriyle temsil edilebilir bir değer olması gerektiği anlamına gelir.

Tür sağlayıcılarının silinmesinin, yalnızca oluşturulduğu derlemede veya projede tüketilebilen türler üretir. Türler kısa ömürlü; diğer bir deyişle, bir derlemeye yazılmazlar ve diğer derlemelerdeki kodla tüketilemez. Bu kişiler *gecikmeli* Üyeler içerebilir ve bu bilgiler, potansiyel olarak sonsuz bir bilgi alanından sağlanmış türleri kullanmanıza olanak sağlar. Büyük ve bağlanmış bir veri kaynağının küçük bir alt kümesini kullanmak için faydalıdır.

## <a name="commonly-used-type-providers"></a>Yaygın olarak kullanılan tür sağlayıcıları

Aşağıdaki yaygın olarak kullanılan kitaplıklar farklı kullanımlar için tür sağlayıcıları içerir:

- [FSharp. Data](https://fsharp.github.io/FSharp.Data/) , JSON, XML, CSV ve HTML belge biçimleri ve kaynakları Için tür sağlayıcıları içerir.
- [SqlProvider](https://fsprojects.github.io/SQLProvider/) , bu veri kaynaklarına karşı nesne eşleme ve F# LINQ sorguları aracılığıyla ilişki veritabanlarına kesin olarak yazılmış erişim sağlar.
- [FSharp. Data. SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) , içindeki T-SQL ' F#y i, derleme zamanında denetlenmiş ekleme için bir dizi tür sağlayıcıya sahiptir.
- [Azure depolama türü sağlayıcısı](https://fsprojects.github.io/AzureStorageTypeProvider/) , Azure Blob 'Ları, tabloları ve kuyrukları için türler sağlar. bu sayede, kaynak adlarını programınızın tamamında dizeler olarak belirtmeye gerek kalmadan bu kaynaklara erişmenize izin verilir.
- [FSharp. Data. GraphQL](https://fsprojects.github.io/FSharp.Data.GraphQL/index.html) , URL ile belirtilen bir graphql sunucusuna dayalı türler sağlayan **graphsqlprovider**'ı içerir.

Gerektiğinde, [kendi özel tür sağlayıcılarınızı](creating-a-type-provider.md)veya başkaları tarafından oluşturulan başvuru türü sağlayıcılarını oluşturabilirsiniz. Örneğin, kuruluşunuz her biri kendi kararlı veri şemasına sahip çok ve artan sayıda adlandırılmış veri kümeleri sağlayan bir veri hizmetine sahip olduğunu varsayın. Şemaları okuyan ve en son kullanılabilir veri kümelerini programcıya türü kesin belirlenmiş bir biçimde sunan bir tür sağlayıcısı oluşturmayı seçebilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.

- [Öğretici: tür sağlayıcısı oluşturma](creating-a-type-provider.md)
- [F# Dili Başvurusu](../../language-reference/index.md)
