---
title: Özelleştirme parametre sıralama - .NET
description: .NET yerel gösterimine parametrelerinizi nasıl sürekliliğe devreder özelleştirmeyi öğrenin.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 877eb00c18c9108fe6bcfb50104ff5ed813e85f3
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065470"
---
# <a name="customizing-parameter-marshaling"></a><span data-ttu-id="5a352-103">Parametreyi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5a352-103">Customizing parameter marshaling</span></span>

<span data-ttu-id="5a352-104">.NET çalışma zamanının varsayılan parametre hazırlama davranışı istediklerinizi yapmaz, kullanım kullanabilirsiniz <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> parametrelerinizi nasıl sıralanmış özelleştirmek için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5a352-104">When the .NET runtime's default parameter marshaling behavior doesn't do what you want, use can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> attribute to customize how your parameters are marshaled.</span></span>

## <a name="customizing-string-parameters"></a><span data-ttu-id="5a352-105">Dize parametreleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5a352-105">Customizing string parameters</span></span>

<span data-ttu-id="5a352-106">.NET, çeşitli biçimlerde hazırlama dizeler için vardır.</span><span class="sxs-lookup"><span data-stu-id="5a352-106">.NET has a variety of formats for marshaling strings.</span></span> <span data-ttu-id="5a352-107">Bu yöntemler, C stili dizeler ve dize biçimleri Windows merkezli ayrı bölümlere ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5a352-107">These methods are split into distinct sections on C-style strings and Windows-centric string formats.</span></span>

### <a name="c-style-strings"></a><span data-ttu-id="5a352-108">C stili dizeler</span><span class="sxs-lookup"><span data-stu-id="5a352-108">C-Style strings</span></span>

<span data-ttu-id="5a352-109">Her biri Bu biçimler yerel kod için null ile sonlandırılmış bir dize geçirir.</span><span class="sxs-lookup"><span data-stu-id="5a352-109">Each of these formats passes a null-terminated string to native code.</span></span> <span data-ttu-id="5a352-110">Bunlar, yerel dizesi kodlayarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a352-110">They differ by the encoding of the native string.</span></span>

| <span data-ttu-id="5a352-111">`System.Runtime.InteropServices.UnmanagedType` Değer</span><span class="sxs-lookup"><span data-stu-id="5a352-111">`System.Runtime.InteropServices.UnmanagedType` value</span></span> | <span data-ttu-id="5a352-112">Encoding</span><span class="sxs-lookup"><span data-stu-id="5a352-112">Encoding</span></span> |
|------------------------------------------------------|----------|
| <span data-ttu-id="5a352-113">LPStr</span><span class="sxs-lookup"><span data-stu-id="5a352-113">LPStr</span></span> | <span data-ttu-id="5a352-114">ANSI</span><span class="sxs-lookup"><span data-stu-id="5a352-114">ANSI</span></span> |
| <span data-ttu-id="5a352-115">LPUTF8Str</span><span class="sxs-lookup"><span data-stu-id="5a352-115">LPUTF8Str</span></span> | <span data-ttu-id="5a352-116">UTF-8</span><span class="sxs-lookup"><span data-stu-id="5a352-116">UTF-8</span></span> | 
| <span data-ttu-id="5a352-117">LPWStr</span><span class="sxs-lookup"><span data-stu-id="5a352-117">LPWStr</span></span> | <span data-ttu-id="5a352-118">UTF-16</span><span class="sxs-lookup"><span data-stu-id="5a352-118">UTF-16</span></span> |
| <span data-ttu-id="5a352-119">LPTStr</span><span class="sxs-lookup"><span data-stu-id="5a352-119">LPTStr</span></span> | <span data-ttu-id="5a352-120">UTF-16</span><span class="sxs-lookup"><span data-stu-id="5a352-120">UTF-16</span></span> |

<span data-ttu-id="5a352-121"><xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=nameWithType> Biçimi biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5a352-121">The <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=nameWithType> format is slightly different.</span></span> <span data-ttu-id="5a352-122">Gibi `LPWStr`, yerel C stili dizeyi UTF-16 kodlamalı dize sıralar.</span><span class="sxs-lookup"><span data-stu-id="5a352-122">Like `LPWStr`, it marshals the string to a native C-style string encoded in UTF-16.</span></span> <span data-ttu-id="5a352-123">Ancak, başvuruya göre dizesine geçmenizi yönetilen imzaya sahip ve eşleşen yerel imza dize değerine göre alır.</span><span class="sxs-lookup"><span data-stu-id="5a352-123">However, the managed signature has you pass in the string by reference and the matching native signature takes the string by value.</span></span> <span data-ttu-id="5a352-124">Bu ayrım değere göre bir dize alır ve değiştirdiği bir yerel API kullanmak üzere yerinde kullanmak zorunda kalmadan sağlar bir `StringBuilder`.</span><span class="sxs-lookup"><span data-stu-id="5a352-124">This distinction allows you to use a native API that takes a string by value and modifies it in-place without having to use a `StringBuilder`.</span></span> <span data-ttu-id="5a352-125">Eşleşmeyen yerel ve yönetilen imzalarla karışıklığa neden eğilimlidir olduğundan el ile şu biçimi kullanarak karşı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5a352-125">We recommend against manually using this format since it's prone to cause confusion with the mismatching native and managed signatures.</span></span>

### <a name="windows-centric-string-formats"></a><span data-ttu-id="5a352-126">Windows merkezli dize biçimleri</span><span class="sxs-lookup"><span data-stu-id="5a352-126">Windows-centric string formats</span></span>

<span data-ttu-id="5a352-127">COM veya OLE arabirimleri ile etkileşim kurulurken, büyük olasılıkla yerel işlevleri dize olarak alın bulabilirsiniz `BSTR` bağımsız değişkenler.</span><span class="sxs-lookup"><span data-stu-id="5a352-127">When interacting with COM or OLE interfaces, you'll likely find that the native functions take strings as `BSTR` arguments.</span></span> <span data-ttu-id="5a352-128">Kullanabileceğiniz <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> türü bir dize olarak hazırlamak için yönetilmeyen bir `BSTR`.</span><span class="sxs-lookup"><span data-stu-id="5a352-128">You can use the <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> unmanaged type to marshal a string as a `BSTR`.</span></span>

<span data-ttu-id="5a352-129">WinRT API'lar ile etkileşim kurma, kullanabileceğiniz <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> biçiminde bir dize olarak hazırlamak için bir `HSTRING`.</span><span class="sxs-lookup"><span data-stu-id="5a352-129">If you're interacting with WinRT APIs, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> format to marshal a string as an `HSTRING`.</span></span>

## <a name="customizing-array-parameters"></a><span data-ttu-id="5a352-130">Dizi parametreleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5a352-130">Customizing array parameters</span></span>

<span data-ttu-id="5a352-131">.NET de sıralama dizi parametreleri için birden çok yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a352-131">.NET also provides you multiple ways to marshal array parameters.</span></span> <span data-ttu-id="5a352-132">Bir C tarzı dizi alan bir API arıyoruz kullanırsanız <xref:System.Runtime.InteropServices.UnmanagedType.LPArray?displayProperty=nameWithType> yönetilmeyen türü.</span><span class="sxs-lookup"><span data-stu-id="5a352-132">If you're calling an API that takes a C-style array, use the <xref:System.Runtime.InteropServices.UnmanagedType.LPArray?displayProperty=nameWithType> unmanaged type.</span></span> <span data-ttu-id="5a352-133">Özelleştirilmiş sıralama dizideki değerleri ihtiyacınız varsa, kullanabileceğiniz <xref:System.Runtime.InteropServices.MarshalAsAttribute.ArraySubType> alanını `[MarshalAs]` söz konusu öznitelik.</span><span class="sxs-lookup"><span data-stu-id="5a352-133">If the values in the array need customized marshaling, you can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.ArraySubType> field on the `[MarshalAs]` attribute for that.</span></span>

<span data-ttu-id="5a352-134">COM API kullanıyorsanız, büyük olasılıkla, dizi parametreleri olarak sıralamanız gerekir `SAFEARRAY*`s.</span><span class="sxs-lookup"><span data-stu-id="5a352-134">If you're using COM APIs, you'll likely have to marshal your array parameters as `SAFEARRAY*`s.</span></span> <span data-ttu-id="5a352-135">Bunu yapmak için kullanabileceğiniz <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> yönetilmeyen türü.</span><span class="sxs-lookup"><span data-stu-id="5a352-135">To do so, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> unmanaged type.</span></span> <span data-ttu-id="5a352-136">Varsayılan tür öğelerinin `SAFEARRAY` tablodaki görülebilir [özelleştirme `object` alanları](./customize-struct-marshaling.md#marshaling-systemobjects).</span><span class="sxs-lookup"><span data-stu-id="5a352-136">The default type of the elements of the `SAFEARRAY` can be seen in the table on [customizing `object` fields](./customize-struct-marshaling.md#marshaling-systemobjects).</span></span> <span data-ttu-id="5a352-137">Kullanabileceğiniz <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> ve <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> tam öğe özelleştirmek için alanları türü `SAFEARRAY`.</span><span class="sxs-lookup"><span data-stu-id="5a352-137">You can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> and <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> fields to customize the exact element type of the `SAFEARRAY`.</span></span>

## <a name="customizing-boolean-or-decimal-parameters"></a><span data-ttu-id="5a352-138">Ondalık ya da Boole parametreleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5a352-138">Customizing boolean or decimal parameters</span></span>

<span data-ttu-id="5a352-139">Ondalık ya da Boole parametreleri hazırlama hakkında daha fazla bilgi için bkz: [yapısı hazırlama özelleştirme](customize-struct-marshaling.md).</span><span class="sxs-lookup"><span data-stu-id="5a352-139">For information on marshaling boolean or decimal parameters, see [Customizing structure marshaling](customize-struct-marshaling.md).</span></span>

## <a name="customizing-object-parameters-windows-only"></a><span data-ttu-id="5a352-140">Nesnesi parametrelerini özelleştirme (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="5a352-140">Customizing object parameters (Windows-only)</span></span>

<span data-ttu-id="5a352-141">Windows üzerinde .NET çalışma zamanı bir nesne parametreleri yerel kod için hazırlamak için farklı yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a352-141">On Windows, the .NET runtime provides a number of different ways to marshal object parameters to native code.</span></span>

### <a name="marshaling-as-specific-com-interfaces"></a><span data-ttu-id="5a352-142">Belirli bir COM arabirimleri olarak hazırlama</span><span class="sxs-lookup"><span data-stu-id="5a352-142">Marshaling as specific COM interfaces</span></span>

<span data-ttu-id="5a352-143">API'nizi bir COM nesnesi için bir işaretçi alır, aşağıdakilerden herhangi birini kullanabilirsiniz `UnmanagedType` biçimleri üzerinde bir `object`-yazılan bu belirli arabirimleri hazırlamak için .NET bildirmek için parametre:</span><span class="sxs-lookup"><span data-stu-id="5a352-143">If your API takes a pointer to a COM object, you can use any of the following `UnmanagedType` formats on an `object`-typed parameter to tell .NET to marshal as these specific interfaces:</span></span>

- `IUnknown`
- `IDispatch`
- `IInspectable`

<span data-ttu-id="5a352-144">Ayrıca, türünüz işaretlenmişse `[ComVisible(true)]` veya hazırlama `object` kullanabileceğiniz türü <xref:System.Runtime.InteropServices.UnmanagedType.Interface?displayProperty=nameWithType> COM çağrılabilir sarmalayıcı COM görünümün türünüz olarak nesnenizin sıralamakta biçimi.</span><span class="sxs-lookup"><span data-stu-id="5a352-144">Additionally, if your type is marked `[ComVisible(true)]` or you're marshaling the `object` type, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Interface?displayProperty=nameWithType> format to marshal your object as a COM callable wrapper for the COM view of your type.</span></span>

### <a name="marshaling-to-a-variant"></a><span data-ttu-id="5a352-145">Hazırlama için bir `VARIANT`</span><span class="sxs-lookup"><span data-stu-id="5a352-145">Marshaling to a `VARIANT`</span></span>

<span data-ttu-id="5a352-146">API'nizi yerel bir Win32 sürerse `VARIANT`, kullanabileceğiniz <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> Biçimlendir, `object` nesnelerinizi olarak hazırlamak için parametre `VARIANT`s.</span><span class="sxs-lookup"><span data-stu-id="5a352-146">If your native API takes a Win32 `VARIANT`, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> format on your `object` parameter to marshal your objects as `VARIANT`s.</span></span> <span data-ttu-id="5a352-147">İlgili belgelere bakın [özelleştirme `object` alanları](customize-struct-marshaling.md#marshaling-systemobjects) .NET türleri arasında bir eşleme için ve `VARIANT` türleri.</span><span class="sxs-lookup"><span data-stu-id="5a352-147">See the documentation on [customizing `object` fields](customize-struct-marshaling.md#marshaling-systemobjects) for a mapping between .NET types and `VARIANT` types.</span></span>

### <a name="custom-marshalers"></a><span data-ttu-id="5a352-148">Özel sıralayıcılara</span><span class="sxs-lookup"><span data-stu-id="5a352-148">Custom marshalers</span></span>

<span data-ttu-id="5a352-149">Yerel bir COM arabirimi farklı bir yönetilen türü proje istiyorsanız kullanabileceğiniz `UnmanagedType.CustomMarshaler` biçimi ve uygulaması <xref:System.Runtime.InteropServices.ICustomMarshaler> kendi özel sıralama kodu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="5a352-149">If you want to project a native COM interface into a different managed type, you can use the `UnmanagedType.CustomMarshaler` format and an implementation of <xref:System.Runtime.InteropServices.ICustomMarshaler> to provide your own custom marshaling code.</span></span>