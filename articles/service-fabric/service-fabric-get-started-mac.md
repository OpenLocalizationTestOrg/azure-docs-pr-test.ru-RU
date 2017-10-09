---
title: "aaaSet среды разработки на toowork Mac OS X с Azure Service Fabric | Документы Microsoft"
description: "Установка среды выполнения hello, пакета SDK и средств и создайте кластер локальной разработки. После завершения этой установки, будет готов toobuild приложений на Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Настройка среды разработки для Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Можно создать toorun приложения Service Fabric для кластеров Linux с помощью Mac OS X. В этой статье рассматриваются как tooset копирование Mac для разработки.

## <a name="prerequisites"></a>Предварительные требования
Service Fabric не запускать на OS X. toorun локального кластера Service Fabric, мы предоставляем предварительно настроенных Ubuntu виртуальную машину, используя Vagrant и VirtualBox. Перед началом работы вам потребуются:

* [Vagrant (1.8.4 или более поздней версии)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Необходимо toouse взаимно поддерживаемые версии Vagrant и VirtualBox. Vagrant может работать с ошибками в неподдерживаемой версии VirtualBox.
>

## <a name="create-hello-local-vm"></a>Создание hello локальной виртуальной Машины
toocreate hello локальной виртуальной Машины, содержащий 5 узлами кластера Service Fabric, выполните следующие шаги hello.

1. Клон hello `Vagrantfile` репозитория

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Перевести этот шаг пребывания hello файл `Vagrantfile` содержащий hello ВМ конфигурации вместе с hello hello расположение виртуальной Машины загружается с.

2. Перейдите toohello локальной копией hello репозитория

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Необязательно) Измените параметры виртуальной Машины по умолчанию hello

    По умолчанию hello локальной виртуальной Машины настраивается следующим образом:

   * 3 ГБ выделенной памяти;
   * Закрытый узла сети, настроенной с IP-адресом 192.168.50.50 Включение транзитная пересылка трафика от узла Mac hello

     Можно изменить эти параметры или добавить другие toohello конфигурации виртуальной Машины в hello `Vagrantfile`. В разделе hello [Vagrant документации](http://www.vagrantup.com/docs) для hello полный список параметров конфигурации.
4. Создание виртуальной Машины hello

    ```bash
    vagrant up
    ```

   На этом шаге загружается образ виртуальной Машины предварительно настроен hello, загрузки его локально, а затем настройте локальный Service Fabric кластера в нем. Следует ожидать его tootake через несколько минут. Если программа установки завершается успешно, появляется в выходных данных hello, которое указывает, выполняется запуск этого кластера hello.

    ![Начало установки кластера после подготовки виртуальной машины][cluster-setup-script]

    >[!TIP]
    > Если hello загрузки виртуальной Машины занимает много времени, его можно загрузить с помощью wget или перелистывания или через браузер, перейдя по toohello связи, заданные **config.vm.box_url** в файле hello `Vagrantfile`. После загрузки локально, изменить `Vagrantfile` toopoint toohello локальный путь, куда вы загрузили hello изображения. Для примера Если вы загрузили too/home/users/test/azureservicefabric.tp8.box изображения hello, затем задайте **config.vm.box_url** toothat пути.
    >

5. Тестирование этого hello кластер настроен правильно, перейдя по tooService Fabric Explorer в http://192.168.50.50:19080-обозревателе (если хранить IP частной сети по умолчанию hello).

    ![Просмотреть в узле hello Mac обозреватель Service Fabric][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Создание приложения на компьютере Mac с помощью Yeoman
Service Fabric предоставляет средства формирования шаблонов, которые позволяют создать приложение Service Fabric из терминала с помощью генератора шаблонов Yeoman. Выполните шаги hello ниже tooensure, у вас есть hello Service Fabric yeoman шаблона генератор работает на компьютере.

1. Требуется toohave Node.js и NPM, которые установлены на mac вы. В противном случае можно установить Node.js и NPM, с помощью Homebrew, с помощью следующих hello. toocheck hello версиях Node.js и NPM, которые установлены на компьютере Mac, можно использовать hello ``-v`` параметр.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.

  ```bash
  npm install -g yo
  ```
3. Установка hello Yeoman генератор требуется toouse, шагов hello в hello Приступая к работе [документации](service-fabric-get-started-linux.md). toocreate службы фабрики приложений с помощью Yeoman, выполните действия hello-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild приложения Java структуры службы на Mac потребуется - JDK 1.8 и Gradle, установленных на компьютере hello.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Установите подключаемый модуль hello Service Fabric для Eclipse Neon

Service Fabric предоставляет подключаемого модуля для hello **Neon Eclipse для интегрированной среды разработки Java** , которые могут упростить процесс создания, построения и развертывания службы Java hello. Выполните действия установки hello, упомянутые в этом общем [документации](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) об установке или обновлении подключаемого модуля Eclipse структуры службы.

>[!TIP]
> По умолчанию мы поддерживаем IP по умолчанию hello, как упоминалось в hello ``Vagrantfile`` в hello ``Local.json`` приложения hello создан. В случае изменения, а развертывание Vagrant с другого IP-адреса, выполните обновление hello соответствующий IP-адрес в ``Local.json`` также вашего приложения.

## <a name="next-steps"></a>Дальнейшие действия
<!-- Links -->
* [Создание первого приложения Azure Service Fabric](service-fabric-create-your-first-linux-application-with-java.md)
* [Getting started with Eclipse Plugin for Service Fabric Java application development](service-fabric-get-started-eclipse.md) (Начало работы с подключаемым модулем Eclipse для разработки приложения Service Fabric на Java)
* [Создание кластера Service Fabric в hello портал Azure](service-fabric-cluster-creation-via-portal.md)
* [Создание кластера Service Fabric hello с помощью диспетчера ресурсов Azure](service-fabric-cluster-creation-via-arm.md)
* [Понять модель приложения hello Service Fabric](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
