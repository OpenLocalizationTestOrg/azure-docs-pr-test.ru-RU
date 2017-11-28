---
title: "aaaCreate и управление виртуальными машинами в DevTest Labs с Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate toouse Azure DevTest Labs и управление виртуальными машинами с помощью Azure CLI 2.0"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="af582-103">Создание и управление виртуальными машинами с помощью hello Azure CLI DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="af582-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="af582-104">В этом кратком руководстве описан процесс создания, запуска, подключения, обновления и очистки виртуальной машины для разработки в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="af582-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="af582-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="af582-105">Before you begin:</span></span>

* <span data-ttu-id="af582-106">Если лаборатория еще не создана, ознакомьтесь с инструкциями в [этой статье](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="af582-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="af582-107">[Установите CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af582-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="af582-108">toostart входа toocreate выполнения az соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="af582-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="af582-109">Создать и проверить hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="af582-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="af582-110">Создайте виртуальную машину с проверкой подлинности по протоколу SSH из образа в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af582-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="af582-111">Поместите hello **группы ресурсов lab** в hello--параметр группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="af582-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="af582-112">Toocreate ВМ с помощью формулы, использовать hello--параметр формулы в [создания виртуальной машины лаборатории az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="af582-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="af582-113">Проверьте, что hello виртуальной Машины доступен.</span><span class="sxs-lookup"><span data-stu-id="af582-113">Verify that hello VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="af582-114">Запуск и подключение виртуальной машины toohello</span><span class="sxs-lookup"><span data-stu-id="af582-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="af582-115">Запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="af582-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="af582-116">Поместите hello **группы ресурсов lab** в hello--параметр группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="af582-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="af582-117">Подключение виртуальной Машины tooa: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) или [удаленного рабочего стола](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="af582-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="af582-118">Обновить виртуальную машину hello</span><span class="sxs-lookup"><span data-stu-id="af582-118">Update hello virtual machine</span></span>
<span data-ttu-id="af582-119">Примените tooa артефактов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="af582-119">Apply artifacts tooa VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="af582-120">Список артефактов, входящих в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="af582-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="af582-121">Остановка и удаление hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="af582-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="af582-122">Остановите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="af582-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="af582-123">Удалите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="af582-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]