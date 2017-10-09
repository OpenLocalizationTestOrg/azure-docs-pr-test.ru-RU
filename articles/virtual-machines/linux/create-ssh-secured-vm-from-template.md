---
title: "aaaCreate виртуальной Машины Linux в Azure из шаблона | Документы Microsoft"
description: "Как toouse hello Azure CLI 2.0 toocreate ВМ Linux на основе шаблона диспетчера ресурсов"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Как toocreate виртуальной машины Linux с помощью шаблонов диспетчера ресурсов Azure
В этой статье показано, как tooquickly развертывание виртуальной машины (VM) Linux с помощью шаблонов диспетчера ресурсов Azure и Azure CLI 2.0 hello. Можно также выполнить следующие действия с hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Обзор шаблонов
Шаблоны Azure Resource Manager являются файлов JSON, которые определяют hello инфраструктурой и настройкой решение Azure. Этот шаблон можно использовать, чтобы повторно развертывать решение на протяжении всего его жизненного цикла и гарантировать, что ресурсы развертываются в согласованном состоянии. toolearn Дополнительные сведения о формате hello hello шаблона и при создании, в разделе [создать свой первый диспетчера ресурсов Azure](../../azure-resource-manager/resource-manager-create-first-template.md). hello tooview синтаксис JSON для типов ресурсов, в разделе [определения ресурсов в шаблоны Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Создать группу ресурсов
Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. Группу ресурсов следует создавать до виртуальной машины. Hello следующий пример создает группу ресурсов с именем *myResourceGroupVM* в hello *eastus* область:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины
Hello следующий пример создает виртуальную Машину [этого шаблона Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) с [создания развертывания группы az](/cli/azure/group/deployment#create). Укажите значение hello собственный открытый ключ SSH, такие как содержимое hello *~/.ssh/id_rsa.pub*. Если вам требуется toocreate пару ключей SSH, см. раздел [как toocreate и использование SSH пары ключей для виртуальных машин Linux в Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

В этом примере указан шаблон, хранящийся в GitHub. Можно также загрузить или создать шаблон и укажите локальный путь hello с hello же `--template-file` параметра.

tooSSH tooyour виртуальной Машины, получить hello общедоступный IP-адрес с [az сети public-ip show](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Затем вы сможете tooyour SSH виртуальной Машины в обычном режиме:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Дальнейшие действия
В этом примере вы создали базовую виртуальную машину Linux. Дополнительные шаблоны диспетчера ресурсов, включающие платформы приложений или создавать более сложные среды, Обзор hello [коллекции шаблонов Azure краткое руководство](https://azure.microsoft.com/documentation/templates/).
