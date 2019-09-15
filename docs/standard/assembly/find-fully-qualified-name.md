---
title: 'Nasıl yapılır: Bir derlemenin tam nitelikli adını bulun'
ms.date: 08/20/2019
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 4fc670adc80a6f4ce7b36074185dcd3bb85fbc67
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991306"
---
# <a name="how-to-find-an-assemblys-fully-qualified-name"></a><span data-ttu-id="87d4c-102">Nasıl yapılır: Bir derlemenin tam nitelikli adını bulun</span><span class="sxs-lookup"><span data-stu-id="87d4c-102">How to: Find an assembly's fully qualified name</span></span>

<span data-ttu-id="87d4c-103">Genel derleme önbelleğinde bir .NET Framework derlemesinin tam adını öğrenmek için genel derleme önbelleği aracını ([Gacutil. exe](../../framework/tools/gacutil-exe-gac-tool.md)) kullanın.</span><span class="sxs-lookup"><span data-stu-id="87d4c-103">To discover the fully qualified name of a .NET Framework assembly in the global assembly cache, use the Global Assembly Cache tool ([Gacutil.exe](../../framework/tools/gacutil-exe-gac-tool.md)).</span></span> <span data-ttu-id="87d4c-104">Bkz [. nasıl yapılır: Genel derleme önbelleğinin](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md)içeriğini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="87d4c-104">See [How to: View the contents of the global assembly cache](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md).</span></span>

<span data-ttu-id="87d4c-105">.NET Core derlemeleri ve genel derleme önbelleğinde olmayan .NET Framework derlemeler için, tam derleme adını çeşitli yollarla alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="87d4c-105">For .NET Core assemblies, and for .NET Framework assemblies that aren't in the global assembly cache, you can get the fully qualified assembly name in a number of ways:</span></span>

- <span data-ttu-id="87d4c-106">Bilgileri konsola veya bir değişkene çıkarmak için kodu kullanabilir veya tam nitelikli adı içeren derlemenin meta verilerini incelemek için [ıldadsm. exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87d4c-106">You can use code to output the information to the console or to a variable, or you can use the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) to examine the assembly's metadata, which contains the fully qualified name.</span></span>

- <span data-ttu-id="87d4c-107">Derleme uygulama tarafından zaten yüklüyse, tam adı almak için <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> özelliğin değerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87d4c-107">If the assembly is already loaded by the application, you can retrieve the value of the <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> property to get the fully qualified name.</span></span> <span data-ttu-id="87d4c-108">Nesnesine bir başvuru <xref:System.Type.Assembly> <xref:System.Type> almak için, bu derlemede tanımlanan öğesinin özelliğini kullanabilirsiniz. <xref:System.Reflection.Assembly></span><span class="sxs-lookup"><span data-stu-id="87d4c-108">You can use the <xref:System.Type.Assembly> property of a <xref:System.Type> defined in that assembly to retrieve a reference to the <xref:System.Reflection.Assembly> object.</span></span> <span data-ttu-id="87d4c-109">Örnek, bir gösterim sağlar.</span><span class="sxs-lookup"><span data-stu-id="87d4c-109">The example provides an illustration.</span></span>

- <span data-ttu-id="87d4c-110">Derlemenin dosya sistemi yolunu biliyorsanız, tam derleme adını almak `static` için (C#) veya `Shared` (Visual Basic) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87d4c-110">If you know the assembly's file system path, you can call the `static` (C#) or `Shared` (Visual Basic) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> method to get the fully qualified assembly name.</span></span> <span data-ttu-id="87d4c-111">Aşağıda basit bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="87d4c-111">The following is a simple example.</span></span>

  ```csharp
  using System;
  using System.Reflection;

  public class Example
  {
     public static void Main()
     {
        Console.WriteLine(AssemblyName.GetAssemblyName(@".\UtilityLibrary.dll"));
     }
  }
  // The example displays output like the following:
  //   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

  ```vb
  Imports System.Reflection

  Public Module Example
     Public Sub Main
        Console.WriteLine(AssemblyName.GetAssemblyName(".\UtilityLibrary.dll"))
     End Sub
  End Module
  ' The example displays output like the following:
  '   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

- <span data-ttu-id="87d4c-112">Tam nitelikli adı içeren derlemenin meta verilerini incelemek için [ıldadsm. exe ' yi (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87d4c-112">You can use the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) to examine the assembly's metadata, which contains the fully qualified name.</span></span>

<span data-ttu-id="87d4c-113">Sürüm, kültür ve derleme adı gibi derleme özniteliklerini ayarlama hakkında daha fazla bilgi için bkz. [derleme özniteliklerini ayarlama](set-attributes.md).</span><span class="sxs-lookup"><span data-stu-id="87d4c-113">For more information about setting assembly attributes such as version, culture, and assembly name, see [Set assembly attributes](set-attributes.md).</span></span> <span data-ttu-id="87d4c-114">Bütünleştirilmiş koda tanımlayıcı ad verme hakkında daha fazla bilgi için bkz. [tanımlayıcı adlı derlemeler oluşturma ve kullanma](create-use-strong-named.md).</span><span class="sxs-lookup"><span data-stu-id="87d4c-114">For more information about giving an assembly a strong name, see [Create and use strong-named assemblies](create-use-strong-named.md).</span></span>

## <a name="example"></a><span data-ttu-id="87d4c-115">Örnek</span><span class="sxs-lookup"><span data-stu-id="87d4c-115">Example</span></span>

<span data-ttu-id="87d4c-116">Aşağıdaki örnek, konsoluna belirtilen bir sınıf içeren bir derlemenin tam adının nasıl görüntüleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="87d4c-116">The following example shows how to display the fully qualified name of an assembly containing a specified class to the console.</span></span> <span data-ttu-id="87d4c-117">Bu, <xref:System.Type.Assembly?displayProperty=nameWithType> Bu derlemede tanımlanan türden bir derlemeye başvuru almak için özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="87d4c-117">It uses the <xref:System.Type.Assembly?displayProperty=nameWithType> property to retrieve a reference to an assembly from a type that's defined in that assembly.</span></span>

```cpp
#using <System.dll>
#using <System.Data.dll>

using namespace System;
using namespace System::Reflection;

ref class asmname
{
public:
    static void Main()
    {
        Type^ t = System::Data::DataSet::typeid;
        String^ s = t->Assembly->FullName->ToString();
        Console::WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
};

int main()
{
    asmname::Main();
}
```

```csharp
using System;
using System.Reflection;

class asmname
{
    public static void Main()
    {
        Type t = typeof(System.Data.DataSet);
        string s = t.Assembly.FullName.ToString();
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
}
```

```vb
Imports System
Imports System.Reflection

Class asmname
    Public Shared Sub Main()
        Dim t As Type = GetType(System.Data.DataSet)
        Dim s As String = t.Assembly.FullName.ToString()
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s)
    End Sub
End Class
```

## <a name="see-also"></a><span data-ttu-id="87d4c-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="87d4c-118">See also</span></span>

- [<span data-ttu-id="87d4c-119">Derleme adları</span><span class="sxs-lookup"><span data-stu-id="87d4c-119">Assembly names</span></span>](names.md)
- [<span data-ttu-id="87d4c-120">Derlemeler oluştur</span><span class="sxs-lookup"><span data-stu-id="87d4c-120">Create assemblies</span></span>](create.md)
- [<span data-ttu-id="87d4c-121">Tanımlayıcı adlı derlemeler oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="87d4c-121">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
- [<span data-ttu-id="87d4c-122">Genel derleme önbelleği</span><span class="sxs-lookup"><span data-stu-id="87d4c-122">Global assembly cache</span></span>](../../framework/app-domains/gac.md)
- [<span data-ttu-id="87d4c-123">Çalışma zamanının derlemeleri nasıl konumlandırır</span><span class="sxs-lookup"><span data-stu-id="87d4c-123">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="87d4c-124">Bütünleştirilmiş kod içeren program</span><span class="sxs-lookup"><span data-stu-id="87d4c-124">Program with assemblies</span></span>](program.md)