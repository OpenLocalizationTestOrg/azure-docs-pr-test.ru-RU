---
title: "aaaCreate вашего первого надежного микрослужбу Azure в Java | Документы Microsoft"
description: "Введение toocreating приложении Microsoft Azure Service Fabric с служб без отслеживания состояния и с отслеживанием состояния."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Приступая к работе с надежными службами
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-services-quick-start.md)
> * [Java в Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

Эта статья объясняет основы hello служб Azure Service Fabric надежного и содержит инструкции по созданию и развертыванию простого надежной службы приложения, написанные на языке Java. В этом видеоролике Microsoft Virtual Academy также показано, как toocreate без сохранения состояния надежной службы:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Установка и настройка
Прежде чем начать, убедитесь, что у вас есть на компьютере среды разработки Service Fabric hello.
Если вам требуется tooset его, перейдите в слишком[Приступая к работе на Mac](service-fabric-get-started-mac.md) или [Приступая к работе в Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Основные понятия
tooget к работе с надежного обмена, можно только необходимые toounderstand несколько основных понятий.

* **Тип службы**. Это ваша реализация службы. Определяется класс hello написании, расширяющий `StatelessService` и любой другой код или зависимости, используемый в этом документе, а также имя и номер версии.
* **Именованный экземпляр службы**: toorun службы, можно создавать именованные экземпляры типа службы, гораздо как при создании экземпляра объекта типа класса. Экземпляры службы фактически являются создаваемыми экземплярами объектов написанного вами класса службы.
* **Узел службы**: hello именованных экземпляров службы, создайте toorun необходимость внутри узла. узел службы Hello — просто процесса, где можно запускать экземпляры службы.
* **Регистрации службы**. Регистрация объединяет все элементы. Hello службы тип должен быть зарегистрирован с hello Service Fabric среды выполнения службы размещения tooallow Service Fabric toocreate его экземпляры toorun.  

## <a name="create-a-stateless-service"></a>Создание службы без отслеживания состояния
Для начала создайте приложение Service Fabric. Hello Service Fabric SDK для Linux включает Yeoman генератор tooprovide hello и формирование шаблонов для приложения Service Fabric в службы без отслеживания состояния. Запустить, выполнив hello следующие Yeoman команды:

```bash
$ yo azuresfjava
```

Следуйте инструкциям toocreate hello **надежной службы без сохранения состояния**. В этом учебнике приложения hello имя «HelloWorldApplication» и hello службы «HelloWorld». результат Hello включает в себя каталоги для hello `HelloWorldApplication` и `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Реализация службы hello
Откройте файл **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Этот класс определяет тип службы hello и запускать программный код. API-Интерфейс службы Hello предоставляет две точки входа для кода:

* Вызывается метод `runAsync()` с открытой точкой входа, в котором можно начать выполнение любой рабочей нагрузки, например длительных вычислений.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Точка входа связи, где можно подключить любой стек связи по выбору. С ее помощью вы можете получать запросы от пользователей и других служб.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

В этом учебнике рассматривается hello `runAsync()` метод точки входа. Используя его, вы можете сразу же начать выполнение кода.

### <a name="runasync"></a>RunAsync
Hello платформа вызывает этот метод при помещенных и готов tooexecute является экземпляр службы. Для службы без отслеживания состояния, это просто означает при открытии hello экземпляр службы. Токен отмены, который предоставляется toocoordinate при закрытии toobe вашего экземпляра службы. В Service Fabric этого цикла открыть/закрыть экземпляра службы может выполняться много раз за время жизни hello hello службы в целом. Это может происходить по ряду причин.

* система Hello перемещает экземпляров служб для распределения ресурсов.
* В коде возникают ошибки.
* обновляется Hello приложения или системы.
* Базовое оборудование Hello возникает сбой.

Это согласование управляется tookeep Service Fabric службы высокой доступности и правильно балансировкой.

Реализация `runAsync()` не должна использовать синхронную блокировку. Реализация runAsync должна возвращать CompletableFuture tooallow hello среды выполнения toocontinue. Если рабочая нагрузка должен tooimplement длительная задача, которая должна выполняться внутри hello CompletableFuture.

#### <a name="cancellation"></a>Отмена
Отмена рабочей нагрузки является совместной усилий под управлением hello, предоставленный токен отмены. Hello система ожидает от вашей tooend задачи (от успешного завершения, отмены или сбоя) перед переходом. Это hello важные toohonor отмены маркера, Готово любой работы и завершить работу `runAsync()` максимально быстро при hello система запрашивает отмену. Hello следующем примере показано, как toohandle событие отмены:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Регистрация службы
Типы служб должны быть зарегистрированы с помощью среды выполнения Service Fabric hello. Тип службы Hello определен в hello `ServiceManifest.xml` и класс, реализующий службу `StatelessService`. Регистрация службы выполняется в hello процесса главную точку входа. В этом примере hello процесс является главной точкой входа `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Запустите приложение hello

Hello Yeoman формирование шаблонов включает gradle сценария toobuild hello приложения и bash сценарии toodeploy и удалить приложение. приложение hello toorun, первое приложение hello сборки с gradle:

```bash
$ gradle
```

Этот сценарий создает пакет приложения Service Fabric, который можно развернуть с помощью интерфейса командной строки Service Fabric.

### <a name="deploy-with-service-fabric-cli"></a>Развертывание с помощью интерфейса командной строки Service Fabric

сценарий install.sh Hello содержит hello необходимые службы структуры CLI команды toodeploy hello пакета приложения. Запустите приложение hello toodeploy install.sh скрипта.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Дальнейшие действия

* [Командная строка Azure Service Fabric](service-fabric-cli.md)
