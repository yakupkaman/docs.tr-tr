---
title: referential integrity constraint
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: ad35df7bcca62ffdbc3842b0817b22c5482a3d4d
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738375"
---
# <a name="referential-integrity-constraint"></a>referential integrity constraint
Varlık Veri Modeli (EDM) içindeki bir *başvurusal bütünlük kısıtlaması* , ilişkisel bir veritabanındaki başvurusal bütünlük kısıtlamasına benzerdir. Bir veritabanı tablosundaki bir sütunun (veya sütunlarının) başka bir tablonun birincil anahtarına başvurmasına benzer şekilde, bir [varlık türünün](entity-type.md) [özelliği](property.md) (veya özellikleri) başka bir varlık türünün [varlık anahtarına](entity-key.md) başvurabilir. Başvurulan varlık türüne kısıtlamanın *asıl sonu* denir. Asıl ucuna başvuran varlık türüne kısıtlamanın *bağımlı sonu* denir.  
  
 Başvurusal bütünlük kısıtlaması, iki varlık türü arasındaki [ilişkinin](association-type.md) parçası olarak tanımlanır. Başvurusal bütünlük kısıtlamasının tanımı aşağıdaki bilgileri belirtir:  
  
- Kısıtlamanın ana ucu. (Varlık anahtarına bağımlı uç tarafından başvurulan bir varlık türü.)  
  
- Sorumlu ucunun varlık anahtarı.  
  
- Kısıtlamanın bağımlı sonu. (Asıl ucunun varlık anahtarına başvuran bir özelliği veya özellikleri olan varlık türü.)  
  
- Bağımlı ucun başvuran özelliği veya özellikleri.  
  
 EDM 'daki başvuru bütünlüğü kısıtlamalarının amacı, geçerli ilişkilerin her zaman mevcut olmasını sağlamaktır. Daha fazla bilgi için bkz. [yabancı anahtar özelliği](foreign-key-property.md).  
  
## <a name="example"></a>Örnek  
 Aşağıdaki diyagramda iki ilişkiye sahip bir kavramsal model görülmektedir: `WrittenBy` ve `PublishedBy`. `Book` varlık türü, `PublishedBy` ilişkilendirmesinde bir başvuru bütünlüğü kısıtlaması tanımlarken `Publisher` varlık türünün varlık anahtarına başvuran `PublisherId`bir özelliğe sahiptir.  
  
 ![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "Başvuru kısıtlama modeli örneği")  
  
 [ADO.NET Entity Framework](./ef/index.md) kavramsal model tanımlamak için kavramsal şema tanım dili ([csdl](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) adlı bir etki ALANıNA özgü dil (DSL) kullanır. Aşağıdaki CSDL, yukarıdaki kavramsal modelde gösterilen `PublishedBy` ilişkilendirmesi üzerinde bir başvurusal bütünlük kısıtlaması tanımlar.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Varlık Veri Modeli Temel Kavramları](entity-data-model-key-concepts.md)
- [Varlık Veri Modeli](entity-data-model.md)
