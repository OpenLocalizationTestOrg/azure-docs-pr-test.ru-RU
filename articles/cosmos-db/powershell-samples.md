---
title: "Примеры PowerShell для Azure Cosmos DB aaaAzure | Документы Microsoft"
description: "Azure PowerShell примеры — toohelp сценарии создания и управления учетными записями Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8815e775f720226e98cc8dcf7743e481c213272b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="32ca6-103">Примеры Azure PowerShell для базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="32ca6-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="32ca6-104">Hello Следующая таблица содержит ссылки toosample Azure скрипты PowerShell для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="32ca6-104">hello following table includes links toosample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="32ca6-105">**Создание учетной записи Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="32ca6-105">**Create an Azure Cosmos DB account**</span></span>||
|<span data-ttu-id="32ca6-106">[Azure Cosmos DB: Create a DocumentDB API account using PowerShell](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) (База данных Azure Cosmos: создание учетной записи API DocumentDB с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="32ca6-106">[Create a DocumentDB API account](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)</span></span>| <span data-ttu-id="32ca6-107">Создает один toouse учетная запись Azure Cosmos DB hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="32ca6-107">Creates a single Azure Cosmos DB account toouse with hello DocumentDB API.</span></span> |
|<span data-ttu-id="32ca6-108">**Масштабирование Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="32ca6-108">**Scale Azure Cosmos DB**</span></span>||
|<span data-ttu-id="32ca6-109">[Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Репликация учетной записи базы данных Azure Cosmos DB в нескольких регионах и настройка приоритетов отработки отказа с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="32ca6-109">[Replicate Azure Cosmos DB account in multiple regions and configure failover priorities](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)</span></span>|<span data-ttu-id="32ca6-110">Глобально реплицирует данные учетной записи в нескольких регионах с указанным приоритетом отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="32ca6-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="32ca6-111">**Безопасность базы данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="32ca6-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="32ca6-112">Получение ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="32ca6-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="32ca6-113">Возвращает hello главной записи первичные и вторичные ключи и первичные и вторичные ключи только для чтения для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="32ca6-113">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="32ca6-114">Получение строки подключения MongoDB</span><span class="sxs-lookup"><span data-stu-id="32ca6-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="32ca6-115">Получает tooconnect строку hello подключения вашей tooyour приложения MongoDB учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="32ca6-115">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="32ca6-116">Повторное создание ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="32ca6-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="32ca6-117">Повторно создает образец hello или только для чтения ключ учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="32ca6-117">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="32ca6-118">Создание брандмауэра</span><span class="sxs-lookup"><span data-stu-id="32ca6-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="32ca6-119">Создает входящих IP доступ управления политики toolimit доступа toohello учетную запись из группы утвержденных машины или облачные службы.</span><span class="sxs-lookup"><span data-stu-id="32ca6-119">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="32ca6-120">**Высокий уровень доступности, аварийное восстановление, архивация и восстановление**</span><span class="sxs-lookup"><span data-stu-id="32ca6-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="32ca6-121">Настройка политики отработки</span><span class="sxs-lookup"><span data-stu-id="32ca6-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="32ca6-122">Задает hello приоритет отработки отказа для каждого региона, в котором реплицируется учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="32ca6-122">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|||