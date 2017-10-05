---
title: "Пример сценария Azure CLI. Сопоставление личного домена с приложением-функцией | Документация Майкрософт"
description: "Пример сценария Azure CLI для сопоставления личного домена с приложением-функцией в Azure."
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
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="fe96c-103">Сопоставление личного домена с приложением-функцией</span><span class="sxs-lookup"><span data-stu-id="fe96c-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="fe96c-104">Этот пример сценария создает приложение-функцию со связанными ресурсами, а затем сопоставляет с ним `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="fe96c-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="fe96c-105">Для сопоставления с личным доменом приложение-функция должно быть создано в плане службы приложений, а не в плане потребления.</span><span class="sxs-lookup"><span data-stu-id="fe96c-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="fe96c-106">Функции Azure поддерживают сопоставление личного домена только с помощью записи A.</span><span class="sxs-lookup"><span data-stu-id="fe96c-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fe96c-107">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fe96c-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fe96c-108">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="fe96c-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="fe96c-109">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fe96c-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="fe96c-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fe96c-110">Sample script</span></span>

<span data-ttu-id="fe96c-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Сопоставление личного домена с приложением-функцией")]</span><span class="sxs-lookup"><span data-stu-id="fe96c-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fe96c-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fe96c-112">Script explanation</span></span>

<span data-ttu-id="fe96c-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fe96c-113">This script uses the following commands.</span></span> <span data-ttu-id="fe96c-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="fe96c-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fe96c-115">Команда</span><span class="sxs-lookup"><span data-stu-id="fe96c-115">Command</span></span> | <span data-ttu-id="fe96c-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="fe96c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe96c-117">az group create</span><span class="sxs-lookup"><span data-stu-id="fe96c-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fe96c-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fe96c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fe96c-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="fe96c-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="fe96c-120">Создает учетную запись хранения, необходимую для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="fe96c-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="fe96c-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fe96c-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fe96c-122">Создает план службы приложений, необходимый для сопоставления личного домена.</span><span class="sxs-lookup"><span data-stu-id="fe96c-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="fe96c-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="fe96c-123">az functionapp create</span></span>]() | <span data-ttu-id="fe96c-124">Создает приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="fe96c-124">Creates a function app.</span></span> |
| [<span data-ttu-id="fe96c-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="fe96c-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="fe96c-126">Сопоставляет личный домен с приложением-функцией.</span><span class="sxs-lookup"><span data-stu-id="fe96c-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe96c-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe96c-127">Next steps</span></span>

<span data-ttu-id="fe96c-128">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe96c-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fe96c-129">Дополнительные примеры сценариев Azure CLI для Функций см. в [документации по Функциям Azure]().</span><span class="sxs-lookup"><span data-stu-id="fe96c-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
