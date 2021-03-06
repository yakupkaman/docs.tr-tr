---
title: Veri Sözleşmelerini Kullanma
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataContractAttribute class
- WCF, data
- data contracts [WCF]
ms.assetid: a3ae7b21-c15c-4c05-abd8-f483bcbf31af
ms.openlocfilehash: 3fd22cc0842c51b331905369915bd055235680c4
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592196"
---
# <a name="using-data-contracts"></a>Veri Sözleşmelerini Kullanma
A *veri anlaşması* hizmet bağlamalarında değiştirilebilmesi için verileri tanımlayan bir istemci arasındaki resmi bir sözleşme. Diğer bir deyişle, iletişim, istemciyi ve hizmeti yalnızca aynı veri sözleşmeleri aynı türleri paylaşılacak gerekmez. Bir veri anlaşması tam olarak, hangi verilerin serileştirilmiş (XML olarak açık) her parametre veya dönüş türü tanımlar değiştirilmek üzere.  
  
## <a name="data-contract-basics"></a>Veri sözleşmesi temelleri  
 Windows Communication Foundation (WCF) veri sözleşmesi serileştiricisi tarafından varsayılan olarak adlandırılan bir serileştirme motoruna (XML gelen ve giden dönüştürmeniz) verileri seri hale getrime ve için kullanır. Tam sayılar ve dizeler gibi tüm .NET Framework ilkel türler ve bunun yanı sıra bazı türleri gibi temel olarak kabul <xref:System.DateTime> ve <xref:System.Xml.XmlElement>, hiçbir bir hazırlık ile seri hale getirilebilir ve varsayılan veri sözleşmeleri sahip olarak kabul edilir. Çoğu .NET Framework türleri, ayrıca mevcut veri sözleşmelerine sahiptir. Seri hale getirilebilir türler tam bir listesi için bkz. [veri sözleşme seri hale getirici tarafından desteklenen türleri](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).  
  
 Oluşturduğunuz yeni karmaşık türler seri hale getirilebilir olması için tanımlanmış bir veri sözleşmesi olması gerekir. Varsayılan olarak, <xref:System.Runtime.Serialization.DataContractSerializer> veri anlaşması algılar ve herkese görünür türlü serileştirir. Tüm ortak okuma/yazma özellikleri ve türünde alanlar serileştirilir. Kullanarak kullanıma serileştirmesi üyelerinden seçebilirsiniz <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>. Kullanarak bir veri anlaşması da açıkça oluşturabilirsiniz <xref:System.Runtime.Serialization.DataContractAttribute> ve <xref:System.Runtime.Serialization.DataMemberAttribute> öznitelikleri. Bu normalde uygulayarak yapılır <xref:System.Runtime.Serialization.DataContractAttribute> öznitelik türü için. Bu öznitelik, sınıflar, yapılar ve numaralandırmalar için uygulanabilir. <xref:System.Runtime.Serialization.DataMemberAttribute> Öznitelik her üyesine, olduğunu belirtmek için veri anlaşması türü sonra uygulanmalıdır bir *veri üyesi*, diğer bir deyişle, seri hale getirilmesi. Daha fazla bilgi için [Serializable türler](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
### <a name="example"></a>Örnek  
 Aşağıdaki örnek, hizmet sözleşmesini (bir arabirim) gösterir <xref:System.ServiceModel.ServiceContractAttribute> ve <xref:System.ServiceModel.OperationContractAttribute> öznitelikler açıkça uygulanıp uygulanmadığı. Bu örnek, bir karmaşık tür kaldırırken kahvenizi ilkel türler bir veri sözleşmesi gerektirmeyen gösterir.  
  
 [!code-csharp[C_DataContract#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#1)]
 [!code-vb[C_DataContract#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#1)]  
  
 Aşağıdaki örnek, bir veri anlaşması için nasıl gösterir `MyTypes.PurchaseOrder` türü uygulayarak oluşturulur <xref:System.Runtime.Serialization.DataContractAttribute> ve <xref:System.Runtime.Serialization.DataMemberAttribute> sınıfını ve üyelerini için öznitelikler.  
  
 [!code-csharp[C_DataContract#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#2)]
 [!code-vb[C_DataContract#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#2)]  
  
### <a name="notes"></a>Notlar  
 Aşağıdaki notlar, veri sözleşme oluşturmayı göz önünde bulundurulması gerekenlerin sağlayın:  
  
- <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> Özniteliği ile işaretlenmemiş türleri kullanıldığında yalnızca kabul. Bu, biri ile işaretlenmemiş türlerini içerir <xref:System.Runtime.Serialization.DataContractAttribute>, <xref:System.SerializableAttribute>, <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, veya <xref:System.Runtime.Serialization.EnumMemberAttribute> öznitelikleri veya diğer herhangi bir yolla seri hale getirilebilir olarak işaretlenmiş (gibi <xref:System.Xml.Serialization.IXmlSerializable>).  
  
- Uygulayabileceğiniz <xref:System.Runtime.Serialization.DataMemberAttribute> alanlar ve özellikler için özniteliği.  
  
- Üye erişilebilirlik düzeyleri (iç, özel, korumalı veya genel), veri sözleşme herhangi bir şekilde etkilemez.  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute> Özniteliği, statik üye uygulanırsa yoksayılır.  
  
- Serileştirme sırasında özelliği veri üyelerini serileştirilecek özelliklerin değerini almak get özelliği kod adı verilir.  
  
- Seri durumundan çıkarma sırasında başlatılmamış bir nesne ilk, hiçbir oluşturucu türüne çağırmaya gerek kalmadan oluşturulur. Ardından tüm veri üyeleri seri.  
  
- Seri durumundan çıkarma sırasında seri durumdan çıkarılmakta olan değerin özelliklerini ayarlamak özellik veri üyeleri için özellik kümesi kod adı verilir.  
  
- Bir veri anlaşması geçerli olması tüm veri üyelerini sıralamak mümkün olmalıdır. Seri hale getirilebilir türler tam bir listesi için bkz. [veri sözleşme seri hale getirici tarafından desteklenen türleri](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).  
  
     Genel türler, genel olmayan türleri tam olarak aynı şekilde ele alınır. Genel parametreler için özel bir gereksinim vardır. Örneğin, şu tür göz önünde bulundurun.  
  
 [!code-csharp[C_DataContract#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#3)]
 [!code-vb[C_DataContract#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#3)]  
  
 Bu tür genel tür parametresi için kullanılıp seri hale getirilebilir türüdür (`T`) serileştirilebilir olup. Tüm veri üyelerini sıralamak mümkün olması gerekir çünkü şu tür yalnızca genel tür parametresi de aşağıdaki kodda gösterildiği gibi seri hale getirilebilir, seri hale getirilebilir olmasıdır.  
  
 [!code-csharp[C_DataContract#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#4)]
 [!code-vb[C_DataContract#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#4)]  
  
 Veri sözleşme tanımlayan bir WCF hizmeti için bir kod örneği için bkz. [temel veri anlaşması](../../../../docs/framework/wcf/samples/basic-data-contract.md) örnek.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- [Seri Hale Getirilebilir Türler](../../../../docs/framework/wcf/feature-details/serializable-types.md)
- [Veri Anlaşması Adları](../../../../docs/framework/wcf/feature-details/data-contract-names.md)
- [Veri Anlaşması Eşitliği](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)
- [Veri Üye Sırası](../../../../docs/framework/wcf/feature-details/data-member-order.md)
- [Veri Anlaşması Bilinen Türler](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)
- [İleri Uyumlu Veri Anlaşmaları](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)
- [Veri Anlaşması Sürümü Oluşturma](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)
- [Sürüm Toleranslı Seri Hale Getirme Geri Çağrıları](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)
- [Veri Üyesi Varsayılan Değerler](../../../../docs/framework/wcf/feature-details/data-member-default-values.md)
- [Veri Anlaşması Seri Hale Getirici Tarafından Desteklenen Türler](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
- [Nasıl yapılır: Bir sınıf veya yapı için temel veri sözleşmesi oluşturma](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)
