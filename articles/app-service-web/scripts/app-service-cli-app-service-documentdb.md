---
title: "Пример сценария Azure CLI. Подключение веб-приложения к Cosmos DB | Документация Майкрософт"
description: "Пример сценария Azure CLI для подключения веб-приложения к Cosmos DB."
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="5e15b-103">Подключение веб-приложения к Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5e15b-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="5e15b-104">В этом сценарии вы узнаете, как создать учетную запись Azure Cosmos DB и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5e15b-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="5e15b-105">Затем вы свяжете Cosmos DB с веб-приложением, используя параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="5e15b-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5e15b-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5e15b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5e15b-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5e15b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5e15b-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5e15b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5e15b-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5e15b-109">Sample script</span></span>

<span data-ttu-id="5e15b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="5e15b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5e15b-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5e15b-111">Script explanation</span></span>

<span data-ttu-id="5e15b-112">Для создания группы ресурсов, веб-приложений, базы данных Cosmos DB и всех связанных ресурсов этот сценарий использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5e15b-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="5e15b-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5e15b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5e15b-114">Команда</span><span class="sxs-lookup"><span data-stu-id="5e15b-114">Command</span></span> | <span data-ttu-id="5e15b-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="5e15b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e15b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5e15b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5e15b-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5e15b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e15b-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5e15b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5e15b-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5e15b-119">Creates an App Service plan.</span></span> <span data-ttu-id="5e15b-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5e15b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5e15b-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5e15b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5e15b-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5e15b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5e15b-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="5e15b-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="5e15b-124">Создает учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5e15b-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="5e15b-125">Здесь будут храниться данные.</span><span class="sxs-lookup"><span data-stu-id="5e15b-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="5e15b-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="5e15b-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="5e15b-127">Выводит список ключей доступа для указанной учетной записи базы данных база данных.</span><span class="sxs-lookup"><span data-stu-id="5e15b-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="5e15b-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="5e15b-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="5e15b-129">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5e15b-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="5e15b-130">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="5e15b-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e15b-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e15b-131">Next steps</span></span>

<span data-ttu-id="5e15b-132">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e15b-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5e15b-133">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5e15b-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
