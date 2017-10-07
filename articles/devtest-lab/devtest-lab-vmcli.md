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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Создание и управление виртуальными машинами с помощью hello Azure CLI DevTest Labs
В этом кратком руководстве описан процесс создания, запуска, подключения, обновления и очистки виртуальной машины для разработки в лаборатории. 

Перед началом работы

* Если лаборатория еще не создана, ознакомьтесь с инструкциями в [этой статье](devtest-lab-create-lab.md).

* [Установите CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart входа toocreate выполнения az соединения с Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Создать и проверить hello виртуальной машины 
Создайте виртуальную машину с проверкой подлинности по протоколу SSH из образа в Marketplace.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Поместите hello **группы ресурсов lab** в hello--параметр группы ресурсов.
>

Toocreate ВМ с помощью формулы, использовать hello--параметр формулы в [создания виртуальной машины лаборатории az](https://docs.microsoft.com/cli/azure/lab/vm#create).


Проверьте, что hello виртуальной Машины доступен.
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

## <a name="start-and-connect-toohello-virtual-machine"></a>Запуск и подключение виртуальной машины toohello
Запустите виртуальную машину.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Поместите hello **группы ресурсов lab** в hello--параметр группы ресурсов.
>

Подключение виртуальной Машины tooa: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) или [удаленного рабочего стола](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Обновить виртуальную машину hello
Примените tooa артефактов виртуальной Машины.
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

Список артефактов, входящих в лаборатории hello.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Остановка и удаление hello виртуальной машины    
Остановите виртуальную машину.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Удалите виртуальную машину.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]