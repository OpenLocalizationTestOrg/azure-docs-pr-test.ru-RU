---
title: "aaaAzure образец скрипта CLI - подключения в базе данных SQL web app tooa | Документы Microsoft"
description: "Сценарий Azure CLI пример — подключить приложение веб-tooa база данных SQL"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="d9768-103">Подключение приложения веб-tooa база данных SQL</span><span class="sxs-lookup"><span data-stu-id="d9768-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="d9768-104">В этом сценарии вы узнаете, как toocreate базы данных Azure SQL и Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d9768-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="d9768-105">Затем будет связан hello SQL базы данных toohello веб-приложения с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="d9768-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d9768-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d9768-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d9768-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="d9768-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d9768-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d9768-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d9768-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d9768-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d9768-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d9768-110">Script explanation</span></span>

<span data-ttu-id="d9768-111">Этот скрипт использует hello следующие команды toocreate группы ресурсов, веб-приложения, базы данных SQL и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d9768-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="d9768-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="d9768-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d9768-113">Команда</span><span class="sxs-lookup"><span data-stu-id="d9768-113">Command</span></span> | <span data-ttu-id="d9768-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="d9768-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d9768-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d9768-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d9768-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d9768-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d9768-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d9768-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d9768-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d9768-118">Creates an App Service plan.</span></span> <span data-ttu-id="d9768-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="d9768-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="d9768-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d9768-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d9768-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="d9768-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d9768-122">az sql server create</span><span class="sxs-lookup"><span data-stu-id="d9768-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="d9768-123">Создает сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d9768-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="d9768-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="d9768-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="d9768-125">Создает новую базу данных с hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d9768-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="d9768-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="d9768-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="d9768-127">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="d9768-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="d9768-128">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="d9768-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d9768-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9768-129">Next steps</span></span>

<span data-ttu-id="d9768-130">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d9768-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d9768-131">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d9768-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
