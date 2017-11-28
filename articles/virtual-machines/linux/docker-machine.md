---
title: "Создание узлов Linux в Azure с помощью Docker Machine | Документация Майкрософт"
description: "Описывается использование машины Docker для создания узлов Docker в Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a><span data-ttu-id="dac4a-103">Создание узлов в Azure с помощью компьютера Docker | Документация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="dac4a-103">How to use Docker Machine to create hosts in Azure</span></span>
<span data-ttu-id="dac4a-104">В этой статье представлены сведения о том, как создать узел в Azure с использованием [компьютера Docker](https://docs.docker.com/machine/).</span><span class="sxs-lookup"><span data-stu-id="dac4a-104">This article details how to use [Docker Machine](https://docs.docker.com/machine/) to create hosts in Azure.</span></span> <span data-ttu-id="dac4a-105">Команда `docker-machine` создает виртуальную машину Linux в Azure, после чего устанавливает Docker.</span><span class="sxs-lookup"><span data-stu-id="dac4a-105">The `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="dac4a-106">Затем можно управлять узлами Docker в Azure с помощью аналогичных локальных средств и рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="dac4a-106">You can then manage your Docker hosts in Azure using the same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="dac4a-107">Создание виртуальных машин с помощью машины Docker</span><span class="sxs-lookup"><span data-stu-id="dac4a-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="dac4a-108">Сначала получите идентификатор подписки Azure с помощью команды [az account show](/cli/azure/account#show) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dac4a-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="dac4a-109">Создайте виртуальные машины узла Docker в Azure с помощью команды `docker-machine create`, используя драйвер *azure*.</span><span class="sxs-lookup"><span data-stu-id="dac4a-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as the driver.</span></span> <span data-ttu-id="dac4a-110">Кроме того, можно ознакомиться с [документацией по драйверу Docker Azure](https://docs.docker.com/machine/drivers/azure/).</span><span class="sxs-lookup"><span data-stu-id="dac4a-110">For more information, see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="dac4a-111">В следующем примере создается виртуальная машина с именем *myVM*, учетная запись пользователя с именем *azureuser* и открывается порт *80* на узле виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dac4a-111">The following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on the host VM.</span></span> <span data-ttu-id="dac4a-112">Выполните вход в учетную запись Azure и предоставьте компьютеру Docker разрешения на создание и управление ресурсами.</span><span class="sxs-lookup"><span data-stu-id="dac4a-112">Follow any prompts to log in to your Azure account and grant Docker Machine permissions to create and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="dac4a-113">Результат должен быть аналогичным приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="dac4a-113">The output looks similar to the following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="dac4a-114">Настройка оболочки Docker</span><span class="sxs-lookup"><span data-stu-id="dac4a-114">Configure your Docker shell</span></span>
<span data-ttu-id="dac4a-115">Чтобы подключиться к узлу Docker в Azure, задайте соответствующие параметры подключения.</span><span class="sxs-lookup"><span data-stu-id="dac4a-115">To connect to your Docker host in Azure, define the appropriate connection settings.</span></span> <span data-ttu-id="dac4a-116">Как указано в конце выходных данных, просмотрите сведения о соединении узла Docker следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dac4a-116">As noted at the end of the output, view the connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="dac4a-117">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="dac4a-117">The output is similar to the following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="dac4a-118">Для задания параметров вы можете либо выполнить предлагаемую команду настройки (`eval $(docker-machine env myvmdocker)`), либо задать переменные среды самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="dac4a-118">To define the connection settings you can either run the suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set the environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="dac4a-119">Запуск контейнера</span><span class="sxs-lookup"><span data-stu-id="dac4a-119">Run a container</span></span>
<span data-ttu-id="dac4a-120">Чтобы увидеть контейнер в действии, запустите основной веб-сервер NGINX.</span><span class="sxs-lookup"><span data-stu-id="dac4a-120">To see a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="dac4a-121">Создайте контейнер с `docker run` и настройте порт 80 для веб-трафика следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dac4a-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="dac4a-122">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="dac4a-122">The output is similar to the following example:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="dac4a-123">Проверьте запущенные контейнеры с помощью `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="dac4a-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="dac4a-124">В следующем примере в выходных данных отображается контейнер NGINX с настроенным портом 80:</span><span class="sxs-lookup"><span data-stu-id="dac4a-124">The following example output shows the NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a><span data-ttu-id="dac4a-125">Проверка контейнера</span><span class="sxs-lookup"><span data-stu-id="dac4a-125">Test the container</span></span>
<span data-ttu-id="dac4a-126">Получите общедоступный IP-адрес узла Docker следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dac4a-126">Obtain the public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="dac4a-127">Чтобы увидеть контейнер в действии, откройте веб-браузер и введите общедоступный IP-адрес, указанный в выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="dac4a-127">To see the container in action, open a web browser and enter the public IP address noted in the output of the preceding command:</span></span>

![Запущенный контейнер nginx](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="dac4a-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dac4a-129">Next steps</span></span>
<span data-ttu-id="dac4a-130">Кроме того, можно создавать узлы с помощью [расширения виртуальной машины Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="dac4a-130">You can also create hosts with the [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="dac4a-131">Примеры использования Docker Compose см. в статье [Приступая к работе с Docker и Compose для определения и запуска многоконтейнерного приложения в Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="dac4a-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
