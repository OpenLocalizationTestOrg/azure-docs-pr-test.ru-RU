---
title: "Пример сценария CLI - aaaAzure наблюдения за веб-приложения в журналы веб-сервера | Документы Microsoft"
description: "Пример скрипта Azure CLI. Мониторинг веб-приложения с помощью журналов веб-сервера"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="3f3b3-103">Мониторинг веб-приложения с помощью журналов веб-сервера</span><span class="sxs-lookup"><span data-stu-id="3f3b3-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="3f3b3-104">В этом случае будет создавать группы ресурсов, план обслуживания приложений, веб-приложения и настройте журналы hello web app tooenable веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="3f3b3-105">Затем вы загружаете hello файлы журналов для просмотра.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3f3b3-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3f3b3-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3f3b3-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3f3b3-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3f3b3-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3f3b3-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3f3b3-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3f3b3-110">Script explanation</span></span>

<span data-ttu-id="3f3b3-111">Этот скрипт использует hello следующие команды toocreate группы ресурсов, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="3f3b3-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3f3b3-113">Команда</span><span class="sxs-lookup"><span data-stu-id="3f3b3-113">Command</span></span> | <span data-ttu-id="3f3b3-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="3f3b3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3f3b3-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3f3b3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3f3b3-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3f3b3-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3f3b3-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3f3b3-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-118">Creates an App Service plan.</span></span> <span data-ttu-id="3f3b3-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="3f3b3-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="3f3b3-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="3f3b3-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3f3b3-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="3f3b3-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="3f3b3-123">Настраивает журналы, в которых сохраниться веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="3f3b3-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="3f3b3-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="3f3b3-125">Hello загружаемые файлы журналов из hello приложения Azure web tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="3f3b3-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f3b3-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3f3b3-126">Next steps</span></span>

<span data-ttu-id="3f3b3-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f3b3-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3f3b3-128">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3f3b3-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
