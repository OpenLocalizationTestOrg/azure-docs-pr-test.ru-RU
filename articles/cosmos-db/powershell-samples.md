---
title: "Примеры Azure PowerShell для базы данных Azure Cosmos DB | Документация Майкрософт"
description: "Примеры Azure PowerShell — это скрипты для создания учетных записей базы данных Azure Cosmos DB и управления ими."
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
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="ead7e-103">Примеры Azure PowerShell для базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ead7e-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="ead7e-104">В следующей таблице содержатся ссылки на примеры скриптов Azure PowerShell для базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ead7e-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="ead7e-105">**Создание учетной записи Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="ead7e-105">**Create an Azure Cosmos DB account**</span></span>||
|<span data-ttu-id="ead7e-106">[Azure Cosmos DB: Create a DocumentDB API account using PowerShell](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) (База данных Azure Cosmos: создание учетной записи API DocumentDB с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ead7e-106">[Create a DocumentDB API account](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)</span></span>| <span data-ttu-id="ead7e-107">Создает одну учетную запись базы данных Azure Cosmos DB для использования с API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ead7e-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="ead7e-108">**Масштабирование базы данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="ead7e-108">**Scale Azure Cosmos DB**</span></span>||
|<span data-ttu-id="ead7e-109">[Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Репликация учетной записи базы данных Azure Cosmos DB в нескольких регионах и настройка приоритетов отработки отказа с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ead7e-109">[Replicate Azure Cosmos DB account in multiple regions and configure failover priorities](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)</span></span>|<span data-ttu-id="ead7e-110">Глобально реплицирует данные учетной записи в нескольких регионах с указанным приоритетом отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="ead7e-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="ead7e-111">**Безопасность базы данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="ead7e-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="ead7e-112">Получение ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="ead7e-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="ead7e-113">Возвращение первичного и вторичного главных ключей для записи и первичного и вторичного ключей только для чтения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ead7e-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="ead7e-114">Получение строки подключения MongoDB</span><span class="sxs-lookup"><span data-stu-id="ead7e-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="ead7e-115">Получает строку подключения для подключения приложения MongoDB к учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ead7e-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="ead7e-116">Повторное создание ключей учетной записи</span><span class="sxs-lookup"><span data-stu-id="ead7e-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="ead7e-117">Повторное создание главного ключа или ключа только для чтения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ead7e-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="ead7e-118">Создание брандмауэра</span><span class="sxs-lookup"><span data-stu-id="ead7e-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="ead7e-119">Создание политики контроля доступа для входящих IP-адресов для разрешения доступа к учетной записи с утвержденных компьютеров и (или) из облачных служб.</span><span class="sxs-lookup"><span data-stu-id="ead7e-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="ead7e-120">**Высокий уровень доступности, аварийное восстановление, архивация и восстановление**</span><span class="sxs-lookup"><span data-stu-id="ead7e-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="ead7e-121">Настройка политики отработки</span><span class="sxs-lookup"><span data-stu-id="ead7e-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="ead7e-122">Задает приоритет отработки отказа каждого региона, в котором реплицируется учетная запись.</span><span class="sxs-lookup"><span data-stu-id="ead7e-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||