---
title: "Пример сценария CLI - aaaAzure добавить приложение в пакете | Документы Microsoft"
description: "Пример сценария Azure CLI для добавления приложения в пакетную службу."
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Добавление приложений tooAzure пакета с помощью Azure CLI

Этот сценарий демонстрирует, как tooset приложения для использования в пуле пакетной службы Azure или задачи. tooset приложения, пакета исполняемого файла, вместе с зависимостями, в ZIP-файл. В данный пример hello исполняемый архив файл будет назван "my-приложения-exe.zip".

## <a name="prerequisites"></a>Предварительные требования

- Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.
- Создайте учетную запись пакетной службы, если у вас ее еще нет. В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Очистка приложения

После запуска hello выше пример сценария, запустите следующие команды tooremove hello приложения и все его отправленное приложение пакетов.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello приложения и отправка пакета приложения.
Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | Создает приложение.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | Обновляет свойства приложения.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Добавляет toohello пакета приложения указанного приложения.  |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).
