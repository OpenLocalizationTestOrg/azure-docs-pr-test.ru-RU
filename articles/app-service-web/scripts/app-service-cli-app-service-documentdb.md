---
title: "Образец скрипта CLI - aaaAzure подключения tooCosmos приложения web DB | Документы Microsoft"
description: "Сценарий Azure CLI пример — подключить web app tooCosmos DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="08ca8-103">Подключение web app tooCosmos DB</span><span class="sxs-lookup"><span data-stu-id="08ca8-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="08ca8-104">В этом сценарии вы узнаете, как toocreate учетную запись Azure Cosmos DB и Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="08ca8-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="08ca8-105">Затем будет связан hello Cosmos DB toohello веб-приложения с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="08ca8-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="08ca8-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="08ca8-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="08ca8-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="08ca8-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="08ca8-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="08ca8-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="08ca8-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="08ca8-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="08ca8-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="08ca8-110">Script explanation</span></span>

<span data-ttu-id="08ca8-111">Этот скрипт использует hello следующие команды toocreate группы ресурсов, веб-приложения, Cosmos DB и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="08ca8-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="08ca8-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="08ca8-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="08ca8-113">Команда</span><span class="sxs-lookup"><span data-stu-id="08ca8-113">Command</span></span> | <span data-ttu-id="08ca8-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="08ca8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08ca8-115">az group create</span><span class="sxs-lookup"><span data-stu-id="08ca8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08ca8-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="08ca8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08ca8-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="08ca8-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="08ca8-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="08ca8-118">Creates an App Service plan.</span></span> <span data-ttu-id="08ca8-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="08ca8-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="08ca8-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="08ca8-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="08ca8-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="08ca8-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="08ca8-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="08ca8-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="08ca8-123">Создает учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08ca8-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="08ca8-124">Это происходит, где будут храниться данные hello.</span><span class="sxs-lookup"><span data-stu-id="08ca8-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="08ca8-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="08ca8-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="08ca8-126">Ключи доступа hello списки hello указана учетная запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08ca8-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="08ca8-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="08ca8-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="08ca8-128">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="08ca8-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="08ca8-129">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="08ca8-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08ca8-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08ca8-130">Next steps</span></span>

<span data-ttu-id="08ca8-131">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08ca8-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08ca8-132">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="08ca8-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
