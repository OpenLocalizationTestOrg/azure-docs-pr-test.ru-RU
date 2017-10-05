---
title: "Пример сценария Azure CLI. Привязка пользовательского SSL-сертификата к веб-приложению | Документация Майкрософт"
description: "Пример сценария Azure CLI. Привязка пользовательского SSL-сертификата к веб-приложению"
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="6e8ee-103">Привязка SSL-сертификата к веб-приложению</span><span class="sxs-lookup"><span data-stu-id="6e8ee-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="6e8ee-104">Этот сценарий создает в службе приложений веб-приложение со связанными ресурсами, а затем привязывает к нему SSL-сертификат имени личного домена.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="6e8ee-105">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="6e8ee-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6e8ee-106">Доступ к странице конфигурации DNS вашего регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="6e8ee-107">Допустимый PFX-файл и пароль для SSL-сертификата, который будет отправлен и привязан.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6e8ee-108">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6e8ee-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="6e8ee-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6e8ee-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="6e8ee-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6e8ee-111">Sample script</span></span>

<span data-ttu-id="6e8ee-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Привязка SSL-сертификата к веб-приложению")]</span><span class="sxs-lookup"><span data-stu-id="6e8ee-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6e8ee-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6e8ee-113">Script explanation</span></span>

<span data-ttu-id="6e8ee-114">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-114">This script uses the following commands.</span></span> <span data-ttu-id="6e8ee-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6e8ee-116">Команда</span><span class="sxs-lookup"><span data-stu-id="6e8ee-116">Command</span></span> | <span data-ttu-id="6e8ee-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="6e8ee-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e8ee-118">az group create</span><span class="sxs-lookup"><span data-stu-id="6e8ee-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6e8ee-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e8ee-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6e8ee-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6e8ee-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6e8ee-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6e8ee-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6e8ee-123">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6e8ee-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="6e8ee-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="6e8ee-125">Сопоставляет пользовательский домен с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="6e8ee-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="6e8ee-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="6e8ee-127">Отправляет SSL-сертификат в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="6e8ee-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="6e8ee-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="6e8ee-129">Привязывает отправленный SSL-сертификат к веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e8ee-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e8ee-130">Next steps</span></span>

<span data-ttu-id="6e8ee-131">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e8ee-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6e8ee-132">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6e8ee-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
