---
title: "hello aaaUsing расширение ВМ Docker для Linux в Azure"
description: "Описывает Docker и расширения виртуальных машин Azure hello и показано, как tooprogrammatically создать виртуальные машины в Azure, которые узлы docker из командной строки hello, с помощью hello Azure CLI."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="81db9-103">С помощью hello расширение ВМ Docker из hello Azure командной строки (CLI Azure)</span><span class="sxs-lookup"><span data-stu-id="81db9-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="81db9-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="81db9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="81db9-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="81db9-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="81db9-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81db9-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="81db9-107">Сведения об использовании hello расширение ВМ Docker с моделью hello диспетчера ресурсов см. в разделе [здесь](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81db9-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="81db9-108">Описывается, как toocreate виртуальную Машину с hello расширение ВМ Docker из hello службы режим управления (asm) в Azure CLI на любой платформе.</span><span class="sxs-lookup"><span data-stu-id="81db9-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="81db9-109">[Docker](https://www.docker.com/) является одним из hello наиболее популярных виртуализации подходов, которые использует [контейнеров Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ разделения данных и вычисления на общих ресурсах.</span><span class="sxs-lookup"><span data-stu-id="81db9-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="81db9-110">Можно использовать расширение ВМ Docker hello и hello [агент Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate виртуальной Машины Docker, на котором размещена любое число контейнеров для приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="81db9-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="81db9-111">toosee общие обсуждения контейнеров и их преимущества, в разделе hello [Docker высокий уровень доски](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="81db9-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="81db9-112">Как toouse hello расширение ВМ Docker с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="81db9-113">расширение виртуальной Машины Docker hello toouse с Azure, необходимо установить версию hello [интерфейса командной строки Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) выше, чем 0.8.6 (как для этой записи hello текущей версии 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="81db9-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="81db9-114">Hello Azure CLI можно установить на Mac, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="81db9-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="81db9-115">Hello полный процесс toouse Docker в Azure очень простой:</span><span class="sxs-lookup"><span data-stu-id="81db9-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="81db9-116">Установите на компьютере hello, из которого нужно toocontrol Azure hello Azure CLI и его зависимости (в Windows, это будет дистрибутив Linux, выполняющийся как виртуальная машина)</span><span class="sxs-lookup"><span data-stu-id="81db9-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="81db9-117">Использовать toocreate команды Azure CLI Docker hello узла виртуальной Машины Docker в Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="81db9-118">Используйте hello локального Docker команды toomanage в контейнеры Docker в ВМ Docker в Azure.</span><span class="sxs-lookup"><span data-stu-id="81db9-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="81db9-119">Установка hello Azure командной строки (CLI Azure)</span><span class="sxs-lookup"><span data-stu-id="81db9-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="81db9-120">tooinstall и настроить hello Azure CLI см. в разделе [как tooinstall hello интерфейса командной строки Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="81db9-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="81db9-121">Установка tooconfirm hello, тип `azure` hello командной строки и через некоторое короткое время вы увидите доступные tooyou команды hello Azure CLI ASCII-графики, который содержит список hello basic.</span><span class="sxs-lookup"><span data-stu-id="81db9-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="81db9-122">Если установки hello работал правильно, можно будет tootype `azure help vm` и увидеть, что одной из команд hello в списке «docker».</span><span class="sxs-lookup"><span data-stu-id="81db9-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="81db9-123">Docker содержит средства для Windows, [машины Docker](https://docs.docker.com/installation/windows/), который можно также использовать tooautomate hello создание клиента docker, можно использовать toowork с виртуальными машинами Azure в качестве узлов docker.</span><span class="sxs-lookup"><span data-stu-id="81db9-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="81db9-124">Подключение hello Azure CLI tootooyour учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="81db9-125">Прежде чем использовать hello Azure CLI необходимо связать учетные данные учетной записи Azure с hello Azure CLI для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="81db9-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="81db9-126">Здравствуйте, раздел [как tooconnect tooyour подписки Azure](../../../xplat-cli-connect.md) объясняет, как загрузить и импортировать tooeither вашей **.publishsettings** файл или связать с ИД организации в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="81db9-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="81db9-127">Существуют некоторые отличия в поведении при использовании одной или hello других методов проверки подлинности, следует убедиться, что документ hello tooread выше toounderstand hello различаются по функциональности.</span><span class="sxs-lookup"><span data-stu-id="81db9-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="81db9-128">Установка Docker и использовать расширение ВМ Docker hello Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="81db9-129">Выполните hello [инструкции по установке Docker](https://docs.docker.com/installation/#installation) tooinstall Docker на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="81db9-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="81db9-130">toouse Docker с виртуальной машины Azure hello Linux изображение, используемое для hello виртуальной Машины должен иметь hello [агент ВМ Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) установлен.</span><span class="sxs-lookup"><span data-stu-id="81db9-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="81db9-131">В настоящее время это обеспечивается только двумя типами образов:</span><span class="sxs-lookup"><span data-stu-id="81db9-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="81db9-132">Ubuntu образ из коллекции образов Azure hello или</span><span class="sxs-lookup"><span data-stu-id="81db9-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="81db9-133">Настраиваемое изображение Linux, созданного с помощью hello агента ВМ Azure Linux установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="81db9-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="81db9-134">В разделе [агент ВМ Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Дополнительные сведения о том, как toobuild пользовательские виртуальной Машины Linux с hello агента ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="81db9-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="81db9-135">С помощью коллекции образов Azure hello</span><span class="sxs-lookup"><span data-stu-id="81db9-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="81db9-136">В Bash или сеанс используйте следующую команду Azure CLI toolocate hello самый последний Ubuntu образ в коллекции toouse hello виртуальной Машины, введя hello</span><span class="sxs-lookup"><span data-stu-id="81db9-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="81db9-137">и выберите одно из имен изображения hello, такие как `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, и используйте hello следующая команда toocreate новой виртуальной Машины с помощью данного образа.</span><span class="sxs-lookup"><span data-stu-id="81db9-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="81db9-138">Описание:</span><span class="sxs-lookup"><span data-stu-id="81db9-138">where:</span></span>

* <span data-ttu-id="81db9-139">*&lt;имя виртуальной машины cloudservice&gt;*  — имя hello hello виртуальной Машины, которая станет hello компьютер указанный контейнер Docker в Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="81db9-140">*&lt;имя пользователя&gt;*  пользователя hello корневого пользователя по умолчанию hello hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="81db9-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="81db9-141">*&lt;пароль&gt;*  — пароль hello hello *username* учетную запись, которая соответствует стандартам hello сложности для Azure</span><span class="sxs-lookup"><span data-stu-id="81db9-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="81db9-142">В настоящее время пароль должен быть по крайней мере 8 символов, содержать одной прописной и одну прописную букву, число и специальный символ, такой как один из hello следующие символы: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="81db9-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="81db9-143">Нет, период hello в конце hello hello предшествующий предложения не специальный символ.</span><span class="sxs-lookup"><span data-stu-id="81db9-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="81db9-144">При успешном выполнении команды hello, вы увидите нечто похожее на следующее hello, в зависимости от hello точные аргументы и параметры, которые вы использовали:</span><span class="sxs-lookup"><span data-stu-id="81db9-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="81db9-145">Создание виртуальной машины может занять несколько минут, но после того, как он был инициализирован (значение hello `ReadyRole`) hello запуска управляющей программы (hello службу Docker) Docker, можно подключить toohello узла контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="81db9-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="81db9-146">hello tootest Docker виртуальных Машин, созданных в Azure, тип</span><span class="sxs-lookup"><span data-stu-id="81db9-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="81db9-147">где  *&lt;vm-name--использовалась&gt;*  является именем hello hello виртуальной машины, который использовался при вызове слишком`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="81db9-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="81db9-148">Вы увидите, что-нибудь подобное toohello следующее, что указывает, что узел Docker ВМ работает в Azure и ожидания команды.</span><span class="sxs-lookup"><span data-stu-id="81db9-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="81db9-149">Теперь можно попробовать tooconnect использует информацию tooobtain клиента docker (в некоторых настроек клиента Docker, например, на Mac, может возникнуть toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="81db9-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="81db9-150">Просто toobe убедиться, что все работы, можно изучить hello виртуальной Машины для hello расширения Docker:</span><span class="sxs-lookup"><span data-stu-id="81db9-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="81db9-151">Проверка подлинности виртуальной машины узла Docker</span><span class="sxs-lookup"><span data-stu-id="81db9-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="81db9-152">Кроме hello hello toocreating ВМ Docker `azure vm docker create` команда также автоматически создает необходимые сертификаты tooallow hello клиентского компьютера tooconnect toohello контейнер Azure узла Docker с помощью протокола HTTPS и hello сертификаты хранятся на обоих Hello клиентского и главного компьютеров соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="81db9-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="81db9-153">При последующих попытках существующих сертификатов hello повторно и совместно с новым узлом hello.</span><span class="sxs-lookup"><span data-stu-id="81db9-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="81db9-154">По умолчанию сертификаты помещаются в `~/.docker`, и Docker будут toorun настроенный порт **2376**.</span><span class="sxs-lookup"><span data-stu-id="81db9-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="81db9-155">Если вы хотите toouse другой порт или каталог, то можно использовать один из следующих hello `azure vm docker create` tooconfigure параметры командной строки к Docker контейнера узла виртуальной Машины toouse другой порт или разные сертификаты при подключении клиентов:</span><span class="sxs-lookup"><span data-stu-id="81db9-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="81db9-156">Hello управляющая программа Docker на узле hello является настроенным toolisten для и пройти проверку подлинности клиентских подключений на hello указанный порт, используя hello сертификаты, созданные hello `azure vm docker create` команды.</span><span class="sxs-lookup"><span data-stu-id="81db9-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="81db9-157">Hello клиентский компьютер должен иметь эти сертификаты toogain доступа toohello Docker узла.</span><span class="sxs-lookup"><span data-stu-id="81db9-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="81db9-158">Узел сети, работающих без эти сертификаты будут уязвимыми tooanyone, можно tooconnect toohello машины.</span><span class="sxs-lookup"><span data-stu-id="81db9-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="81db9-159">Перед изменением конфигурации по умолчанию hello, убедитесь, что вы понимаете hello рисков tooyour компьютеры и приложения.</span><span class="sxs-lookup"><span data-stu-id="81db9-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81db9-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81db9-160">Next steps</span></span>
* <span data-ttu-id="81db9-161">Будут готовы toogo toohello [руководство пользователя по Docker] и использовать ВМ Docker.</span><span class="sxs-lookup"><span data-stu-id="81db9-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="81db9-162">. в разделе toocreate поддержкой Docker виртуальной Машины в новый портал hello, [как toouse hello расширение ВМ Docker с hello портала].</span><span class="sxs-lookup"><span data-stu-id="81db9-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="81db9-163">Hello расширение ВМ Docker Azure также поддерживает Docker Compose, использующий декларативный tootake файл YAML приложении моделируется разработчика любой среде и создания согласованного развертывания.</span><span class="sxs-lookup"><span data-stu-id="81db9-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="81db9-164">В разделе [начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure].</span><span class="sxs-lookup"><span data-stu-id="81db9-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[как toouse hello расширение ВМ Docker с hello портала]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[руководство пользователя по Docker]:https://docs.docker.com/userguide/

[начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure]:../docker-compose-quickstart.md
