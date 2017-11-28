---
title: "aaaUse Docker Compose на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Как toouse Docker и создать на виртуальных машинах Linux с hello Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="d6d10-103">Получить работы с Docker и составление toodefine и запустите приложение контейнера несколькими в Azure</span><span class="sxs-lookup"><span data-stu-id="d6d10-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="d6d10-104">С [составление](http://github.com/docker/compose), используйте toodefine простой текстовый файл приложения, состоящего из нескольких контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="d6d10-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="d6d10-105">Затем вы запустили приложение с помощью одной команды, которая поддерживает все toodeploy в определенной среде.</span><span class="sxs-lookup"><span data-stu-id="d6d10-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="d6d10-106">Например в этой статье рассказывается, как tooquickly настроить блог WordPress с серверной базы данных MariaDB SQL на Виртуальной машине Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d6d10-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="d6d10-107">Также можно создать tooset копирование более сложных приложений.</span><span class="sxs-lookup"><span data-stu-id="d6d10-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="d6d10-108">Настройка виртуальной машины Linux как узла Docker</span><span class="sxs-lookup"><span data-stu-id="d6d10-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="d6d10-109">Можно использовать различные процедуры Azure и доступных образов или шаблонов диспетчера ресурсов в Azure Marketplace hello toocreate виртуальной Машины Linux и настроить его для использования в качестве узла Docker.</span><span class="sxs-lookup"><span data-stu-id="d6d10-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="d6d10-110">Просмотреть, например [среды с помощью hello расширение ВМ Docker toodeploy](dockerextension.md) tooquickly Создание Виртуальной машине Ubuntu с hello расширения виртуальной Машины Azure Docker с помощью [шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d6d10-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="d6d10-111">При использовании расширение ВМ Docker hello ВМ автоматически настроить узел Docker и составление уже установлена.</span><span class="sxs-lookup"><span data-stu-id="d6d10-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="d6d10-112">Создание узлов Docker с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d6d10-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="d6d10-113">Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d6d10-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d6d10-114">Сначала создайте группу ресурсов для среды Docker командой [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d6d10-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d6d10-115">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение:</span><span class="sxs-lookup"><span data-stu-id="d6d10-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="d6d10-116">Затем разверните виртуальную Машину с [создания развертывания группы az](/cli/azure/group/deployment#create) , включает в себя расширение виртуальной Машины Azure Docker hello из [этого шаблона диспетчера ресурсов Azure на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d6d10-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="d6d10-117">Укажите собственные значения для параметров *newStorageAccountName*, *adminUsername*, *adminPassword* и *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="d6d10-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="d6d10-118">Он занимает несколько минут для развертывания toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="d6d10-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="d6d10-119">После завершения развертывания hello [переместить шаг toonext](#verify-that-compose-is-installed) tooSSH tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6d10-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="d6d10-120">При необходимости строки toohello tooinstead возвращаемого элемента управления и позволяют hello развертывания по-прежнему в фоновом режиме hello, добавьте hello `--no-wait` флаг toohello предшествующий команды.</span><span class="sxs-lookup"><span data-stu-id="d6d10-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="d6d10-121">Этот процесс позволяет tooperform другие действия в hello CLI во время развертывания hello продолжается несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d6d10-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="d6d10-122">Затем можно просмотреть подробные сведения о состоянии узла Docker hello с [Показать ВМ az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="d6d10-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="d6d10-123">Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d6d10-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="d6d10-124">Если эта команда возвращает *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины в даст hello.</span><span class="sxs-lookup"><span data-stu-id="d6d10-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="d6d10-125">Проверка установки Compose</span><span class="sxs-lookup"><span data-stu-id="d6d10-125">Verify that Compose is installed</span></span>
<span data-ttu-id="d6d10-126">После завершения развертывания hello SSH tooyour новый узел Docker с помощью DNS-имя hello указанный во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d6d10-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="d6d10-127">Можно использовать `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview подробные сведения о виртуальной Машины, включая hello DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="d6d10-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="d6d10-128">toocheck, составления устанавливается на hello виртуальных Машин, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6d10-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="d6d10-129">Увидеть результаты, аналогичные слишком*1.6.2 docker создания, построения 4d 72027*.</span><span class="sxs-lookup"><span data-stu-id="d6d10-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="d6d10-130">Если используется другой метод toocreate узел Docker и требуется tooinstall составления самостоятельно, см. раздел hello [составления документации](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="d6d10-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="d6d10-131">Создание файла конфигурации docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="d6d10-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="d6d10-132">Далее нужно создать `docker-compose.yml` файл, который является просто текстового файла конфигурации, toorun контейнеры Docker toodefine hello на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6d10-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="d6d10-133">файл Hello указывает toorun hello изображения на каждый контейнер (или может быть сборки из файла Dockerfile), необходимые переменные среды и зависимости, порты и hello ссылки между контейнерами.</span><span class="sxs-lookup"><span data-stu-id="d6d10-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="d6d10-134">Дополнительные сведения о синтаксисе YML-файла приведены в [справке по файлу Compose](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="d6d10-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="d6d10-135">Создать hello *docker compose.yml* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d6d10-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="d6d10-136">Используйте вашей tooadd привычном текстовом редакторе файл toohello некоторых данных.</span><span class="sxs-lookup"><span data-stu-id="d6d10-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="d6d10-137">Hello следующий пример использует hello *vi* редактора:</span><span class="sxs-lookup"><span data-stu-id="d6d10-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="d6d10-138">Вставьте следующий пример в текстовый файл hello.</span><span class="sxs-lookup"><span data-stu-id="d6d10-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="d6d10-139">Эта конфигурация использует изображения из hello [DockerHub реестра](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Привет открыть источник ведения блогов и система управления содержимым) и связанные базы данных MariaDB SQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="d6d10-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="d6d10-140">Введите собственное значение *MYSQL_ROOT_PASSWORD* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d6d10-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="d6d10-141">Начать с создания сообщения hello контейнеров</span><span class="sxs-lookup"><span data-stu-id="d6d10-141">Start hello containers with Compose</span></span>
<span data-ttu-id="d6d10-142">В hello же каталоге, что ваш *docker compose.yml* файл, запустите следующую команду hello (в зависимости от среды, может потребоваться toorun `docker-compose` с помощью `sudo`):</span><span class="sxs-lookup"><span data-stu-id="d6d10-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="d6d10-143">Эта команда запускает контейнеры Docker hello, указанный в *docker compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="d6d10-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="d6d10-144">Он принимает одну или две для этого шага toocomplete минуты.</span><span class="sxs-lookup"><span data-stu-id="d6d10-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="d6d10-145">Можно увидеть примерно toohello вывода следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d6d10-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="d6d10-146">Быть убедиться, что hello toouse **-d** параметра при запуске, чтобы контейнеры hello выполняться непрерывно в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="d6d10-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="d6d10-147">tooverify, функционируют контейнеры hello типа `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="d6d10-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="d6d10-148">Вы увидите нечто вроде этого:</span><span class="sxs-lookup"><span data-stu-id="d6d10-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="d6d10-149">Теперь можно подключиться tooWordPress непосредственно на hello виртуальной Машины на порт 80.</span><span class="sxs-lookup"><span data-stu-id="d6d10-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="d6d10-150">Откройте веб-браузер и введите hello DNS-имя виртуальной Машины (например, `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="d6d10-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="d6d10-151">Теперь вы увидите экран, где можно завершить установку hello и приступить к работе с приложением hello запуска WordPress hello.</span><span class="sxs-lookup"><span data-stu-id="d6d10-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Начальный экран WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="d6d10-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6d10-153">Next steps</span></span>
* <span data-ttu-id="d6d10-154">Go toohello [руководство пользователя по модулю виртуальной Машины Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) Дополнительные параметры tooconfigure Docker и создать ВМ Docker.</span><span class="sxs-lookup"><span data-stu-id="d6d10-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="d6d10-155">Например один вариант — Создать yml hello tooput файл (преобразованный tooJSON) непосредственно в конфигурации hello hello расширение ВМ Docker.</span><span class="sxs-lookup"><span data-stu-id="d6d10-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="d6d10-156">Извлечение hello [составления Справочник по командной строке](http://docs.docker.com/compose/reference/) и [руководство пользователя по](http://docs.docker.com/compose/) Дополнительные примеры создания и развертывания приложений с несколькими контейнера.</span><span class="sxs-lookup"><span data-stu-id="d6d10-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="d6d10-157">Использовать шаблон диспетчера ресурсов Azure, либо ваш собственный или один были получены из hello [сообщества](https://azure.microsoft.com/documentation/templates/), toodeploy ВМ Azure с Docker и приложения для установки создания.</span><span class="sxs-lookup"><span data-stu-id="d6d10-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="d6d10-158">Здравствуйте, например, [развертывание блог WordPress с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) Docker использует шаблон и создать tooquickly развертывание WordPress с серверной на Виртуальной машине Ubuntu MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6d10-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="d6d10-159">Попытайтесь интегрировать Docker Compose с кластером Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="d6d10-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="d6d10-160">Сценарии приведены в статье [Using Swarm with Compose](https://docs.docker.com/compose/swarm/) (Совместное использование Compose и Swarm).</span><span class="sxs-lookup"><span data-stu-id="d6d10-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
