---
title: "Примеры Azure CLI для Azure Cosmos DB | Документация Майкрософт"
description: "Примеры Azure CLI для создания учетных записей, баз данных, контейнеров, регионов и брандмауэров Azure Cosmos DB и управления ими."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 11/29/2017
ms.author: mimig
ms.openlocfilehash: 432ffc80d602a9e4eaf83fba15f0e6ebabd13603
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Примеры Azure CLI для Azure Cosmos DB

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)] 

В следующей таблице содержатся ссылки на примеры сценариев Azure CLI для Azure Cosmos DB. Страницы справки для всех команд интерфейса командной строки Azure Cosmos DB доступны в [справочнике по Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Создание учетной записи, базы данных и контейнеров Azure Cosmos DB**||
|[Создание учетной записи SQL API](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Создает одной учетной записи Azure Cosmos DB API, базы данных и контейнер для использования с API-Интерфейсы SQL. |
| [Создание учетной записи API MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Создание отдельной учетной записи, базы данных и коллекции API MongoDB в Azure Cosmos DB. |
|**Масштабирование Azure Cosmos DB**||
| [Масштабирование пропускной способности контейнера](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Изменение подготовленной пропускной способности контейнера.|
|[Репликация учетной записи базы данных Azure Cosmos DB в нескольких регионах и настройка приоритетов отработки отказа](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Глобальная репликация данные учетной записи в нескольких регионах с указанным приоритетом отработки отказа.|
|**Безопасность базы данных Azure Cosmos DB**||
| [Получение ключей учетной записи](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Возвращение первичного и вторичного главных ключей для записи и первичного и вторичного ключей только для чтения для учетной записи.|
| [Получение строки подключения MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Получает строку подключения для подключения приложения MongoDB к учетной записи базы данных Azure Cosmos DB.|
|[Повторное создание ключей учетной записи](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Повторное создание главного ключа или ключа только для чтения для учетной записи.|
|[Создание брандмауэра](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Создание политики контроля доступа для входящих IP-адресов для разрешения доступа к учетной записи с утвержденных компьютеров и (или) из облачных служб.|
|**Высокий уровень доступности, аварийное восстановление, архивация и восстановление**||
|[Настройка политики отработки](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Настройка приоритета отработки отказа для каждого региона, в котором реплицируется учетная запись.|
|**Подключение Azure Cosmos DB к ресурсам**||
|[Подключение веб-приложения к Azure Cosmos DB](../app-service/scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json)|Создание и подключение базы данных Azure Cosmos DB и веб-приложения Azure.|
|||
