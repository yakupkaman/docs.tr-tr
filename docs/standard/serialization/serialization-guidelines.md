---
title: Serileştirme yönergeleri
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serialization, guidelines
- binary serialization, guidelines
ms.assetid: ebbeddff-179d-443f-bf08-9c373199a73a
ms.openlocfilehash: 067f32a026e3354e6c4256602ed17fd7d7bde0b8
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78159799"
---
# <a name="serialization-guidelines"></a>Serileştirme yönergeleri
Bu belgenin bir API tasarlama serileştirilecek göz önünde için yönergeleri listeler.  

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
 .NET, çeşitli serileştirme senaryoları için iyileştirilmiş üç ana serileştirme teknolojisi sunar. Aşağıdaki tabloda bu teknolojiler ve bu teknolojilerle ilgili önemli .NET türleri listelenmektedir.  
  
|Teknoloji|İlgili sınıflar|Notlar|  
|----------------|----------------------|-----------|  
|Veri sözleşmesi serileştirme|<xref:System.Runtime.Serialization.DataContractAttribute><br /><br /> <xref:System.Runtime.Serialization.DataMemberAttribute><br /><br /> <xref:System.Runtime.Serialization.DataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.NetDataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer><br /><br /> <xref:System.Runtime.Serialization.ISerializable>|Genel kalıcılığı<br /><br /> Web Hizmetleri<br /><br /> JSON|  
|XML seri hale getirme|<xref:System.Xml.Serialization.XmlSerializer>|XML biçimi <br />tam denetim ile|  
|Çalışma zamanı-seri hale getirme (ikili ve SOAP)|<xref:System.SerializableAttribute><br /><br /> <xref:System.Runtime.Serialization.ISerializable><br /><br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|.NET uzaktan iletişim|  
  
 Yeni türleri tasarımı yaparken, varsa, bu teknolojiler türlerden desteklemesi gerekir. karar. Bu seçim yapın ve bu tür desteğini sağlamak nasıl aşağıdaki yönergeleri açıklanmaktadır. Bu yönergeleri uygulamanızın veya kitaplık uygulamasında kullanması gereken hangi serileştirme teknolojiyi seçmenizde yardımcı anlamına gelmez. Bu tür yönergeleri için API tasarım doğrudan ilişkili değildir ve bu nedenle bu konu kapsamında değildir.  
  
## <a name="guidelines"></a>Yönergeler  
  
- Yeni türleri tasarım serileştirme hakkında düşünün.  
  
     Serileştirme, her tür için önemli bir tasarım olduğundan, programların türdeki örnekleri kalıcı hale getirmesinin veya iletmesinin gerekebileceği için bu bir tasarıma sahiptir.  
  
### <a name="choosing-the-right-serialization-technology-to-support"></a>Destekleyecek doğru serileştirme teknolojisini seçme  
 Belirtilen her türlü none, bir veya daha fazla seri hale getirme teknolojilerini destekler.  
  
- Yazdığınız örneklerin Web hizmetlerinde kalıcı olması veya kullanılması gerekiyorsa, *veri sözleşmesi serileştirmesini* desteklemeyi düşünün.  
  
- Tür serileştirildiğinde üretilen XML biçimi üzerinde daha fazla denetime ihtiyacınız varsa, veri sözleşmesi serileştirmesine ek olarak veya yerine *XML serileştirmesini* desteklemeyi düşünün.  
  
     Bu, veri sözleşme serileştirmesi tarafından desteklenmeyen bir XML yapısı kullanmanız gereken (örneğin, XML özniteliklerini üretmek için), birlikte çalışabilirlik senaryolarında gerekli olabilir.  
  
- Yazdığınız örneklerin .NET uzaktan Iletişim sınırları arasında gezinilmesi gerekiyorsa, *çalışma zamanı serileştirmesini* desteklemeyi düşünün.  
  
- Sadece genel Kalıcılık nedenlerle destekleme çalışma zamanı serileştirme veya XML serileştirme özen gösterin. Bunun yerine veri sözleşmesi serileştirmesini tercih et  
  
#### <a name="supporting-data-contract-serialization"></a>Veri sözleşmesi serileştirmesini destekleme  
 Türler, türü <xref:System.Runtime.Serialization.DataContractAttribute> ve <xref:System.Runtime.Serialization.DataMemberAttribute> üyelere (alanlar ve Özellikler) uygulayarak veri sözleşmesi serileştirmesini destekleyebilir.  
  
 [!code-csharp[SerializationGuidelines#1](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#1)]
 [!code-vb[SerializationGuidelines#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#1)]  
  
1. Türün kısmi güvende kullanılabilmesi için, türden veri üyelerini genel olarak işaretlemeyi düşünün. Tam güvende, veri sözleşme serileştiricileri ortak türleri ve üyeleri seri hale getirilebilir ve serisini kaldıramıyor, ancak kısmi güvende yalnızca ortak üyeler seri hale getirilebilir ve seri durumdan çıkarılamaz.  
  
2. Data-MemberAttribute içeren tüm özelliklerde bir alıcı ve ayarlayıcı uygulayın. Veri sözleşme serileştiricileri, tür için hem alıcının hem de ayarlayıcının seri hale getirilebilir olarak kabul edilmesini gerektirir. Tür kısmi güvende kullanılmazsa, özellik erişimcilerinin biri veya her ikisi ortak olabilir.  
  
     [!code-csharp[SerializationGuidelines#2](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#2)]
     [!code-vb[SerializationGuidelines#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#2)]  
  
3. Seri durumdan çıkarılmış örnekleri başlatma için serileştirme geri çağırmaları kullanmayı DÜŞÜNÜN.  
  
     Nesneler seri durumdan kaldırıldığında oluşturucular çağrılmaz. Bu nedenle, normal oluşturma sırasında yürütülen tüm mantığın *serileştirme geri çağırmalarından*biri olarak uygulanması gerekir.  
  
     [!code-csharp[SerializationGuidelines#3](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#3)]
     [!code-vb[SerializationGuidelines#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#3)]  
  
     <xref:System.Runtime.Serialization.OnDeserializedAttribute> özniteliği en yaygın olarak kullanılan geri çağırma özniteliğidir. Ailedeki diğer öznitelikler <xref:System.Runtime.Serialization.OnDeserializingAttribute>, <xref:System.Runtime.Serialization.OnSerializingAttribute>ve <xref:System.Runtime.Serialization.OnSerializedAttribute>. Seri durumundan çıkarma, serileştirme önce ve son olarak seri hale getirme sonra önce sırasıyla yürütülen geri çağırmaları işaretlemek için kullanılabilir.  
  
4. DÜŞÜNÜN kullanarak <xref:System.Runtime.Serialization.KnownTypeAttribute> karmaşık Nesne grafiği işlenirken kullanılması gereken somut türler belirtmek için.  
  
     Örneğin, seri durumdan çıkarılmış bir veri üyesinin türü bir soyut sınıf tarafından temsil ediliyorsa, seri hale getirici, hangi somut türün örneklendirileceğine ve üyeye atanacağına karar vermek için *bilinen tür* bilgilerine gereksinim duyar. Bilinen tür özniteliği kullanılarak belirtilmemişse, seri hale getirici 'e açıkça geçirilmesi gerekecektir (bunu, bilinen türleri seri hale getirici oluşturucusuna geçirerek yapabilirsiniz) veya yapılandırma dosyasında belirtilmesi gerekir.  
  
     [!code-csharp[SerializationGuidelines#4](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#4)]
     [!code-vb[SerializationGuidelines#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#4)]  
  
     Bilinen türlerin listesinin statik olarak bilinmediği durumlarda ( **kişi** sınıfı derlendiğinde), **KnownTypeAttribute** , çalışma zamanında bilinen türlerin bir listesini döndüren bir yönteme da işaret edebilir.  
  
5. Oluştururken veya serializable türler değiştirme İleri ve geriye dönük uyumluluk düşünün.  
  
     Bu türden gelecek sürümlerin serileştirilmiş akışlarının, türün geçerli sürümüne seri durumdan çıkarılabileceğini ve bunun tersini aklınızda bulundurun. Veri sözleşmesi özniteliklerine açık parametreler kullanarak sözleşmeyi korumak için özel bir işlem yapılmadığı takdirde, hatta özel ve dahili olan veri üyelerinin, ad, tür ve hatta sıralarını bu türün gelecekteki sürümlerinde değiştiremediğinize emin olun. . Seri hale getirilebilir türlerde değişiklik yaparken serileştirme test uyumluluğu. Yeni sürümü eski bir sürüme serisini çıkarmayı deneyin, tersi de geçerlidir.  
  
6. Türün farklı sürümleri arasında gidiş dönüşü sağlamak için <xref:System.Runtime.Serialization.IExtensibleDataObject> arabirimini uygulamayı düşünün.  
  
     Arabirim, seri hale getiricinin, gidiş dönüşü sırasında hiçbir veri kaybolmamasını sağlar. <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> Özelliği olan geçerli sürümü için bilinmeyen tür, gelecekteki sürümüne tüm verileri depolar. Geçerli sürüm daha sonra seri hale getirilmişse ve gelecekteki bir sürüme seri durumdan çıkarılacağından, ek veriler, ' ın ' de **ExtensionData** Özellik değeri aracılığıyla serileştirilmiş akışta kullanılabilir.  
  
     [!code-csharp[SerializationGuidelines#5](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#5)]
     [!code-vb[SerializationGuidelines#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#5)]  
  
     Daha fazla bilgi için bkz. [Ileri uyumlu veri sözleşmeleri](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
#### <a name="supporting-xml-serialization"></a>XML Serileştirmeyi destekleme  
 Veri anlaşması serileştirme .NET Framework, ancak veri sözleşmesi serileştirmesi tarafından desteklenmeyen serileştirme senaryoları vardır. Örneğin, seri hale getirici tarafından üretilen veya tüketilen XML şekli üzerinde size tam denetim vermez. Bu tür hassas denetim gerekliyse, *XML serileştirmesi* kullanılmalıdır ve bu serileştirme teknolojisini desteklemek için türlerinizi tasarlamanız gerekir.  
  
1. Oluşturulan XML şeklini denetlemek için çok güçlü bir nedeniniz yoksa, özel olarak XML serileştirme için türlerinizi tasarlamaktan KAÇıNıN. Bu serileştirme teknolojisinin yerini, önceki bölümde ele alınan veri sözleşmesi serileştirmesi almıştır.  
  
     Diğer bir deyişle, türün XML serileştirme ile kullanılacağını bilmiyorsanız, <xref:System.Xml.Serialization> ad alanından yeni türlere öznitelikler uygulamayın. Aşağıdaki örnek, **System. xml. Serialization** öğesinin xml tarafından üretilen şekli denetlemek için nasıl kullanılabileceğini gösterir.  
  
     [!code-csharp[SerializationGuidelines#6](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#6)]
     [!code-vb[SerializationGuidelines#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#6)]  
  
2. XML serileştirme özniteliklerini uygulayarak, seri hale getirilen XML 'nin şekli üzerinde daha fazla denetime sahip olmak istiyorsanız, <xref:System.Xml.Serialization.IXmlSerializable> arabirimini uygulamayı düşünün. <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> ve <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>arabirimin iki yöntemi, serileştirilmiş XML akışını tam olarak denetlemenize olanak tanır. Ayrıca, <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> özniteliği uygulanarak tür için oluşturulan XML şemasını da denetleyebilirsiniz.  
  
#### <a name="supporting-runtime-serialization"></a>Çalışma zamanı serileştirmesini destekleme  
 *Çalışma zamanı serileştirme* .NET uzaktan iletişim tarafından kullanılan bir teknolojidir. Türlerinizi .NET uzaktan Iletişim kullanılarak aktarılyacağını düşünüyorsanız, çalışma zamanı serileştirmesini desteklediklerinden emin olmanız gerekir.  
  
 *Çalışma zamanı serileştirme* için temel destek <xref:System.SerializableAttribute> özniteliği uygulanarak sağlanır ve daha gelişmiş senaryolar basit bir *çalışma zamanı seri hale getirilebilir bir model* (uygulama-<xref:System.Runtime.Serialization.ISerializable> ve bir serileştirme Oluşturucusu sağlar) uygulamayı içerir.  
  
1. Çalışma zamanı serileştirme türlerinizi .NET uzaktan iletişim ile kullanılacaksa destekleyen DÜŞÜNÜN. Örneğin, <xref:System.AddIn> ad alanı .NET Remoting kullanır ve bu nedenle **System. AddIn** eklentileri arasında değiş tokuş edilen tüm türlerin çalışma zamanı serileştirmesini desteklemesi gerekir.  
  
     [!code-csharp[SerializationGuidelines#7](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#7)]
     [!code-vb[SerializationGuidelines#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#7)]  
  
2. Serileştirme işlemi üzerinde komple denetim istiyorsanız, *çalışma zamanı serileştirilebilir modelini* uygulamayı düşünün. Örneğin, verileri serileştirilmiş veya seri durumdan çıkarılan şekilde dönüştürmek istiyorsanız.  
  
     Düzen çok basit yöneliktir. Yapmanız gereken tek şey <xref:System.Runtime.Serialization.ISerializable> arabirimini uygular ve nesne seri durumdan çıkarıldığınızda kullanılan özel bir oluşturucu sağlar.  
  
     [!code-csharp[SerializationGuidelines#8](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#8)]
     [!code-vb[SerializationGuidelines#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#8)]  
  
3. Serileştirme oluşturucuyu korumalı hale getirin ve burada örnekte gösterildiği gibi, tam olarak adlandırılan ve adında iki parametre sağlayın.  
  
     [!code-csharp[SerializationGuidelines#9](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#9)]
     [!code-vb[SerializationGuidelines#9](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#9)]  
  
4. ISerializable üyelerini açıkça uygulayın.  
  
     [!code-csharp[SerializationGuidelines#10](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#10)]
     [!code-vb[SerializationGuidelines#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#10)]  
  
5. **ISerializable. GetObjectData** uygulamasına bir bağlantı isteği uygulayın. Bu, yalnızca tam olarak güvenilen çekirdek ve çalışma zamanı serileştirici üyeye erişimine sahip olmasını sağlar.  
  
     [!code-csharp[SerializationGuidelines#11](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#11)]
     [!code-vb[SerializationGuidelines#11](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#11)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Veri Anlaşmalarını Kullanma](../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [Veri Anlaşması Seri Hale Getirici](../../../docs/framework/wcf/feature-details/data-contract-serializer.md)
- [Veri Anlaşması Seri Hale Getirici Tarafından Desteklenen Türler](../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
- [İkili Serileştirme](binary-serialization.md)
- [.NET uzaktan Iletişim](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))
- [XML ve SOAP Serileştirme](xml-and-soap-serialization.md)
- [Güvenlik ve serileştirme](../../../docs/framework/misc/security-and-serialization.md)
