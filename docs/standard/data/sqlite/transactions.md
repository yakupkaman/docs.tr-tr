---
title: İşlemler
ms.date: 12/13/2019
description: İşlemleri nasıl kullanacağınızı öğrenin.
ms.openlocfilehash: 4b72a1573a560ffd1bfd0f54d46ab3b135280976
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75447141"
---
# <a name="transactions"></a><span data-ttu-id="88b05-103">İşlemler</span><span class="sxs-lookup"><span data-stu-id="88b05-103">Transactions</span></span>

<span data-ttu-id="88b05-104">İşlemler, birden çok SQL deyimini veritabanına tek bir atomik birim olarak işlenen tek bir iş biriminde gruplandırmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="88b05-104">Transactions let you group multiple SQL statements into a single unit of work that is committed to the database as one atomic unit.</span></span> <span data-ttu-id="88b05-105">İşlemdeki herhangi bir deyim başarısız olursa, önceki deyimler tarafından yapılan değişiklikler geri alınabilir.</span><span class="sxs-lookup"><span data-stu-id="88b05-105">If any statement in the transaction fails, changes made by the previous statements can be rolled back.</span></span> <span data-ttu-id="88b05-106">İşlem başlatıldığında veritabanının ilk durumu korunur.</span><span class="sxs-lookup"><span data-stu-id="88b05-106">The initial state of the database when the transaction was started is preserved.</span></span> <span data-ttu-id="88b05-107">Bir işlemin kullanılması, veritabanında aynı anda çok sayıda değişiklik yaparken SQLite 'un performansını da artırır.</span><span class="sxs-lookup"><span data-stu-id="88b05-107">Using a transaction can also improve performance on SQLite when making numerous changes to the database at once.</span></span>

## <a name="concurrency"></a><span data-ttu-id="88b05-108">Eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="88b05-108">Concurrency</span></span>

<span data-ttu-id="88b05-109">SQLite 'ta, tek seferde veritabanında bekleyen değişikliklere yalnızca bir işlem izin verilir.</span><span class="sxs-lookup"><span data-stu-id="88b05-109">In SQLite, only one transaction is allowed to have changes pending in the database at a time.</span></span> <span data-ttu-id="88b05-110">Bu nedenle, başka bir işlemin tamamlanabilmesi çok uzun sürerse <xref:Microsoft.Data.Sqlite.SqliteCommand> <xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> ve `Execute` yöntemlerine yapılan çağrılar zaman aşımına uğrar.</span><span class="sxs-lookup"><span data-stu-id="88b05-110">Because of this, calls to <xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> and the `Execute` methods on <xref:Microsoft.Data.Sqlite.SqliteCommand> may time out if another transaction takes too long to complete.</span></span>

<span data-ttu-id="88b05-111">Kilitleme, yeniden denemeler ve zaman aşımları hakkında daha fazla bilgi için bkz. [veritabanı hataları](database-errors.md).</span><span class="sxs-lookup"><span data-stu-id="88b05-111">For more information about locking, retries, and timeouts, see [Database errors](database-errors.md).</span></span>

## <a name="isolation-levels"></a><span data-ttu-id="88b05-112">Yalıtım düzeyleri</span><span class="sxs-lookup"><span data-stu-id="88b05-112">Isolation levels</span></span>

<span data-ttu-id="88b05-113">İşlem, SQLite içinde varsayılan olarak **seri hale getirilebilir** .</span><span class="sxs-lookup"><span data-stu-id="88b05-113">Transactions are **serializable** by default in SQLite.</span></span> <span data-ttu-id="88b05-114">Bu yalıtım düzeyi, bir işlem içinde yapılan tüm değişikliklerin tamamen yalıtılmış olmasını güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="88b05-114">This isolation level guarantees that any changes made within a transaction are completely isolated.</span></span> <span data-ttu-id="88b05-115">İşlemin dışında yürütülen diğer deyimler işlemin değişikliklerinden etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="88b05-115">Other statements executed outside of the transaction aren't affected by the transaction's changes.</span></span>

<span data-ttu-id="88b05-116">SQLite, paylaşılan bir önbellek kullanılırken **read UNCOMMITTED** öğesini de destekler.</span><span class="sxs-lookup"><span data-stu-id="88b05-116">SQLite also supports **read uncommitted** when using a shared cache.</span></span> <span data-ttu-id="88b05-117">Bu düzey, kirli okuma, tekrarlanabilir okuma ve hayalet düzeylerine izin verir:</span><span class="sxs-lookup"><span data-stu-id="88b05-117">This level allows dirty reads, nonrepeatable reads, and phantoms:</span></span>

- <span data-ttu-id="88b05-118">Bir işlemde bekleyen değişiklikler işlem dışında bir sorgu tarafından döndürüldüğünde *kirli okuma* oluşur, ancak işlemdeki değişiklikler geri alınır.</span><span class="sxs-lookup"><span data-stu-id="88b05-118">A *dirty read* occurs when changes pending in one transaction are returned by a query outside of the transaction, but the changes in the transaction are rolled back.</span></span> <span data-ttu-id="88b05-119">Sonuçlar veritabanına hiçbir daha önce teslim edilmemiş verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="88b05-119">The results contain data that was never actually committed to the database.</span></span>

- <span data-ttu-id="88b05-120">Bir işlem aynı satırı iki kez sorguladığında, *tekrarlanabilir bir okuma* gerçekleşir, ancak başka bir işlem tarafından iki sorgu arasında değiştirildiğinden sonuçlar farklıdır.</span><span class="sxs-lookup"><span data-stu-id="88b05-120">A *nonrepeatable read* occurs when a transaction queries same row twice, but the results are different because it was changed between the two queries by another transaction.</span></span>

- <span data-ttu-id="88b05-121">*Hayali* nesnelerin, bir işlem sırasında bir sorgunun where yan tümcesini karşılamak için değiştirilen veya eklenen satırlardır.</span><span class="sxs-lookup"><span data-stu-id="88b05-121">*Phantoms* are rows that get changed or added to meet the where clause of a query during a transaction.</span></span> <span data-ttu-id="88b05-122">İzin veriliyorsa aynı sorgu aynı işlemde iki kez yürütüldüğünde aynı sorgu farklı satırlar döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="88b05-122">If allowed, the same query could return different rows when executed twice in the same transaction.</span></span>

<span data-ttu-id="88b05-123">Microsoft. Data. SQLite, <xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> geçirilen IsolationLevel 'ı en düşük düzey olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="88b05-123">Microsoft.Data.Sqlite treats the IsolationLevel passed to <xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> as a minimum level.</span></span> <span data-ttu-id="88b05-124">Gerçek yalıtım düzeyi READ UNCOMMITTED veya Serializable olarak yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="88b05-124">The actual isolation level will be promoted to either read uncommitted or serializable.</span></span>

<span data-ttu-id="88b05-125">Aşağıdaki kod, bir kirli okumayı benzetir.</span><span class="sxs-lookup"><span data-stu-id="88b05-125">The following code simulates a dirty read.</span></span> <span data-ttu-id="88b05-126">Bağlantı dizesinin `Cache=Shared`içermesi gerektiğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="88b05-126">Note, the connection string must include `Cache=Shared`.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DirtyReadSample/Program.cs?name=snippet_DirtyRead)]