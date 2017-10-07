---
title: "Пример сценария CLI - aaaAzure создать веб-приложение ASP.NET Core в контейнере Docker | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание веб-приложения ASP.NET Core в контейнере Docker"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="dde6d-103">Создание веб-приложения ASP.NET Core в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="dde6d-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="dde6d-104">В этом сценарии вы узнаете, как служба плана и веб-приложения и развертывания с помощью контейнера Docker приложения ASP.NET Core toocreate группу ресурсов приложения Linux.</span><span class="sxs-lookup"><span data-stu-id="dde6d-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dde6d-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dde6d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dde6d-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="dde6d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dde6d-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dde6d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="dde6d-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="dde6d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dde6d-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="dde6d-109">Script explanation</span></span>

<span data-ttu-id="dde6d-110">Этот скрипт использует hello следующие команды toocreate группы ресурсов, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dde6d-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="dde6d-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="dde6d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dde6d-112">Команда</span><span class="sxs-lookup"><span data-stu-id="dde6d-112">Command</span></span> | <span data-ttu-id="dde6d-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="dde6d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dde6d-114">az group create</span><span class="sxs-lookup"><span data-stu-id="dde6d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dde6d-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dde6d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dde6d-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="dde6d-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dde6d-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dde6d-117">Creates an App Service plan.</span></span> <span data-ttu-id="dde6d-118">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="dde6d-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="dde6d-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="dde6d-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dde6d-120">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="dde6d-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dde6d-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="dde6d-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="dde6d-122">Задает контейнер Docker hello hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="dde6d-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dde6d-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dde6d-123">Next steps</span></span>

<span data-ttu-id="dde6d-124">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dde6d-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dde6d-125">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dde6d-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
