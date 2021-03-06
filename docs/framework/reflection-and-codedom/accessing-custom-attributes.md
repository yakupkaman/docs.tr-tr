---
title: Özel Özniteliklere Erişim
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- custom attributes, accessibility
- attributes [.NET Framework], accessing
- reflection, custom attributes
ms.assetid: 1d8e3398-00d8-47d5-a084-214f9859d3d7
ms.openlocfilehash: a5651e9dc8cf40e737dd523ec5d29e876a9c0765
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73130296"
---
# <a name="accessing-custom-attributes"></a>Özel Özniteliklere Erişim
Öznitelikler program öğeleriyle ilişkilendirildikten sonra, var olan ve değerlerini sorgulamak için yansıma kullanılabilir. .NET Framework sürüm 1,0 ve 1,1 ' de, özel öznitelikler yürütme bağlamında incelenir. .NET Framework sürüm 2,0, yürütme için yüklenemeyen kodu incelemek için kullanılabilen yeni bir yükleme bağlamı (yalnızca yansıma bağlamı) sağlar.  
  
## <a name="the-reflection-only-context"></a>Yalnızca yansıma bağlamı  
 Yalnızca yansıma bağlamına yüklenen kod yürütülemez. Bu, özel özniteliklerin örneklerinin oluşturulamadığını belirtir, çünkü bu, oluşturucuların yürütülmesi gerekir. Özel öznitelikleri yalnızca yansıma bağlamında yüklemek ve incelemek için <xref:System.Reflection.CustomAttributeData> sınıfını kullanın. Statik <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> yönteminin uygun aşırı yüklemesini kullanarak bu sınıfın örneklerini elde edebilirsiniz. Bkz. [nasıl yapılır: derlemeleri yalnızca yansıma bağlamına yükleme](how-to-load-assemblies-into-the-reflection-only-context.md).  
  
## <a name="the-execution-context"></a>Yürütme bağlamı  
 Yürütme bağlamındaki öznitelikleri sorgulamak için ana yansıma yöntemleri <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType> ve <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>.  
  
 Özel bir özniteliğin erişilebilirliği, eklendiği derlemeye göre denetlenir. Bu, özel özniteliğin eklendiği derlemede bulunan bir türün bir yönteminin özel özniteliğin oluşturucusunu çağırıp çağıramayacağını denetlemeye eşdeğerdir.  
  
 <xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=nameWithType> gibi yöntemler tür bağımsız değişkeninin görünürlüğünü ve erişilebilirliğini kontrol edin. Yalnızca Kullanıcı tanımlı türü içeren derlemede bulunan kod, **GetCustomAttributes**kullanarak bu türde özel bir öznitelik alabilir.  
  
 Aşağıdaki C# örnek tipik bir özel öznitelik tasarım modelidir. Çalışma zamanı özel öznitelik yansıma modelini gösterir.  
  
```csharp
System.DLL  
public class DescriptionAttribute : Attribute  
{  
}  
  
System.Web.DLL  
internal class MyDescriptionAttribute : DescriptionAttribute  
{  
}  
  
public class LocalizationExtenderProvider  
{  
    [MyDescriptionAttribute(...)]  
    public CultureInfo GetLanguage(...)  
    {  
    }  
}  
```  
  
 Çalışma zamanı, **GetLanguage** yöntemine iliştirilmiş <xref:System.ComponentModel.DescriptionAttribute> ortak özel öznitelik türü için özel öznitelikleri almaya çalışıyorsa, aşağıdaki eylemleri gerçekleştirir:  
  
1. Çalışma zamanı, **Type bağımsız değişkeni** **Type. GetCustomAttributes**(tür *türü*) public olup olmadığını denetler ve bu nedenle görünür ve erişilebilir olur.  
  
2. Çalışma zamanı, **DescriptionAttribute** 'tan türetilmiş Kullanıcı tanımlı **MyDescriptionAttribute** türünün görünür ve **System. Web. dll** derlemesi Içinde erişilebilir olduğunu denetler ve burada **GetLanguage yöntemine iliştirilir** ().  
  
3. Çalışma zamanı, **MyDescriptionAttribute** oluşturucusunun, **System. Web. dll** derlemesi içinde görünür ve erişilebilir olduğunu denetler.  
  
4. Çalışma zamanı, **MyDescriptionAttribute** yapıcısını özel öznitelik parametreleriyle çağırır ve yeni nesneyi çağırana döndürür.  
  
 Özel öznitelik yansıtma modeli, Kullanıcı tanımlı türlerin, türün tanımlandığı derleme dışındaki örneklerini sızdırabilir. Bu, çalışma zamanı sistem kitaplığındaki, **RuntimeMethodInfo** nesnelerinin dizisini döndüren <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> gibi Kullanıcı tanımlı türlerin örneklerini döndüren üyelerden farklı değildir. Bir istemcinin Kullanıcı tanımlı bir özel öznitelik türü hakkında bilgi bulmasını engellemek için, tür üyelerini ortak olacak şekilde tanımlayın.  
  
 Aşağıdaki örnek, özel özniteliklere erişim sağlamak için yansıma kullanmanın temel yolunu gösterir.  
  
 [!code-cpp[CustomAttributeData#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source2.cpp#2)]
 [!code-csharp[CustomAttributeData#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source2.cs#2)]
 [!code-vb[CustomAttributeData#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source2.vb#2)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [Tür Bilgilerini Görüntüleme](viewing-type-information.md)
- [Yansımayla İlgili Güvenlik Konuları](security-considerations-for-reflection.md)
