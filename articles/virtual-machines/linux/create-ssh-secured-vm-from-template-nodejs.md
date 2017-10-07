---
title: "aaaCreate ВМ Linux с помощью шаблона Azure с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Создание виртуальной Машины Linux в Azure, с помощью Azure CLI 1.0 hello и шаблона диспетчера ресурсов Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="b1191-103">Как toocreate в виртуальной Машине Linux с помощью hello Azure CLI 1.0 шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b1191-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="b1191-104">В этой статье показано, как tooquickly развернуть виртуальную машину Linux, используя hello Azure CLI 1.0 и шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b1191-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="b1191-105">требуются Hello статьи:</span><span class="sxs-lookup"><span data-stu-id="b1191-105">hello article requires:</span></span>

* <span data-ttu-id="b1191-106">Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="b1191-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b1191-107">Hello [Azure CLI 1.0](../../cli-install-nodejs.md) вход в систему `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b1191-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b1191-108">Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b1191-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="b1191-109">Можно также быстро развернуть шаблон виртуальной Машины Linux с помощью hello [портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1191-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b1191-110">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="b1191-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b1191-111">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="b1191-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b1191-112">[Azure CLI 1.0](#quick-command-summary) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="b1191-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b1191-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="b1191-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="b1191-114">Краткая сводка по командам</span><span class="sxs-lookup"><span data-stu-id="b1191-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b1191-115">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="b1191-115">Detailed Walkthrough</span></span>
<span data-ttu-id="b1191-116">Шаблоны позволяют вам toocreate виртуальные машины в Azure с параметрами, которые должны toocustomize во время запуска hello, параметры, такие как имена пользователей и имена узлов.</span><span class="sxs-lookup"><span data-stu-id="b1191-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="b1191-117">В этой статье мы запустим шаблон Azure с использованием виртуальной машины Ubuntu и группы безопасности сети (NSG) с портом 22, открытым для SSH.</span><span class="sxs-lookup"><span data-stu-id="b1191-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="b1191-118">Шаблоны Azure Resource Manager — это JSON-файлы, которые можно использовать для простых задач, таких как однократный запуск виртуальной машины Ubuntu, как в нашем примере.</span><span class="sxs-lookup"><span data-stu-id="b1191-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="b1191-119">Шаблоны Azure также может быть сложных конфигураций Azure используется tooconstruct всего сред как стек тестирования, разработки или рабочей среде развертывания.</span><span class="sxs-lookup"><span data-stu-id="b1191-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="b1191-120">Создание виртуальной Машины с Linux hello</span><span class="sxs-lookup"><span data-stu-id="b1191-120">Create hello Linux VM</span></span>
<span data-ttu-id="b1191-121">Здравствуйте, следуя примере кода показано, как toocall `azure group create` toocreate ресурса группы и развертывание защищенных SSH ВМ Linux на hello используя [этого шаблона диспетчера ресурсов Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b1191-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="b1191-122">Помните, что в данном примере необходим toouse имена, которые являются уникальными tooyour среды.</span><span class="sxs-lookup"><span data-stu-id="b1191-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="b1191-123">В этом примере используется *myResourceGroup* как имя группы ресурсов hello и *myVM* как имя виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="b1191-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="b1191-124">Hello результат должен выглядеть hello после блока выходных данных:</span><span class="sxs-lookup"><span data-stu-id="b1191-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="b1191-125">Этот пример развертывания ВМ с помощью hello `--template-uri` параметра.</span><span class="sxs-lookup"><span data-stu-id="b1191-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="b1191-126">Можно также загрузить или создать шаблон локально и передать hello шаблон, использующий hello `--template-file` параметр с использованием файла шаблона toohello пути в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="b1191-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="b1191-127">Hello Azure CLI запросит hello параметры, необходимые для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b1191-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1191-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1191-128">Next steps</span></span>
<span data-ttu-id="b1191-129">Поиск hello [коллекции шаблонов](https://azure.microsoft.com/documentation/templates/) toodiscover toodeploy платформ какие приложения далее.</span><span class="sxs-lookup"><span data-stu-id="b1191-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

