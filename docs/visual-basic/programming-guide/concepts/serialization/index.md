---
title: Serileştirme
ms.date: 07/20/2015
ms.assetid: 67379a76-5465-4af8-a781-0b0b25a62d9a
ms.openlocfilehash: 9ce97e541cb204b92663464e36d9e8f221ccc3f2
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351913"
---
# <a name="serialization-visual-basic"></a>Serileştirme (Visual Basic)
Serileştirme, nesneyi depolamak veya belleğe, veritabanına veya bir dosyaya aktarmak için bir nesneyi bayt akışına dönüştürme işlemidir. Temel amacı, bir nesnenin durumunu gerektiğinde yeniden oluşturmak için kaydetmeyecektir. Ters işlem serisini kaldırma olarak adlandırılır.  
  
## <a name="how-serialization-works"></a>Serileştirme çalışma şekli  
 Bu çizimde serileştirme işleminin genel işlemi gösterilmektedir.  
  
![Serileştirme grafiği](./media/index/serialization-process.gif)
  
 Nesne yalnızca verileri değil bir akışa serileştirilir, ancak nesnenin sürümü, kültürü ve derleme adı gibi bilgiler hakkında bilgi. Bu akıştan, bir veritabanında, bir dosyada veya bellekte depolanabilir.  
  
### <a name="uses-for-serialization"></a>Serileştirme için kullanımlar  
 Serileştirme, geliştiricinin bir nesnenin durumunu kaydetmesine ve bu verileri gerektiği gibi yeniden oluşturmasından, Ayrıca nesnelerin depolanmasını ve veri değişimini sağlar. Bir geliştirici, serileştirme aracılığıyla nesneyi bir Web hizmeti aracılığıyla uzak uygulamaya gönderme, bir etki alanından diğerine geçirme, bir nesneyi bir güvenlik duvarı üzerinden bir XML dizesi olarak geçirme veya güvenliği koruma gibi eylemler gerçekleştirebilir. uygulamalar arasında kullanıcıya özgü bilgiler.  
  
### <a name="making-an-object-serializable"></a>Bir nesneyi seri hale getirilebilir hale getirme  
 Bir nesneyi seri hale getirmek için, seri hale getirilecek nesnenin, seri hale getirilen nesneyi içeren bir akışın ve bir <xref:System.Runtime.Serialization.Formatter>olması gerekir. <xref:System.Runtime.Serialization> nesneleri serileştirmek ve seri durumdan çıkarmak için gerekli sınıfları içerir.  
  
 Bu türün örneklerinin seri hale getirilebilir olduğunu göstermek için <xref:System.SerializableAttribute> özniteliğini bir türe uygulayın. Seri hale getirme girişiminde bulunursa bir <xref:System.Runtime.Serialization.SerializationException> özel durumu oluşturulur ancak türün <xref:System.SerializableAttribute> özniteliği yok.  
  
 Sınıfınızın içindeki bir alanın seri hale getirilebilir olmasını istemiyorsanız <xref:System.NonSerializedAttribute> özniteliğini uygulayın. Seri hale getirilebilir türdeki bir alan belirli bir ortama özel bir işaretçi, tanıtıcı veya başka bir veri yapısı içeriyorsa ve alan farklı bir ortamda anlamlı bir reconstituted değilse, bu durumda seri hale getirilebilir olmayan bir şekilde oluşturulabilir.  
  
 Serileştirilmiş bir sınıf, <xref:System.SerializableAttribute>olarak işaretlenen diğer sınıfların nesnelerine başvurular içeriyorsa, bu nesneler de serileştirilir.  
  
## <a name="binary-and-xml-serialization"></a>İkili ve XML serileştirme  
 İkili veya XML serileştirme kullanılabilir. İkili serileştirme ' de, salt okunan, hatta tüm Üyeler ve performans geliştirilir. XML serileştirme, nesne paylaşımının ve birlikte çalışabilirlik amacıyla kullanımının daha fazla esnekliğine sahip olmak üzere daha okunabilir kod sağlar.  
  
### <a name="binary-serialization"></a>İkili Serileştirme  
 İkili serileştirme, depolama veya soket tabanlı ağ akışları gibi kullanımlar için sıkıştırılmış serileştirme oluşturmak üzere ikili kodlama kullanır.  
  
### <a name="xml-serialization"></a>XML seri hale getirme  
 XML serileştirme, bir nesnenin ortak alanlarını ve özelliklerini veya parametrelerinin parametrelerini ve dönüş değerlerini belirli bir XML şeması tanım dili (XSD) belgesine uygun bir XML akışı olarak serileştirir. XML serileştirme, XML 'e dönüştürülen ortak özellikler ve alanlarla kesin olarak belirlenmiş sınıflarda oluşur. <xref:System.Xml.Serialization>, XML serileştirilmek ve seri durumdan çıkarmak için gerekli sınıfları içerir.  
  
 Sınıfın bir örneğini seri hale getirmek veya seri hale getirmek <xref:System.Xml.Serialization.XmlSerializer> denetlemek için sınıflara ve sınıf üyelerine öznitelikler uygulayabilirsiniz.  
  
## <a name="basic-and-custom-serialization"></a>Temel ve özel serileştirme  
 Serileştirme, temel ve özel olmak üzere iki şekilde gerçekleştirilebilir. Temel serileştirme, nesneyi otomatik olarak seri hale getirmek için .NET Framework kullanır.  
  
### <a name="basic-serialization"></a>Temel Serileştirme  
 Temel seri hale getirmeyle ilgili tek gereksinim, nesnenin <xref:System.SerializableAttribute> özniteliğin uygulanmış olması olur. <xref:System.NonSerializedAttribute>, belirli alanların serileştirilme tutulmasını sağlamak için kullanılabilir.  
  
 Temel serileştirme kullandığınızda nesnelerin sürümü oluşturma sorunları oluşturabilir, bu durumda özel serileştirme tercih edilebilir. Temel serileştirme, serileştirme gerçekleştirmenin en kolay yoludur, ancak süreç üzerinde çok fazla denetim sağlamaz.  
  
### <a name="custom-serialization"></a>Özel Serileştirme  
 Özel seri hale getirmek için, tam olarak hangi nesnelerin serileştirildiği ve nasıl yapılacağını belirtebilirsiniz. Sınıfın <xref:System.SerializableAttribute> işaretlenmesi ve <xref:System.Runtime.Serialization.ISerializable> arabirimini uygulamanız gerekir.  
  
 Nesnenizin bir özel şekilde seri durumdan çıkarılabilmesini istiyorsanız özel bir Oluşturucu kullanmanız gerekir.  
  
## <a name="designer-serialization"></a>Tasarımcı serileştirme  
 Tasarımcı serileştirme, genellikle geliştirme araçlarıyla ilişkili nesne kalıcılığı türünü içeren özel bir serileştirme biçimidir. Tasarımcı serileştirme bir nesne grafiğini, daha sonra nesne grafiğini kurtarmak için kullanılabilecek bir kaynak dosyaya dönüştürme işlemidir. Kaynak dosya, kod, biçimlendirme veya hatta SQL tablo bilgisi içerebilir.  
  
## <a name="BKMK_RelatedTopics"></a>İlgili konular ve örnekler  
 [İzlenecek yol: Visual Studio 'da bir nesneyi kalıcı hale getirme (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/walkthrough-persisting-an-object-in-visual-studio.md)  
 Serileştirme 'in nesnelerin örnekleri arasında bir nesne verilerini kalıcı hale getirmek için nasıl kullanılabileceğini gösterir. Bu, değerleri depolamanızı ve nesnenin bir sonraki örneklendirilmesi durumunda bunları almanızı sağlar.  
  
 [Nasıl yapılır: bir XML dosyasından nesne verilerini okuma (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md)  
 Daha önce <xref:System.Xml.Serialization.XmlSerializer> sınıfını kullanarak bir XML dosyasına yazılmış nesne verilerinin nasıl okunacağını gösterir.  
  
 [Nasıl yapılır: nesne verilerini bir XML dosyasına yazma (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)  
 <xref:System.Xml.Serialization.XmlSerializer> sınıfını kullanarak bir sınıftan XML dosyasına nesnenin nasıl yazılacağını gösterir.
