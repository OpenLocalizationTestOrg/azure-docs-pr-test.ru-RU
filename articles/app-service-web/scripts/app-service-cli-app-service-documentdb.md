---
title: "Пример сценария Azure CLI. Подключение веб-приложения к Cosmos DB | Документация Майкрософт"
description: "Пример сценария Azure CLI для подключения веб-приложения к Cosmos DB."
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a>Подключение веб-приложения к Cosmos DB

В этом сценарии вы узнаете, как создать учетную запись Azure Cosmos DB и веб-приложение Azure. Затем вы свяжете Cosmos DB с веб-приложением, используя параметры приложения.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Описание скрипта

Для создания группы ресурсов, веб-приложений, базы данных Cosmos DB и всех связанных ресурсов этот сценарий использует следующие команды. Для каждой команды в таблице приведены ссылки на соответствующую документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Создает план службы приложений. Это как ферма сервера для веб-приложения Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Создает веб-приложение Azure. |
| [az cosmosdb create](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | Создает учетную запись Cosmos DB. Здесь будут храниться данные. |
| [az cosmosdb list-keys](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | Выводит список ключей доступа для указанной учетной записи базы данных база данных. |
| [az webapp config appsettings set](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Создает или обновляет параметр приложения для веб-приложения Azure. Параметры приложения представляются в качестве переменных среды для приложения. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).
