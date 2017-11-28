---
title: "Образец скрипта CLI - aaaAzure привязки пользовательских веб-приложения tooa SSL сертификат | Документы Microsoft"
description: "Пример сценария Azure CLI - привязка пользовательского приложения web tooa сертификат SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="ad854-103">Привязка пользовательских веб-приложения tooa SSL сертификата</span><span class="sxs-lookup"><span data-stu-id="ad854-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="ad854-104">Этот образец скрипта создает веб-приложения в службе приложений с его связанные ресурсы, а затем привязывает hello SSL-сертификат tooit имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="ad854-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="ad854-105">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="ad854-105">For this sample, you will need:</span></span>

* <span data-ttu-id="ad854-106">Доступ к странице конфигурации регистратора домена tooyour DNS.</span><span class="sxs-lookup"><span data-stu-id="ad854-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="ad854-107">Является допустимым. Сертификата PFX-файла и пароль для hello SSL требуется tooupload и привязку.</span><span class="sxs-lookup"><span data-stu-id="ad854-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ad854-108">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ad854-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ad854-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="ad854-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ad854-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ad854-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="ad854-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ad854-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ad854-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ad854-112">Script explanation</span></span>

<span data-ttu-id="ad854-113">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ad854-113">This script uses hello following commands.</span></span> <span data-ttu-id="ad854-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="ad854-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ad854-115">Команда</span><span class="sxs-lookup"><span data-stu-id="ad854-115">Command</span></span> | <span data-ttu-id="ad854-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="ad854-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad854-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ad854-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ad854-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ad854-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ad854-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ad854-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ad854-120">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ad854-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ad854-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ad854-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ad854-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="ad854-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ad854-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="ad854-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="ad854-124">Сопоставляет пользовательский домен tooa веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ad854-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="ad854-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="ad854-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="ad854-126">Загружает веб-приложение tooa сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="ad854-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="ad854-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="ad854-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="ad854-128">Привязывает отправленного SSL сертификат tooa веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="ad854-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad854-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad854-129">Next steps</span></span>

<span data-ttu-id="ad854-130">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad854-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ad854-131">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ad854-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
