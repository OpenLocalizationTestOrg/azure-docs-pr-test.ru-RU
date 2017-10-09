---
title: "aaaAzure CLI образцы для Azure Cosmos DB | Документы Microsoft"
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
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="76a75-103">Примеры Azure CLI для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76a75-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="76a75-104">Hello следующей таблице представлены сценарии Azure CLI toosample ссылки для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76a75-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="76a75-105">Ссылка страницы для всех команд DB Cosmos Azure CLI, доступные в hello [Azure CLI 2.0 ссылка](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="76a75-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="76a75-106">**Создание учетной записи, базы данных и контейнеров Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="76a75-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="76a75-107">Azure Cosmos DB: создание учетной записи API DocumentDB с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="76a75-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="76a75-108">Создает одной учетной записи Azure Cosmos DB API, базы данных и контейнер для использования с hello DocumentDB, диаграммы или API-интерфейсы таблицы.</span><span class="sxs-lookup"><span data-stu-id="76a75-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="76a75-109">Создание учетной записи API MongoDB</span><span class="sxs-lookup"><span data-stu-id="76a75-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="76a75-110">Создание отдельной учетной записи, базы данных и коллекции API MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76a75-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="76a75-111">**Масштабирование Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="76a75-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="76a75-112">Масштабирование пропускной способности контейнера</span><span class="sxs-lookup"><span data-stu-id="76a75-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="76a75-113">Изменения hello подготовить througput в контейнере.</span><span class="sxs-lookup"><span data-stu-id="76a75-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="76a75-114">Репликация учетной записи базы данных Azure Cosmos DB в нескольких регионах и настройка приоритетов отработки отказа</span><span class="sxs-lookup"><span data-stu-id="76a75-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="76a75-115">Глобальная репликация данные учетной записи в нескольких регионах с указанным приоритетом отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="76a75-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="76a75-116">**Безопасность базы данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="76a75-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="76a75-117">Получение ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="76a75-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="76a75-118">Возвращает hello главной записи первичные и вторичные ключи и первичные и вторичные ключи только для чтения для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="76a75-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="76a75-119">Получение строки подключения MongoDB</span><span class="sxs-lookup"><span data-stu-id="76a75-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="76a75-120">Получает tooconnect строку hello подключения вашей tooyour приложения MongoDB учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76a75-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="76a75-121">Повторное создание ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="76a75-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="76a75-122">Повторно создает образец hello или только для чтения ключ учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="76a75-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="76a75-123">Создание брандмауэра</span><span class="sxs-lookup"><span data-stu-id="76a75-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="76a75-124">Создает входящих IP доступ управления политики toolimit доступа toohello учетную запись из группы утвержденных машины или облачные службы.</span><span class="sxs-lookup"><span data-stu-id="76a75-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="76a75-125">**Высокий уровень доступности, аварийное восстановление, архивация и восстановление**</span><span class="sxs-lookup"><span data-stu-id="76a75-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="76a75-126">Настройка политики отработки</span><span class="sxs-lookup"><span data-stu-id="76a75-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="76a75-127">Задает hello приоритет отработки отказа для каждого региона, в котором реплицируется учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="76a75-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="76a75-128">**Подключение Azure Cosmos DB к ресурсам**</span><span class="sxs-lookup"><span data-stu-id="76a75-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="76a75-129">Подключение web app tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76a75-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="76a75-130">Создание и подключение базы данных Azure Cosmos DB и веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="76a75-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
