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
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="664ca-104">Настройка среды разработки для Mac OS X</span><span class="sxs-lookup"><span data-stu-id="664ca-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="664ca-105">Windows</span><span class="sxs-lookup"><span data-stu-id="664ca-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="664ca-106">Linux</span><span class="sxs-lookup"><span data-stu-id="664ca-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="664ca-107">OSX</span><span class="sxs-lookup"><span data-stu-id="664ca-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="664ca-108">Можно создать toorun приложения Service Fabric для кластеров Linux с помощью Mac OS X. В этой статье рассматриваются как tooset копирование Mac для разработки.</span><span class="sxs-lookup"><span data-stu-id="664ca-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="664ca-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="664ca-109">Prerequisites</span></span>
<span data-ttu-id="664ca-110">Service Fabric не запускать на OS X. toorun локального кластера Service Fabric, мы предоставляем предварительно настроенных Ubuntu виртуальную машину, используя Vagrant и VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="664ca-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="664ca-111">Перед началом работы вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="664ca-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="664ca-112">Vagrant (1.8.4 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="664ca-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="664ca-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="664ca-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="664ca-114">Необходимо toouse взаимно поддерживаемые версии Vagrant и VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="664ca-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="664ca-115">Vagrant может работать с ошибками в неподдерживаемой версии VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="664ca-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="664ca-116">Создание hello локальной виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="664ca-116">Create hello local VM</span></span>
<span data-ttu-id="664ca-117">toocreate hello локальной виртуальной Машины, содержащий 5 узлами кластера Service Fabric, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="664ca-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="664ca-118">Клон hello `Vagrantfile` репозитория</span><span class="sxs-lookup"><span data-stu-id="664ca-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="664ca-119">Перевести этот шаг пребывания hello файл `Vagrantfile` содержащий hello ВМ конфигурации вместе с hello hello расположение виртуальной Машины загружается с.</span><span class="sxs-lookup"><span data-stu-id="664ca-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="664ca-120">Перейдите toohello локальной копией hello репозитория</span><span class="sxs-lookup"><span data-stu-id="664ca-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="664ca-121">(Необязательно) Измените параметры виртуальной Машины по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="664ca-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="664ca-122">По умолчанию hello локальной виртуальной Машины настраивается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="664ca-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="664ca-123">3 ГБ выделенной памяти;</span><span class="sxs-lookup"><span data-stu-id="664ca-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="664ca-124">Закрытый узла сети, настроенной с IP-адресом 192.168.50.50 Включение транзитная пересылка трафика от узла Mac hello</span><span class="sxs-lookup"><span data-stu-id="664ca-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="664ca-125">Можно изменить эти параметры или добавить другие toohello конфигурации виртуальной Машины в hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="664ca-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="664ca-126">В разделе hello [Vagrant документации](http://www.vagrantup.com/docs) для hello полный список параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="664ca-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="664ca-127">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="664ca-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="664ca-128">На этом шаге загружается образ виртуальной Машины предварительно настроен hello, загрузки его локально, а затем настройте локальный Service Fabric кластера в нем.</span><span class="sxs-lookup"><span data-stu-id="664ca-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="664ca-129">Следует ожидать его tootake через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="664ca-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="664ca-130">Если программа установки завершается успешно, появляется в выходных данных hello, которое указывает, выполняется запуск этого кластера hello.</span><span class="sxs-lookup"><span data-stu-id="664ca-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![Начало установки кластера после подготовки виртуальной машины][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="664ca-132">Если hello загрузки виртуальной Машины занимает много времени, его можно загрузить с помощью wget или перелистывания или через браузер, перейдя по toohello связи, заданные **config.vm.box_url** в файле hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="664ca-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="664ca-133">После загрузки локально, изменить `Vagrantfile` toopoint toohello локальный путь, куда вы загрузили hello изображения.</span><span class="sxs-lookup"><span data-stu-id="664ca-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="664ca-134">Для примера Если вы загрузили too/home/users/test/azureservicefabric.tp8.box изображения hello, затем задайте **config.vm.box_url** toothat пути.</span><span class="sxs-lookup"><span data-stu-id="664ca-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="664ca-135">Тестирование этого hello кластер настроен правильно, перейдя по tooService Fabric Explorer в http://192.168.50.50:19080-обозревателе (если хранить IP частной сети по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="664ca-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Просмотреть в узле hello Mac обозреватель Service Fabric][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="664ca-137">Создание приложения на компьютере Mac с помощью Yeoman</span><span class="sxs-lookup"><span data-stu-id="664ca-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="664ca-138">Service Fabric предоставляет средства формирования шаблонов, которые позволяют создать приложение Service Fabric из терминала с помощью генератора шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="664ca-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="664ca-139">Выполните шаги hello ниже tooensure, у вас есть hello Service Fabric yeoman шаблона генератор работает на компьютере.</span><span class="sxs-lookup"><span data-stu-id="664ca-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="664ca-140">Требуется toohave Node.js и NPM, которые установлены на mac вы.</span><span class="sxs-lookup"><span data-stu-id="664ca-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="664ca-141">В противном случае можно установить Node.js и NPM, с помощью Homebrew, с помощью следующих hello.</span><span class="sxs-lookup"><span data-stu-id="664ca-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="664ca-142">toocheck hello версиях Node.js и NPM, которые установлены на компьютере Mac, можно использовать hello ``-v`` параметр.</span><span class="sxs-lookup"><span data-stu-id="664ca-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="664ca-143">Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.</span><span class="sxs-lookup"><span data-stu-id="664ca-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="664ca-144">Установка hello Yeoman генератор требуется toouse, шагов hello в hello Приступая к работе [документации](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="664ca-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="664ca-145">toocreate службы фабрики приложений с помощью Yeoman, выполните действия hello-</span><span class="sxs-lookup"><span data-stu-id="664ca-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="664ca-146">toobuild приложения Java структуры службы на Mac потребуется - JDK 1.8 и Gradle, установленных на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="664ca-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="664ca-147">Установите подключаемый модуль hello Service Fabric для Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="664ca-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="664ca-148">Service Fabric предоставляет подключаемого модуля для hello **Neon Eclipse для интегрированной среды разработки Java** , которые могут упростить процесс создания, построения и развертывания службы Java hello.</span><span class="sxs-lookup"><span data-stu-id="664ca-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="664ca-149">Выполните действия установки hello, упомянутые в этом общем [документации](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) об установке или обновлении подключаемого модуля Eclipse структуры службы.</span><span class="sxs-lookup"><span data-stu-id="664ca-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="664ca-150">По умолчанию мы поддерживаем IP по умолчанию hello, как упоминалось в hello ``Vagrantfile`` в hello ``Local.json`` приложения hello создан.</span><span class="sxs-lookup"><span data-stu-id="664ca-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="664ca-151">В случае изменения, а развертывание Vagrant с другого IP-адреса, выполните обновление hello соответствующий IP-адрес в ``Local.json`` также вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="664ca-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="664ca-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="664ca-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="664ca-153">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="664ca-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="664ca-154">[Getting started with Eclipse Plugin for Service Fabric Java application development](service-fabric-get-started-eclipse.md) (Начало работы с подключаемым модулем Eclipse для разработки приложения Service Fabric на Java)</span><span class="sxs-lookup"><span data-stu-id="664ca-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="664ca-155">Создание кластера Service Fabric в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="664ca-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="664ca-156">Создание кластера Service Fabric hello с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="664ca-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="664ca-157">Понять модель приложения hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="664ca-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
