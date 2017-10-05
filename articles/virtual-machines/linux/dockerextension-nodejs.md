---
title: "Использование расширения виртуальной машины Docker для Azure с Azure CLI 1.0 | Документация Майкрософт"
description: "Сведения об использовании расширения виртуальной машины Docker для быстрого и безопасного развертывания среды Docker в Azure с помощью шаблона Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a3cbcf63533f4042dcd695e141655c5814bd7068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="c82d1-103">Создание среды Docker в Azure с использованием расширения виртуальной машины Docker посредством Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c82d1-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="c82d1-104">Docker — это популярная платформа управления контейнерами и работы с образами, которая позволяет быстро работать с контейнерами в Linux (а также в Windows).</span><span class="sxs-lookup"><span data-stu-id="c82d1-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="c82d1-105">В Azure развертывание Docker можно выполнить несколькими разными способами в соответствии с конкретными потребностями.</span><span class="sxs-lookup"><span data-stu-id="c82d1-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="c82d1-106">В этой статье рассматривается использование расширения виртуальной машины Docker и шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c82d1-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="c82d1-107">Дополнительные сведения о различных методах развертывания, в том числе с помощью Docker Machine и служб контейнеров Azure, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c82d1-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="c82d1-108">Чтобы быстро создать прототип приложения, можно создать один узел Docker с помощью [машины Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="c82d1-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="c82d1-109">В более крупных стабильных средах можно использовать расширение виртуальной машины Docker для Azure, которое также поддерживает компонент [Docker Compose](https://docs.docker.com/compose/overview/), обеспечивающий согласованное развертывание контейнеров.</span><span class="sxs-lookup"><span data-stu-id="c82d1-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="c82d1-110">В этой статье приведены подробные сведения об использовании расширения виртуальных машин Docker для Azure.</span><span class="sxs-lookup"><span data-stu-id="c82d1-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="c82d1-111">Чтобы создать готовые к работе, масштабируемые среды с дополнительными средствами планирования и управления, можно развернуть [кластер Docker Swarm в службах контейнеров Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c82d1-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c82d1-112">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="c82d1-112">CLI versions to complete the task</span></span>
<span data-ttu-id="c82d1-113">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="c82d1-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="c82d1-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="c82d1-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c82d1-115">[Azure CLI 2.0](dockerextension.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c82d1-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="c82d1-116">Общие сведения о расширении виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="c82d1-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="c82d1-117">Расширение виртуальных машин Docker для Azure устанавливает и настраивает управляющую программу Docker, клиент Docker и Docker Compose на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="c82d1-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="c82d1-118">В отличие от использования только машины Docker или самостоятельного создания узла Docker с этим расширением вы получаете дополнительные элементы управления и компоненты.</span><span class="sxs-lookup"><span data-stu-id="c82d1-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="c82d1-119">Благодаря этим дополнительным компонентам, таким как [Docker Compose](https://docs.docker.com/compose/overview/), расширение виртуальных машин Docker для Azure подходит для более надежных сред разработки или рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="c82d1-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="c82d1-120">Шаблоны Azure Resource Manager определяют структуру всей среды.</span><span class="sxs-lookup"><span data-stu-id="c82d1-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="c82d1-121">Они позволяют создавать и настраивать ресурсы, такие как виртуальные машины узла Docker, хранилище, элементы управления доступом на основе ролей (RBAC) и службу диагностики.</span><span class="sxs-lookup"><span data-stu-id="c82d1-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="c82d1-122">Эти шаблоны можно повторно использовать для создания дополнительных развертываний ресурсов в согласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="c82d1-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="c82d1-123">Дополнительные сведения об Azure Resource Manager и шаблонах см. в статье [Общие сведения об Azure Resource Manager ](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c82d1-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="c82d1-124">Развертывание шаблона с помощью расширения виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="c82d1-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="c82d1-125">Чтобы создать виртуальную машину Ubuntu, на которой установлено расширение виртуальной машины Docker для Azure (для установки и настройки узла Docker), мы используем готовый шаблон быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="c82d1-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="c82d1-126">Шаблон можно найти в разделе [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)(Простое развертывание виртуальной машины Ubuntu с Docker).</span><span class="sxs-lookup"><span data-stu-id="c82d1-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c82d1-127">Кроме того, потребуется установить [последнюю версию интерфейса командной строки Azure](../../cli-install-nodejs.md) и выполнить вход в систему в режиме Resource Manager, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c82d1-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c82d1-128">Разверните шаблон с помощью интерфейса командной строки Azure, указав универсальный код ресурса (URI) шаблона.</span><span class="sxs-lookup"><span data-stu-id="c82d1-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="c82d1-129">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *westus*.</span><span class="sxs-lookup"><span data-stu-id="c82d1-129">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span> <span data-ttu-id="c82d1-130">Укажите собственное имя группы ресурсов и расположение, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c82d1-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c82d1-131">В ответ на запросы укажите имя учетной записи хранения, имя пользователя и пароль, а также DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="c82d1-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="c82d1-132">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="c82d1-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="c82d1-133">Интерфейс командной строки Azure отобразит командную строку всего через несколько секунд, но создание и настройка узла Docker с помощью расширения виртуальных машин Docker для Azure еще не завершено.</span><span class="sxs-lookup"><span data-stu-id="c82d1-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="c82d1-134">Подождите несколько минут до завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="c82d1-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="c82d1-135">Сведения о состоянии узла Docker можно просмотреть с помощью команды `azure vm show`.</span><span class="sxs-lookup"><span data-stu-id="c82d1-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="c82d1-136">В следующем примере проверяется состояние виртуальной машины с именем *myDockerVM* (имя по умолчанию, указанное в шаблоне; не изменяйте его) в группе ресурсов *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c82d1-136">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="c82d1-137">Введите имя группы ресурсов, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c82d1-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="c82d1-138">После выполнения команды `azure vm show` вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="c82d1-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="c82d1-139">В начале выходных данных отображается состояние **ProvisioningState** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c82d1-139">Near the top of the output, you see the **ProvisioningState** of the VM.</span></span> <span data-ttu-id="c82d1-140">Если отображается состояние *Succeeded*, значит, развертывание завершено, и вы можете подключиться к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c82d1-140">When this displays *Succeeded*, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="c82d1-141">В конце выходных данных *FQDN* отображает полное доменное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="c82d1-141">Towards the end of the output, *FQDN* displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="c82d1-142">Это полное доменное имя будет использовано для подключения к узлу Docker по протоколу SSH на последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="c82d1-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="c82d1-143">Развертывание первого контейнера nginx</span><span class="sxs-lookup"><span data-stu-id="c82d1-143">Deploy your first nginx container</span></span>
<span data-ttu-id="c82d1-144">После завершения развертывания установите SSH-подключение к новому узлу Docker из локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="c82d1-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="c82d1-145">Введите собственное имя пользователя и полное доменное имя, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c82d1-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c82d1-146">После входа в систему узла Docker запустите контейнер nginx.</span><span class="sxs-lookup"><span data-stu-id="c82d1-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="c82d1-147">После скачивания образа nginx и запуска контейнера результаты должны выглядеть примерно так, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="c82d1-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="c82d1-148">Проверьте состояние контейнеров, запущенных на узле Docker, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c82d1-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="c82d1-149">Результаты должны выглядеть примерно так, как показано ниже. В них должно быть указано, что контейнер nginx запущен, а TCP-порты 80 и 443 перенаправлены.</span><span class="sxs-lookup"><span data-stu-id="c82d1-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="c82d1-150">Чтобы увидеть контейнер в действии, откройте веб-браузер и введите полное доменное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="c82d1-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="c82d1-152">Пример шаблона расширения виртуальной машины Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="c82d1-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="c82d1-153">В предыдущем примере использовался готовый шаблон быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="c82d1-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="c82d1-154">Расширение виртуальной машины Docker для Azure можно также развернуть с помощью собственных шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c82d1-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="c82d1-155">Для этого добавьте следующий код в свои шаблоны Resource Manager, указав вместо *vmName* имя своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c82d1-155">To do so, add the following to your Resource Manager templates, defining the *vmName* of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="c82d1-156">Подробное пошаговое руководство по использованию шаблонов Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c82d1-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c82d1-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c82d1-157">Next steps</span></span>
<span data-ttu-id="c82d1-158">Возможно, вам потребуется [настроить TCP-порт управляющей программы Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), [ознакомиться с параметрами безопасности Docker](https://docs.docker.com/engine/security/security/) или развернуть контейнеры с помощью [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="c82d1-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="c82d1-159">Дополнительные сведения о расширении виртуальных машин Docker для Azure см. в [репозитории GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="c82d1-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="c82d1-160">Дополнительные сведения о вариантах развертывания Docker в Azure см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="c82d1-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="c82d1-161">Использование машины Docker с драйвером Azure</span><span class="sxs-lookup"><span data-stu-id="c82d1-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="c82d1-162">[Приступая к работе с решениями Docker и Compose для определения и запуска многоконтейнерного приложения на виртуальной машине Azure](docker-compose-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="c82d1-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="c82d1-163">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="c82d1-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

