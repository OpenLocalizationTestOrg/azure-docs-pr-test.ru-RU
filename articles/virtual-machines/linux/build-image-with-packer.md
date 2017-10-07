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
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Как виртуальная машина Linux toocreate toouse Packer образы в Azure
Каждой виртуальной машины (VM) в Azure создается из образа, определяющего hello дистрибутив Linux и версию операционной системы. Образы могут содержать предварительно установленные приложения и конфигурации. Hello Azure Marketplace предоставляет большое количество изображений первый и сторонних разработчиков для наиболее общие распределения и среды приложения или можно создать адаптированные пользовательских образов tooyour потребностями. В этой статье описаны как toouse Привет открыть инструмент источника [Packer](https://www.packer.io/) toodefine и построения пользовательских образов в Azure.


## <a name="create-azure-resource-group"></a>Создание группы ресурсов Azure
Во время сборки hello Packer создает временные ресурсы Azure, при построении hello исходной виртуальной Машины. toocapture, исходной виртуальной Машины для использования в качестве образа, необходимо определить группу ресурсов. Hello выходные данные процесса сборки hello Packer хранится в этой группе ресурсов.

Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Создание учетных данных Azure
Packer выполняет проверку подлинности с помощью субъекта-службы Azure. Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer. Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.

Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется Packer выходные данные:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Пример выходных данных hello hello предшествующий команды выглядит следующим образом:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, необходимо также идентификатор подписки Azure с tooobtain [az учетной записи, отображают](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

В следующем шаге hello используйте hello выходные данные этих двух команд.


## <a name="define-packer-template"></a>Определение шаблона Packer
toobuild изображения, нужно создать шаблон в формате JSON. В шаблоне hello определения построители и provisioners, выполняющих hello фактический процесс построения. Имеет packer [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html) , позволяющий toodefine Azure ресурсы, такие как службы основной hello учетных данных, созданных в предыдущих шага hello.

Создайте файл с именем *ubuntu.json* и вставить hello после содержимого. Ввести собственные значения для следующего hello:

| Параметр                           | Где tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Первая строка выходных данных из `az ad sp` создает команду *appId* |
| *client_secret*                     | Вторая строка выходных данных из `az ad sp` создает команду *password* |
| *tenant_id*                         | Третья строка выходных данных из `az ad sp` создает команду *tenant* |
| *subscription_id*                   | Выходные данные команды `az account show` |
| *managed_image_resource_group_name* | Имя группы ресурсов, созданный на первом шаге hello |
| *managed_image_name*                | Имя образа hello управляемого диска, который создается |


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

Этот шаблон создает изображение Ubuntu 16.04 LTS, устанавливает NGINX, а затем deprovisions hello виртуальной Машины.

> [!NOTE]
> Если развернуть на учетные данные пользователя tooprovision этот шаблон, настроить hello средство подготовки команды, deprovisions hello tooread агент Azure `-deprovision` вместо `deprovision+user`.
> Hello `+user` флаг удаляет все учетные записи пользователей из hello исходной виртуальной Машины.


## <a name="build-packer-image"></a>Создание образа Packer
Если у вас еще нет Packer установлен на локальном компьютере, [следуйте инструкциям по установке hello Packer](https://www.packer.io/docs/install/index.html).

Для создания образа hello задайте вашей Packer файл шаблона следующим образом:

```bash
./packer build ubuntu.json
```

Пример выходных данных hello hello предшествующий команды выглядит следующим образом:

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


## <a name="create-vm-from-azure-image"></a>Создание виртуальной машины на основе образа Azure
Теперь можно создать виртуальную машину из образа с помощью команды [az vm create](/cli/azure/vm#create). Укажите образ, созданный с помощью hello hello `--image` параметра. Hello следующий пример создает Виртуальную машину с именем *myVM* из *myPackerImage* и создает ключи SSH, если они еще не существует:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Занимает несколько минут toocreate hello виртуальной Машины. После создания виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI. Этот адрес будет используется tooaccess hello NGINX сайта из веб-браузера.

tooallow веб-трафика tooreach виртуальной Машины, откройте порт 80 с hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Тестирование виртуальной машины и NGINX
Теперь можно открыть веб-браузер и введите `http://publicIpAddress` в адресную строку hello. Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс. Откроется страница NGINX по умолчанию Hello как hello в следующем примере:

![Сайт nginx по умолчанию](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Дальнейшие действия
В этом примере используется Packer toocreate образ виртуальной Машины с NGINX уже установлена. Можно использовать этот образ виртуальной Машины наряду с существующие рабочие процессы развертывания, например toodeploy tooVMs вашего приложения, созданные на основе hello изображение с Ansible, Chef или Puppet.

Дополнительный пример шаблонов Packer для других дистрибутивов Linux см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).