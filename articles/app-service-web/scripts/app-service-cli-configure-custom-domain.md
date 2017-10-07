---
title: "aaaAzure образец скрипта CLI - карты веб-приложения tooa личного домена | Документы Microsoft"
description: "Пример сценария Azure CLI - карта пользовательского домена tooa веб-приложения"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="147c9-103">Карта пользовательского домена tooa веб-приложения</span><span class="sxs-lookup"><span data-stu-id="147c9-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="147c9-104">Этот образец скрипта создает веб-приложения в службе приложений с его связанные ресурсы и затем отображает `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="147c9-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="147c9-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="147c9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="147c9-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="147c9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="147c9-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="147c9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="147c9-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="147c9-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="147c9-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="147c9-109">Script explanation</span></span>

<span data-ttu-id="147c9-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="147c9-110">This script uses hello following commands.</span></span> <span data-ttu-id="147c9-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="147c9-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="147c9-112">Команда</span><span class="sxs-lookup"><span data-stu-id="147c9-112">Command</span></span> | <span data-ttu-id="147c9-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="147c9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="147c9-114">az group create</span><span class="sxs-lookup"><span data-stu-id="147c9-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="147c9-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="147c9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="147c9-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="147c9-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="147c9-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="147c9-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="147c9-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="147c9-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="147c9-119">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="147c9-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="147c9-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="147c9-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="147c9-121">Сопоставляет пользовательский домен tooa веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="147c9-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="147c9-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="147c9-122">Next steps</span></span>

<span data-ttu-id="147c9-123">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="147c9-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="147c9-124">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="147c9-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
