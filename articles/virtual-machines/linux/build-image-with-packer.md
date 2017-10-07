---
title: "aaaHow toocreate образов виртуальных Машин Linux Azure с Packer | Документы Microsoft"
description: "Узнайте, как toouse Packer toocreate образы виртуальных машин Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="b9bc6-103">Как виртуальная машина Linux toocreate toouse Packer образы в Azure</span><span class="sxs-lookup"><span data-stu-id="b9bc6-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="b9bc6-104">Каждой виртуальной машины (VM) в Azure создается из образа, определяющего hello дистрибутив Linux и версию операционной системы.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="b9bc6-105">Образы могут содержать предварительно установленные приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="b9bc6-106">Hello Azure Marketplace предоставляет большое количество изображений первый и сторонних разработчиков для наиболее общие распределения и среды приложения или можно создать адаптированные пользовательских образов tooyour потребностями.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="b9bc6-107">В этой статье описаны как toouse Привет открыть инструмент источника [Packer](https://www.packer.io/) toodefine и построения пользовательских образов в Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="b9bc6-108">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b9bc6-108">Create Azure resource group</span></span>
<span data-ttu-id="b9bc6-109">Во время сборки hello Packer создает временные ресурсы Azure, при построении hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="b9bc6-110">toocapture, исходной виртуальной Машины для использования в качестве образа, необходимо определить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="b9bc6-111">Hello выходные данные процесса сборки hello Packer хранится в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="b9bc6-112">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b9bc6-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b9bc6-113">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="b9bc6-114">Создание учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="b9bc6-114">Create Azure credentials</span></span>
<span data-ttu-id="b9bc6-115">Packer выполняет проверку подлинности с помощью субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="b9bc6-116">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="b9bc6-117">Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="b9bc6-118">Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется Packer выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="b9bc6-119">Пример выходных данных hello hello предшествующий команды выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="b9bc6-120">tooauthenticate tooAzure, необходимо также идентификатор подписки Azure с tooobtain [az учетной записи, отображают](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="b9bc6-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="b9bc6-121">В следующем шаге hello используйте hello выходные данные этих двух команд.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="b9bc6-122">Определение шаблона Packer</span><span class="sxs-lookup"><span data-stu-id="b9bc6-122">Define Packer template</span></span>
<span data-ttu-id="b9bc6-123">toobuild изображения, нужно создать шаблон в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="b9bc6-124">В шаблоне hello определения построители и provisioners, выполняющих hello фактический процесс построения.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="b9bc6-125">Имеет packer [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html) , позволяющий toodefine Azure ресурсы, такие как службы основной hello учетных данных, созданных в предыдущих шага hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="b9bc6-126">Создайте файл с именем *ubuntu.json* и вставить hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="b9bc6-127">Ввести собственные значения для следующего hello:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="b9bc6-128">Параметр</span><span class="sxs-lookup"><span data-stu-id="b9bc6-128">Parameter</span></span>                           | <span data-ttu-id="b9bc6-129">Где tooobtain</span><span class="sxs-lookup"><span data-stu-id="b9bc6-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="b9bc6-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-130">*client_id*</span></span>                         | <span data-ttu-id="b9bc6-131">Первая строка выходных данных из `az ad sp` создает команду *appId*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="b9bc6-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-132">*client_secret*</span></span>                     | <span data-ttu-id="b9bc6-133">Вторая строка выходных данных из `az ad sp` создает команду *password*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="b9bc6-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-134">*tenant_id*</span></span>                         | <span data-ttu-id="b9bc6-135">Третья строка выходных данных из `az ad sp` создает команду *tenant*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="b9bc6-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-136">*subscription_id*</span></span>                   | <span data-ttu-id="b9bc6-137">Выходные данные команды `az account show`</span><span class="sxs-lookup"><span data-stu-id="b9bc6-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="b9bc6-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="b9bc6-139">Имя группы ресурсов, созданный на первом шаге hello</span><span class="sxs-lookup"><span data-stu-id="b9bc6-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="b9bc6-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="b9bc6-140">*managed_image_name*</span></span>                | <span data-ttu-id="b9bc6-141">Имя образа hello управляемого диска, который создается</span><span class="sxs-lookup"><span data-stu-id="b9bc6-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="b9bc6-142">Этот шаблон создает изображение Ubuntu 16.04 LTS, устанавливает NGINX, а затем deprovisions hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b9bc6-143">Если развернуть на учетные данные пользователя tooprovision этот шаблон, настроить hello средство подготовки команды, deprovisions hello tooread агент Azure `-deprovision` вместо `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="b9bc6-144">Hello `+user` флаг удаляет все учетные записи пользователей из hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="b9bc6-145">Создание образа Packer</span><span class="sxs-lookup"><span data-stu-id="b9bc6-145">Build Packer image</span></span>
<span data-ttu-id="b9bc6-146">Если у вас еще нет Packer установлен на локальном компьютере, [следуйте инструкциям по установке hello Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="b9bc6-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="b9bc6-147">Для создания образа hello задайте вашей Packer файл шаблона следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="b9bc6-148">Пример выходных данных hello hello предшествующий команды выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="b9bc6-149">Создание виртуальной машины на основе образа Azure</span><span class="sxs-lookup"><span data-stu-id="b9bc6-149">Create VM from Azure Image</span></span>
<span data-ttu-id="b9bc6-150">Теперь можно создать виртуальную машину из образа с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b9bc6-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b9bc6-151">Укажите образ, созданный с помощью hello hello `--image` параметра.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="b9bc6-152">Hello следующий пример создает Виртуальную машину с именем *myVM* из *myPackerImage* и создает ключи SSH, если они еще не существует:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="b9bc6-153">Занимает несколько минут toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="b9bc6-154">После создания виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="b9bc6-155">Этот адрес будет используется tooaccess hello NGINX сайта из веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="b9bc6-156">tooallow веб-трафика tooreach виртуальной Машины, откройте порт 80 с hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="b9bc6-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="b9bc6-157">Тестирование виртуальной машины и NGINX</span><span class="sxs-lookup"><span data-stu-id="b9bc6-157">Test VM and NGINX</span></span>
<span data-ttu-id="b9bc6-158">Теперь можно открыть веб-браузер и введите `http://publicIpAddress` в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="b9bc6-159">Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="b9bc6-160">Откроется страница NGINX по умолчанию Hello как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b9bc6-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Сайт nginx по умолчанию](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="b9bc6-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9bc6-162">Next steps</span></span>
<span data-ttu-id="b9bc6-163">В этом примере используется Packer toocreate образ виртуальной Машины с NGINX уже установлена.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="b9bc6-164">Можно использовать этот образ виртуальной Машины наряду с существующие рабочие процессы развертывания, например toodeploy tooVMs вашего приложения, созданные на основе hello изображение с Ansible, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="b9bc6-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="b9bc6-165">Дополнительный пример шаблонов Packer для других дистрибутивов Linux см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="b9bc6-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>