---
title: Sonuçlar
description: Hataya dayanıklı kod yazmanıza yardımcı F# olması için ' Result ' türünü nasıl kullanacağınızı öğrenin.
ms.date: 04/24/2017
ms.openlocfilehash: 187aa26ccbaac7e0ec998756377bb7b0489eb1ab
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73424845"
---
# <a name="results"></a>Sonuçlar

4,1 ' F# den başlayarak, birleştirilebilen hata toleranslı kod yazmak için kullanabileceğiniz `Result<'T,'TFailure>` bir tür vardır.

## <a name="syntax"></a>Sözdizimi

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> =
    | Ok of ResultValue:'T
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a>Açıklamalar

Sonuç türünün, 4,1 ' de F# tanıtılan bir [Yapı ayrılmış birleşimi](discriminated-unions.md#struct-discriminated-unions)olduğunu unutmayın.  Yapısal eşitlik semantiği burada geçerlidir.

`Result` türü genellikle F# topluluk Içinde [Railway odaklı programlama](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) olarak adlandırılan monadıc hata işleme içinde kullanılır.  Aşağıdaki önemsiz örnekte bu yaklaşım gösterilmektedir.

```fsharp
// Define a simple type which has fields that can be validated
type Request =
    { Name: string
      Email: string }

// Define some logic for what defines a valid name.
//
// Generates a Result which is an Ok if the name validates;
// otherwise, it generates a Result which is an Error.
let validateName req =
    match req.Name with
    | null -> Error "No name found."
    | "" -> Error "Name is empty."
    | "bananas" -> Error "Bananas is not a name."
    | _ -> Ok req

// Similarly, define some email validation logic.
let validateEmail req =
    match req.Email with
    | null -> Error "No email found."
    | "" -> Error "Email is empty."
    | s when s.EndsWith("bananas.com") -> Error "No email from bananas.com is allowed."
    | _ -> Ok req

let validateRequest reqResult =
    reqResult
    |> Result.bind validateName
    |> Result.bind validateEmail

let test() =
    // Now, create a Request and pattern match on the result.
    let req1 = { Name = "Phillip"; Email = "phillip@contoso.biz" }
    let res1 = validateRequest (Ok req1)
    match res1 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req.Name req.Email
    | Error e -> printfn "Error: %s" e
    // Prints: "My request was valid!  Name: Phillip Email: phillip@consoto.biz"

    let req2 = { Name = "Phillip"; Email = "phillip@bananas.com" }
    let res2 = validateRequest (Ok req2)
    match res2 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req.Name req.Email
    | Error e -> printfn "Error: %s" e
    // Prints: "Error: No email from bananas.com is allowed."

test()
```

Görebileceğiniz gibi, tümünün bir `Result`döndürmesini zorlarsanız, çeşitli doğrulama işlevlerini birbirine kolayca zincirleyebilirsiniz.  Bu, bunun gibi işlevleri, sizin için gerekli olduğu kadar birleştirilebilen küçük parçalara bölmenize olanak tanır.  Bu Ayrıca, bir doğrulamanın sonunda, daha yüksek bir program doğruluğu uygulayan, bir doğrulama sayısının sonunda [kalıp eşleştirmesinin](pattern-matching.md) kullanımını *zorunlu kılma* değeri de vardır.

## <a name="see-also"></a>Ayrıca bkz.

- [Ayrılmış Birleşimler](discriminated-unions.md)
- [Desen Eşleştirme](pattern-matching.md)
