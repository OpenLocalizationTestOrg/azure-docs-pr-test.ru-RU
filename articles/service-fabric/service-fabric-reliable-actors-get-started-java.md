---
title: "aaaCreate вашего первого на основе субъектов Azure микрослужбу в Java | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги создания, отладки и развертывания простой службы на основе субъектов, с помощью службы структуры службы Reliable Actor hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
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

Эта статья объясняет основы hello Azure Service Fabric Reliable Actors и содержит инструкции по созданию и развертыванию простого приложения Reliable Actor в Java.

## <a name="installation-and-setup"></a>Установка и настройка
Прежде чем начать, убедитесь, что у вас есть на компьютере среды разработки Service Fabric hello.
Если вам требуется tooset его, перейдите в слишком[Приступая к работе на Mac](service-fabric-get-started-mac.md) или [Приступая к работе в Linux](service-fabric-get-started-linux.md).

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

## <a name="create-an-actor-service"></a>Создание службы субъекта
Сначала создайте приложение Service Fabric. Hello Service Fabric SDK для Linux включает Yeoman генератор tooprovide hello и формирование шаблонов для приложения Service Fabric в службы без отслеживания состояния. Запустить, выполнив hello следующие Yeoman команды:

```bash
$ yo azuresfjava
```

Следуйте инструкциям toocreate hello **надежной службы субъекта**. Для этого учебника назовите hello приложения «HelloWorldActorApplication» и hello субъект «HelloWorldActor». будет создана Hello после формирования шаблонов:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Простые стандартные блоки в решении на базе надежных субъектов
описанные выше основные понятия Hello переводиться hello основные стандартные блоки службы Reliable Actor.

### <a name="actor-interface"></a>Интерфейс субъекта
Содержит определение интерфейса hello для субъекта hello. Этот интерфейс определяет контракт hello субъект, который является общим для hello субъекта реализация и вызов hello субъект, поэтому он обычно смысле toodefine его в месте, которое отделить от реализации субъекта hello и могут использоваться в нескольких других клиентов hello службы или клиентского приложения.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Служба субъекта
Служба субъекта содержит реализацию и код регистрации субъекта. Hello субъекта класс реализует интерфейс hello субъекта. Здесь субъект выполняет свою работу.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Регистрация субъекта
необходимо зарегистрировать службу Hello субъекта с типом службы в среде выполнения Service Fabric hello. В порядок hello toorun службу субъектов субъекта экземпляры, тип субъекта также должен быть зарегистрирован с hello службу субъектов. Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Тестовый клиент
Это простое тестовое приложение клиента можно запускать отдельно от tootest приложения Service Fabric hello службы субъекта. Это пример из где hello ActorProxy можно использовать tooactivate и взаимодействия с экземплярами субъекта. Он не развертывается с вашей службой.

### <a name="hello-application"></a>приложение Hello
Наконец пакеты приложения hello hello субъекта-службы и другие службы, который может быть добавлена в hello будущих вместе для развертывания. Он содержит hello *ApplicationManifest.xml* и заполнителями для пакета службы субъекта hello.

## <a name="run-hello-application"></a>Запустите приложение hello

Hello Yeoman формирование шаблонов включает gradle сценария toobuild hello приложения и bash сценарии toodeploy и удалить приложение. приложение hello toodeploy, первое приложение hello сборки с gradle:

```bash
$ gradle
```

Этот сценарий создаст пакет приложения Service Fabric, который можно развернуть с помощью инструментов интерфейса командной строки Service Fabric.

### <a name="deploy-service-fabric-cli"></a>Развертывание интерфейса командной строки Service Fabric

сценарий install.sh Hello содержит hello необходимые службы структуры CLI (sfctl) команды toodeploy hello пакета приложения.
Запустите приложение hello install.sh сценария toodeploy hello.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Дальнейшие действия

* [Командная строка Azure Service Fabric](service-fabric-cli.md)
