---
title: "Образец скрипта CLI - aaaAzure привязки пользовательского приложения функции tooa сертификат SSL | Документы Microsoft"
description: "Пример сценария Azure CLI - привязка пользовательского SSL сертификат tooa функции приложения в Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="7da39-103">Привязка пользовательского приложения функции tooa сертификат SSL</span><span class="sxs-lookup"><span data-stu-id="7da39-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="7da39-104">Этот скрипт создает функцию приложение в службе приложений с его связанные ресурсы, а затем привязывает hello SSL-сертификат tooit имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="7da39-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="7da39-105">Для этого примера вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="7da39-105">For this sample, you need:</span></span>

* <span data-ttu-id="7da39-106">Доступ к странице конфигурации регистратора домена tooyour DNS.</span><span class="sxs-lookup"><span data-stu-id="7da39-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="7da39-107">Является допустимым. Сертификата PFX-файла и пароль для hello SSL требуется tooupload и привязку.</span><span class="sxs-lookup"><span data-stu-id="7da39-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="7da39-108">toobind сертификат SSL, функция приложения должны создаваться в плане обслуживания приложений, а не в план потребления.</span><span class="sxs-lookup"><span data-stu-id="7da39-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7da39-109">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7da39-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7da39-110">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7da39-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7da39-111">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7da39-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7da39-112">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="7da39-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7da39-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7da39-113">Script explanation</span></span>

<span data-ttu-id="7da39-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7da39-114">This script uses hello following commands.</span></span> <span data-ttu-id="7da39-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="7da39-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7da39-116">Команда</span><span class="sxs-lookup"><span data-stu-id="7da39-116">Command</span></span> | <span data-ttu-id="7da39-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="7da39-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7da39-118">az group create</span><span class="sxs-lookup"><span data-stu-id="7da39-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7da39-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7da39-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7da39-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7da39-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7da39-121">Создает SSL-сертификаты toobind требуется план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="7da39-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="7da39-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="7da39-122">az functionapp create</span></span>]() | <span data-ttu-id="7da39-123">Создает приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="7da39-123">Creates a function app.</span></span> |
| [<span data-ttu-id="7da39-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="7da39-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="7da39-125">Сопоставляет приложении функция toohello пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="7da39-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="7da39-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="7da39-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="7da39-127">Передает функции приложения tooa сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="7da39-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="7da39-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="7da39-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="7da39-129">Привязывает загруженного приложения функции tooa сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="7da39-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7da39-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7da39-130">Next steps</span></span>

<span data-ttu-id="7da39-131">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7da39-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7da39-132">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure]().</span><span class="sxs-lookup"><span data-stu-id="7da39-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
