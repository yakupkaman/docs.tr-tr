---
title: Seedwork (etki alanı modeliniz için yeniden kullanılabilir kök sınıflar ve arabirimler)
description: Kapsayıcılı .NET uygulamaları için .NET mikro hizmetleri mimarisi | DDD tabanlı bir etki alanı modeline yönelik uygulamayı başlatmak için başlangıç noktası olarak seedwork kavramını kullanın.
ms.date: 10/08/2018
ms.openlocfilehash: a49f9e0b40ea306a846d9fb472bac388eedbfe02
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2019
ms.locfileid: "70296812"
---
# <a name="seedwork-reusable-base-classes-and-interfaces-for-your-domain-model"></a><span data-ttu-id="a54bc-103">Seedwork (etki alanı modeliniz için yeniden kullanılabilir kök sınıflar ve arabirimler)</span><span class="sxs-lookup"><span data-stu-id="a54bc-103">Seedwork (reusable base classes and interfaces for your domain model)</span></span>

<span data-ttu-id="a54bc-104">Çözüm klasörü bir *Seedwork* klasörü içerir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-104">The solution folder contains a *SeedWork* folder.</span></span> <span data-ttu-id="a54bc-105">Bu klasör, etki alanı varlıklarınız ve değer nesneleriniz için temel olarak kullanabileceğiniz özel temel sınıflar içerir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-105">This folder contains custom base classes that you can use as a base for your domain entities and value objects.</span></span> <span data-ttu-id="a54bc-106">Bu temel sınıfları kullanarak her bir etki alanının nesne sınıfında gereksiz kodunuz olamaz.</span><span class="sxs-lookup"><span data-stu-id="a54bc-106">Use these base classes so you do not have redundant code in each domain’s object class.</span></span> <span data-ttu-id="a54bc-107">Bu sınıf türlerinin klasörü, *Framework*gibi bir şey değil *seedwork* olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-107">The folder for these types of classes is called *SeedWork* and not something like *Framework*.</span></span> <span data-ttu-id="a54bc-108">Bu, bir çerçeve olarak kabul edilmeden önce yeniden kullanılabilir sınıfların yalnızca küçük bir alt kümesini içerdiğinden *Seedwork* olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-108">It's called *SeedWork* because the folder contains just a small subset of reusable classes which cannot really be considered a framework.</span></span> <span data-ttu-id="a54bc-109">*Seedwork* , [Marwler](https://martinfowler.com/bliki/Seedwork.html) tarafından sunulan [Michael feassileri](https://www.artima.com/forums/flat.jsp?forum=106&thread=8826) ve populartarafından sunulan bir terimdir, ancak bu klasörün ortak, sharedkernel veya benzer bir şekilde adını da değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54bc-109">*Seedwork* is a term introduced by [Michael Feathers](https://www.artima.com/forums/flat.jsp?forum=106&thread=8826) and popularized by [Martin Fowler](https://martinfowler.com/bliki/Seedwork.html) but you could also name that folder Common, SharedKernel, or similar.</span></span>

<span data-ttu-id="a54bc-110">Şekil 7-12, etki alanı modelinin sıralama mikro hizmetindeki seedwork 'i oluşturan sınıfları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-110">Figure 7-12 shows the classes that form the seedwork of the domain model in the ordering microservice.</span></span> <span data-ttu-id="a54bc-111">Varlık, ValueObject ve numaralandırma gibi bazı özel temel sınıflara ek olarak birkaç arabirim vardır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-111">It has a few custom base classes like Entity, ValueObject, and Enumeration, plus a few interfaces.</span></span> <span data-ttu-id="a54bc-112">Bu arabirimler (ırepository ve IUnitOfWork) altyapı katmanını uygulanması gerekenler hakkında bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-112">These interfaces (IRepository and IUnitOfWork) inform the infrastructure layer about what needs to be implemented.</span></span> <span data-ttu-id="a54bc-113">Bu arabirimler, uygulama katmanından bağımlılık ekleme yoluyla da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-113">Those interfaces are also used through Dependency Injection from the application layer.</span></span>

![Temel sınıfları ve arabirimleri içeren SeedWork klasörünün ayrıntılı içeriği: Entity.cs, Enumeration.cs, IAggregateRoot.cs, IRepository.cs, IUnitOfWork.cs ve ValueObject.cs](./media/image13.PNG)

<span data-ttu-id="a54bc-115">**Şekil 7-12**.</span><span class="sxs-lookup"><span data-stu-id="a54bc-115">**Figure 7-12**.</span></span> <span data-ttu-id="a54bc-116">"Seedwork" temel sınıfları ve arabirimleri için örnek bir etki alanı modeli kümesi</span><span class="sxs-lookup"><span data-stu-id="a54bc-116">A sample set of domain model “seedwork" base classes and interfaces</span></span>

<span data-ttu-id="a54bc-117">Bu, birçok geliştiricinin bir biçimsel çerçeve değil projeler arasında paylaştığı kopyalama ve yapıştırma yeniden kullanımının türüdür.</span><span class="sxs-lookup"><span data-stu-id="a54bc-117">This is the type of copy and paste reuse that many developers share between projects, not a formal framework.</span></span> <span data-ttu-id="a54bc-118">Seedçalışmalardan herhangi bir katmanda veya kitaplıkta sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54bc-118">You can have seedworks in any layer or library.</span></span> <span data-ttu-id="a54bc-119">Ancak, sınıf ve arabirimlerin kümesi yeterince büyük olursa, tek bir sınıf kitaplığı oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54bc-119">However, if the set of classes and interfaces gets big enough, you might want to create a single class library.</span></span>

## <a name="the-custom-entity-base-class"></a><span data-ttu-id="a54bc-120">Özel varlık temel sınıfı</span><span class="sxs-lookup"><span data-stu-id="a54bc-120">The custom Entity base class</span></span>

<span data-ttu-id="a54bc-121">Aşağıdaki kod, varlık KIMLIĞI, [eşitlik işleçleri](../../../csharp/language-reference/operators/equality-operators.md), varlık başına bir etki alanı olay listesi vb. gibi herhangi bir etki alanı varlığı tarafından aynı şekilde kullanılabilecek kodu yerleştirebileceğiniz bir varlık temel sınıfı örneğidir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-121">The following code is an example of an Entity base class where you can place code that can be used the same way by any domain entity, such as the entity ID, [equality operators](../../../csharp/language-reference/operators/equality-operators.md), a domain event list per entity, etc.</span></span>

```csharp
// COMPATIBLE WITH ENTITY FRAMEWORK CORE (1.1 and later)
public abstract class Entity
{
    int? _requestedHashCode;
    int _Id;    
    private List<INotification> _domainEvents;
    public virtual int Id 
    {
        get
        {
            return _Id;
        }
        protected set
        {
            _Id = value;
        }
    }

    public List<INotification> DomainEvents => _domainEvents;        
    public void AddDomainEvent(INotification eventItem)
    {
        _domainEvents = _domainEvents ?? new List<INotification>();
        _domainEvents.Add(eventItem);
    }
    public void RemoveDomainEvent(INotification eventItem)
    {
        if (_domainEvents is null) return;
        _domainEvents.Remove(eventItem);
    }

    public bool IsTransient()
    {
        return this.Id == default(Int32);
    }

    public override bool Equals(object obj)
    {
        if (obj == null || !(obj is Entity))
            return false;
        if (Object.ReferenceEquals(this, obj))
            return true;
        if (this.GetType() != obj.GetType())
            return false;
        Entity item = (Entity)obj;
        if (item.IsTransient() || this.IsTransient())
            return false;
        else
            return item.Id == this.Id;
    }

    public override int GetHashCode()
    {
        if (!IsTransient())
        {
            if (!_requestedHashCode.HasValue)
                _requestedHashCode = this.Id.GetHashCode() ^ 31;
            // XOR for random distribution. See:
            // https://blogs.msdn.microsoft.com/ericlippert/2011/02/28/guidelines-and-rules-for-gethashcode/
            return _requestedHashCode.Value;
        }
        else
            return base.GetHashCode();
    }
    public static bool operator ==(Entity left, Entity right)
    {
        if (Object.Equals(left, null))
            return (Object.Equals(right, null));
        else
            return left.Equals(right);
    }
    public static bool operator !=(Entity left, Entity right)
    {
        return !(left == right);
    }
}
```

<span data-ttu-id="a54bc-122">Varlık başına bir etki alanı olay listesi kullanan önceki kod, etki alanı olaylarına odaklanıldığında sonraki bölümlerde açıklanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-122">The previous code using a domain event list per entity will be explained in the next sections when focusing on domain events.</span></span>

## <a name="repository-contracts-interfaces-in-the-domain-model-layer"></a><span data-ttu-id="a54bc-123">Etki alanı modeli katmanındaki depo sözleşmeleri (arabirimler)</span><span class="sxs-lookup"><span data-stu-id="a54bc-123">Repository contracts (interfaces) in the domain model layer</span></span>

<span data-ttu-id="a54bc-124">Depo sözleşmeleri, her toplama için kullanılacak depoların sözleşme gereksinimlerini ifade eden .NET arayüzleridir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-124">Repository contracts are simply .NET interfaces that express the contract requirements of the repositories to be used for each aggregate.</span></span>

<span data-ttu-id="a54bc-125">Depoların kendisi, EF Core kodla veya başka herhangi bir altyapı bağımlılığı ve kodla (LINQ, SQL vb.), etki alanı modeli içinde uygulanmamalıdır; depolar yalnızca etki alanı modelinde tanımladığınız arabirimleri uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-125">The repositories themselves, with EF Core code or any other infrastructure dependencies and code (Linq, SQL, etc.), must not be implemented within the domain model; the repositories should only implement the interfaces you define in the domain model.</span></span>

<span data-ttu-id="a54bc-126">Bu yöntemle ilgili bir örüntü (depo arabirimlerini etki alanı model katmanına yerleştirme), ayrılmış arabirim deseninin bir sıdır.</span><span class="sxs-lookup"><span data-stu-id="a54bc-126">A pattern related to this practice (placing the repository interfaces in the domain model layer) is the Separated Interface pattern.</span></span> <span data-ttu-id="a54bc-127">Marwler tarafından [açıklandığı](https://www.martinfowler.com/eaaCatalog/separatedInterface.html) gibi, "bir pakette arabirim tanımlamak, ancak başka bir pakette uygulamak Için ayrılmış arabirim kullanın.</span><span class="sxs-lookup"><span data-stu-id="a54bc-127">As [explained](https://www.martinfowler.com/eaaCatalog/separatedInterface.html) by Martin Fowler, “Use Separated Interface to define an interface in one package but implement it in another.</span></span> <span data-ttu-id="a54bc-128">Bu şekilde, arabirime bağımlılığı gerektiren bir istemci, uygulamanın tamamen farkında olabilir. "</span><span class="sxs-lookup"><span data-stu-id="a54bc-128">This way a client that needs the dependency to the interface can be completely unaware of the implementation.”</span></span>

<span data-ttu-id="a54bc-129">Ayrılmış arabirim deseninin ardından uygulama katmanının (Bu durumda, mikro hizmet için Web API Projesi) etki alanı modelinde tanımlanan gereksinimlere bağımlılığı olması, ancak altyapıya/kalıcılığı doğrudan bağımlılığı yoktur katmanı.</span><span class="sxs-lookup"><span data-stu-id="a54bc-129">Following the Separated Interface pattern enables the application layer (in this case, the Web API project for the microservice) to have a dependency on the requirements defined in the domain model, but not a direct dependency to the infrastructure/persistence layer.</span></span> <span data-ttu-id="a54bc-130">Buna ek olarak, havuzları kullanarak altyapı/Kalıcılık katmanında uygulanan uygulamayı yalıtmak için bağımlılık ekleme 'yi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54bc-130">In addition, you can use Dependency Injection to isolate the implementation, which is implemented in the infrastructure/ persistence layer using repositories.</span></span>

<span data-ttu-id="a54bc-131">Örneğin, ıorderrepository arabirimine sahip aşağıdaki örnek, OrderRepository sınıfının altyapı katmanında uygulamanız gereken işlemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a54bc-131">For example, the following example with the IOrderRepository interface defines what operations the OrderRepository class will need to implement at the infrastructure layer.</span></span> <span data-ttu-id="a54bc-132">Uygulamanın geçerli uygulamasında, sorgular Basitleştirilmiş CQRS yaklaşımını takip altına göre bölündüğü için, bu kodun yalnızca veritabanına sipariş eklemesi veya güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a54bc-132">In the current implementation of the application, the code just needs to add or update orders to the database, since queries are split following the simplified CQRS approach.</span></span>

```csharp
// Defined at IOrderRepository.cs
public interface IOrderRepository : IRepository<Order>
{
    Order Add(Order order);

    void Update(Order order);

    Task<Order> GetAsync(int orderId);
}

// Defined at IRepository.cs (Part of the Domain Seedwork)
public interface IRepository<T> where T : IAggregateRoot
{
    IUnitOfWork UnitOfWork { get; }
}
```

## <a name="additional-resources"></a><span data-ttu-id="a54bc-133">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a54bc-133">Additional resources</span></span>

- <span data-ttu-id="a54bc-134">**Marwler. Ayrılmış arabirim.**</span><span class="sxs-lookup"><span data-stu-id="a54bc-134">**Martin Fowler. Separated Interface.**</span></span> \
  <https://www.martinfowler.com/eaaCatalog/separatedInterface.html>

>[!div class="step-by-step"]
><span data-ttu-id="a54bc-135">[Önceki](net-core-microservice-domain-model.md)İleri
>[](implement-value-objects.md)</span><span class="sxs-lookup"><span data-stu-id="a54bc-135">[Previous](net-core-microservice-domain-model.md)
[Next](implement-value-objects.md)</span></span>