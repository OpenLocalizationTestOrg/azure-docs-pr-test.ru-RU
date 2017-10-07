---
title: "Образец скрипта CLI - aaaAzure подключения tooa redis веб-приложения кэша | Документы Microsoft"
description: "Сценарий Azure CLI пример — подключить кэш redis tooa web app"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a>Подключение веб-приложения tooa redis кэша

В этом сценарии вы узнаете, как toocreate Azure redis кэша и Azure веб-приложение. Затем будет связан hello redis кэша toohello веб-приложения с помощью параметров приложения.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды redis toocreate группу ресурсов веб-приложения, кэш и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Создает план службы приложений. Это как ферма сервера для веб-приложения Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Создает веб-приложение Azure. |
| [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) | Создает экземпляр кэша Redis. Это происходит, где будут храниться данные hello. |
| [az redis list-keys](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | Список ключей доступа hello для экземпляра кэша redis hello. |
| [az webapp config appsettings set](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Создает или обновляет параметр приложения для веб-приложения Azure. Параметры приложения представляются в качестве переменных среды для приложения. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).
