---
title: "aaaAzure образец скрипта CLI - сопоставить приложении функция tooa личного домена | Документы Microsoft"
description: "Azure CLI образец скрипта - карты приложении функция tooa настраиваемого домена в Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a>Карта приложении функция tooa пользовательского домена

Этот скрипт создает функцию приложение с ресурсами и затем отображает `www.<yourdomain>` tooit. toomap tooa пользовательского домена, функция приложения должны создаваться в плане обслуживания приложений, а не в план потребления. Функции Azure поддерживают сопоставление личного домена только с помощью записи A.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Создает учетную запись хранилища, необходимый приложению функции hello. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Создает пользовательский домен toomap требуется план служб приложений. |
| [az functionapp create]() | Создает приложение-функцию. |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Сопоставляет приложении функция tooa пользовательского домена. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные примеры сценариев, использующих функции CLI можно найти в hello [документации Azure функции]().
