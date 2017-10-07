---
title: "Пример сценария CLI - hello hostname Get, порты и ключи для кэша Azure Redis aaaAzure | Документы Microsoft"
description: "Azure CLI образец скрипта - Get hello hostname, порты и ключи для экземпляра кэша Redis для Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Получить имя узла hello, порты и ключи для кэша Redis для Azure

В этом сценарии вы узнаете, способ использования экземпляра кэша Azure Redis tooan tooconnect tooretrieve hello hostname, порты и ключей.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды tooretrieve hello hostname, ключи и порты для экземпляра кэша Redis для Azure hello. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Извлекает сведения об экземпляре кэша Redis для Azure. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Извлекает ключи доступа для экземпляра кэша Redis для Azure. |


## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные образцы сценариев CLI кэша Redis Azure можно найти в hello [документации кэш Azure Redis](../cli-samples.md).
