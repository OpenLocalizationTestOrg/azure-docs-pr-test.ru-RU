---
title: "Создание виртуальной машины с несколькими сетевыми картами с помощью шаблона Azure Resource Manager | Документация Майкрософт"
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
ms.openlocfilehash: 85bfa264c6cf2b0586816a47b3ab72f3aee8ec96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="aecc9-103">Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="aecc9-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="aecc9-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aecc9-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="aecc9-105">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо [классической](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="aecc9-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="aecc9-106">В приведенных ниже действиях используются следующие группы ресурсов: *IaaSStory* для веб-серверов и *IaaSStory-BackEnd* для серверов базы данных.</span><span class="sxs-lookup"><span data-stu-id="aecc9-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aecc9-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aecc9-107">Prerequisites</span></span>
<span data-ttu-id="aecc9-108">Перед созданием серверов базы данных необходимо создать группу ресурсов *IaaSStory* со всеми ресурсами, необходимыми для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="aecc9-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="aecc9-109">Чтобы создать эти ресурсы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="aecc9-109">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="aecc9-110">Перейдите к [странице шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="aecc9-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="aecc9-111">На странице шаблона справа от **Родительская группа ресурсов** щелкните **Deploy to Azure** (Развернуть в Azure).</span><span class="sxs-lookup"><span data-stu-id="aecc9-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="aecc9-112">При необходимости измените значения параметров, а затем следуйте инструкциям на портале предварительной версии Azure для развертывания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aecc9-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aecc9-113">Имена учетных записей хранения должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="aecc9-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="aecc9-114">Они не могут повторяться в Azure.</span><span class="sxs-lookup"><span data-stu-id="aecc9-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-the-deployment-template"></a><span data-ttu-id="aecc9-115">Сведения о шаблоне развертывания</span><span class="sxs-lookup"><span data-stu-id="aecc9-115">Understand the deployment template</span></span>
<span data-ttu-id="aecc9-116">Перед развертыванием шаблона, предоставляемого с этой документацией, убедитесь, что вы понимаете, что он делает.</span><span class="sxs-lookup"><span data-stu-id="aecc9-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="aecc9-117">Следующие действия предоставляют хороший обзор шаблона.</span><span class="sxs-lookup"><span data-stu-id="aecc9-117">The following steps provide a good overview of the template:</span></span>

1. <span data-ttu-id="aecc9-118">Перейдите к [странице шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="aecc9-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="aecc9-119">Щелкните по файлу **azuredeploy.json** , чтобы открыть файл шаблона.</span><span class="sxs-lookup"><span data-stu-id="aecc9-119">Click **azuredeploy.json** to open the template file.</span></span>
3. <span data-ttu-id="aecc9-120">Обратите внимание на параметр *osType* , показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-120">Notice the *osType* parameter listed below.</span></span> <span data-ttu-id="aecc9-121">Этот параметр используется для выбора образа виртуальной машины сервера базы данных и нескольких параметров, связанных с операционной системой.</span><span class="sxs-lookup"><span data-stu-id="aecc9-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS to use for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="aecc9-122">Прокрутите список переменных и проверьте определение переменных **dbVMSetting** , перечисленных ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="aecc9-123">Он получает один из элементов массива, содержащегося в переменной **dbVMSettings** .</span><span class="sxs-lookup"><span data-stu-id="aecc9-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span></span> <span data-ttu-id="aecc9-124">Если вы знакомы с терминологией разработки программного обеспечения, переменные **dbVMSettings** можно считать хэш-таблицей или словарем.</span><span class="sxs-lookup"><span data-stu-id="aecc9-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="aecc9-125">Предположим, требуется развернуть виртуальные машины Windows с SQL в серверной части.</span><span class="sxs-lookup"><span data-stu-id="aecc9-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span></span> <span data-ttu-id="aecc9-126">Тогда значение **osType** должно быть равно *Windows*, и переменная **dbVMSetting** будет содержать элемент, показанный ниже, который представляет первое значение в переменной **dbVMSettings**.</span><span class="sxs-lookup"><span data-stu-id="aecc9-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span></span>

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

6. <span data-ttu-id="aecc9-127">Обратите внимание, что **vmSize** содержит значение *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="aecc9-127">Notice the **vmSize** contains the value *Standard_DS3*.</span></span> <span data-ttu-id="aecc9-128">С несколькими сетевыми адаптерами разрешается использовать только определенные размеры виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="aecc9-128">Only certain VM sizes allow for the use of multiple NICs.</span></span> <span data-ttu-id="aecc9-129">Чтобы проверить, какие размеры виртуальных машин поддерживают несколько сетевых интерфейсов, ознакомьтесь со статьями о размерах виртуальных машин [под управлением Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aecc9-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="aecc9-130">Прокрутите вниз до **ресурсов** и обратите внимание на первый элемент.</span><span class="sxs-lookup"><span data-stu-id="aecc9-130">Scroll down to **resources** and notice the first element.</span></span> <span data-ttu-id="aecc9-131">Он описывает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="aecc9-131">It describes a storage account.</span></span> <span data-ttu-id="aecc9-132">Эта учетная запись хранения будет использоваться для дисков данных, используемых в каждой виртуальной машине баз данных.</span><span class="sxs-lookup"><span data-stu-id="aecc9-132">This storage account will be used to maintain the data disks used by each database VM.</span></span> <span data-ttu-id="aecc9-133">В этом сценарии у каждой виртуальной машины баз данных есть диск ОС, который размещен в обычном хранилище, и два диска данных, размещенных в хранилище SSD (хранилище класса Premium).</span><span class="sxs-lookup"><span data-stu-id="aecc9-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

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

8. <span data-ttu-id="aecc9-134">Прокрутите вниз до следующего ресурса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-134">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="aecc9-135">Этот ресурс представляет сетевой адаптер, используемый для доступа к базе данных в каждой виртуальной машине баз данных.</span><span class="sxs-lookup"><span data-stu-id="aecc9-135">This resource represents the NIC used for database access in each database VM.</span></span> <span data-ttu-id="aecc9-136">Обратите внимание на использование функции **копирования** в этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="aecc9-136">Notice the use of the **copy** function in this resource.</span></span> <span data-ttu-id="aecc9-137">Этот шаблон позволяет развертывать столько виртуальных машин, сколько вы хотите, на основе параметра **dbCount** .</span><span class="sxs-lookup"><span data-stu-id="aecc9-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span></span> <span data-ttu-id="aecc9-138">Поэтому необходимо создать такое же количество сетевых адаптеров для доступа к базе данных, по одному для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aecc9-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span></span>

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

9. <span data-ttu-id="aecc9-139">Прокрутите вниз до следующего ресурса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-139">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="aecc9-140">Этот ресурс представляет сетевой адаптер, используемый для управления в каждой виртуальной машине баз данных.</span><span class="sxs-lookup"><span data-stu-id="aecc9-140">This resource represents the NIC used for management in each database VM.</span></span> <span data-ttu-id="aecc9-141">Опять же, для каждой виртуальной машины баз данных необходимо иметь один из этих сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="aecc9-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="aecc9-142">Обратите внимание на элемент **networkSecurityGroup** , связывающий сетевую группу безопасности, обеспечивающую доступ к RDP или SSH, только с этим сетевым адаптером.</span><span class="sxs-lookup"><span data-stu-id="aecc9-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span></span>

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

10. <span data-ttu-id="aecc9-143">Прокрутите вниз до следующего ресурса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-143">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="aecc9-144">Этот ресурс представляет группу доступности, которая будет общей для всех виртуальных машин в базе данных.</span><span class="sxs-lookup"><span data-stu-id="aecc9-144">This resource represents an availability set to be shared by all database VMs.</span></span> <span data-ttu-id="aecc9-145">Таким образом, можно гарантировать, что как минимум одна виртуальная машина в наборе всегда будет запущена во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="aecc9-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span></span>

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

11. <span data-ttu-id="aecc9-146">Прокрутите вниз до следующего ресурса.</span><span class="sxs-lookup"><span data-stu-id="aecc9-146">Scroll down to the next resource.</span></span> <span data-ttu-id="aecc9-147">Этот ресурс представляет виртуальные машины баз данных, как показано в первых нескольких строках, приведенных ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-147">This resource represents the database VMs, as seen in the first few lines listed below.</span></span> <span data-ttu-id="aecc9-148">Снова обратите внимание на функцию **копирования**, которая гарантирует, что на основе параметра **dbCount** создается несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="aecc9-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span></span> <span data-ttu-id="aecc9-149">Также обратите внимание на коллекцию **dependsOn** .</span><span class="sxs-lookup"><span data-stu-id="aecc9-149">Also notice the **dependsOn** collection.</span></span> <span data-ttu-id="aecc9-150">В ней два сетевых адаптера, которые необходимо создать до развертывания виртуальной машины, а также группа доступности и учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="aecc9-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span></span>

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

12. <span data-ttu-id="aecc9-151">Прокрутите вниз ресурс виртуальной машины до элемента **networkProfile** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span></span> <span data-ttu-id="aecc9-152">Обратите внимание, что для каждой виртуальной машины используются два сетевых адаптера.</span><span class="sxs-lookup"><span data-stu-id="aecc9-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="aecc9-153">При создании нескольких сетевых интерфейсов для виртуальной машины необходимо задать для свойства **primary** одного из сетевых интерфейсов значение *true*, а для остальных *false*.</span><span class="sxs-lookup"><span data-stu-id="aecc9-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span></span>

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

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="aecc9-154">Развертывание шаблона ARM с помощью кнопки развертывания</span><span class="sxs-lookup"><span data-stu-id="aecc9-154">Deploy the ARM template by using click to deploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aecc9-155">Перед выполнением следующих действий убедитесь, что вы выполнили [предварительные требования](#Pre-requisites) .</span><span class="sxs-lookup"><span data-stu-id="aecc9-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span></span>
> 

<span data-ttu-id="aecc9-156">Образец шаблона, который находится в общедоступном репозитории, использует файл параметров, содержащий значения по умолчанию для создания описанного выше сценария.</span><span class="sxs-lookup"><span data-stu-id="aecc9-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="aecc9-157">Чтобы развернуть этот шаблон, перейдите по [этой ссылке](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), щелкните **Deploy to Azure** (Развернуть в Azure) справа от **Группа внутренних ресурсов (см. документацию)**, при необходимости замените значения параметров по умолчанию и следуйте инструкциям на портале.</span><span class="sxs-lookup"><span data-stu-id="aecc9-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

<span data-ttu-id="aecc9-158">На следующем рисунке показано содержимое новой группы ресурсов после развертывания.</span><span class="sxs-lookup"><span data-stu-id="aecc9-158">The figure below shows the contents of the new resource group, after deployment.</span></span>

![Внутренняя группа ресурсов](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="aecc9-160">Развертывание шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="aecc9-160">Deploy the template by using PowerShell</span></span>
<span data-ttu-id="aecc9-161">Чтобы развернуть шаблон, скачанный с помощью PowerShell, установите и настройте PowerShell, выполнив действия, описанные в [этой статье](/powershell/azure/overview), а затем сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="aecc9-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article and then complete the following steps:</span></span>

<span data-ttu-id="aecc9-162">Запустите командлет **`New-AzureRmResourceGroup`** для создания группы ресурсов с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="aecc9-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="aecc9-163">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="aecc9-163">Expected output:</span></span>

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

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="aecc9-164">Развертывание шаблона с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="aecc9-164">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="aecc9-165">Чтобы развернуть шаблон с помощью интерфейса командной строки Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="aecc9-165">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="aecc9-166">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="aecc9-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="aecc9-167">Выполните команду **`azure config mode`** , чтобы переключиться в режим диспетчера ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="aecc9-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="aecc9-168">Ожидаемые выходные данные должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aecc9-168">The expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="aecc9-169">Откройте [файл параметров](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), выберите его содержимое и сохраните его в файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="aecc9-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="aecc9-170">В этом примере мы сохранили файл параметров в файл *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="aecc9-170">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="aecc9-171">Выполните командлет **`azure group deployment create`** , чтобы развернуть новую виртуальную сеть с помощью файлов шаблона и параметров, которые вы загрузили и изменили раньше.</span><span class="sxs-lookup"><span data-stu-id="aecc9-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="aecc9-172">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="aecc9-172">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="aecc9-173">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="aecc9-173">Expected output:</span></span>
   
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

