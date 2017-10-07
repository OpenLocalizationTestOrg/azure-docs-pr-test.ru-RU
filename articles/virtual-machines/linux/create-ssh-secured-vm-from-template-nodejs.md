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
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Как toocreate в виртуальной Машине Linux с помощью hello Azure CLI 1.0 шаблона диспетчера ресурсов Azure
В этой статье показано, как tooquickly развернуть виртуальную машину Linux, используя hello Azure CLI 1.0 и шаблона диспетчера ресурсов Azure. требуются Hello статьи:

* Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [Azure CLI 1.0](../../cli-install-nodejs.md) вход в систему `azure login`.
* Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.

Можно также быстро развернуть шаблон виртуальной Машины Linux с помощью hello [портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-command-summary) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="quick-command-summary"></a>Краткая сводка по командам
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство
Шаблоны позволяют вам toocreate виртуальные машины в Azure с параметрами, которые должны toocustomize во время запуска hello, параметры, такие как имена пользователей и имена узлов. В этой статье мы запустим шаблон Azure с использованием виртуальной машины Ubuntu и группы безопасности сети (NSG) с портом 22, открытым для SSH.

Шаблоны Azure Resource Manager — это JSON-файлы, которые можно использовать для простых задач, таких как однократный запуск виртуальной машины Ubuntu, как в нашем примере.  Шаблоны Azure также может быть сложных конфигураций Azure используется tooconstruct всего сред как стек тестирования, разработки или рабочей среде развертывания.

## <a name="create-hello-linux-vm"></a>Создание виртуальной Машины с Linux hello
Здравствуйте, следуя примере кода показано, как toocall `azure group create` toocreate ресурса группы и развертывание защищенных SSH ВМ Linux на hello используя [этого шаблона диспетчера ресурсов Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Помните, что в данном примере необходим toouse имена, которые являются уникальными tooyour среды. В этом примере используется *myResourceGroup* как имя группы ресурсов hello и *myVM* как имя виртуальной Машины hello.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

Hello результат должен выглядеть hello после блока выходных данных:

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

Этот пример развертывания ВМ с помощью hello `--template-uri` параметра.  Можно также загрузить или создать шаблон локально и передать hello шаблон, использующий hello `--template-file` параметр с использованием файла шаблона toohello пути в качестве аргумента. Hello Azure CLI запросит hello параметры, необходимые для шаблона hello.

## <a name="next-steps"></a>Дальнейшие действия
Поиск hello [коллекции шаблонов](https://azure.microsoft.com/documentation/templates/) toodiscover toodeploy платформ какие приложения далее.

