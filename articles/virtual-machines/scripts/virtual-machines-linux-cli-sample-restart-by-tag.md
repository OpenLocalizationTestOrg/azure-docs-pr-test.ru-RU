---
title: "aaaAzure образец скрипта CLI - перезапустить виртуальные машины | Документы Microsoft"
description: "Пример сценария Azure CLI. Перезапуск виртуальных машин с использованием тега и идентификатора"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Перезапуск виртуальных машин

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

В этом примере показано два способа tooget некоторые виртуальные машины и перезапустить их.

Сначала Hello перезапускает все виртуальные машины hello в группе ресурсов hello.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Hello второй возвращает hello тегом виртуальных машин с помощью `az resouce list` фильтрует toohello ресурсы, которые являются виртуальными машинами и перезапускает этих виртуальных машин.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Этот пример работает в оболочке Bash. Параметры запуска на клиенте Windows Azure CLI скриптов см [работающих в Windows Azure CLI hello](../windows/cli-options.md).


## <a name="sample-script"></a>Пример скрипта

Образец Hello имеет три сценарии.
Здравствуйте, первый из них обеспечивать hello виртуальные машины.
Он использует параметр ожидания нет hello, поэтому команда hello возвращается без ожидания на каждой виртуальной Машины, toobe подготовлены.
Во-вторых Hello ожидает полной подготовки toobe ВМ hello.
Третий сценарий Hello перезапускает все виртуальные машины hello, которые были подготовлены, а затем просто hello тегами для виртуальных машин.

### <a name="provision-hello-vms"></a>Hello подготовки виртуальных машин

Этот скрипт создает группу ресурсов, а затем он создает toorestart три виртуальные машины.
Две из них имеют теги.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Ожидание

Этот сценарий проверяет состояние подготовки каждые 20 секунд, пока все три виртуальных машин или один из них происходит сбой tooprovision hello.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Перезапустите hello виртуальные машины

Этот сценарий перезапускает все виртуальные машины hello в группе ресурсов hello и перезапускает только виртуальные машины с тегами hello.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

После выполнения сценария образец hello hello, следующая команда может быть групп ресурсов используется tooremove hello, виртуальные машины и все связанные ресурсы.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Создает hello виртуальных машин.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | При использовании `--query` hello tooensure виртуальных машин, подготавливаются перед перезапуском их, а затем tooget hello идентификаторы toorestart hello виртуальных машин их. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | При использовании `--query` tooget hello идентификаторы hello виртуальных машин с помощью тега hello. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Перезапускает ВМ hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
