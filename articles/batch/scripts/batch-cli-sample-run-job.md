---
title: "Образец скрипта CLI - выполнении задания с использованием пакета aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI для выполнения задания в пакетной службе."
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Выполнение заданий в пакетной службе Azure с помощью Azure CLI

Этот скрипт создает пакетного задания и добавляет ряд задач toohello задания. Он также демонстрирует, как toomonitor задания и его задач. Наконец он показывает, как tooquery hello пакетная служба эффективно для получения сведений о hello рабочих заданий.

## <a name="prerequisites"></a>Предварительные требования

- Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.
- Создайте учетную запись пакетной службы, если у вас ее еще нет. В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.
- Настройте toorun приложения из задачи запуска, если это еще не было сделано. В разделе [Добавление приложений tooAzure пакета с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) приведен пример скрипта, создающий приложение и отправляет tooAzure пакета приложения.
- Настройте пул, на какие hello задание будет выполняться. Пример скрипта создания пула с использованием конфигурации облачной службы или конфигурации виртуальной машины см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Очистка задания

После запуска hello выше образец скрипта запуска hello, следующая команда tooremove задания и всех его задач. Обратите внимание, что пул hello будет toobe удалена отдельно. Дополнительные сведения о создании и удалении пулов см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](./batch-cli-sample-manage-pool.md).

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello пакетного задания и задачи. Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Выполняет аутентификацию учетной записи пакетной службы.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Создает задание пакетной службы.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Обновляет свойства задания пакетной службы.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Получает сведения об указанном задании пакетной службы.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Добавляет toohello задач указан пакетного задания.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Извлекает сведения hello задачи из hello указан пакетного задания.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Список задач hello, связанный с указанным заданием hello.  |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).
