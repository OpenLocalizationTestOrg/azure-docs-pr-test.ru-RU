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
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="2a46c-104">Подготовка среды разработки в Linux</span><span class="sxs-lookup"><span data-stu-id="2a46c-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a46c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="2a46c-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="2a46c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="2a46c-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="2a46c-107">OSX</span><span class="sxs-lookup"><span data-stu-id="2a46c-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="2a46c-108">toodeploy и запустите [приложения Azure Service Fabric](service-fabric-application-model.md) на компьютере разработки Linux установке среды выполнения hello и общие пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="2a46c-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="2a46c-109">Вы также можете установить дополнительные пакеты SDK для Java и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2a46c-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a46c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2a46c-110">Prerequisites</span></span>

<span data-ttu-id="2a46c-111">для разработки поддерживаются Hello следующих версий операционной системы:</span><span class="sxs-lookup"><span data-stu-id="2a46c-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="2a46c-112">Ubuntu 16.04 (`Xenial Xerus`).</span><span class="sxs-lookup"><span data-stu-id="2a46c-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="2a46c-113">Обновление списка источников APT</span><span class="sxs-lookup"><span data-stu-id="2a46c-113">Update your APT sources</span></span>
<span data-ttu-id="2a46c-114">tooinstall hello SDK и hello связанного пакета среды выполнения через программу командной строки hello apt get, необходимо сначала обновить источникам дополнительные средства упаковки (APT).</span><span class="sxs-lookup"><span data-stu-id="2a46c-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="2a46c-115">Откройте окно терминала.</span><span class="sxs-lookup"><span data-stu-id="2a46c-115">Open a terminal.</span></span>
2. <span data-ttu-id="2a46c-116">Добавьте список источников tooyour репозитория Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="2a46c-117">Добавить hello `dotnet` список источников tooyour репозитория.</span><span class="sxs-lookup"><span data-stu-id="2a46c-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="2a46c-118">Добавить hello tooyour APT keyring ключа новую защитную конфиденциальности Gnu (GnuPG или GPG).</span><span class="sxs-lookup"><span data-stu-id="2a46c-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="2a46c-119">Добавьте hello официальный Docker GPG ключа tooyour APT keyring.</span><span class="sxs-lookup"><span data-stu-id="2a46c-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="2a46c-120">Настройки хранилища Docker hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="2a46c-121">Обновление пакета списках на основании hello вновь добавлен репозиториев.</span><span class="sxs-lookup"><span data-stu-id="2a46c-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="2a46c-122">Установка и настройка hello пакета SDK для установки локального кластера</span><span class="sxs-lookup"><span data-stu-id="2a46c-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="2a46c-123">После обновления исходных файлов, можно установить пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="2a46c-124">Установите пакет Service Fabric SDK hello, подтверждение установки hello и соглашаетесь toohello лицензионное соглашение.</span><span class="sxs-lookup"><span data-stu-id="2a46c-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="2a46c-125">Hello следующие команды автоматизировать принимающая hello лицензии для Service Fabric пакетов:</span><span class="sxs-lookup"><span data-stu-id="2a46c-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="2a46c-126">Настройка локального кластера</span><span class="sxs-lookup"><span data-stu-id="2a46c-126">Set up a local cluster</span></span>
  <span data-ttu-id="2a46c-127">Если hello Установка выполнена успешно, можно будет toostart локального кластера.</span><span class="sxs-lookup"><span data-stu-id="2a46c-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="2a46c-128">Запустите сценарий установки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="2a46c-129">Откройте веб-браузер и перейдите в слишком[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="2a46c-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="2a46c-130">Если hello кластер запущен, вы увидите панель мониторинга Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Обозреватель Service Fabric Explorer в Linux][sfx-linux]

  <span data-ttu-id="2a46c-132">На этом этапе можно развертывать готовые пакеты приложений Service Fabric или новые приложения на базе гостевых контейнеров или гостевых исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="2a46c-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="2a46c-133">toobuild новых служб с помощью hello Java или пакетами SDK .NET Core, выполните действия установки дополнительных hello, которые приведены в последующих разделах.</span><span class="sxs-lookup"><span data-stu-id="2a46c-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="2a46c-134">Автономные кластеры не поддерживаются в Linux.</span><span class="sxs-lookup"><span data-stu-id="2a46c-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="2a46c-135">Hello Предварительная версия поддерживает только одно поле и несколькими компьютерами кластеры Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="2a46c-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="2a46c-136">Настройка службы структуры CLI hello</span><span class="sxs-lookup"><span data-stu-id="2a46c-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="2a46c-137">Hello [службы структуры CLI](service-fabric-cli.md) содержит команды для взаимодействия с сущностями Service Fabric, включая кластеров и приложения.</span><span class="sxs-lookup"><span data-stu-id="2a46c-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="2a46c-138">Он основан на python, поэтому следует убедиться, что toohave python и шагов установки, прежде чем продолжить hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2a46c-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="2a46c-139">Установка и настройка генераторы hello для контейнеров и исполняемые файлы гостя</span><span class="sxs-lookup"><span data-stu-id="2a46c-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="2a46c-140">Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Service Fabric из терминала с помощью генератора шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="2a46c-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="2a46c-141">Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для работы на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2a46c-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="2a46c-142">Установите Node.js и NPM на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2a46c-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="2a46c-143">Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.</span><span class="sxs-lookup"><span data-stu-id="2a46c-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="2a46c-144">Установка генератор контейнера hello Yeo структуры службы и генератор execuatble гостевой из NPM</span><span class="sxs-lookup"><span data-stu-id="2a46c-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="2a46c-145">После установки hello выше генераторы должно быть возможности toocreate приложений с помощью гостевых служб исполняемого файла или контейнера, запустив `yo azuresfguest` или `yo azuresfcontainer` соответственно.</span><span class="sxs-lookup"><span data-stu-id="2a46c-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="2a46c-146">Установка hello необходимые Java артефакты (необязательный параметр, если требуется toouse hello Java модели программирования)</span><span class="sxs-lookup"><span data-stu-id="2a46c-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="2a46c-147">службы toobuild Service Fabric, с помощью Java, убедитесь, что установлена 1.8 JDK установлен вместе с Gradle, который используется для выполнения задачи построения.</span><span class="sxs-lookup"><span data-stu-id="2a46c-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="2a46c-148">Следующий фрагмент кода Hello устанавливает Open JDK 1.8 вместе с Gradle.</span><span class="sxs-lookup"><span data-stu-id="2a46c-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="2a46c-149">библиотеки службы структуры Java Hello извлекаются из Maven.</span><span class="sxs-lookup"><span data-stu-id="2a46c-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="2a46c-150">Установка hello Eclipse Neon подключаемого модуля (необязательно)</span><span class="sxs-lookup"><span data-stu-id="2a46c-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="2a46c-151">Можно установить подключаемый модуль Eclipse hello для структуры службы из внутри hello **интегрированной среды разработки Eclipse для разработчиков Java**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="2a46c-152">Eclipse toocreate Service Fabric гостевой исполняемый файл приложения и приложения контейнера можно использовать в приложениях Java структуры tooService сложения.</span><span class="sxs-lookup"><span data-stu-id="2a46c-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="2a46c-153">В Eclipse, убедитесь, что у последней Neon Eclipse и hello последнюю версию Buildship (1.0.17 или более поздней версии) установлен.</span><span class="sxs-lookup"><span data-stu-id="2a46c-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="2a46c-154">Для проверки версии установленных компонентов hello выберите **справки** > **сведения об установке**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="2a46c-155">Можно обновить с помощью инструкций hello в Buildship [Eclipse Buildship: подключаемые модули Eclipse для Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="2a46c-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="2a46c-156">tooinstall hello Service Fabric подключаемый модуль, выберите **справки** > **Установка нового программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="2a46c-157">В hello **работать с** введите **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="2a46c-158">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-158">Click **Add**.</span></span>

    ![Страница приветствия доступного программного обеспечения][sf-eclipse-plugin]

5. <span data-ttu-id="2a46c-160">Выберите hello **ServiceFabric** подключаемый модуль, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="2a46c-161">Выполните шаги установки hello и примите лицензионное соглашение hello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="2a46c-162">Если уже имеется hello подключаемого модуля Eclipse структуры службы установлены, убедитесь, что имеется hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="2a46c-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="2a46c-163">Можно проверить, выбрав **справки** > **сведения об установке** и затем найти Service Fabric в hello список модулей. Выберите **обновление**, если доступна более новая версия.</span><span class="sxs-lookup"><span data-stu-id="2a46c-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="2a46c-164">Дополнительные сведения см. в статье [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="2a46c-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="2a46c-165">Установка hello .NET Core SDK (не обязательно, если требуется, чтобы в модели программирования .NET Core hello toouse)</span><span class="sxs-lookup"><span data-stu-id="2a46c-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="2a46c-166">Hello .NET Core SDK предоставляет библиотеки hello и шаблоны, которые находятся служб Service Fabric требуется toobuild с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2a46c-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="2a46c-167">Установка пакета SDK для .NET Core hello путем выполнения следующих hello-</span><span class="sxs-lookup"><span data-stu-id="2a46c-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="2a46c-168">Обновление hello SDK и среды выполнения</span><span class="sxs-lookup"><span data-stu-id="2a46c-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="2a46c-169">tooupdate toohello последнюю версию пакета SDK для hello и среды выполнения, запустите следующие команды hello (отмените выбор hello пакетов SDK, которые не требуется):</span><span class="sxs-lookup"><span data-stu-id="2a46c-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="2a46c-170">tooupdate hello Java SDK двоичных файлов Maven, необходимые сведения о версии tooupdate hello hello соответствующего двоичного файла в hello ``build.gradle`` последнюю версию файла toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="2a46c-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="2a46c-171">tooknow точно которых требуется версия tooupdate hello, можно ссылаться tooany ``build.gradle`` файл выборок, Приступая к работе Service Fabric [здесь](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2a46c-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="2a46c-172">Обновление hello пакетов может вызвать под управлением кластера toostop вашей локальной разработки система.</span><span class="sxs-lookup"><span data-stu-id="2a46c-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="2a46c-173">Перезапустите локальный кластер после обновления по инструкциям hello на этой странице.</span><span class="sxs-lookup"><span data-stu-id="2a46c-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a46c-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a46c-174">Next steps</span></span>

* [<span data-ttu-id="2a46c-175">Создание первого Java-приложения Service Fabric в Linux</span><span class="sxs-lookup"><span data-stu-id="2a46c-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="2a46c-176">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="2a46c-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="2a46c-177">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2a46c-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="2a46c-178">Настройка среды разработки для Mac OS X</span><span class="sxs-lookup"><span data-stu-id="2a46c-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="2a46c-179">Использовать toomanage hello CLI структуры службы приложения</span><span class="sxs-lookup"><span data-stu-id="2a46c-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="2a46c-180">Различия между Service Fabric для Linux (предварительная версия) и Windows (общедоступная версия)</span><span class="sxs-lookup"><span data-stu-id="2a46c-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* <span data-ttu-id="2a46c-181">[Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="2a46c-181">[Get started with Service Fabric CLI](service-fabric-cli.md)</span></span>

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
