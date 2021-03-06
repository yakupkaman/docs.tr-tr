---
title: 'Nasıl yapılır: Veritabanına Satır Ekleme'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 44d99680-69c7-4879-a732-f6771b334211
ms.openlocfilehash: 8186b90a666a7b75ce626cccb7cc28af38de7c5b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781868"
---
# <a name="how-to-insert-rows-into-the-database"></a>Nasıl yapılır: Veritabanına Satır Ekleme

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] İlişkili<xref:System.Data.Linq.Table%601> koleksiyona nesneler ekleyerek ve sonra değişiklikleri veritabanına göndererek bir veritabanına satır eklersiniz. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Değişikliklerinizi uygun SQL `INSERT` komutlarına çevirir.

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] `Insert`, Ve`Delete`veritabanı işlemleri için varsayılan yöntemleri geçersiz kılabilirsiniz. `Update` Daha fazla bilgi için bkz. [Insert, Update ve DELETE Işlemlerini özelleştirme](customizing-insert-update-and-delete-operations.md).
>
> Visual Studio kullanan geliştiriciler, aynı amaçla saklı yordamlar geliştirmek için Nesne İlişkisel Tasarımcısı kullanabilir.

Aşağıdaki adımlarda, geçerli <xref:System.Data.Linq.DataContext> bir veritabanının Northwind veritabanına bağladığı varsayılır. Daha fazla bilgi için [nasıl yapılır: Bir veritabanına](how-to-connect-to-a-database.md)bağlanın.

### <a name="to-insert-a-row-into-the-database"></a>Veritabanına bir satır eklemek için

1. Gönderilecek sütun verilerini içeren yeni bir nesne oluşturun.

2. Yeni nesneyi [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] `Table` veritabanındaki hedef tabloyla ilişkili koleksiyona ekleyin.

3. Değişikliği veritabanına gönderebilirsiniz.

## <a name="example"></a>Örnek

Aşağıdaki kod örneği, türünde `Order` yeni bir nesne oluşturur ve uygun değerlerle doldurur. Daha sonra yeni nesneyi `Order` koleksiyona ekler. Son olarak, değişikliği veritabanına `Orders` tabloya yeni bir satır olarak gönderir.

[!code-csharp[System.Data.Linq.Table#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#1)]
[!code-vb[System.Data.Linq.Table#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#1)]

## <a name="see-also"></a>Ayrıca bkz.

- [Nasıl yapılır: Değişiklik çakışmalarını yönetme](how-to-manage-change-conflicts.md)
- [DataContext Metotları (O/R Tasarımcısı)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [Nasıl yapılır: Güncelleştirme, ekleme ve silme işlemleri gerçekleştirmek için saklı yordamlar atama (O/R Tasarımcısı)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [Veri Değişiklikleri Yapma ve Gönderme](making-and-submitting-data-changes.md)
