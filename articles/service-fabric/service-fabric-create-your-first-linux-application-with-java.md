---
title: "Создание приложения Java Reliable Actors для Linux в Azure Service Fabric | Документация Майкрософт"
description: "Узнайте как создавать приложение Java Reliable Actors Service Fabric в течении пяти минут."
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
ms.openlocfilehash: baf948587ede31fe3d5b4f6f0981269b4cfe4d3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Создание первого приложения Java Reliable Actors для Linux в Service Fabric
> [!div class="op_single_selector"]
> * [C# для Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java для Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# для Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Используя это краткое руководство, вы создадите первое Java-приложение Azure Service Fabric в среде разработки Linux всего за несколько минут.  В результате вы получите простое приложение Java с одной службой, работающее в кластере локальной разработки.  

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы установите пакет SDK для Service Fabric, интерфейс командной строки Service Fabric и настройте кластер разработки в своей [среде разработки Linux](service-fabric-get-started-linux.md). Если вы используете Mac OS X, можно [настроить среду разработки Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).

Вам также потребуется установить [интерфейс командной строки Service Fabric](service-fabric-cli.md).

### <a name="install-and-set-up-the-generators-for-java"></a>Установка и настройка генераторов для Java
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Java в Service Fabric из терминала с помощью генератора шаблонов Yeoman. Чтобы установить генератор шаблонов Service Fabric Yeoman для Java на компьютере, сделайте следующее.
1. Установите Node.js и NPM на компьютере.

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.

  ```bash
  sudo npm install -g yo
  ```
3. Установите генератор Java-приложений Service Fabric Yeoman из NPM.

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-the-application"></a>Создание приложения
Приложение Service Fabric содержит одну или несколько служб, каждая из которых выполняет определенную роль в работе приложения. Генератор, установленный в предыдущем разделе, упрощает создание первой службы и добавление последующих.  Кроме того, можно создать, собрать и развернуть Java-приложения Service Fabric с помощью подключаемого модуля для Eclipse. См. статью [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md). В этом руководстве используйте Yeoman для создания приложения с одной службой, которая сохраняет и получает значение счетчика.

1. В окне терминала введите ``yo azuresfjava``.
2. Присвойте имя приложению.
3. Выберите тип первой службы и присвойте ей имя. Для этого примера выберите службу Reliable Actor. Дополнительные сведения о других типах служб см. в статье [Общие сведения о модели программирования Service Fabric](service-fabric-choose-framework.md).
   ![Генератор Service Fabric Yeoman для Java][sf-yeoman]

## <a name="build-the-application"></a>Создание приложения
Шаблоны Service Fabric для Yeoman включают скрипт сборки для [Gradle](https://gradle.org/), который можно использовать для создания приложения из терминала.
Зависимости Java в Service Fabric извлекаются из Maven. Чтобы создавать приложения Java в Service Fabric и работать с ними, сначала установите JDK и Gradle. Если эти компоненты еще не установлены, запустите следующие команды для установки JDK (openjdk 8 jdk) и Gradle:

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

Используйте следующую команду, чтобы собрать и упаковать приложение:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a>Развертывание приложения
Созданное приложение можно развернуть в локальном кластере.

1. Подключитесь к удаленному кластеру Service Fabric.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. С помощью скрипта установки (включен в шаблон) скопируйте пакет приложения в хранилище образов кластера, зарегистрируйте тип приложения и создайте экземпляр приложения.

    ```bash
    ./install.sh
    ```

Созданное приложение развертывается так же, как и любое другое приложение Service Fabric. Дополнительные сведения см. в документации по [управлению приложениями Service Fabric с помощью интерфейса командной строки Service Fabric](service-fabric-application-lifecycle-sfctl.md).

Параметры для этих команд можно найти в созданном манифесте в пакете приложения.

Когда приложение будет развернуто, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) по адресу [http://localhost:19080/Explorer](http://localhost:19080/Explorer).
Затем разверните узел **Приложения**. Вы увидите одну запись для типа приложения и еще одну — для первого экземпляра этого типа.

## <a name="start-the-test-client-and-perform-a-failover"></a>Запуск тестового клиента и отработка отказа
Проекты субъекта предполагают использование дополнительных средств. Например, для отправки сообщений им требуется другая служба или клиент. Шаблон субъекта включает простой тестовый скрипт, обеспечивающий взаимодействие со службой субъекта.

1. Запустите этот скрипт с помощью служебной программы для отслеживания, чтобы просмотреть выходные данные службы субъекта.  Сценарий теста вызывает для субъекта метод `setCountAsync()`, увеличивающий значение счетчика. Затем для субъекта вызывается метод `getCountAsync()`, чтобы получить новое значение счетчика и вывести его на консоль.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. В Service Fabric Explorer найдите узел, в котором размещена первичная реплика службы субъекта. В нашем примере это узел 3. Первичная реплика службы обрабатывает операции чтения и записи.  Затем изменения в состоянии службы реплицируются во вторичные реплики, выполняющиеся на узлах 0 и 1, как показано на снимке экрана ниже.

    ![Поиск первичной реплики в Service Fabric Explorer][sfx-primary]

3. В разделе **Узлы** щелкните найденный узел, а затем выберите в меню "Действия" пункт **Отключить (перезапустить)**. После этого узел, на котором запущена первичная реплика службы, перезапускается и выполняется принудительная отработка отказа с переходом на одну из вторичных реплик, запущенных на другом узле.  Вторичная реплика повышается до первичной, на другом узле создается еще одна вторичная реплика, и первичная реплика начинает выполнять операции чтения и записи. После перезапуска узла обратите внимание на выходные данные тестового клиента: счетчик будет увеличиваться несмотря на отработку отказа.

## <a name="remove-the-application"></a>Удаление приложения
С помощью скрипта для удаления экземпляра приложения (включен в шаблон) отмените регистрацию пакета приложения и удалите его из хранилища образов кластера.

```bash
./uninstall.sh
```

В обозревателе Service Fabric вы увидите, что приложение и его тип больше не отображаются в узле **Приложения**.

## <a name="service-fabric-java-libraries-on-maven"></a>Библиотеки Java для Service Fabric в Maven
Библиотеки Java для Service Fabric размещены в Maven. Чтобы использовать библиотеки Java для Service Fabric из **mavenCentral**, вы можете добавить зависимости в файлы ``pom.xml`` или ``build.gradle`` своих проектов.

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

Поддержка транспортного уровня для приложения Java в Service Fabric. Вам не нужно явно добавлять эту зависимость в приложения Reliable Actors или Reliable Services, если ваша программа не находится на транспортном уровне.

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

Поддержка на уровне системы для платформы Service Fabric, которая взаимодействует с собственной средой выполнения Service Fabric. Вам не нужно явно добавлять эту зависимость в приложения Reliable Actors или Reliable Services. Эта зависимость извлекается автоматически из Maven при включении других зависимостей, описанных выше.

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

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a>Перенос устаревших приложений Java из Service Fabric для использования с Maven
Мы недавно переместили библиотеки Java для Service Fabric из пакета SDK для Java Service Fabric в репозиторий Maven. Хотя в новых приложениях, созданных с помощью Yeoman или Eclipse, создаются последние обновленные проекты (которые могут работать с Maven), вы можете обновить существующие приложения Service Fabric Java без отслеживания состояния (или приложения Reliable Actors), в которых ранее использовался пакет SDK для Service Fabric Java, чтобы использовать зависимости Java для Service Fabric из Maven. Выполните [инструкции](service-fabric-migrate-old-javaapp-to-use-maven.md), чтобы устаревшие приложения могли взаимодействовать с Maven.

## <a name="next-steps"></a>Дальнейшие действия

* [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md)
* [Общие сведения о надежных субъектах Service Fabric](service-fabric-reliable-actors-introduction.md)
* [Azure Service Fabric command line](service-fabric-cli.md) (Командная строка Azure Service Fabric)
* [Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)
* [Командная строка Azure Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
