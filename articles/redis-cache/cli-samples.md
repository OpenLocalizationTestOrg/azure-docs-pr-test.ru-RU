---
title: "Примеры кэша Redis для Azure CLI | Документы Майкрософт"
description: "Примеры Azure CLI для кэша Redis для Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a0f3b294f2a655a5ff891d4fd1be9137080349a6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a>Примеры Azure CLI для кэша Redis для Azure

В следующей таблице содержатся ссылки на скрипты Bash, созданные с помощью Azure CLI.

| | |
|---|---|
|**Создание кэша**||
| [Создание кэша](./scripts/create-cache.md) | Создает группу ресурсов и базовый уровень кэша Redis для Azure. |
| [Создание кэша уровня "Премиум" с кластеризацией](./scripts/create-premium-cache-cluster.md) | Создает группу ресурсов и кэш уровня "Премиум" с включенной кластеризацией.|
| [Получение сведений о кэше](./scripts/show-cache.md) | Возвращает сведения об экземпляре кэша Redis для Azure, включая состояние подготовки. |
| [Получение имени узла, портов и ключей](./scripts/cache-keys-ports.md) | Возвращает имя узла, порты и ключи для экземпляра кэша Redis для Azure. |
|**Веб-приложение и кэш**||
| [Подключение веб-приложения к кэшу Redis](./../app-service/scripts/app-service-cli-app-service-redis.md) | Создает веб-приложение Azure и кэш Redis, а затем добавляет сведения о подключении кэша Redis в параметры приложения. |
|**Удаление кэша**||
| [Удаление кэша](./scripts/delete-cache.md) | Удаляет экземпляр кэша Redis для Azure.  |
| | |

Дополнительные сведения об Azure CLI 2.0 см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Установка Azure CLI 2.0) и [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).