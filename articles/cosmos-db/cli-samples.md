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
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="52061-103">Примеры Azure CLI для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="52061-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="52061-104">В следующей таблице содержатся ссылки на примеры сценариев Azure CLI для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52061-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="52061-105">Страницы справки для всех команд интерфейса командной строки Azure Cosmos DB доступны в [справочнике по Azure CLI 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="52061-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="52061-106">**Создание учетной записи, базы данных и контейнеров Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="52061-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="52061-107">Azure Cosmos DB: создание учетной записи API DocumentDB с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="52061-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="52061-108">Создание одной учетной записи, базы данных и контейнера API Azure Cosmos DB для использования с API DocumentDB, Graph или таблицей.</span><span class="sxs-lookup"><span data-stu-id="52061-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="52061-109">Создание учетной записи API MongoDB</span><span class="sxs-lookup"><span data-stu-id="52061-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="52061-110">Создание отдельной учетной записи, базы данных и коллекции API MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52061-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="52061-111">**Масштабирование Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="52061-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="52061-112">Масштабирование пропускной способности контейнера</span><span class="sxs-lookup"><span data-stu-id="52061-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="52061-113">Изменение подготовленной пропускной способности контейнера.</span><span class="sxs-lookup"><span data-stu-id="52061-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="52061-114">Репликация учетной записи базы данных Azure Cosmos DB в нескольких регионах и настройка приоритетов отработки отказа</span><span class="sxs-lookup"><span data-stu-id="52061-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="52061-115">Глобальная репликация данные учетной записи в нескольких регионах с указанным приоритетом отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="52061-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="52061-116">**Безопасность базы данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="52061-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="52061-117">Получение ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="52061-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="52061-118">Возвращение первичного и вторичного главных ключей для записи и первичного и вторичного ключей только для чтения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="52061-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="52061-119">Получение строки подключения MongoDB</span><span class="sxs-lookup"><span data-stu-id="52061-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="52061-120">Получает строку подключения для подключения приложения MongoDB к учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52061-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="52061-121">Повторное создание ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="52061-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="52061-122">Повторное создание главного ключа или ключа только для чтения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="52061-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="52061-123">Создание брандмауэра</span><span class="sxs-lookup"><span data-stu-id="52061-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="52061-124">Создание политики контроля доступа для входящих IP-адресов для разрешения доступа к учетной записи с утвержденных компьютеров и (или) из облачных служб.</span><span class="sxs-lookup"><span data-stu-id="52061-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="52061-125">**Высокий уровень доступности, аварийное восстановление, архивация и восстановление**</span><span class="sxs-lookup"><span data-stu-id="52061-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="52061-126">Настройка политики отработки</span><span class="sxs-lookup"><span data-stu-id="52061-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="52061-127">Настройка приоритета отработки отказа для каждого региона, в котором реплицируется учетная запись.</span><span class="sxs-lookup"><span data-stu-id="52061-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="52061-128">**Подключение Azure Cosmos DB к ресурсам**</span><span class="sxs-lookup"><span data-stu-id="52061-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="52061-129">Подключение веб-приложения к Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="52061-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="52061-130">Создание и подключение базы данных Azure Cosmos DB и веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="52061-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
