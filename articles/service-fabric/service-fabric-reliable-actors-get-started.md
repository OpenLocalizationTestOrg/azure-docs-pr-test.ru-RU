---
title: "aaaCreate вашего первого на основе субъектов Azure микрослужбу в C# | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги создания, отладки и развертывания простой службы на основе субъектов, с помощью службы структуры службы Reliable Actor hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Приступая к работе с Reliable Actors
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-actors-get-started.md)
> * [Java в Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

В этой статье объясняется hello основные сведения о службе Azure Fabric службы Reliable actor и описан процесс создания, отладки и развертывания простого Reliable Actor приложения в Visual Studio.

## <a name="installation-and-setup"></a>Установка и настройка
Прежде чем начать, проверьте наличие на компьютере среды разработки Service Fabric hello.
Если вам требуется tooset его, см. Подробные инструкции по [как tooset среды разработки hello](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Основные понятия
tooget выполнению службы Reliable Actor, нужно только необходимые toounderstand несколько основных понятий.

* **Служба субъекта**. Службы Reliable Actor упакованы в надежные службы, которая может быть развернута в инфраструктуре Service Fabric hello. Экземпляры субъектов активируются в именованном экземпляре службы.
* **Регистрация субъекта**. Как с помощью надежного обмена службы Reliable Actor должен toobe зарегистрирована среда выполнения Service Fabric hello. Кроме того тип субъекта hello должен toobe зарегистрирован со средой выполнения hello субъекта.
* **Интерфейс субъекта**. интерфейс Hello субъекта является toodefine используется строго типизированный открытый интерфейс субъекта. В hello терминологии модели Reliable Actor hello субъекта интерфейс определяет hello может понять и обрабатывать типы сообщений, которые hello субъекта. интерфейс Hello субъекта используется другим субъектам и клиентские приложения слишком «отправить» (асинхронно) субъекта toohello сообщений. Субъекты Reliable Actors могут реализовывать несколько интерфейсов.
* **Класс ActorProxy**. Hello класс ActorProxy используется tooinvoke клиентского приложения hello методы, предоставляемые через интерфейс hello субъекта. Hello ActorProxy класс предоставляет две важные функции:
  
  * Разрешение имен: это может toolocate hello субъекта в кластере hello (поиск hello узел кластера hello, где размещается).
  * Обработка сбоев: он повторите вызовы методов и повторно разрешить расположение субъекта hello после, например, сбой, который требует toobe субъекта hello переместить tooanother узел в кластере hello.

следующие правила, которые относятся интерфейсы tooactor Hello, следует отметить:

* методы интерфейса субъекта не могут быть перегружены;
* методы интерфейса субъекта не должны иметь выходных, ссылочных или необязательных параметров.
* универсальные интерфейсы не поддерживаются.

## <a name="create-a-new-project-in-visual-studio"></a>Создание проекта в Visual Studio
Запустите Visual Studio 2015 или Visual Studio 2017 от имени администратора и создайте проект приложения Service Fabric.

![Средства Service Fabric для Visual Studio — новый проект][1]

Hello Далее диалогового окна можно выбрать hello типа проекта, которые должны toocreate.

![Шаблоны проекта Service Fabric][5]

Для проекта "HelloWorld" hello воспользуемся служба Service Fabric службы Reliable Actor hello.

После создания решения hello, вы увидите hello следующие структуры:

![Структура проекта Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Простые стандартные блоки в решении на базе надежных субъектов
Как правило, решение на основе модели Reliable Actors состоит из трех проектов.

* **проект приложения Hello (MyActorApplication)**. Это проект hello, которая упаковывает всех служб hello вместе для развертывания. Он содержит hello *ApplicationManifest.xml* и скриптов PowerShell для управления приложения hello.
* **интерфейс Hello проекта (MyActor.Interfaces)**. Это hello проект, который содержит определение интерфейса hello для субъекта hello. В проекте MyActor.Interfaces hello можно определить hello интерфейсы, которые будут использоваться с субъектами hello в решении hello. Субъект интерфейсов могут быть определены в любой проект с любым именем, однако hello интерфейс определяет контракт hello субъекта, который совместно используется hello субъекта реализация и вызов hello субъект, поэтому он обычно toodefine смысле клиентов hello в сборку, являющуюся отделить от реализации субъекта hello и может совместно использоваться несколькими проектами.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **проект службы субъекта Hello (MyActor)**. Это — hello проекта, используемого toodefine hello Service Fabric служба, которая является постоянной toohost hello субъекта. Он содержит реализацию hello hello субъекта. Коллекция субъекта реализуется класс, производный от базового типа hello `Actor` и реализует hello интерфейсы, определенные в проекте MyActor.Interfaces hello. Класс субъекта также должен реализовывать конструктор, принимающий `ActorService` экземпляра и `ActorId` и передает их toohello базового `Actor` класса. Это позволяет внедрять зависимости платформы как зависимости конструктора.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

необходимо зарегистрировать службу Hello субъекта с типом службы в среде выполнения Service Fabric hello. В порядок hello toorun службу субъектов субъекта экземпляры, тип субъекта также должен быть зарегистрирован с hello службу субъектов. Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Если у вас есть только одно определение субъекта начать новый проект в Visual Studio, регистрацию hello включается по умолчанию в коде hello, создаваемый Visual Studio. При указании других сторон в службе hello требуется tooadd hello субъекта регистрации с помощью:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Hello субъекты структуры службы среда выполнения выдает некоторые [события и счетчики производительности, связанные с методами tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Они полезны при диагностике и мониторинге производительности.
> 
> 

## <a name="debugging"></a>Отладка
Hello средств Service Fabric для Visual Studio поддерживает отладку на локальном компьютере. Можно запустить сеанс отладки, hello нажатие клавиши F5. Visual Studio скомпилирует (при необходимости) пакеты. Он также развертывает приложение hello hello локальном кластере Service Fabric и присоединяет отладчик hello.

Во время развертывания hello, вы увидите ход выполнения hello в hello **вывода** окна.

![Окно вывода отладки Service Fabric][3]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [использование платформы Service Fabric hello службы Reliable Actor](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
