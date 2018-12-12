---
title: Null başvuru türleri
description: Bu makalede eklenen boş değer atanabilir başvuru türleri, genel bir bakış sağlanmaktadır C# 8. Özellik null başvuru özel durumlar, yeni ve mevcut projeler için karşı güvenliği nasıl sağladığını öğreneceksiniz.
ms.date: 12/03/2018
ms.openlocfilehash: f18fc9dbce2f934b216b3eb0b80658fec6b44c46
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53156488"
---
# <a name="nullable-reference-types"></a><span data-ttu-id="f3644-104">Null başvuru türleri</span><span class="sxs-lookup"><span data-stu-id="f3644-104">Nullable reference types</span></span>

<span data-ttu-id="f3644-105">C#8.0 tanıtır **null başvuru türleri** ve **atanamayan başvuru türleri** önemli deyimleri hakkında başvuru türü değişkenler özelliklerini yapmanızı sağlayan:</span><span class="sxs-lookup"><span data-stu-id="f3644-105">C# 8.0 introduces **nullable reference types** and **non-nullable reference types** that enable you to make important statements about the properties for reference type variables:</span></span>

- <span data-ttu-id="f3644-106">**Başvuru null olması beklenen değil**.</span><span class="sxs-lookup"><span data-stu-id="f3644-106">**A reference is not supposed to be null**.</span></span> <span data-ttu-id="f3644-107">Değişkenleri null kullanılmaması, derleyici bu değişkenleri ilk olmadan başvuru güvenli olduğundan emin olun kuralları zorlar. null olmayan denetleniyor:</span><span class="sxs-lookup"><span data-stu-id="f3644-107">When variables aren't supposed to be null, the compiler enforces rules that ensure it is safe to dereference these variables without first checking that it isn't null:</span></span>
  - <span data-ttu-id="f3644-108">Değişken için bir null olmayan değer başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f3644-108">The variable must be initialized to a non-null value.</span></span>
  - <span data-ttu-id="f3644-109">Değişken değeri hiçbir zaman atanabilir `null`.</span><span class="sxs-lookup"><span data-stu-id="f3644-109">The variable can never be assigned the value `null`.</span></span>
- <span data-ttu-id="f3644-110">**Başvuru null**.</span><span class="sxs-lookup"><span data-stu-id="f3644-110">**A reference may be null**.</span></span> <span data-ttu-id="f3644-111">Değişkenleri null olabilir, derleyici bir null başvuru için doğru denetlediyseniz emin olmak için farklı kuralları zorlar.</span><span class="sxs-lookup"><span data-stu-id="f3644-111">When variables may be null, the compiler enforces different rules to ensure that you've correctly checked for a null reference:</span></span>
  - <span data-ttu-id="f3644-112">Değer null değil derleyici garanti edebilir, değişken yalnızca başvurusu kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-112">The variable may only be dereferenced when the compiler can guarantee that the value isn't null.</span></span>
  - <span data-ttu-id="f3644-113">Bu değişkenler varsayılan başlatılması `null` değeri ve değer atanabilir `null` diğer kod.</span><span class="sxs-lookup"><span data-stu-id="f3644-113">These variables may be initialized with the default `null` value and may be assigned the value `null` in other code.</span></span>

<span data-ttu-id="f3644-114">Bu yeni özellik, önceki sürümlerinde başvuru değişkenleri işlenmesi üzerinden önemli avantajlar sağlar. C# tasarım amacı uygulanamadı belirlendiği değişken bildirimi.</span><span class="sxs-lookup"><span data-stu-id="f3644-114">This new feature provides significant benefits over the handling of reference variables in earlier versions of C# where the design intent couldn't be determined from the variable declaration.</span></span> <span data-ttu-id="f3644-115">Derleyici, başvuru türleri için null başvuru özel durumları karşı güvenliği sağlamadı:</span><span class="sxs-lookup"><span data-stu-id="f3644-115">The compiler didn't provide safety against null reference exceptions for reference types:</span></span>

- <span data-ttu-id="f3644-116">**Bir başvuru null olabilir**.</span><span class="sxs-lookup"><span data-stu-id="f3644-116">**A reference can be null**.</span></span> <span data-ttu-id="f3644-117">Bir başvuru türü null'a veya daha sonra null olarak atanan uyarı verilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-117">No warnings are issued when a reference type is initialized to null, or later assigned to null.</span></span>
- <span data-ttu-id="f3644-118">**Başvuru null değil olarak kabul edilir**.</span><span class="sxs-lookup"><span data-stu-id="f3644-118">**A reference is assumed to be not null**.</span></span> <span data-ttu-id="f3644-119">Derleyici, başvuru türleri başvurusu kaldırıldığında tüm uyarılar sorun değil.</span><span class="sxs-lookup"><span data-stu-id="f3644-119">The compiler doesn't issue any warnings when reference types are dereferenced.</span></span> <span data-ttu-id="f3644-120">(Null olabilir bir değişken başvuru olduğunda boş değer atanabilir başvurularla derleyici uyarıları verir).</span><span class="sxs-lookup"><span data-stu-id="f3644-120">(With nullable references,  the compiler issues warnings whenever you dereference a variable that may be null).</span></span>

<span data-ttu-id="f3644-121">A **boş değer atanabilir bir başvuru türü** aynı söz dizimini kullanarak belirtilen [boş değer atanabilen değer türleri](programming-guide/nullable-types/index.md): bir `?` değişkenin türüne eklenir.</span><span class="sxs-lookup"><span data-stu-id="f3644-121">A **nullable reference type** is noted using the same syntax as [nullable value types](programming-guide/nullable-types/index.md): a `?` is appended to the type of the variable.</span></span> <span data-ttu-id="f3644-122">Örneğin, bir null olabilen bir dize değişkeni aşağıdaki değişken bildirimini temsil eden `name`:</span><span class="sxs-lookup"><span data-stu-id="f3644-122">For example, the following variable declaration represents a nullable string variable, `name`:</span></span>

```csharp
string? name;
```

<span data-ttu-id="f3644-123">Herhangi bir değişken burada `?` değil eklenir adı türüdür bir **NULL olmayan bir başvuru türü**.</span><span class="sxs-lookup"><span data-stu-id="f3644-123">Any variable where the `?` is not appended to the type name is a **non-nullable reference type**.</span></span> <span data-ttu-id="f3644-124">Bu özellik etkinleştirildiğinde, varolan kodda tüm başvuru türü değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="f3644-124">That includes all reference type variables in existing code when you have enabled this feature.</span></span>

<span data-ttu-id="f3644-125">Derleyici statik analiz, null olmayan değer için boş değer atanabilir bir başvuru biliniyorsa belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f3644-125">The compiler uses static analysis to determine if a nullable reference is known to be non-null.</span></span> <span data-ttu-id="f3644-126">Null olabilir, boş değer atanabilir bir başvuru başvuru varsa derleyici sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="f3644-126">The compiler warns you if you dereference a nullable reference when it may be null.</span></span> <span data-ttu-id="f3644-127">Kullanarak bu davranışı geçersiz kılabilirsiniz **null forgiving işleci** (`!`) izleyen bir değişken adı.</span><span class="sxs-lookup"><span data-stu-id="f3644-127">You can override this behavior by using the **null-forgiving operator** (`!`) following a variable name.</span></span> <span data-ttu-id="f3644-128">Örneğin, biliyorsanız `name` değişken null değil ancak derleyici bir uyarı verir, derleyicinin analiz geçersiz kılmak için aşağıdaki kodu yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f3644-128">For example, if you know the `name` variable isn't null but the compiler issues a warning, you can write the following code to override the compiler's analysis:</span></span>

```csharp
name!.Length;
```

<span data-ttu-id="f3644-129">Bu işleci hakkında ayrıntıları edinebilirsiniz [Taslak null başvuru türleri](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types-specification.md#the-null-forgiving-operator) github'da belirtimi teklifi.</span><span class="sxs-lookup"><span data-stu-id="f3644-129">You can read details about this operator in the [draft nullable reference types](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types-specification.md#the-null-forgiving-operator) specification proposal on GitHub.</span></span>

## <a name="nullable-contexts"></a><span data-ttu-id="f3644-130">Boş değer atanabilir bağlamları</span><span class="sxs-lookup"><span data-stu-id="f3644-130">Nullable contexts</span></span>

<span data-ttu-id="f3644-131">Boş değer atanabilir bağlamları derleyici başvuru türü değişkenler yorumlaması için ayrıntılı denetim olanağı.</span><span class="sxs-lookup"><span data-stu-id="f3644-131">Nullable contexts enable fine-grained control for how the compiler interprets reference type variables.</span></span> <span data-ttu-id="f3644-132">Boş değer atanabilir bağlamı herhangi belirli kaynak satırı, `enabled` veya `disabled`.</span><span class="sxs-lookup"><span data-stu-id="f3644-132">The nullable context of any given source line is `enabled` or `disabled`.</span></span> <span data-ttu-id="f3644-133">Öncesi düşünebilirsinizC# tüm kodunuzda derleme olarak 8 derleyici bir `disabled` boş değer atanabilir Bağlam: Herhangi bir başvuru türü null olabilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-133">You can think of the pre-C# 8 compiler as compiling all your code in a `disabled` nullable context: Any reference type may be null.</span></span> <span data-ttu-id="f3644-134">Bir başvuru türü değişkenler başvurusu kaldırıldığında uyarı oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="f3644-134">Warnings are not generated when variables of a reference type are dereferenced.</span></span>

<span data-ttu-id="f3644-135">Boş değer atanabilir bağlamı, yeni bir pragma kullanılarak denetlenir:</span><span class="sxs-lookup"><span data-stu-id="f3644-135">The nullable context is controlled using a new pragma:</span></span>

- <span data-ttu-id="f3644-136">`#nullable enable` boş değer atanabilir bağlamının etkin ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f3644-136">`#nullable enable` sets the nullable context to enabled.</span></span>
- <span data-ttu-id="f3644-137">`#nullable disable` boş değer atanabilir bağlam devre dışı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f3644-137">`#nullable disable` sets the nullable context to disabled.</span></span>

<span data-ttu-id="f3644-138">Varsayılan null bağlam `disabled`.</span><span class="sxs-lookup"><span data-stu-id="f3644-138">The default nullable context is `disabled`.</span></span> <span data-ttu-id="f3644-139">Bu karar, mevcut kod değişiklikleri ve yeni bir uyarı olmadan derlediğinden anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f3644-139">That decision means that your existing code compiles without changes and without generating any new warnings.</span></span>

<span data-ttu-id="f3644-140">Derleyici, devre dışı bırakılmış bir boş değer atanabilir bağlamında aşağıdaki kuralları kullanır:</span><span class="sxs-lookup"><span data-stu-id="f3644-140">The compiler uses the following rules in a disabled nullable context:</span></span>

- <span data-ttu-id="f3644-141">Boş değer atanabilir başvuruları devre dışı bırakılmış bir bağlamda bildiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3644-141">You can't declare nullable references in a disabled context.</span></span>
- <span data-ttu-id="f3644-142">Tüm başvuru değişkenleri null atanabilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-142">All reference variables may be assigned to null.</span></span>
- <span data-ttu-id="f3644-143">Başvuru türünde bir değişken başvurusu kaldırıldığında uyarı üretilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-143">No warnings are generated when a variable of a reference type is dereferenced.</span></span>
- <span data-ttu-id="f3644-144">Devre dışı bırakılmış bir bağlamda null forgiving işleci kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f3644-144">The null-forgiving operator may not be used in a disabled context.</span></span>

<span data-ttu-id="f3644-145">Davranış önceki sürümleri aynıdır C#.</span><span class="sxs-lookup"><span data-stu-id="f3644-145">The behavior is the same as previous versions of C#.</span></span>

<span data-ttu-id="f3644-146">Derleyici, etkin bir boş değer atanabilir bağlamında aşağıdaki kuralları kullanır:</span><span class="sxs-lookup"><span data-stu-id="f3644-146">The compiler uses the following rules in an enabled nullable context:</span></span>

- <span data-ttu-id="f3644-147">Herhangi bir değişken başvuru türünde bir **atanamayan başvuru**.</span><span class="sxs-lookup"><span data-stu-id="f3644-147">Any variable of a reference type is a **non-nullable reference**.</span></span>
- <span data-ttu-id="f3644-148">Herhangi bir değer atanamayan başvurusu güvenli bir şekilde başvurusu kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-148">Any non-nullable reference may be dereferenced safely.</span></span>
- <span data-ttu-id="f3644-149">Herhangi bir boş değer atanabilir bir başvuru türü (tarafından belirtildiği `?` Değişken bildiriminde türden sonra) null olabilir.</span><span class="sxs-lookup"><span data-stu-id="f3644-149">Any nullable reference type (noted by `?` after the type in the variable declaration) may be null.</span></span> <span data-ttu-id="f3644-150">Statik analiz değeri, başvurusu kaldırıldığında, null olmayan değer biliniyorsa belirler.</span><span class="sxs-lookup"><span data-stu-id="f3644-150">Static analysis determines if the value is known to be non-null when it is dereferenced.</span></span> <span data-ttu-id="f3644-151">Aksi halde, derleyici sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="f3644-151">If not, the compiler warns you.</span></span>
- <span data-ttu-id="f3644-152">Null forgiving işleci, bir null başvuru null olmadığını bildirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3644-152">You can use the null-forgiving operator to declare that a nullable reference isn't null.</span></span>

<span data-ttu-id="f3644-153">Daha zengin bir dil bilgisi nullable bağlamlarını için önerilen ve gelecekteki önizlemelere kullanılabilir olacak.</span><span class="sxs-lookup"><span data-stu-id="f3644-153">A richer grammar is proposed for nullable contexts and will be available in future previews.</span></span> <span data-ttu-id="f3644-154">Boş değer atanabilir bağlamları hakkında daha fazla bilgi için bkz. [boş değer atanabilir başvurusu belirtiminin](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types-specification.md#nullable-contexts) taslak.</span><span class="sxs-lookup"><span data-stu-id="f3644-154">For more information about nullable contexts, see the [nullable reference specification](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types-specification.md#nullable-contexts) draft.</span></span>

## <a name="null-states-of-nullable-references"></a><span data-ttu-id="f3644-155">Null başvuru null durumları</span><span class="sxs-lookup"><span data-stu-id="f3644-155">Null states of nullable references</span></span>

<span data-ttu-id="f3644-156">Derleyici statik analiz belirlemek için kullanır. **null durumu** herhangi bir null başvuru.</span><span class="sxs-lookup"><span data-stu-id="f3644-156">The compiler uses static analysis to determine the **null state** of any nullable reference.</span></span> <span data-ttu-id="f3644-157">Null ya da durumudur **değil null** veya **belki de null**.</span><span class="sxs-lookup"><span data-stu-id="f3644-157">The null state is either **not null** or **maybe null**.</span></span> <span data-ttu-id="f3644-158">Derleyici bunun belirlendiğinde bir null başvuru başvuru varsa **belki de null**, derleyici sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="f3644-158">If you dereference a nullable reference when the compiler has determined it's **maybe null**, the compiler warns you.</span></span> <span data-ttu-id="f3644-159">Boş değer atanabilir bir başvuru durumu **belki de null** sürece derleyici iki koşullardan birini belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f3644-159">The state of a nullable reference is **maybe null** unless the compiler can determine one of two conditions:</span></span>

1. <span data-ttu-id="f3644-160">Değişken kesinlikle bir null olmayan değere atandı.</span><span class="sxs-lookup"><span data-stu-id="f3644-160">The variable has been definitely assigned to a non-null value.</span></span>
1. <span data-ttu-id="f3644-161">Değişkeni null karşı XML'deki başvurmadan önce iade edildi.</span><span class="sxs-lookup"><span data-stu-id="f3644-161">The variable has been checked against null before de-referencing it.</span></span>

<span data-ttu-id="f3644-162">NULL olmayan başvurular hiçbir zaman null değerine ayarlanırsa, derleyici zorlar.</span><span class="sxs-lookup"><span data-stu-id="f3644-162">The compiler enforces that non-nullable references may never be set to the null value.</span></span> <span data-ttu-id="f3644-163">Bunları bir null olmayan değere başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3644-163">You must initialize them to a non-null value.</span></span> <span data-ttu-id="f3644-164">Aksi takdirde, NULL olmayan bir başvuru başlatılan değildi derleyici sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="f3644-164">If you don't, the compiler warns that a non-nullable reference wasn't initialized.</span></span> <span data-ttu-id="f3644-165">Boş değer atanabilir bir başvuru NULL olmayan bir başvuru atama her derleyici Ayrıca, sizi uyarır **null olabilir**.</span><span class="sxs-lookup"><span data-stu-id="f3644-165">The compiler also warns you whenever you assign a non-nullable reference to a nullable reference that **may be null**.</span></span> <span data-ttu-id="f3644-166">Yalnızca atayabilirsiniz boş değer atanabilir bir başvuru NULL olmayan bir başvuru, null başvuru ise gelir **değil null**.</span><span class="sxs-lookup"><span data-stu-id="f3644-166">That implies you can only assign a non-nullable reference to a nullable reference if that nullable reference is **not null**.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f3644-167">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="f3644-167">Learn more</span></span>

- [<span data-ttu-id="f3644-168">Taslak null başvuru belirtimi</span><span class="sxs-lookup"><span data-stu-id="f3644-168">Draft Nullable reference specification</span></span>](https://github.com/dotnet/csharplang/blob/master/proposals/nullable-reference-types-specification.md)
- [<span data-ttu-id="f3644-169">Boş değer atanabilir başvuruları öğreticiye giriş</span><span class="sxs-lookup"><span data-stu-id="f3644-169">Intro to nullable references tutorial</span></span>](tutorials/nullable-reference-types.md)