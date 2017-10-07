---
title: "Коллекция сериализации объектов в Azure Service Fabric aaaReliable | Документы Microsoft"
description: "Сериализация объектов надежных коллекций в Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="b98d5-103">Сериализация объектов надежной коллекции в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b98d5-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="b98d5-104">Надежные коллекций репликацию и сохранить их, являются устойчивыми ошибки компьютеров и энергоснабжения toomake элементов.</span><span class="sxs-lookup"><span data-stu-id="b98d5-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="b98d5-105">Элементы tooreplicate и toopersist, tooserialize необходимость надежного коллекций их.</span><span class="sxs-lookup"><span data-stu-id="b98d5-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="b98d5-106">Надежные коллекций получить hello соответствующий сериализатор для данного типа из надежного диспетчер состояний.</span><span class="sxs-lookup"><span data-stu-id="b98d5-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="b98d5-107">Диспетчер состояния надежное содержит встроенных сериализаторов и позволяет toobe пользовательские сериализаторы, зарегистрированных для данного типа.</span><span class="sxs-lookup"><span data-stu-id="b98d5-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="b98d5-108">Встроенные сериализаторы</span><span class="sxs-lookup"><span data-stu-id="b98d5-108">Built-in Serializers</span></span>

<span data-ttu-id="b98d5-109">Диспетчер надежных состояний включает встроенный сериализатор для некоторых распространенных типов, поэтому они по умолчанию могут эффективно сериализоваться.</span><span class="sxs-lookup"><span data-stu-id="b98d5-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="b98d5-110">Для других типов надежного диспетчер состояния возвращается toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="b98d5-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="b98d5-111">Встроенных сериализаторов более эффективны, так как они знают их типы нельзя изменить, и не обязательно tooinclude сведения о типе hello как имя его типа.</span><span class="sxs-lookup"><span data-stu-id="b98d5-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="b98d5-112">Диспетчер надежных состояний имеет встроенный сериализатор для следующих типов:</span><span class="sxs-lookup"><span data-stu-id="b98d5-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="b98d5-113">Guid</span><span class="sxs-lookup"><span data-stu-id="b98d5-113">Guid</span></span>
- <span data-ttu-id="b98d5-114">bool</span><span class="sxs-lookup"><span data-stu-id="b98d5-114">bool</span></span>
- <span data-ttu-id="b98d5-115">byte</span><span class="sxs-lookup"><span data-stu-id="b98d5-115">byte</span></span>
- <span data-ttu-id="b98d5-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="b98d5-116">sbyte</span></span>
- <span data-ttu-id="b98d5-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="b98d5-117">byte[]</span></span>
- <span data-ttu-id="b98d5-118">char;</span><span class="sxs-lookup"><span data-stu-id="b98d5-118">char</span></span>
- <span data-ttu-id="b98d5-119">string</span><span class="sxs-lookup"><span data-stu-id="b98d5-119">string</span></span>
- <span data-ttu-id="b98d5-120">decimal</span><span class="sxs-lookup"><span data-stu-id="b98d5-120">decimal</span></span>
- <span data-ttu-id="b98d5-121">double</span><span class="sxs-lookup"><span data-stu-id="b98d5-121">double</span></span>
- <span data-ttu-id="b98d5-122">float;</span><span class="sxs-lookup"><span data-stu-id="b98d5-122">float</span></span>
- <span data-ttu-id="b98d5-123">int</span><span class="sxs-lookup"><span data-stu-id="b98d5-123">int</span></span>
- <span data-ttu-id="b98d5-124">uint</span><span class="sxs-lookup"><span data-stu-id="b98d5-124">uint</span></span>
- <span data-ttu-id="b98d5-125">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="b98d5-125">long</span></span>
- <span data-ttu-id="b98d5-126">ulong</span><span class="sxs-lookup"><span data-stu-id="b98d5-126">ulong</span></span>
- <span data-ttu-id="b98d5-127">short</span><span class="sxs-lookup"><span data-stu-id="b98d5-127">short</span></span>
- <span data-ttu-id="b98d5-128">ushort</span><span class="sxs-lookup"><span data-stu-id="b98d5-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="b98d5-129">Настраиваемая сериализация</span><span class="sxs-lookup"><span data-stu-id="b98d5-129">Custom Serialization</span></span>

<span data-ttu-id="b98d5-130">Пользовательские сериализаторы, часто используемые tooincrease производительности или tooencrypt hello данных по сети hello и на диске.</span><span class="sxs-lookup"><span data-stu-id="b98d5-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="b98d5-131">Среди всего прочего пользовательские сериализаторы часто более эффективен, чем универсальный сериализатора, так как они не должны tooserialize сведения о типе hello.</span><span class="sxs-lookup"><span data-stu-id="b98d5-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="b98d5-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) является tooregister используется нестандартный сериализатор для hello данного типа T. Регистрация должна выполняться в построении hello hello StatefulServiceBase tooensure, перед началом восстановления все надежного коллекции имеют доступ к tooread соответствующий сериализатор toohello их материализованных данных.</span><span class="sxs-lookup"><span data-stu-id="b98d5-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="b98d5-133">Настраиваемые сериализаторы имеют приоритет над встроенными сериализаторами.</span><span class="sxs-lookup"><span data-stu-id="b98d5-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="b98d5-134">Например при регистрации настраиваемого сериализатора для int является целых чисел используется tooserialize вместо hello встроенный сериализатор для int.</span><span class="sxs-lookup"><span data-stu-id="b98d5-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="b98d5-135">Как tooimplement настраиваемого сериализатора</span><span class="sxs-lookup"><span data-stu-id="b98d5-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="b98d5-136">Пользовательский сериализатор tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b98d5-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="b98d5-137">IStateSerializer<T> включает перегрузку Write и Read, которая принимает дополнительное базовое значение, называемое T.</span><span class="sxs-lookup"><span data-stu-id="b98d5-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="b98d5-138">Этот API предназначен для разностной сериализации.</span><span class="sxs-lookup"><span data-stu-id="b98d5-138">This API is for differential serialization.</span></span> <span data-ttu-id="b98d5-139">Сейчас функция разностной сериализации не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="b98d5-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="b98d5-140">Следовательно эти две перегрузки не вызываются, пока не будет предоставлена и разрешена разностная сериализация.</span><span class="sxs-lookup"><span data-stu-id="b98d5-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="b98d5-141">Ниже приведен пример настраиваемого типа под названием OrderKey, который содержит четыре свойства.</span><span class="sxs-lookup"><span data-stu-id="b98d5-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="b98d5-142">Ниже приведен пример реализации IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="b98d5-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="b98d5-143">Обратите внимание, что перегрузки Read и Write, которые принимают базовое значение, вызывают соответствующую перегрузку для прямой совместимости.</span><span class="sxs-lookup"><span data-stu-id="b98d5-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="b98d5-144">Возможность обновления</span><span class="sxs-lookup"><span data-stu-id="b98d5-144">Upgradability</span></span>
<span data-ttu-id="b98d5-145">В [пошаговое обновление приложения](service-fabric-application-upgrade.md), hello обновление будет применен tooa подмножество узлов, один домен обновления одновременно.</span><span class="sxs-lookup"><span data-stu-id="b98d5-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="b98d5-146">Во время этого процесса некоторых доменов обновления будет в новой версии приложения hello и некоторых доменов обновления будет hello более старую версию приложения.</span><span class="sxs-lookup"><span data-stu-id="b98d5-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="b98d5-147">Во время этого этапа hello hello новой версии приложения должен быть доступ tooread hello старой версии данных и hello старой версии приложения должен быть доступ tooread hello новая версия данных.</span><span class="sxs-lookup"><span data-stu-id="b98d5-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="b98d5-148">Если формат данных hello не является несовместимым, hello обновлением вперед и назад может сбой, или в худшем случае данные могут теряются и поврежден.</span><span class="sxs-lookup"><span data-stu-id="b98d5-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="b98d5-149">Если вы используете встроенный сериализатор, у вас tooworry о совместимости.</span><span class="sxs-lookup"><span data-stu-id="b98d5-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="b98d5-150">Однако при использовании настраиваемого сериализатора или hello DataContractSerializer hello данные имеют toobe бесконечно обратную и прямую совместимость.</span><span class="sxs-lookup"><span data-stu-id="b98d5-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="b98d5-151">Иными словами каждая версия сериализатор должен будет tooserialize toobe и десериализацию любой версии типа hello.</span><span class="sxs-lookup"><span data-stu-id="b98d5-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="b98d5-152">Пользователи контракта данных должны следовать правилам четко определенных версий hello для добавления, удаления и изменения полей.</span><span class="sxs-lookup"><span data-stu-id="b98d5-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="b98d5-153">Контракт данных также имеет поддержку работа с полями неизвестный, прикрепления процесс сериализации и десериализации hello и работе с наследованием класса.</span><span class="sxs-lookup"><span data-stu-id="b98d5-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="b98d5-154">Дополнительные сведения см. в разделе [Использование контракта данных](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="b98d5-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="b98d5-155">Пользовательский сериализатор пользователи должны соблюдаться правила toohello hello сериализатора, они используют toomake, что он обратную и прямую совместимость.</span><span class="sxs-lookup"><span data-stu-id="b98d5-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="b98d5-156">Поддержка всех версий стандартным способом является добавление сведений о размере только добавление дополнительных свойств и начале hello.</span><span class="sxs-lookup"><span data-stu-id="b98d5-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="b98d5-157">Таким образом каждая версия может считывать столько может и перейдите в оставшейся части hello hello потока.</span><span class="sxs-lookup"><span data-stu-id="b98d5-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b98d5-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b98d5-158">Next steps</span></span>
  * [<span data-ttu-id="b98d5-159">Влияние сериализации данных на обновление приложений</span><span class="sxs-lookup"><span data-stu-id="b98d5-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="b98d5-160">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="b98d5-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="b98d5-161">[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b98d5-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="b98d5-162">[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b98d5-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="b98d5-163">Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="b98d5-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="b98d5-164">Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="b98d5-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="b98d5-165">Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b98d5-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
