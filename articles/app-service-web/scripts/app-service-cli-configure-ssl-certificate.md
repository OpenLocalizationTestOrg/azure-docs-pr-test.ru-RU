---
title: "Образец скрипта CLI - aaaAzure привязки пользовательских веб-приложения tooa SSL сертификат | Документы Microsoft"
description: "Пример сценария Azure CLI - привязка пользовательского приложения web tooa сертификат SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a>Привязка пользовательских веб-приложения tooa SSL сертификата

Этот образец скрипта создает веб-приложения в службе приложений с его связанные ресурсы, а затем привязывает hello SSL-сертификат tooit имя пользовательского домена. Для этого примера потребуется:

* Доступ к странице конфигурации регистратора домена tooyour DNS.
* Является допустимым. Сертификата PFX-файла и пароль для hello SSL требуется tooupload и привязку.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Создает план службы приложений. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Создает веб-приложение Azure. |
| [az webapp config hostname add](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | Сопоставляет пользовательский домен tooa веб-приложения. |
| [az webapp config ssl upload](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | Загружает веб-приложение tooa сертификат SSL. |
| [az webapp config ssl bind](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | Привязывает отправленного SSL сертификат tooa веб-приложение. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).
