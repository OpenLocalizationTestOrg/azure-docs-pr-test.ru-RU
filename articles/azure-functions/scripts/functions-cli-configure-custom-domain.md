---
title: "aaaAzure образец скрипта CLI - сопоставить приложении функция tooa личного домена | Документы Microsoft"
description: "Azure CLI образец скрипта - карты приложении функция tooa настраиваемого домена в Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="20c10-103">Карта приложении функция tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="20c10-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="20c10-104">Этот скрипт создает функцию приложение с ресурсами и затем отображает `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="20c10-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="20c10-105">toomap tooa пользовательского домена, функция приложения должны создаваться в плане обслуживания приложений, а не в план потребления.</span><span class="sxs-lookup"><span data-stu-id="20c10-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="20c10-106">Функции Azure поддерживают сопоставление личного домена только с помощью записи A.</span><span class="sxs-lookup"><span data-stu-id="20c10-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="20c10-107">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="20c10-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="20c10-108">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="20c10-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="20c10-109">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20c10-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="20c10-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="20c10-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="20c10-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="20c10-111">Script explanation</span></span>

<span data-ttu-id="20c10-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="20c10-112">This script uses hello following commands.</span></span> <span data-ttu-id="20c10-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="20c10-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="20c10-114">Команда</span><span class="sxs-lookup"><span data-stu-id="20c10-114">Command</span></span> | <span data-ttu-id="20c10-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="20c10-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20c10-116">az group create</span><span class="sxs-lookup"><span data-stu-id="20c10-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="20c10-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="20c10-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20c10-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="20c10-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="20c10-119">Создает учетную запись хранилища, необходимый приложению функции hello.</span><span class="sxs-lookup"><span data-stu-id="20c10-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="20c10-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="20c10-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="20c10-121">Создает пользовательский домен toomap требуется план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="20c10-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="20c10-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="20c10-122">az functionapp create</span></span>]() | <span data-ttu-id="20c10-123">Создает приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="20c10-123">Creates a function app.</span></span> |
| [<span data-ttu-id="20c10-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="20c10-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="20c10-125">Сопоставляет приложении функция tooa пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="20c10-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20c10-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20c10-126">Next steps</span></span>

<span data-ttu-id="20c10-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20c10-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="20c10-128">Дополнительные примеры сценариев, использующих функции CLI можно найти в hello [документации Azure функции]().</span><span class="sxs-lookup"><span data-stu-id="20c10-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
