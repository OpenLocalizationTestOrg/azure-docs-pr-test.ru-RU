---
title: "размещает aaaCreate Docker в Azure с машины Docker | Документы Microsoft"
description: "Описывает использование узлов docker toocreate машин Docker в Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="43499-103">Создание узлов Docker в Azure с помощью машины Docker</span><span class="sxs-lookup"><span data-stu-id="43499-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="43499-104">Под управлением [Docker](https://www.docker.com/) контейнеры требует узла виртуальной Машины выполняющегося hello управляющей программы docker.</span><span class="sxs-lookup"><span data-stu-id="43499-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="43499-105">В этом разделе описывается способ toouse hello [машины docker](https://docs.docker.com/machine/) команда toocreate новые виртуальные машины Linux настроены hello управляющей программы Docker в Azure.</span><span class="sxs-lookup"><span data-stu-id="43499-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="43499-106">**Примечание.**</span><span class="sxs-lookup"><span data-stu-id="43499-106">**Note:**</span></span> 

* <span data-ttu-id="43499-107">*Для выполнения действий, описанных в этой статье, требуется машина Docker версии 0.9.0-rc2 или более поздней версии.*</span><span class="sxs-lookup"><span data-stu-id="43499-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="43499-108">*Контейнеры Windows поддерживаются через docker машину в hello ближайшее будущее*</span><span class="sxs-lookup"><span data-stu-id="43499-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="43499-109">Создание виртуальных машин с помощью машины Docker</span><span class="sxs-lookup"><span data-stu-id="43499-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="43499-110">Создание docker узлов виртуальных машин в Azure с hello `docker-machine create` команду, указав hello `azure` драйвера.</span><span class="sxs-lookup"><span data-stu-id="43499-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="43499-111">Hello Azure драйвер требуется идентификатор вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="43499-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="43499-112">Можно использовать hello [Azure CLI](cli-install-nodejs.md) или hello [портала Azure](https://portal.azure.com) tooretrieve подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="43499-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="43499-113">**С помощью портала Azure hello**</span><span class="sxs-lookup"><span data-stu-id="43499-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="43499-114">Выберите **подписки** из hello левой панели навигации страницы и скопируйте hello идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="43499-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="43499-115">**С помощью hello Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="43499-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="43499-116">Тип ```azure account list``` и идентификатор подписки hello копирования.</span><span class="sxs-lookup"><span data-stu-id="43499-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="43499-117">Тип `docker-machine create --driver azure` toosee hello параметры и их значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="43499-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="43499-118">Можно также просмотреть hello [документации по драйверу Azure Docker](https://docs.docker.com/machine/drivers/azure/) Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="43499-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="43499-119">Hello примере полагается на hello [значения по умолчанию](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), но при необходимости значение эти значения:</span><span class="sxs-lookup"><span data-stu-id="43499-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="43499-120">dns Azure для hello имя, связанное с общедоступным IP-hello и сертификаты, созданные.</span><span class="sxs-lookup"><span data-stu-id="43499-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="43499-121">Это hello DNS-имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="43499-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="43499-122">Hello ВМ можно затем безопасно остановить, выпуск hello динамических IP-адресов и предоставляют возможность tooreconnect hello после ВМ hello снова начинается с новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="43499-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="43499-123">префикс имени Hello должно быть уникальным для той области UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="43499-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="43499-124">Открытие порта 80 в hello виртуальной Машины для исходящего доступа к Интернету</span><span class="sxs-lookup"><span data-stu-id="43499-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="43499-125">размер hello хранилище быстрее premium tooutilize виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="43499-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="43499-126">хранилище Premium, используемый для диска ВМ hello</span><span class="sxs-lookup"><span data-stu-id="43499-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="43499-127">Выбор узла Docker с помощью машины Docker</span><span class="sxs-lookup"><span data-stu-id="43499-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="43499-128">При наличии запись машины docker для узла, можно задать узел по умолчанию hello при выполнении команды docker.</span><span class="sxs-lookup"><span data-stu-id="43499-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="43499-129">с использованием PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43499-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="43499-130">Использование Bash</span><span class="sxs-lookup"><span data-stu-id="43499-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="43499-131">Теперь можно запускать команды docker с указанным узлом hello</span><span class="sxs-lookup"><span data-stu-id="43499-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="43499-132">Запуск контейнера</span><span class="sxs-lookup"><span data-stu-id="43499-132">Run a container</span></span>
<span data-ttu-id="43499-133">С настройки узла можно запустить простой web server tootest ли узла был настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="43499-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="43499-134">Здесь мы использовать стандартный nginx образ, указать, что он должен прослушивать порт 80 и, если hello узла виртуальная машина перезапускается, hello контейнер будет перезапустить также (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="43499-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="43499-135">Hello вывод должен выглядеть примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43499-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="43499-136">Тестовый контейнер hello</span><span class="sxs-lookup"><span data-stu-id="43499-136">Test hello container</span></span>
<span data-ttu-id="43499-137">Проверьте запущенные контейнеры с помощью `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="43499-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="43499-138">И, в контейнер типа запускается hello toosee `docker-machine ip <VM name>` tooenter toofind hello IP адрес в браузере hello:</span><span class="sxs-lookup"><span data-stu-id="43499-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Запущенный контейнер nginx](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="43499-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="43499-140">Summary</span></span>
<span data-ttu-id="43499-141">С помощью машины Docker можно легко подготовить узлы Docker в Azure к выполнению проверок отдельных узлов Docker.</span><span class="sxs-lookup"><span data-stu-id="43499-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="43499-142">Для рабочей среды размещения контейнеров, в разделе hello [контейнера службы Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="43499-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="43499-143">toodevelop основных приложений .NET в Visual Studio, в разделе [Docker средства для Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="43499-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

