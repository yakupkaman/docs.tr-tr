---
title: Bulutta yerel uygulamalarda elaun arama
description: Bulutta yerel uygulamalara elastik arama özellikleri ekleme hakkında bilgi edinin.
author: robvet
ms.date: 01/22/2020
ms.openlocfilehash: 6ea237eddc89a8c6843d6b34b05b1b71515a99b6
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794879"
---
# <a name="elasticsearch-in-a-cloud-native-app"></a><span data-ttu-id="99f24-103">Bulutta yerel bir uygulamada elaun arama</span><span class="sxs-lookup"><span data-stu-id="99f24-103">Elasticsearch in a cloud-native app</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="99f24-104">Elaun Search, farklı türlerde veriler arasında karmaşık arama özellikleri sağlayan bir dağıtılmış arama ve analiz sistemidir.</span><span class="sxs-lookup"><span data-stu-id="99f24-104">Elasticsearch is a distributed search and analytics system that enables complex search capabilities across diverse types of data.</span></span> <span data-ttu-id="99f24-105">Açık kaynak ve yaygın popüler.</span><span class="sxs-lookup"><span data-stu-id="99f24-105">It's open source and widely popular.</span></span> <span data-ttu-id="99f24-106">Aşağıdaki şirketlerin, Elai aramasını kendi uygulamasına nasıl tümleştirtireceğini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="99f24-106">Consider how the following companies integrate Elasticsearch into their application:</span></span>

- <span data-ttu-id="99f24-107">Tam metin ve artımlı (yazarken ara) araması için [Vikipedi](https://blog.wikimedia.org/2014/01/06/wikimedia-moving-to-elasticsearch/) .</span><span class="sxs-lookup"><span data-stu-id="99f24-107">[Wikipedia](https://blog.wikimedia.org/2014/01/06/wikimedia-moving-to-elasticsearch/) for full-text and incremental (search as you type) searching.</span></span>
- <span data-ttu-id="99f24-108">8\.000.000 kod depolarında dizin oluşturmak ve kullanıma sunmak için [GitHub](https://www.elastic.co/customers/github) .</span><span class="sxs-lookup"><span data-stu-id="99f24-108">[GitHub](https://www.elastic.co/customers/github) to index and expose over 8 million code repositories.</span></span>  
- <span data-ttu-id="99f24-109">Kapsayıcı kitaplığını bulunabilir hale getirmek için [Docker](https://www.elastic.co/customers/docker) .</span><span class="sxs-lookup"><span data-stu-id="99f24-109">[Docker](https://www.elastic.co/customers/docker) for making its container library discoverable.</span></span>

<span data-ttu-id="99f24-110">Elaun Search, [Apache Lucene](https://lucene.apache.org/core/) tam metin arama altyapısının üzerine kurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="99f24-110">Elasticsearch is built on top of the [Apache Lucene](https://lucene.apache.org/core/) full-text search engine.</span></span> <span data-ttu-id="99f24-111">Lucene yüksek performanslı belge dizini oluşturma ve sorgulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="99f24-111">Lucene provides high-performance document indexing and querying.</span></span> <span data-ttu-id="99f24-112">Ters erişimli bir dizin oluşturma düzeniyle verileri dizinlendirir; sayfaları anahtar sözcüklere eşlemek yerine, bir kitabın sonundaki bir sözlükte olduğu gibi, anahtar sözcükleri sayfalara eşler.</span><span class="sxs-lookup"><span data-stu-id="99f24-112">It indexes data with an inverted indexing scheme – instead of mapping pages to keywords, it maps keywords to pages just like a glossary at the end of a book.</span></span> <span data-ttu-id="99f24-113">Lucene güçlü sorgu sözdizimi özelliklerine sahiptir ve verileri şu şekilde sorgulayabilir:</span><span class="sxs-lookup"><span data-stu-id="99f24-113">Lucene has powerful query syntax capabilities and can query data by:</span></span>

- <span data-ttu-id="99f24-114">Terim (tam kelime)</span><span class="sxs-lookup"><span data-stu-id="99f24-114">Term (a full word)</span></span> 
- <span data-ttu-id="99f24-115">Ön ek (Word ile başlar)</span><span class="sxs-lookup"><span data-stu-id="99f24-115">Prefix (starts-with word)</span></span>
- <span data-ttu-id="99f24-116">Joker karakter ("\*" veya "?" filtrelerini kullanarak)</span><span class="sxs-lookup"><span data-stu-id="99f24-116">Wildcard (using "\*" or "?" filters)</span></span>
- <span data-ttu-id="99f24-117">Tümcecik (bir belgedeki metin dizisi)</span><span class="sxs-lookup"><span data-stu-id="99f24-117">Phrase (a sequence of text in a document)</span></span>
- <span data-ttu-id="99f24-118">Boole değeri (sorguları birleştiren karmaşık aramalar)</span><span class="sxs-lookup"><span data-stu-id="99f24-118">Boolean value (complex searches combining queries)</span></span>

<span data-ttu-id="99f24-119">Lucene arama için düşük düzey bir sıhhi tesisat sağlarken, Elaun Search, Lucene üzerinde bulunan sunucuyu sağlar.</span><span class="sxs-lookup"><span data-stu-id="99f24-119">While Lucene provides low-level plumbing for searching, Elasticsearch provides the server that sits on top of Lucene.</span></span> <span data-ttu-id="99f24-120">Elaun Search, Lucene 'in dizin oluşturma ve arama işlevselliğine erişme için yeniden bir API de dahil olmak üzere, çalışma Lucene 'i basitleştirmek için daha yüksek düzeyde işlevsellik ekler.</span><span class="sxs-lookup"><span data-stu-id="99f24-120">Elasticsearch adds higher-level functionality to simplify working Lucene, including a RESTful API to access Lucene’s indexing and searching functionality.</span></span> <span data-ttu-id="99f24-121">Ayrıca, büyük ölçeklenebilirlik, hataya dayanıklılık ve yüksek kullanılabilirliğe sahip dağıtılmış bir altyapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="99f24-121">It also provides a distributed infrastructure capable of massive scalability, fault tolerance, and high availability.</span></span>

<span data-ttu-id="99f24-122">Karmaşık arama gereksinimlerine sahip daha büyük bulut yerel uygulamalar için, Azure 'da yönetilen hizmet olarak Elaun Search kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99f24-122">For larger cloud-native applications with complex search requirements, Elasticsearch is available as managed service in Azure.</span></span> <span data-ttu-id="99f24-123">Microsoft Azure Market, geliştiricilerin Azure 'da bir elaya arama kümesi dağıtmak için kullanabileceği önceden yapılandırılmış Şablonlar sunar.</span><span class="sxs-lookup"><span data-stu-id="99f24-123">The Microsoft Azure Marketplace features preconfigured templates which developers can use to deploy an Elasticsearch cluster on Azure.</span></span>

<span data-ttu-id="99f24-124">Microsoft Azure Market, geliştiriciler Azure 'da bir elaa arama kümesini hızlı bir şekilde dağıtmak için oluşturulmuş önceden yapılandırılmış şablonları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="99f24-124">From the Microsoft Azure Marketplace, developers can use preconfigured templates built to quickly deploy an Elasticsearch cluster on Azure.</span></span> <span data-ttu-id="99f24-125">Azure tarafından yönetilen teklifi kullanarak en çok 50 veri düğümü, 20 koordinasyon düğümü ve üç adanmış ana düğüm dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99f24-125">Using the Azure-managed offering, you can deploy up to 50 data nodes, 20 coordinating nodes, and three dedicated master nodes.</span></span>

## <a name="summary"></a><span data-ttu-id="99f24-126">Özet</span><span class="sxs-lookup"><span data-stu-id="99f24-126">Summary</span></span>

<span data-ttu-id="99f24-127">Bu bölümde, bulutta yerel sistemlerdeki verilere ayrıntılı bir bakış sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="99f24-127">This chapter presented a detailed look at data in cloud-native systems.</span></span> <span data-ttu-id="99f24-128">Bulut Yerel sistemlerdeki veri depolama desenleriyle tek parçalı uygulamalarda veri depolama alanı ile çalışmaya başladık.</span><span class="sxs-lookup"><span data-stu-id="99f24-128">We started by contrasting data storage in monolithic applications with data storage patterns in cloud-native systems.</span></span> <span data-ttu-id="99f24-129">Platformlar arası, dağıtılmış işlemler ve yüksek hacimli sistemlerle başa çıkmak üzere desenler de dahil olmak üzere, bulutta yerel sistemlerde uygulanan veri desenlerine baktık.</span><span class="sxs-lookup"><span data-stu-id="99f24-129">We looked at data patterns implemented in cloud-native systems, including cross-service queries, distributed transactions, and patterns to deal with high-volume systems.</span></span> <span data-ttu-id="99f24-130">NoSQL verileriyle SQL 'in maliyetli olduğunu belirledik.</span><span class="sxs-lookup"><span data-stu-id="99f24-130">We contrasted SQL with NoSQL data.</span></span> <span data-ttu-id="99f24-131">Azure 'da bulunan ve hem Microsoft merkezli hem de açık kaynaklı seçenekleri içeren veri depolama seçeneklerine baktık.</span><span class="sxs-lookup"><span data-stu-id="99f24-131">We looked at data storage options available in Azure that include both Microsoft-centric and open-source options.</span></span> <span data-ttu-id="99f24-132">Son olarak, önbelleğe alma ve elak aramasını bulutta yerel bir uygulamada ele aldık.</span><span class="sxs-lookup"><span data-stu-id="99f24-132">Finally, we discussed caching and Elasticsearch in a cloud-native application.</span></span>

### <a name="references"></a><span data-ttu-id="99f24-133">Referanslar</span><span class="sxs-lookup"><span data-stu-id="99f24-133">References</span></span>

- [<span data-ttu-id="99f24-134">Komut ve Sorgu Sorumluluklarının Ayrılığı (CQRS) deseninin</span><span class="sxs-lookup"><span data-stu-id="99f24-134">Command and Query Responsibility Segregation (CQRS) pattern</span></span>](https://docs.microsoft.com/azure/architecture/patterns/cqrs)

- [<span data-ttu-id="99f24-135">Olay kaynağını belirleme kalıbı</span><span class="sxs-lookup"><span data-stu-id="99f24-135">Event Sourcing pattern</span></span>](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)

- [<span data-ttu-id="99f24-136">RDBMSs vs. NoSQL veritabanları: genel bakış</span><span class="sxs-lookup"><span data-stu-id="99f24-136">RDBMSs vs. NoSQL Databases: Overview</span></span>](https://maxivak.com/rdbms-vs-nosql-databases/)

- [<span data-ttu-id="99f24-137">Neden RDBMS bölümü dayanıklı değildir ve neden kullanılabilir?</span><span class="sxs-lookup"><span data-stu-id="99f24-137">Why isn't RDBMS Partition Tolerant in CAP Theorem and why is it Available?</span></span>](https://stackoverflow.com/questions/36404765/why-isnt-rdbms-partition-tolerant-in-cap-theorem-and-why-is-it-available)

- [<span data-ttu-id="99f24-138">Gerçekleştirilmiş görünüm</span><span class="sxs-lookup"><span data-stu-id="99f24-138">Materialized View</span></span>](https://docs.microsoft.com/azure/architecture/patterns/materialized-view)

- [<span data-ttu-id="99f24-139">Açık kaynak veritabanları hakkında bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="99f24-139">All you really need to know about open source databases</span></span>](https://www.ibm.com/blogs/systems/all-you-really-need-to-know-about-open-source-databases/)

- [<span data-ttu-id="99f24-140">Telafi Işlem kriteri</span><span class="sxs-lookup"><span data-stu-id="99f24-140">Compensating Transaction pattern</span></span>](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction)

- [<span data-ttu-id="99f24-141">Saga kalıbı</span><span class="sxs-lookup"><span data-stu-id="99f24-141">Saga Pattern</span></span>](https://microservices.io/patterns/data/saga.html)

- [<span data-ttu-id="99f24-142">Saga desenleri | Mikro hizmetleri kullanarak iş işlemlerini uygulama</span><span class="sxs-lookup"><span data-stu-id="99f24-142">Saga Patterns | How to implement business transactions using microservices</span></span>](https://blog.couchbase.com/saga-pattern-implement-business-transactions-using-microservices-part/)

- [<span data-ttu-id="99f24-143">Telafi Işlem kriteri</span><span class="sxs-lookup"><span data-stu-id="99f24-143">Compensating Transaction pattern</span></span>](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction)

- [<span data-ttu-id="99f24-144">9-Ball ' ın arkasında alma: Cosmos DB tutarlılık düzeyleri açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="99f24-144">Getting Behind the 9-Ball: Cosmos DB Consistency Levels Explained</span></span>](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/)

- [<span data-ttu-id="99f24-145">Farklı NoSQL veritabanlarının Bölüm II türlerini keşfetme</span><span class="sxs-lookup"><span data-stu-id="99f24-145">Exploring the different types of NoSQL Databases Part II</span></span>](https://www.3pillarglobal.com/insights/exploring-the-different-types-of-nosql-databases)

- [<span data-ttu-id="99f24-146">RDBMS 'de NoSQL ve NewSQL veritabanları. John Ryan ile görüşme</span><span class="sxs-lookup"><span data-stu-id="99f24-146">On RDBMS, NoSQL and NewSQL databases. Interview with John Ryan</span></span>](http://www.odbms.org/blog/2018/03/on-rdbms-nosql-and-newsql-databases-interview-with-john-ryan/)
  
- [<span data-ttu-id="99f24-147">SQL vs NoSQL vs NewSQL: tam karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="99f24-147">SQL vs NoSQL vs NewSQL: The Full Comparison</span></span>](https://www.xenonstack.com/blog/sql-vs-nosql-vs-newsql/)

- [<span data-ttu-id="99f24-148">TIRE: Kubernetes-Native veritabanlarının dört özelliği</span><span class="sxs-lookup"><span data-stu-id="99f24-148">DASH: Four Properties of Kubernetes-Native Databases</span></span>](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/)

- [<span data-ttu-id="99f24-149">CockroachDB</span><span class="sxs-lookup"><span data-stu-id="99f24-149">CockroachDB</span></span>](https://www.cockroachlabs.com/)

- [<span data-ttu-id="99f24-150">TiDB</span><span class="sxs-lookup"><span data-stu-id="99f24-150">TiDB</span></span>](https://pingcap.com/en/)

- [<span data-ttu-id="99f24-151">Yugabrivtedb</span><span class="sxs-lookup"><span data-stu-id="99f24-151">YugabyteDB</span></span>](https://www.yugabyte.com/)

- [<span data-ttu-id="99f24-152">Vitess</span><span class="sxs-lookup"><span data-stu-id="99f24-152">Vitess</span></span>](https://vitess.io/)

- [<span data-ttu-id="99f24-153">Elana Search: kesin kılavuz</span><span class="sxs-lookup"><span data-stu-id="99f24-153">Elasticsearch: The Definitive Guide</span></span>](http://shop.oreilly.com/product/0636920028505.do)
  
- [<span data-ttu-id="99f24-154">Apache Lucene 'e giriş</span><span class="sxs-lookup"><span data-stu-id="99f24-154">Introduction to Apache Lucene</span></span>](https://www.baeldung.com/lucene)

>[!div class="step-by-step"]
><span data-ttu-id="99f24-155">[Önceki](azure-caching.md)
>[İleri](resiliency.md)</span><span class="sxs-lookup"><span data-stu-id="99f24-155">[Previous](azure-caching.md)
[Next](resiliency.md)</span></span> <!-- Next Chapter -->