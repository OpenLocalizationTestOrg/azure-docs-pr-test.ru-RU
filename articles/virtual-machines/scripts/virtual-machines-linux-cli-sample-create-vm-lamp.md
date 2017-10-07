---
title: "Пример сценария CLI - aaaAzure развертывание hello стек LAMP в Load-Balanced виртуальную компьюте Мя_входа наборе масштабирования | Документы Microsoft"
description: "Использовать пользовательский сценарий расширения toodeploy hello стек LAMP загрузки = сбалансированная масштабирования виртуальных машин на Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Развертывание стек LAMP hello в наборе масштабирования виртуальных машин с балансировкой нагрузки

В этом примере создается набор масштабирования виртуальной машины и применяет расширение, работающей на каждую виртуальную машину в наборе масштабирования hello стек LAMP hello toodeploy пользовательского скрипта.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Подключение

Используйте этот код toosee, как задать tooconnect tooyour виртуальных машин и масштаба.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Запустите следующие группы ресурсов hello tooremove команд, hello набор масштабирования и виртуальные машины и все связанные ресурсы hello.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Создает масштабируемый набор виртуальных машин. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Добавляет конечную точку с балансировкой нагрузки. |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Создание расширения hello, выполняет пользовательский скрипт hello развертывания виртуальной машины |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Проведение hello экземпляров виртуальных Машин, которые были развернуты до применения hello расширение пользовательского скрипта hello toohello набора масштабирования. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Вертикальное масштабирование шкалы hello, задать, добавив дополнительные экземпляры виртуальной Машины. Hello пользовательского скрипта выполняется на их при развертывании. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Получение IP-адреса hello hello виртуальные машины, созданные в образце hello. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Получение hello внешнего и внутреннего порты, используемые подсистемой балансировки нагрузки hello. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
