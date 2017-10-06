---
title: "aaaAzure образец скрипта CLI - Управление пулами в пакете | Документы Microsoft"
description: "Пример скрипта Azure CLI для управления пулами в пакетной службе"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Управление пулами пакетной службы Azure с помощью Azure CLI

Эти сценарий демонстрирует некоторые hello средства, доступные в Azure CLI toocreate hello и Управление пулами вычислительных узлов в hello пакетной службы Azure.

> [!NOTE]
> Hello команды в этом примере создают виртуальные машины Azure. Работающих виртуальных машин будет начисляется плата за счет tooyour. После завершения выполнения образца hello toominimize выставления счетов удалить hello виртуальных машин. См. раздел [Очистка пулов](#clean-up-pools).

Пулы пакетной службы можно настроить двумя способами: с помощью настройки облачных служб (только для Windows) или настройки виртуальных машин (для Windows и Linux). Следующие скрипты образца Hello показывают, как toocreate пулы с обеих конфигураций.

## <a name="prerequisites"></a>Предварительные требования

- Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.
- Создайте учетную запись пакетной службы, если у вас ее еще нет. В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.
- Настройте toorun приложения из задачи запуска, если это еще не было сделано. В разделе [Добавление приложений tooAzure пакета с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) приведен пример скрипта, создающий приложение и отправляет tooAzure пакета приложения.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Пример скрипта для пула с настройкой облачной службы

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Пример скрипта для пула с настройкой виртуальной машины

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Очистка пулов

После запуска hello выше образец скрипта запуска hello, следующая команда toodelete hello пулов.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello и манипулировать пулы пакета.
Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Проверка подлинности учетной записи пакетной службы.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Список доступных приложений hello в hello пакетной учетной записи.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | Создание пула виртуальных машин.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | Обновление свойств пула.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Отображение списка доступных номеров SKU агента узла и сведений об образе.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Изменение размера hello количество работающих виртуальных машин в hello указано пула.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | Отображение свойств hello пула.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Удалить hello указанного пула.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Включение автоматического масштабирования в пуле и применение формулы.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Отключение автоматического масштабирования в пуле.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | Список всех hello вычислительных узлов в hello указанного пула.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Перезагрузите hello указанного вычислительных узлов.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | Узлы в списке hello Delete из hello указаны пула.  |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).

