---
title: "aaaCreate своего первого приложения Azure микрослужбами Linux с использованием C# | Документы Microsoft"
description: "Создание и развертывание приложения Service Fabric с помощью C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Создание первого приложения Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# для Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java для Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# для Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric предоставляет пакеты SDK для создания служб в среде Linux с помощью .NET Core и Java. В этом учебнике мы рассмотрим, как toocreate приложения для Linux и построения службы с помощью C# (.NET Core).

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы [настройте среду разработки Linux](service-fabric-get-started-linux.md). Если вы используете Mac OS X, вы можете [настроить универсальную среду Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).

Необходимо также tooinstall hello [службы структуры CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Установка и настройка генераторы hello для c#
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения CSharp в Service Fabric из терминала с помощью генератора шаблонов Yeoman. Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для c# работает на компьютере.
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Создание приложения hello
Приложение Service Fabric может содержать одну или несколько служб, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello. Hello Service Fabric [Yeoman](http://yeoman.io/) генератор для c#, который устанавливается на последнем шаге, делает его легко toocreate свою первую службу и tooadd более позднее. Воспользуемся Yeoman toocreate приложения с одной службой.

1. В конечном введите hello, следующая команда toostart построение hello формирование шаблонов:`yo azuresfcsharp`
2. Присвойте имя приложению.
3. Выберите тип свою первую службу hello и назовите его. Для целей этого учебника hello следует выбрать вариант надежного службу субъектов.

   ![Генератор Service Fabric Yeoman для C#][sf-yeoman]

> [!NOTE]
> Дополнительные сведения о параметрах hello см. в разделе [Service Fabric, общие сведения о модели программирования](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Создание приложения hello
шаблоны Yeoman структуры службы Hello содержат сценарий построения, которые можно использовать приложение hello toobuild из hello терминалов (после перехода в папке приложения toohello).

  ```sh
 cd myapp
 ./build.sh
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

После развертывания приложения hello, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) в [http://localhost:19080/обозреватель](http://localhost:19080/Explorer). Разверните hello **приложений** узел и обратите внимание, что теперь есть запись для типа приложения и другой для hello первого экземпляра этого типа.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Запустите тестовый клиент hello и отработка отказа
Проекты субъекта предполагают использование дополнительных средств. Они требуют другой службой или клиентом toosend их сообщений. шаблон субъекта Hello включает простой тестовый скрипт, можно использовать toointeract с службу субъектов hello.

1. Запустите скрипт hello, используя hello Контрольные значения программа toosee hello выходные данные hello субъекта службы.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. В обозреватель Service Fabric найдите узел размещения hello первичной реплики для службы субъекта hello. В приведенном далее снимке экрана приветствия это узел 3.

    ![Поиск hello первичной реплики в обозреватель Service Fabric][sfx-primary]
3. Щелкните узел hello можно найти в предыдущем шаге hello, а затем выберите **деактивировать (перезапустите)** из меню "действия" hello. Это действие перезапускает один узел в локальном принудительного перехода на другой ресурс tooa вторичной реплики, запущенный на другом узле кластера. При выполнении этого действия, Обратите внимания toohello вывода из тестового клиента hello и обратите внимание, что счетчика hello продолжается tooincrement несмотря на hello перехода на другой ресурс.

## <a name="adding-more-services-tooan-existing-application"></a>Добавление существующего приложения tooan дополнительные службы

tooadd другой tooan приложение службы уже созданные с помощью `yo`, выполните следующие шаги hello:
1. Измените корневой каталог toohello существующее приложение hello.  Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.
2. Запустите `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>Миграция с project.json too.csproj
1. Выполнение «перенос dotnet» в корневом каталоге проекта выполнит миграцию всех hello project.json toocsproj формат.
2. Обновление hello проект ссылается на соответствующим образом toocsproj файлов проекта.
3. Обновите файлы toocsproj имена файла проекта hello в build.sh.

## <a name="next-steps"></a>Дальнейшие действия

* [Общие сведения о надежных субъектах Service Fabric](service-fabric-reliable-actors-introduction.md)
* [Взаимодействие с кластерами Service Fabric, с помощью службы структуры CLI hello](service-fabric-cli.md)
* [Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)
* [Командная строка Azure Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
