---
title: "Сериализация объектов надежной коллекции в Azure Service Fabric | Документация Майкрософт"
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="ed2c6-103">Сериализация объектов надежной коллекции в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ed2c6-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="ed2c6-104">Надежные коллекции реплицируют и сохраняют свои элементы, чтобы обеспечить надежность их работы в случае сбоев машин и отключения электроэнергии.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="ed2c6-105">Для репликации и сохранения элементов надежным коллекциям необходимо сериализовать их.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="ed2c6-106">Надежные коллекции получают соответствующий сериализатор для данного типа из диспетчера надежных состояний.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="ed2c6-107">Диспетчер надежных состояний содержит встроенные сериализаторы и позволяет регистрировать пользовательские сериализаторы для данного типа.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="ed2c6-108">Встроенные сериализаторы</span><span class="sxs-lookup"><span data-stu-id="ed2c6-108">Built-in Serializers</span></span>

<span data-ttu-id="ed2c6-109">Диспетчер надежных состояний включает встроенный сериализатор для некоторых распространенных типов, поэтому они по умолчанию могут эффективно сериализоваться.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="ed2c6-110">Для других типов диспетчер надежных состояний использует [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="ed2c6-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="ed2c6-111">Встроенные сериализаторы эффективнее, так как их типы не могут измениться и им не нужно включать сведения о типе, например его имя.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="ed2c6-112">Диспетчер надежных состояний имеет встроенный сериализатор для следующих типов:</span><span class="sxs-lookup"><span data-stu-id="ed2c6-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="ed2c6-113">Guid</span><span class="sxs-lookup"><span data-stu-id="ed2c6-113">Guid</span></span>
- <span data-ttu-id="ed2c6-114">bool</span><span class="sxs-lookup"><span data-stu-id="ed2c6-114">bool</span></span>
- <span data-ttu-id="ed2c6-115">byte</span><span class="sxs-lookup"><span data-stu-id="ed2c6-115">byte</span></span>
- <span data-ttu-id="ed2c6-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="ed2c6-116">sbyte</span></span>
- <span data-ttu-id="ed2c6-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="ed2c6-117">byte[]</span></span>
- <span data-ttu-id="ed2c6-118">char;</span><span class="sxs-lookup"><span data-stu-id="ed2c6-118">char</span></span>
- <span data-ttu-id="ed2c6-119">string</span><span class="sxs-lookup"><span data-stu-id="ed2c6-119">string</span></span>
- <span data-ttu-id="ed2c6-120">decimal</span><span class="sxs-lookup"><span data-stu-id="ed2c6-120">decimal</span></span>
- <span data-ttu-id="ed2c6-121">double</span><span class="sxs-lookup"><span data-stu-id="ed2c6-121">double</span></span>
- <span data-ttu-id="ed2c6-122">float;</span><span class="sxs-lookup"><span data-stu-id="ed2c6-122">float</span></span>
- <span data-ttu-id="ed2c6-123">int</span><span class="sxs-lookup"><span data-stu-id="ed2c6-123">int</span></span>
- <span data-ttu-id="ed2c6-124">uint</span><span class="sxs-lookup"><span data-stu-id="ed2c6-124">uint</span></span>
- <span data-ttu-id="ed2c6-125">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="ed2c6-125">long</span></span>
- <span data-ttu-id="ed2c6-126">ulong</span><span class="sxs-lookup"><span data-stu-id="ed2c6-126">ulong</span></span>
- <span data-ttu-id="ed2c6-127">short</span><span class="sxs-lookup"><span data-stu-id="ed2c6-127">short</span></span>
- <span data-ttu-id="ed2c6-128">ushort</span><span class="sxs-lookup"><span data-stu-id="ed2c6-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="ed2c6-129">Настраиваемая сериализация</span><span class="sxs-lookup"><span data-stu-id="ed2c6-129">Custom Serialization</span></span>

<span data-ttu-id="ed2c6-130">Настраиваемые сериализаторы обычно используются для повышения производительности или шифрования данных при передаче по сети и хранении на диске.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="ed2c6-131">Помимо прочего, настраиваемые сериализаторы часто являются более эффективными, чем универсальные сериализаторы, так как вам не нужно сериализовать информацию о типе.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="ed2c6-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) используется для регистрации настраиваемого сериализатора для данного типа T. Эта регистрация должна произойти при построении StatefulServiceBase, чтобы гарантировать, что до начала восстановления все надежные коллекции будут иметь доступ к соответствующим сериализаторам для чтения сохраненных данных.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="ed2c6-133">Настраиваемые сериализаторы имеют приоритет над встроенными сериализаторами.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="ed2c6-134">Например, когда регистрируется настраиваемый сериализатор для типа int, он используется для сериализации целых чисел вместо встроенного сериализатора для int.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="ed2c6-135">Реализация настраиваемого сериализатора</span><span class="sxs-lookup"><span data-stu-id="ed2c6-135">How to implement a custom serializer</span></span>

<span data-ttu-id="ed2c6-136">Настраиваемый сериализатор должен реализовать интерфейс [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1).</span><span class="sxs-lookup"><span data-stu-id="ed2c6-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="ed2c6-137">IStateSerializer<T> включает перегрузку Write и Read, которая принимает дополнительное базовое значение, называемое T.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="ed2c6-138">Этот API предназначен для разностной сериализации.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-138">This API is for differential serialization.</span></span> <span data-ttu-id="ed2c6-139">Сейчас функция разностной сериализации не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="ed2c6-140">Следовательно эти две перегрузки не вызываются, пока не будет предоставлена и разрешена разностная сериализация.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="ed2c6-141">Ниже приведен пример настраиваемого типа под названием OrderKey, который содержит четыре свойства.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="ed2c6-142">Ниже приведен пример реализации IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="ed2c6-143">Обратите внимание, что перегрузки Read и Write, которые принимают базовое значение, вызывают соответствующую перегрузку для прямой совместимости.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="ed2c6-144">Возможность обновления</span><span class="sxs-lookup"><span data-stu-id="ed2c6-144">Upgradability</span></span>
<span data-ttu-id="ed2c6-145">При [последовательном обновлении приложения](service-fabric-application-upgrade.md)обновление применяется к подмножеству узлов, переходя от одного домена обновления к другому.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="ed2c6-146">Во время этого процесса некоторые домены обновления будут использовать более раннюю версию приложения, чем другие.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="ed2c6-147">В ходе развертывания новая версия вашего приложения должна иметь способность считывать старые версии данных, а старая версия приложения — новую версию данных.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="ed2c6-148">Если формат данных не обладает прямой и обратной совместимостью, обновление может завершиться неудачей либо данные могут быть утрачены.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="ed2c6-149">При использовании встроенного сериализатора вам не нужно беспокоиться о совместимости.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="ed2c6-150">Однако при использовании настраиваемого сериализатора или DataContractSerializer данные должны быть бесконечно прямо или обратно совместимы.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="ed2c6-151">Иными словами, каждая версия сериализатора должна иметь возможность сериализовать и десериализовать тип любой версии.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="ed2c6-152">Пользователи контракта данных должны следовать строго заданным правилам управления версиями при добавлении, удалении или изменении полей.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="ed2c6-153">Кроме того, контракт данных обладает поддержкой обработки неизвестных полей, участвующих в процессе сериализации и десериализации, а также наследования классов.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="ed2c6-154">Дополнительные сведения см. в разделе [Использование контракта данных](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed2c6-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="ed2c6-155">Пользователи настраиваемого сериализатора должны придерживаться рекомендаций в отношении сериализатора, который они используют, чтобы обеспечить его прямую и обратную совместимость.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="ed2c6-156">Распространенный способ обеспечения поддержки всех версий — добавление сведений о размере в начале и добавление только необязательных свойств.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="ed2c6-157">Таким образом, каждая версия считает только то, что сможет, и перепрыгнет через оставшуюся часть потока.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed2c6-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed2c6-158">Next steps</span></span>
  * [<span data-ttu-id="ed2c6-159">Влияние сериализации данных на обновление приложений</span><span class="sxs-lookup"><span data-stu-id="ed2c6-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="ed2c6-160">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="ed2c6-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="ed2c6-161">[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="ed2c6-162">[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="ed2c6-163">Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="ed2c6-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="ed2c6-164">[Дополнительные разделы](service-fabric-application-upgrade-advanced.md)содержат сведения о работе с расширенными функциями при обновлении приложения.</span><span class="sxs-lookup"><span data-stu-id="ed2c6-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="ed2c6-165">Сведения об устранении распространенных проблем при обновлении приложений см. в статье [Устранение неполадок при обновлениях приложений](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ed2c6-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
