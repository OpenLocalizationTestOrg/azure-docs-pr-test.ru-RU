---
title: "aaaCreate приложения Java службы reliable Actor Azure Service Fabric для Linux | Документы Microsoft"
description: "Узнайте, как toocreate и развертывать приложения Java Service Fabric службы reliable Actor в течение пяти минут."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Создание первого приложения Java Reliable Actors для Linux в Service Fabric
> [!div class="op_single_selector"]
> * [C# для Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java для Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# для Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Используя это краткое руководство, вы создадите первое Java-приложение Azure Service Fabric в среде разработки Linux всего за несколько минут.  По завершении вы получите простое приложение Java одна служба запущена на кластере локальная разработка hello.  

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы установки hello Service Fabric SDK, hello CLI структуры службы и настроить кластер разработки в вашей [среды разработки Linux](service-fabric-get-started-linux.md). Если вы используете Mac OS X, можно [настроить среду разработки Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).

Необходимо также tooinstall hello [службы структуры CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Установка и настройка генераторы hello для Java
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Java в Service Fabric из терминала с помощью генератора шаблонов Yeoman. Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для Java работа на компьютере.
1. Установите Node.js и NPM на компьютере.

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.

  ```bash
  sudo npm install -g yo
  ```
3. Установка приложения генератора hello Yeo Java структуры службы из NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Создание приложения hello
Приложение Service Fabric содержит одну или несколько служб, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello. Генератор Hello установлены в последнем разделе hello, делает его легко toocreate свою первую службу и tooadd более позднее.  Кроме того, можно создать, собрать и развернуть Java-приложения Service Fabric с помощью подключаемого модуля для Eclipse. См. статью [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md). В этом кратком руководстве используйте Yeoman toocreate приложения с одной службы, который сохраняет и возвращает значение счетчика.

1. В окне терминала введите ``yo azuresfjava``.
2. Присвойте имя приложению.
3. Выберите тип свою первую службу hello и назовите его. Для этого примера выберите службу Reliable Actor. Дополнительные сведения о hello других типов служб, в разделе [Service Fabric, общие сведения о модели программирования](service-fabric-choose-framework.md).
   ![Генератор Service Fabric Yeoman для Java][sf-yeoman]

## <a name="build-hello-application"></a>Создание приложения hello
шаблоны Hello Yeoman структуры службы включают сценарий построения для [Gradle](https://gradle.org/), который можно использовать приложение hello toobuild из hello терминалов.
Зависимости Java в Service Fabric извлекаются из Maven. toobuild и hello приложений Java структуры службы, необходимо tooensure, что у вас есть JDK и установлены Gradle. Если еще не установлен, можно запустить hello tooinstall JDK(openjdk-8-jdk) и Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

пакет и toobuild hello, выполнения приложения hello следующее:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Развертывание приложения hello
После построения приложения hello, вы можете развернуть локальный кластер toohello.

1. Подключите toohello локальный кластер Service Fabric.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Сценарий установки выполнения hello в toocopy шаблона hello hello хранилище образов кластера для приложения пакет toohello, регистрация типа приложения hello и создание экземпляра приложения hello.

    ```bash
    ./install.sh
    ```

Развертывание приложения hello построения является Здравствуйте таким же, как любое другое приложение Service Fabric. См. в документации hello [управление приложением Service Fabric с hello службы структуры CLI](service-fabric-application-lifecycle-sfctl.md) подробные инструкции.

Команды toothese параметры можно найти в манифестах hello создан внутри пакета приложения hello.

После развертывания приложения hello, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) в [http://localhost:19080/обозреватель](http://localhost:19080/Explorer).
Разверните hello **приложений** узел и обратите внимание, что теперь есть запись для типа приложения и другой для hello первого экземпляра этого типа.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Запустите тестовый клиент hello и отработка отказа
Субъекты никакие действия выполняться не сами по себе, они требуют другой службой или клиентом toosend их сообщений. шаблон субъекта Hello включает простой тестовый скрипт, можно использовать toointeract с службу субъектов hello.

1. Запустите скрипт hello, используя hello Контрольные значения программа toosee hello выходные данные hello субъекта службы.  Hello тестовый скрипт вызывает hello `setCountAsync()` tooincrement субъекта hello счетчик, метод вызывает hello `getCountAsync()` метод hello субъекта tooget hello новое значение счетчика и отображает это значение toohello консоли.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. Найдите hello узла размещения hello первичной реплики для службы hello субъекта Service Fabric Explorer. В приведенном далее снимке экрана приветствия это узел 3. дескрипторы реплики основной службы Hello операций чтения и записи.  Изменения в состоянии ожидания toohello вторичных реплик, работающих на узлах, 0 и 1 в приведенном ниже снимке экрана приветствия затем реплицируются.

    ![Поиск hello первичной реплики в обозреватель Service Fabric][sfx-primary]

3. В **узлы**, щелкните узел hello можно найти в предыдущем шаге hello, а затем выберите **деактивировать (перезапустите)** из меню "действия" hello. Это действие перезапускает hello узла, под управлением реплики основной службы hello и инициирует переход на другой ресурс tooone hello вторичных реплик, запущенный на другом узле.  Вторичная реплика — унаследованная tooprimary, другой дополнительной реплике создается на другом узле, и первичная реплика hello запускает tootake операций чтения и записи. Как перезапуска узла hello, просмотр выходных данных hello hello тестового клиента и обратите внимание, что счетчика hello продолжается tooincrement несмотря на hello перехода на другой ресурс.

## <a name="remove-hello-application"></a>Удалить приложение hello
Использовать сценарий удаления hello в экземпляр приложения hello toodelete шаблона hello, отмените регистрацию пакета приложения hello и удаления пакета приложения hello хранилище образов кластера hello.

```bash
./uninstall.sh
```

В обозреватель Service Fabric видно, что приложение hello и тип приложения больше не отображались в hello **приложений** узла.

## <a name="service-fabric-java-libraries-on-maven"></a>Библиотеки Java для Service Fabric в Maven
Библиотеки Java для Service Fabric размещены в Maven. Можно добавить зависимости hello в hello ``pom.xml`` или ``build.gradle`` библиотеки Service Fabric Java toouse проекты из **mavenCentral**.

### <a name="actors"></a>Субъекты

Поддержка субъекта Service Fabric Reliable Actors для приложения.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Службы

Поддержка службы без отслеживания состояния Service Fabric для приложения.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Прочее
#### <a name="transport"></a>Транспортировка

Поддержка транспортного уровня для приложения Java в Service Fabric. Не обязательно tooexplicitly добавлять этот tooyour зависимостей Reliable Actor и приложения служб, без программирования на уровне транспорта hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Поддержка Service Fabric

Поддержка уровня системы для службы структуры, говорящий toonative среда выполнения Service Fabric. Нет необходимости tooexplicitly добавьте эту зависимость tooyour Reliable Actor или приложений службы. Это возвращает автоматически получены из Maven, при включении hello другие зависимости выше.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Миграция старый toobe приложений Java структуры службы, используемые с Maven
Служба Fabric Java библиотеки недавно были удалены из репозитория tooMaven Service Fabric Java SDK. Хотя hello новые приложения, созданные с помощью Yeoman или Eclipse, создаст последних измененных проектов (которые будут может toowork с Maven), необходимо обновить существующие структуры службы без сохранения состояния и приложения Java субъектов, которые использовали hello службы Структуры пакета Java SDK более ранних версиях зависимости службы структуры Java hello toouse из Maven. Выполните шаги hello упомянутые [здесь](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure старые приложения работает с Maven.

## <a name="next-steps"></a>Дальнейшие действия

* [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md)
* [Общие сведения о надежных субъектах Service Fabric](service-fabric-reliable-actors-introduction.md)
* [Взаимодействовать с помощью hello CLI структуры службы кластеров Service Fabric](service-fabric-cli.md)
* [Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)
* [Командная строка Azure Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
