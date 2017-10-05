---
title: "Создание виртуальной машины Linux с помощью шаблона Azure и Azure CLI 1.0 | Документация Майкрософт"
description: "Создание виртуальной машины Linux в Azure с помощью Azure CLI 1.0 и шаблона Azure Resource Manager."
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
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="ef324-103">Как создать виртуальную машину Linux с помощью Azure CLI 1.0 и шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef324-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="ef324-104">В этой статье показано, как быстро развернуть виртуальную машину Linux с помощью Azure CLI 1.0 и шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef324-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="ef324-105">Для работы с этой статьей потребуется:</span><span class="sxs-lookup"><span data-stu-id="ef324-105">The article requires:</span></span>

* <span data-ttu-id="ef324-106">Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="ef324-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="ef324-107">[Azure CLI 1.0](../../cli-install-nodejs.md) с выполненным входом (с помощью команды `azure login`).</span><span class="sxs-lookup"><span data-stu-id="ef324-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="ef324-108">Интерфейс командной строки Azure *нужно* переключить в режим Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="ef324-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="ef324-109">Вы также можете быстро развернуть шаблон виртуальной машины Linux с помощью [портала Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef324-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ef324-110">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="ef324-110">CLI versions to complete the task</span></span>
<span data-ttu-id="ef324-111">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="ef324-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ef324-112">[Azure CLI 1.0](#quick-command-summary) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="ef324-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ef324-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef324-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="ef324-114">Краткая сводка по командам</span><span class="sxs-lookup"><span data-stu-id="ef324-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ef324-115">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="ef324-115">Detailed Walkthrough</span></span>
<span data-ttu-id="ef324-116">Шаблоны позволяют создавать виртуальные машины в Azure с параметрами, которые можно настроить во время запуска, включая имена пользователей и имена узлов.</span><span class="sxs-lookup"><span data-stu-id="ef324-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="ef324-117">В этой статье мы запустим шаблон Azure с использованием виртуальной машины Ubuntu и группы безопасности сети (NSG) с портом 22, открытым для SSH.</span><span class="sxs-lookup"><span data-stu-id="ef324-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="ef324-118">Шаблоны Azure Resource Manager — это JSON-файлы, которые можно использовать для простых задач, таких как однократный запуск виртуальной машины Ubuntu, как в нашем примере.</span><span class="sxs-lookup"><span data-stu-id="ef324-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="ef324-119">Шаблоны Azure можно также использовать при создании сложных конфигураций Azure на уровне среды (для сред тестирования и разработки, а также для стеков развертывания в рабочих средах).</span><span class="sxs-lookup"><span data-stu-id="ef324-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="ef324-120">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="ef324-120">Create the Linux VM</span></span>
<span data-ttu-id="ef324-121">В следующем примере кода показано, как вызвать `azure group create` , чтобы одновременно создать группу ресурсов и развернуть виртуальную машину Linux, защищенную с помощью SSH, используя [этот шаблон Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ef324-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="ef324-122">Помните, что в данном примере необходимо использовать имена, уникальные для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="ef324-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="ef324-123">В этом примере *myResourceGroup* используется как имя группы ресурсов и *myVM* — как имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ef324-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="ef324-124">В результате должен отобразиться следующий блок выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ef324-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
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

<span data-ttu-id="ef324-125">В этом примере виртуальная машина развертывается с помощью параметра `--template-uri` .</span><span class="sxs-lookup"><span data-stu-id="ef324-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="ef324-126">Вы также можете скачать или создать шаблон локально, а затем передать его с помощью параметра `--template-file` , указав в качестве аргумента путь к файлу шаблона.</span><span class="sxs-lookup"><span data-stu-id="ef324-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="ef324-127">Azure CLI запрашивает параметры, необходимые для шаблона.</span><span class="sxs-lookup"><span data-stu-id="ef324-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef324-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef324-128">Next steps</span></span>
<span data-ttu-id="ef324-129">В [коллекции шаблонов](https://azure.microsoft.com/documentation/templates/) вы сможете найти другие платформы приложений для развертывания.</span><span class="sxs-lookup"><span data-stu-id="ef324-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

