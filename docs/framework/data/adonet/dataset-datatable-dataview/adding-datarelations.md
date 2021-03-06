---
title: DataRelations Ekleme
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
ms.openlocfilehash: 8157d296636d0f8661a35af35de561f5cc49c30b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784814"
---
# <a name="adding-datarelations"></a>DataRelations Ekleme
Birden çok <xref:System.Data.DataSet> <xref:System.Data.DataTable> nesne ile, bir tabloyu başka bir <xref:System.Data.DataRelation> tabloyla ilişkilendirmek, tablolar arasında gezinmek ve ilişkili bir tablodan alt veya üst satırları döndürmek için nesneleri kullanabilirsiniz.  
  
 Bir **DataRelation** oluşturmak için gereken bağımsız değişkenler, oluşturulmakta olan **DataRelation** için bir addır ve ilişkide üst ve alt sütunları olarak işlev gösteren <xref:System.Data.DataColumn> sütunlara bir veya daha fazla başvuru dizisi. Bir **DataRelation**oluşturduktan sonra, tablolar arasında gezinmek ve değerleri almak için kullanabilirsiniz.  
  
 ' A bir **DataRelation** <xref:System.Data.DataSet> eklemek, varsayılan olarak bir <xref:System.Data.UniqueConstraint> üst tabloya ve <xref:System.Data.ForeignKeyConstraint> alt tablosuna bir ekler. Bu varsayılan kısıtlamalar hakkında daha fazla bilgi için bkz. [DataTable kısıtlamaları](datatable-constraints.md).  
  
 Aşağıdaki kod örneği, bir <xref:System.Data.DataSet>içinde iki <xref:System.Data.DataTable> nesne kullanarak bir DataRelation oluşturur. Her <xref:System.Data.DataTable> biri, iki <xref:System.Data.DataTable> nesne arasında bağlantı görevi gören **CustId**adlı bir sütun içerir. Örnek, <xref:System.Data.DataSet>ilişki koleksiyonuna tek bir **DataRelation** ekler. Örnekteki ilk bağımsız değişken, oluşturulmakta olan **DataRelation** 'ın adını belirtir. İkinci bağımsız değişken üst **DataColumn** ' i ayarlar ve üçüncü bağımsız değişken alt **DataColumn**' i ayarlar.  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 Bir **DataRelation** Ayrıca, **true**olarak ayarlandığında, alt TABLODAKI satırların, kullanılarak <xref:System.Data.DataSet.WriteXml%2A> XML öğeleri olarak yazıldığında üst tablodaki iç içe olmasına neden olan **iç içe** bir özelliği vardır. Daha fazla bilgi için bkz. [veri KÜMESINDE XML kullanma](using-xml-in-a-dataset.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [DataSets, DataTables ve DataViews](index.md)
- [ADO.NET’e Genel Bakış](../ado-net-overview.md)
