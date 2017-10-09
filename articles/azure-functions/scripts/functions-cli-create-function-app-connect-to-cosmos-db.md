---
title: "Это функция Azure, которая подключается tooan Azure Cosmos DB aaaCreate | Документы Microsoft"
description: "Сценарий Azure CLI пример — создание это функция Azure, которая подключается tooan Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Создайте функцию Azure, которая подключается tooan Azure Cosmos DB

Этот образец скрипта создает функции приложения Azure и подключении базы данных Azure Cosmos DB tooan.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Пример скрипта

Этот образец приложения Azure функция создает и добавляет Cosmos DB конечной точки и доступа ключа tooapp параметров.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Очистка развертывания

После выполнения сценария образец hello hello выполните команду может быть группа ресурсов используется tooremove hello и все связанные ресурсы.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | TooAzure входа. |
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создайте группу ресурсов с расположением. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Создайте учетную запись хранения. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | Создайте приложение-функцию. |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | Создайте базу данных DocumentDB. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Очистка |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).




