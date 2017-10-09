---
title: "aaaCreate виртуальной Машины с несколькими сетевыми картами - шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Создание виртуальной машины с несколькими сетевыми картами с помощью шаблона Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="a0bb1-103">Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="a0bb1-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a0bb1-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a0bb1-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a0bb1-105">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a0bb1-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="a0bb1-106">Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0bb1-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0bb1-107">Prerequisites</span></span>
<span data-ttu-id="a0bb1-108">Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="a0bb1-109">завершить эти ресурсы toocreate hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="a0bb1-110">Перейдите в слишком[страницы шаблона hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="a0bb1-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="a0bb1-111">На странице шаблона hello, toohello справа от **родительской группы ресурсов**, нажмите кнопку **развертывание tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="a0bb1-112">При необходимости измените значения параметров hello, а затем выполните действия hello в группе ресурсов hello toodeploy портала предварительной версии Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0bb1-113">Имена учетных записей хранения должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="a0bb1-114">Они не могут повторяться в Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="a0bb1-115">Понять шаблон развертывания hello</span><span class="sxs-lookup"><span data-stu-id="a0bb1-115">Understand hello deployment template</span></span>
<span data-ttu-id="a0bb1-116">Прежде чем развертывать hello шаблона, поставляемого с этой документации, убедитесь, что вы понимаете, что он делает.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="a0bb1-117">следующие шаги Hello предоставляют хороший обзор hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="a0bb1-118">Перейдите в слишком[страницы шаблона hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="a0bb1-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="a0bb1-119">Нажмите кнопку **azuredeploy.json** tooopen файл шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="a0bb1-120">Обратите внимание hello *osType* параметров, перечисленных ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="a0bb1-121">Этот параметр не используется tooselect параметры, относящиеся к какой toouse образ виртуальной Машины для сервера базы данных hello, наряду с несколькими операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="a0bb1-122">Прокрутите вниз список toohello переменных и проверить определение hello для hello **dbVMSetting** переменные, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="a0bb1-123">Он получает один из элементов массива hello в hello **dbVMSettings** переменной.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="a0bb1-124">Если вы знакомы с терминологией разработки программного обеспечения, можно просмотреть hello **dbVMSettings** переменной как хэш-таблицу или словарь.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="a0bb1-125">Предположим, что вы решите toodeploy виртуальных машин Windows под управлением SQL в серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="a0bb1-126">Затем hello значение **osType** бы *Windows*и hello **dbVMSetting** переменной будет содержать элемент hello, перечисленные ниже, который представляет первое значение hello hello **dbVMSettings** переменной.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="a0bb1-127">Обратите внимание hello **vmSize** содержит значение hello *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="a0bb1-128">Только некоторые размеры виртуальной Машины позволяют использовать несколько сетевых адаптеров hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="a0bb1-129">Чтобы узнать, какие размеры виртуальных Машин поддерживает несколько сетевых адаптеров, считывая hello [размеры виртуальных Машин Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [размеры виртуальных Машин Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статей.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="a0bb1-130">Прокрутите список вниз слишком**ресурсов** и первый элемент hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="a0bb1-131">Он описывает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-131">It describes a storage account.</span></span> <span data-ttu-id="a0bb1-132">Эта учетная запись хранения будет дисков данных используется toomaintain hello, используемой каждой базой данных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="a0bb1-133">В этом сценарии у каждой виртуальной машины баз данных есть диск ОС, который размещен в обычном хранилище, и два диска данных, размещенных в хранилище SSD (хранилище класса Premium).</span><span class="sxs-lookup"><span data-stu-id="a0bb1-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="a0bb1-134">Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0bb1-135">Этот ресурс представляет hello сетевых Адаптеров используются для доступа к базе данных в каждой базе данных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="a0bb1-136">Использование уведомления hello hello **копирования** функция в этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="a0bb1-137">Hello шаблон позволяет toodeploy много виртуальных машин необходимо, на основе hello **dbCount** параметра.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="a0bb1-138">Следовательно, вы должны быть toocreate hello того же количества сетевых адаптеров для доступа к базе данных, один для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="a0bb1-139">Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0bb1-140">Этот ресурс представляет hello сетевых Адаптеров используются для управления в каждой базе данных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="a0bb1-141">Опять же, для каждой виртуальной машины баз данных необходимо иметь один из этих сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="a0bb1-142">Обратите внимание hello **networkSecurityGroup** элемент, связывание NSG, который позволяет доступ toothis tooRDP/SSH сетевой Адаптер только.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="a0bb1-143">Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0bb1-144">Этот ресурс представляет toobe набор доступности совместно используется всеми виртуальными машинами базы данных.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="a0bb1-145">Таким образом, вы гарантирует, что всегда будет существовать одна виртуальная машина в hello задать во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="a0bb1-146">Прокрутите вниз toohello следующего ресурса.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="a0bb1-147">Этот ресурс представляет hello базы данных виртуальных машин, как показано в hello первые несколько строк, перечисленных ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="a0bb1-148">Использование уведомления hello hello **копирования** функция, гарантируя, что создаются несколько виртуальных машин на основании hello **dbCount** параметра.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="a0bb1-149">Также Обратите внимание, hello **dependsOn** коллекции.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="a0bb1-150">В нем перечислены два сетевых адаптера, необходимые toobe создан до hello, развернутых виртуальных Машин вместе с набор доступности hello и hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="a0bb1-151">Прокрутите вниз toohello ресурсов виртуальной Машины hello **параметров масштабирования виртуальных** элемента, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="a0bb1-152">Обратите внимание, что для каждой виртуальной машины используются два сетевых адаптера.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="a0bb1-153">При создании нескольких сетевых адаптеров для виртуальной Машины, необходимо задать hello **основной** свойство одного из сетевых адаптеров hello слишком*true*, и hello rest слишком*false*.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="a0bb1-154">Развертывание с помощью шаблона hello ARM щелкните toodeploy</span><span class="sxs-lookup"><span data-stu-id="a0bb1-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0bb1-155">Убедитесь, что вы выполните hello [предварительным](#Pre-requisites) действия, прежде чем следовать приведенным ниже инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="a0bb1-156">шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="a0bb1-157">toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello справа от **внутренний ресурс группы (см. документацию)** щелкните **развертывание tooAzure**, замените Здравствуйте, значения параметров по умолчанию, при необходимости и следуйте инструкциям hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="a0bb1-158">на следующем рисунке Hello показано содержимое hello hello группы ресурсов, после развертывания.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Внутренняя группа ресурсов](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="a0bb1-160">Развертывание hello шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0bb1-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="a0bb1-161">шаблон toodeploy hello, загруженный с помощью PowerShell, установите и настройте PowerShell, выполнив шаги hello в hello [установите и настройте PowerShell](/powershell/azure/overview) статьи, а затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="a0bb1-162">Запустите hello  **`New-AzureRmResourceGroup`**  toocreate командлет группы ресурсов с помощью hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="a0bb1-163">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="a0bb1-164">Развертывание hello шаблона с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0bb1-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="a0bb1-165">toodeploy hello шаблона с использованием hello Azure CLI, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="a0bb1-166">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a0bb1-167">Запустите hello  **`azure config mode`**  tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a0bb1-168">Hello ожидается вывод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="a0bb1-169">Откройте hello [файл параметров](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), выберите его содержимое и сохраните файл tooa на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="a0bb1-170">В этом примере мы сохранить файл параметров hello слишком*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="a0bb1-171">Запустите hello  **`azure group deployment create`**  файлы новой виртуальной сети с помощью шаблонов hello и параметров командлета toodeploy hello вы загрузили и изменить выше.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="a0bb1-172">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="a0bb1-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="a0bb1-173">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a0bb1-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

