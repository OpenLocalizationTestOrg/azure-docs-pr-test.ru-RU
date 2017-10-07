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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Сериализация объектов надежной коллекции в Azure Service Fabric
Надежные коллекций репликацию и сохранить их, являются устойчивыми ошибки компьютеров и энергоснабжения toomake элементов.
Элементы tooreplicate и toopersist, tooserialize необходимость надежного коллекций их.

Надежные коллекций получить hello соответствующий сериализатор для данного типа из надежного диспетчер состояний.
Диспетчер состояния надежное содержит встроенных сериализаторов и позволяет toobe пользовательские сериализаторы, зарегистрированных для данного типа.

## <a name="built-in-serializers"></a>Встроенные сериализаторы

Диспетчер надежных состояний включает встроенный сериализатор для некоторых распространенных типов, поэтому они по умолчанию могут эффективно сериализоваться. Для других типов надежного диспетчер состояния возвращается toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Встроенных сериализаторов более эффективны, так как они знают их типы нельзя изменить, и не обязательно tooinclude сведения о типе hello как имя его типа.

Диспетчер надежных состояний имеет встроенный сериализатор для следующих типов: 
- Guid
- bool
- byte
- sbyte
- byte[]
- char;
- string
- decimal
- double
- float;
- int
- uint
- длинное целое число
- ulong
- short
- ushort

## <a name="custom-serialization"></a>Настраиваемая сериализация

Пользовательские сериализаторы, часто используемые tooincrease производительности или tooencrypt hello данных по сети hello и на диске. Среди всего прочего пользовательские сериализаторы часто более эффективен, чем универсальный сериализатора, так как они не должны tooserialize сведения о типе hello. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) является tooregister используется нестандартный сериализатор для hello данного типа T. Регистрация должна выполняться в построении hello hello StatefulServiceBase tooensure, перед началом восстановления все надежного коллекции имеют доступ к tooread соответствующий сериализатор toohello их материализованных данных.

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
> Настраиваемые сериализаторы имеют приоритет над встроенными сериализаторами. Например при регистрации настраиваемого сериализатора для int является целых чисел используется tooserialize вместо hello встроенный сериализатор для int.

### <a name="how-tooimplement-a-custom-serializer"></a>Как tooimplement настраиваемого сериализатора

Пользовательский сериализатор tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) интерфейса.

> [!NOTE]
> IStateSerializer<T> включает перегрузку Write и Read, которая принимает дополнительное базовое значение, называемое T. Этот API предназначен для разностной сериализации. Сейчас функция разностной сериализации не предоставляется. Следовательно эти две перегрузки не вызываются, пока не будет предоставлена и разрешена разностная сериализация.

Ниже приведен пример настраиваемого типа под названием OrderKey, который содержит четыре свойства.

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

Ниже приведен пример реализации IStateSerializer<OrderKey>.
Обратите внимание, что перегрузки Read и Write, которые принимают базовое значение, вызывают соответствующую перегрузку для прямой совместимости.

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

## <a name="upgradability"></a>Возможность обновления
В [пошаговое обновление приложения](service-fabric-application-upgrade.md), hello обновление будет применен tooa подмножество узлов, один домен обновления одновременно. Во время этого процесса некоторых доменов обновления будет в новой версии приложения hello и некоторых доменов обновления будет hello более старую версию приложения. Во время этого этапа hello hello новой версии приложения должен быть доступ tooread hello старой версии данных и hello старой версии приложения должен быть доступ tooread hello новая версия данных. Если формат данных hello не является несовместимым, hello обновлением вперед и назад может сбой, или в худшем случае данные могут теряются и поврежден.

Если вы используете встроенный сериализатор, у вас tooworry о совместимости.
Однако при использовании настраиваемого сериализатора или hello DataContractSerializer hello данные имеют toobe бесконечно обратную и прямую совместимость.
Иными словами каждая версия сериализатор должен будет tooserialize toobe и десериализацию любой версии типа hello.

Пользователи контракта данных должны следовать правилам четко определенных версий hello для добавления, удаления и изменения полей. Контракт данных также имеет поддержку работа с полями неизвестный, прикрепления процесс сериализации и десериализации hello и работе с наследованием класса. Дополнительные сведения см. в разделе [Использование контракта данных](https://msdn.microsoft.com/library/ms733127.aspx).

Пользовательский сериализатор пользователи должны соблюдаться правила toohello hello сериализатора, они используют toomake, что он обратную и прямую совместимость.
Поддержка всех версий стандартным способом является добавление сведений о размере только добавление дополнительных свойств и начале hello.
Таким образом каждая версия может считывать столько может и перейдите в оставшейся части hello hello потока.

## <a name="next-steps"></a>Дальнейшие действия
  * [Влияние сериализации данных на обновление приложений](service-fabric-application-upgrade-data-serialization.md)
  * [Справочник разработчика по надежным коллекциям](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.
  * [Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.
  * Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).
  * Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).
  * Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).
