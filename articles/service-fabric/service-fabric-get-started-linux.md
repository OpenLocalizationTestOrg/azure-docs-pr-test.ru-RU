---
title: "aaaSet среды разработки для Linux | Документы Microsoft"
description: "Установка среды выполнения hello и пакета SDK и создайте кластер локальную разработку в Linux. После завершения этой установки, будет готов toobuild приложений."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Подготовка среды разработки в Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy и запустите [приложения Azure Service Fabric](service-fabric-application-model.md) на компьютере разработки Linux установке среды выполнения hello и общие пакета SDK. Вы также можете установить дополнительные пакеты SDK для Java и .NET Core.

## <a name="prerequisites"></a>Предварительные требования

для разработки поддерживаются Hello следующих версий операционной системы:

* Ubuntu 16.04 (`Xenial Xerus`).

## <a name="update-your-apt-sources"></a>Обновление списка источников APT
tooinstall hello SDK и hello связанного пакета среды выполнения через программу командной строки hello apt get, необходимо сначала обновить источникам дополнительные средства упаковки (APT).

1. Откройте окно терминала.
2. Добавьте список источников tooyour репозитория Service Fabric hello.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Добавить hello `dotnet` список источников tooyour репозитория.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Добавить hello tooyour APT keyring ключа новую защитную конфиденциальности Gnu (GnuPG или GPG).

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Добавьте hello официальный Docker GPG ключа tooyour APT keyring.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Настройки хранилища Docker hello.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Обновление пакета списках на основании hello вновь добавлен репозиториев.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Установка и настройка hello пакета SDK для установки локального кластера

После обновления исходных файлов, можно установить пакет SDK для hello. Установите пакет Service Fabric SDK hello, подтверждение установки hello и соглашаетесь toohello лицензионное соглашение.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Hello следующие команды автоматизировать принимающая hello лицензии для Service Fabric пакетов:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Настройка локального кластера
  Если hello Установка выполнена успешно, можно будет toostart локального кластера.

  1. Запустите сценарий установки кластера hello.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Откройте веб-браузер и перейдите в слишком[Service Fabric Explorer](http://localhost:19080/Explorer). Если hello кластер запущен, вы увидите панель мониторинга Service Fabric Explorer hello.

      ![Обозреватель Service Fabric Explorer в Linux][sfx-linux]

  На этом этапе можно развертывать готовые пакеты приложений Service Fabric или новые приложения на базе гостевых контейнеров или гостевых исполняемых файлов. toobuild новых служб с помощью hello Java или пакетами SDK .NET Core, выполните действия установки дополнительных hello, которые приведены в последующих разделах.


  > [!NOTE]
  > Автономные кластеры не поддерживаются в Linux. Hello Предварительная версия поддерживает только одно поле и несколькими компьютерами кластеры Azure Linux.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Настройка службы структуры CLI hello

Hello [службы структуры CLI](service-fabric-cli.md) содержит команды для взаимодействия с сущностями Service Fabric, включая кластеров и приложения. Он основан на python, поэтому следует убедиться, что toohave python и шагов установки, прежде чем продолжить hello следующую команду:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Установка и настройка генераторы hello для контейнеров и исполняемые файлы гостя
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Service Fabric из терминала с помощью генератора шаблонов Yeoman. Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для работы на компьютере.

1. Установите Node.js и NPM на компьютере.

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.

  ```bash
  sudo npm install -g yo
  ```
3. Установка генератор контейнера hello Yeo структуры службы и генератор execuatble гостевой из NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

После установки hello выше генераторы должно быть возможности toocreate приложений с помощью гостевых служб исполняемого файла или контейнера, запустив `yo azuresfguest` или `yo azuresfcontainer` соответственно.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Установка hello необходимые Java артефакты (необязательный параметр, если требуется toouse hello Java модели программирования)

службы toobuild Service Fabric, с помощью Java, убедитесь, что установлена 1.8 JDK установлен вместе с Gradle, который используется для выполнения задачи построения. Следующий фрагмент кода Hello устанавливает Open JDK 1.8 вместе с Gradle. библиотеки службы структуры Java Hello извлекаются из Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Установка hello Eclipse Neon подключаемого модуля (необязательно)

Можно установить подключаемый модуль Eclipse hello для структуры службы из внутри hello **интегрированной среды разработки Eclipse для разработчиков Java**. Eclipse toocreate Service Fabric гостевой исполняемый файл приложения и приложения контейнера можно использовать в приложениях Java структуры tooService сложения.

1. В Eclipse, убедитесь, что у последней Neon Eclipse и hello последнюю версию Buildship (1.0.17 или более поздней версии) установлен. Для проверки версии установленных компонентов hello выберите **справки** > **сведения об установке**. Можно обновить с помощью инструкций hello в Buildship [Eclipse Buildship: подключаемые модули Eclipse для Gradle][buildship-update].

2. tooinstall hello Service Fabric подключаемый модуль, выберите **справки** > **Установка нового программного обеспечения**.

3. В hello **работать с** введите **http://dl.microsoft.com/eclipse**.

4. Щелкните **Добавить**.

    ![Страница приветствия доступного программного обеспечения][sf-eclipse-plugin]

5. Выберите hello **ServiceFabric** подключаемый модуль, а затем нажмите кнопку **Далее**.

6. Выполните шаги установки hello и примите лицензионное соглашение hello.

Если уже имеется hello подключаемого модуля Eclipse структуры службы установлены, убедитесь, что имеется hello последнюю версию. Можно проверить, выбрав **справки** > **сведения об установке** и затем найти Service Fabric в hello список модулей. Выберите **обновление**, если доступна более новая версия.

Дополнительные сведения см. в статье [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Установка hello .NET Core SDK (не обязательно, если требуется, чтобы в модели программирования .NET Core hello toouse)
Hello .NET Core SDK предоставляет библиотеки hello и шаблоны, которые находятся служб Service Fabric требуется toobuild с .NET Core. Установка пакета SDK для .NET Core hello путем выполнения следующих hello-

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Обновление hello SDK и среды выполнения

tooupdate toohello последнюю версию пакета SDK для hello и среды выполнения, запустите следующие команды hello (отмените выбор hello пакетов SDK, которые не требуется):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate hello Java SDK двоичных файлов Maven, необходимые сведения о версии tooupdate hello hello соответствующего двоичного файла в hello ``build.gradle`` последнюю версию файла toopoint toohello. tooknow точно которых требуется версия tooupdate hello, можно ссылаться tooany ``build.gradle`` файл выборок, Приступая к работе Service Fabric [здесь](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Обновление hello пакетов может вызвать под управлением кластера toostop вашей локальной разработки система. Перезапустите локальный кластер после обновления по инструкциям hello на этой странице.

## <a name="next-steps"></a>Дальнейшие действия

* [Создание первого Java-приложения Service Fabric в Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md)
* [Создание первого приложения Azure Service Fabric](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Настройка среды разработки для Mac OS X](service-fabric-get-started-mac.md)
* [Использовать toomanage hello CLI структуры службы приложения](service-fabric-application-lifecycle-sfctl.md)
* [Различия между Service Fabric для Linux (предварительная версия) и Windows (общедоступная версия)](service-fabric-linux-windows-differences.md)
* [Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
