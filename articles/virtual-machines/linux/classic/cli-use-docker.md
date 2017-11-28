---
title: "Использование расширения виртуальных машин Docker для Linux на Azure"
description: "Описание механизма Docker и расширений Виртуальных машин Azure, а также программного создания виртуальных машин в Azure как узлов Docker с помощью интерфейса CLI Azure."
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
ms.openlocfilehash: a542332c921862241f1f000e6a8f0a0ae0e8a934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="7a3b8-103">Использование расширения виртуальных машин Docker в интерфейсе командной строки Azure (CLI Azure)</span><span class="sxs-lookup"><span data-stu-id="7a3b8-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7a3b8-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7a3b8-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7a3b8-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7a3b8-107">Дополнительные сведения об использовании расширения виртуальной машины Docker с моделью Resource Manager см. [здесь](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7a3b8-108">В этой статье показано, как создать виртуальную машину с расширением виртуальных машин Docker в режиме управления службами (asm) в интерфейсе командной строки Azure на любой платформе.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="7a3b8-109">[Docker](https://www.docker.com/) — один из самых популярных подходов к виртуализации, использующий [контейнеры Linux](http://en.wikipedia.org/wiki/LXC) вместо виртуальных машин как способ изоляции данных и вычислений при использовании общих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="7a3b8-110">Можно использовать расширение виртуальной машины Docker и [агент Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) для создания виртуальной машины Docker, в которой можно разместить любое количество контейнеров для приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="7a3b8-111">Обзорное обсуждение контейнеров и их преимуществ см. на [доске по Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="7a3b8-112">Использование расширения виртуальных машин Docker в Azure</span><span class="sxs-lookup"><span data-stu-id="7a3b8-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="7a3b8-113">Чтобы использовать расширения виртуальных машин Docker в Azure, необходимо установить версию [интерфейса командной строки Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) более позднюю, чем 0.8.6 (на момент написания статьи текущей версией является 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="7a3b8-114">Вы можете установить CLI Azure на компьютерах под управлением Mac, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="7a3b8-115">Процесс использования Docker в Azure прост.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="7a3b8-116">Установите CLI Azure и его зависимости на компьютере, с которого вы хотите управлять Azure (в случае Windows это будет дистрибутив Linux, запущенный в виде виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="7a3b8-117">Используйте команды Docker в CLI Azure, чтобы создать узел виртуальных машин Docker в Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="7a3b8-118">Используйте команды локального Docker для управления своим контейнерами на узле виртуальных машин Docker в Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="7a3b8-119">Установка интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="7a3b8-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="7a3b8-120">Сведения об установке и настройке интерфейса командной строки Azure см. в статье [Установка Azure CLI](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="7a3b8-121">Чтобы подтвердить установку, введите `azure` в командной строке, и через некоторое время отобразится рисунок ASCII интерфейса командной строки Azure, в котором перечислены основные доступные вам команды.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="7a3b8-122">Если установка прошла без ошибок, вы можете ввести `azure help vm` и увидеть в списке команд docker.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="7a3b8-123">В Docker имеются инструменты для Windows, [Docker Machine](https://docs.docker.com/installation/windows/), позволяющие также автоматизировать создание клиента Docker, который можно использовать для работы с виртуальными машинами Azure в качестве узлов Docker.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="7a3b8-124">Подключение CLI Azure к учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="7a3b8-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="7a3b8-125">Чтобы вы смогли использовать CLI Azure, свяжите учетные данные учетной записи Azure с CLI Azure для вашей платформы.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="7a3b8-126">В разделе [Подключение к подписке Azure](../../../xplat-cli-connect.md) описано, как скачать и импортировать **PUBLISHSETTINGS** -файл либо связать интерфейс командной строки Azure с идентификатором организации.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3b8-127">Есть некоторые различия в действиях при использовании первого или второго способа аутентификации, так что не забудьте прочитать вышеуказанный документ, чтобы понять различие в функциональности.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="7a3b8-128">Установка Docker и использование расширения виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="7a3b8-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="7a3b8-129">Следуйте [инструкции по установке Docker](https://docs.docker.com/installation/#installation) для того, чтобы установить Docker локально на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="7a3b8-130">Для использования Docker на виртуальной машине Azure в образе Linux, который используется для нее, необходимо установить [агент виртуальных машин Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="7a3b8-131">В настоящее время это обеспечивается только двумя типами образов:</span><span class="sxs-lookup"><span data-stu-id="7a3b8-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="7a3b8-132">образ Ubuntu из коллекции образов Azure или</span><span class="sxs-lookup"><span data-stu-id="7a3b8-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="7a3b8-133">пользовательский образ Linux, созданный вами, с установленным и настроенным агентом виртуальных машин Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="7a3b8-134">Дополнительные сведения о создании собственной виртуальной машины с агентом Azure см. в [руководстве пользователя агента Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a3b8-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="7a3b8-135">Использование коллекции образов Azure</span><span class="sxs-lookup"><span data-stu-id="7a3b8-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="7a3b8-136">В сеансе Bash или сеансе терминала используйте команду</span><span class="sxs-lookup"><span data-stu-id="7a3b8-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="7a3b8-137">в интерфейсе командной строки Azure для поиска последнего образа Ubuntu в коллекции виртуальных машин, выберите одно из имен образов, например `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, и используйте указанную ниже команду для создания виртуальной машины с помощью этого образа.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="7a3b8-138">где:</span><span class="sxs-lookup"><span data-stu-id="7a3b8-138">where:</span></span>

* <span data-ttu-id="7a3b8-139">*&lt;vm-cloudservice name&gt;* — имя виртуальной машины, которая станет главным компьютером для контейнеров Docker в Azure;</span><span class="sxs-lookup"><span data-stu-id="7a3b8-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="7a3b8-140">*&lt;имени пользователя&gt;* is the имени пользователя of the default root user of the VM</span><span class="sxs-lookup"><span data-stu-id="7a3b8-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="7a3b8-141">*&lt;password&gt;* — пароль для *имени пользователя* учетной записи, который отвечает требованиям к сложности, предъявляемым для Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="7a3b8-142">В настоящий момент пароль должен включать не менее 8 символов, содержать как минимум один символ в нижнем и в верхнем регистре, цифру и один из следующих специальных символов: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="7a3b8-143">Точка в конце предыдущего выражения НЕ является специальным символом.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="7a3b8-144">Если команда прошла успешно, вы увидите нечто вроде следующего, в зависимости от конкретных аргументов и параметров, используемых вами:</span><span class="sxs-lookup"><span data-stu-id="7a3b8-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="7a3b8-145">Создание виртуальной машины может занять несколько минут, но после ее подготовки (значение состояния — `ReadyRole`) будет запущена управляющая программа Docker (служба Docker), и вы сможете подключиться к узлу контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="7a3b8-146">Для проверки виртуальной машины Docker, только что созданной в Azure, введите</span><span class="sxs-lookup"><span data-stu-id="7a3b8-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="7a3b8-147">где *&lt;vm-name-you-used&gt;* — имя виртуальной машины, которое было использовано при вызове `azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="7a3b8-148">Вы должны увидеть вывод, похожий на пример ниже, который указывает, что виртуальная машина узла Docker в Azure работает и ожидает ваших команд.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="7a3b8-149">Теперь можно попытаться подключиться с помощью клиента Docker, чтобы получить информацию (в некоторых экземплярах клиента Docker, например в ОС Mac, может потребоваться использовать `sudo`):</span><span class="sxs-lookup"><span data-stu-id="7a3b8-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

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

<span data-ttu-id="7a3b8-150">Чтобы убедиться, что все работает, можно проверить виртуальную машину для расширения Docker:</span><span class="sxs-lookup"><span data-stu-id="7a3b8-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="7a3b8-151">Проверка подлинности виртуальной машины узла Docker</span><span class="sxs-lookup"><span data-stu-id="7a3b8-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="7a3b8-152">Помимо создания виртуальной машины Docker, команда `azure vm docker create` также автоматически создает необходимые сертификаты, чтобы разрешить подключение клиентского компьютера Docker к узлу контейнера Azure с помощью HTTPS. Сертификаты хранятся как на клиентских компьютерах, так и на хост-компьютерах, в зависимости от обстоятельств.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="7a3b8-153">При последующих попытках существующие сертификаты используются повторно и совместно с новым узлом.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="7a3b8-154">По умолчанию сертификаты помещаются в `~/.docker`, а Docker настраивается для запуска с использованием порта **2376**.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="7a3b8-155">Если вы хотите использовать другой порт или каталог, то вы можете использовать один из следующих параметров командной строки `azure vm docker create` для настройки виртуальной машины, в которой размещены контейнеры Docker, на использование другого порта или других сертификатов для подключения клиентов:</span><span class="sxs-lookup"><span data-stu-id="7a3b8-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="7a3b8-156">Управляющая программа Docker на узле настроена на прослушивание и проверку подлинности клиентских подключений на указанном порту с использованием сертификатов, созданных с помощью команды `azure vm docker create` .</span><span class="sxs-lookup"><span data-stu-id="7a3b8-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="7a3b8-157">Клиентские компьютеры должны иметь эти сертификаты, чтобы получить доступ к узлу Docker.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3b8-158">Сетевой узел, работающий без этих сертификатов, будет уязвим для всех, кто может подключиться к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="7a3b8-159">Перед тем как изменить конфигурацию по умолчанию, убедитесь, что вы понимаете все риски, которым могут быть подвержены компьютеры и приложения.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7a3b8-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a3b8-160">Next steps</span></span>
* <span data-ttu-id="7a3b8-161">Переходите к [руководству пользователя Docker] и использованию виртуальной машины Docker.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="7a3b8-162">Для создания виртуальной машины с поддержкой Docker на новом портале см. раздел [Использование расширения виртуальных машин Docker на классическом портале Azure].</span><span class="sxs-lookup"><span data-stu-id="7a3b8-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="7a3b8-163">Расширение виртуальной машины Docker для Azure также поддерживает Docker Compose, использующий декларативный файл YAML, позволяющий использовать смоделированное разработчиком приложение в любой среде и обеспечить согласованное развертывание.</span><span class="sxs-lookup"><span data-stu-id="7a3b8-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="7a3b8-164">Ознакомьтесь с разделом [Приступая к работе с решениями Docker и Compose для определения и запуска многоконтейнерного приложения на виртуальной машине Azure].</span><span class="sxs-lookup"><span data-stu-id="7a3b8-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
<span data-ttu-id="7a3b8-165">[Использование расширения виртуальных машин Docker на классическом портале Azure]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span><span class="sxs-lookup"><span data-stu-id="7a3b8-165">[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span></span>

<span data-ttu-id="7a3b8-166">[руководству пользователя Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="7a3b8-166">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>

<span data-ttu-id="7a3b8-167">[Приступая к работе с решениями Docker и Compose для определения и запуска многоконтейнерного приложения на виртуальной машине Azure]:../docker-compose-quickstart.md</span><span class="sxs-lookup"><span data-stu-id="7a3b8-167">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md</span></span>
