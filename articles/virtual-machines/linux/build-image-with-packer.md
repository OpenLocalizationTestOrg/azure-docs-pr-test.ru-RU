---
title: "Создание образов виртуальных машин Linux в Azure с помощью Packer | Документация Майкрософт"
description: "Сведения об использовании Packer для создания образов виртуальных машин Linux в Azure"
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
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="d24fb-103">Создание образов виртуальных машин Linux в Azure с помощью Packer</span><span class="sxs-lookup"><span data-stu-id="d24fb-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="d24fb-104">Каждая виртуальная машина в Azure создается из образа, определяющего дистрибутив Linux и версию операционной системы.</span><span class="sxs-lookup"><span data-stu-id="d24fb-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="d24fb-105">Образы могут содержать предварительно установленные приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d24fb-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="d24fb-106">Azure Marketplace предоставляет большое количество образов Майкрософт и сторонних разработчиков для наиболее распространенных операционных систем и приложений. Кроме того, вы можете создать собственные настраиваемые образы, отвечающие конкретным потребностям.</span><span class="sxs-lookup"><span data-stu-id="d24fb-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="d24fb-107">В этой статье описывается определение и создание пользовательских образов в Azure с использованием средства с открытым кодом [Packer](https://www.packer.io/).</span><span class="sxs-lookup"><span data-stu-id="d24fb-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="d24fb-108">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d24fb-108">Create Azure resource group</span></span>
<span data-ttu-id="d24fb-109">В процессе сборки исходной виртуальной машины Packer создает временные ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="d24fb-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="d24fb-110">Чтобы сохранить эту исходную виртуальную машину для использования в качестве образа, необходимо определить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d24fb-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="d24fb-111">Выходные данные процесса сборки Packer хранятся в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d24fb-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="d24fb-112">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d24fb-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d24fb-113">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="d24fb-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="d24fb-114">Создание учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="d24fb-114">Create Azure credentials</span></span>
<span data-ttu-id="d24fb-115">Packer выполняет проверку подлинности с помощью субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="d24fb-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="d24fb-116">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer.</span><span class="sxs-lookup"><span data-stu-id="d24fb-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="d24fb-117">Вы можете определять разрешения на то, какие операции может выполнять субъект-служба в Azure, и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="d24fb-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="d24fb-118">Создайте субъект-службу с помощью командлета [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) и выведите учетные данные, необходимые для Packer:</span><span class="sxs-lookup"><span data-stu-id="d24fb-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="d24fb-119">Ниже приведен пример выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="d24fb-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="d24fb-120">Для проверки подлинности в Azure также необходимо получить идентификатор подписки Azure с помощью команды [az account show](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="d24fb-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="d24fb-121">Используйте выходные данные этих двух команд на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="d24fb-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="d24fb-122">Определение шаблона Packer</span><span class="sxs-lookup"><span data-stu-id="d24fb-122">Define Packer template</span></span>
<span data-ttu-id="d24fb-123">Чтобы собрать образы, создайте шаблон в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d24fb-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="d24fb-124">В шаблоне определите средства разработки и подготовки, выполняющие процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="d24fb-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="d24fb-125">Packer использует [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html), которое позволяет определить ресурсы Azure, такие как учетные данные субъекта-службы, созданные на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="d24fb-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="d24fb-126">Создайте файл с именем *ubuntu.json* и вставьте следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="d24fb-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="d24fb-127">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d24fb-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="d24fb-128">Параметр</span><span class="sxs-lookup"><span data-stu-id="d24fb-128">Parameter</span></span>                           | <span data-ttu-id="d24fb-129">Где можно получить</span><span class="sxs-lookup"><span data-stu-id="d24fb-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="d24fb-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="d24fb-130">*client_id*</span></span>                         | <span data-ttu-id="d24fb-131">Первая строка выходных данных из `az ad sp` создает команду *appId*</span><span class="sxs-lookup"><span data-stu-id="d24fb-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="d24fb-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="d24fb-132">*client_secret*</span></span>                     | <span data-ttu-id="d24fb-133">Вторая строка выходных данных из `az ad sp` создает команду *password*</span><span class="sxs-lookup"><span data-stu-id="d24fb-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="d24fb-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="d24fb-134">*tenant_id*</span></span>                         | <span data-ttu-id="d24fb-135">Третья строка выходных данных из `az ad sp` создает команду *tenant*</span><span class="sxs-lookup"><span data-stu-id="d24fb-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="d24fb-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="d24fb-136">*subscription_id*</span></span>                   | <span data-ttu-id="d24fb-137">Выходные данные команды `az account show`</span><span class="sxs-lookup"><span data-stu-id="d24fb-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="d24fb-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="d24fb-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="d24fb-139">Имя группы ресурсов, созданной на первом шаге</span><span class="sxs-lookup"><span data-stu-id="d24fb-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="d24fb-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="d24fb-140">*managed_image_name*</span></span>                | <span data-ttu-id="d24fb-141">Имя создаваемого образа управляемого диска</span><span class="sxs-lookup"><span data-stu-id="d24fb-141">Name for the managed disk image that is created</span></span> |


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

<span data-ttu-id="d24fb-142">Этот шаблон создает образ Ubuntu 16.04 LTS, устанавливает NGINX, а затем отзывает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d24fb-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d24fb-143">Если вы расширите этот шаблон, чтобы подготовить учетные данные пользователя, настройте команду средства подготовки, которая отзывает агент Azure для чтения `-deprovision` вместо `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="d24fb-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="d24fb-144">Флаг `+user` удаляет все учетные записи пользователей из исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d24fb-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="d24fb-145">Создание образа Packer</span><span class="sxs-lookup"><span data-stu-id="d24fb-145">Build Packer image</span></span>
<span data-ttu-id="d24fb-146">Если средство Packer еще не установлено на локальном компьютере, [следуйте инструкциям по его установке](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="d24fb-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="d24fb-147">Создайте образ, указав файл шаблона Packer следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d24fb-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="d24fb-148">Ниже приведен пример выходных данных предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="d24fb-148">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="d24fb-149">Создание виртуальной машины на основе образа Azure</span><span class="sxs-lookup"><span data-stu-id="d24fb-149">Create VM from Azure Image</span></span>
<span data-ttu-id="d24fb-150">Теперь можно создать виртуальную машину из образа с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d24fb-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d24fb-151">Укажите образ, созданный с помощью параметра `--image`.</span><span class="sxs-lookup"><span data-stu-id="d24fb-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="d24fb-152">В следующем примере создаются виртуальная машина с именем *myVM* из образа *myPackerImage* и ключи SSH, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="d24fb-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="d24fb-153">Создание виртуальной машины занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d24fb-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="d24fb-154">Когда виртуальная машина создана, запишите значение `publicIpAddress`, отображаемое в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d24fb-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="d24fb-155">Это адрес для доступа к сайту NGINX через веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="d24fb-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="d24fb-156">Чтобы разрешить передачу веб-трафика для виртуальной машины, откройте порт 80 для Интернета командой [az vm open-port](/cli/azure/vm#open-port).</span><span class="sxs-lookup"><span data-stu-id="d24fb-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="d24fb-157">Тестирование виртуальной машины и NGINX</span><span class="sxs-lookup"><span data-stu-id="d24fb-157">Test VM and NGINX</span></span>
<span data-ttu-id="d24fb-158">Теперь можно открыть веб-браузер и ввести в адресной строке `http://publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d24fb-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="d24fb-159">Укажите собственный общедоступный IP-адрес, настроенный при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d24fb-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="d24fb-160">Отобразится страница NGINX по умолчанию, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d24fb-160">The default NGINX page is displayed as in the following example:</span></span>

![Сайт nginx по умолчанию](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="d24fb-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d24fb-162">Next steps</span></span>
<span data-ttu-id="d24fb-163">В этом примере с помощью Packer вы создали образ виртуальной машины с уже установленным NGINX.</span><span class="sxs-lookup"><span data-stu-id="d24fb-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="d24fb-164">Этот образ виртуальной машины можно использовать наряду с имеющимися рабочими процессами развертывания, как например развертывание приложений на виртуальных машинах, созданных из образа с помощью Ansible, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="d24fb-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="d24fb-165">Дополнительный пример шаблонов Packer для других дистрибутивов Linux см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="d24fb-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>