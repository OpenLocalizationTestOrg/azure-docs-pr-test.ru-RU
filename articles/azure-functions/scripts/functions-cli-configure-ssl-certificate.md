---
title: "Пример сценария Azure CLI. Привязка настраиваемого SSL-сертификата к приложению-функции | Документация Майкрософт"
description: "Пример сценария Azure CLI для привязки настраиваемого SSL-сертификата к приложению-функции в Azure."
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="937eb-103">Привязка пользовательского SSL-сертификата к приложению-функции</span><span class="sxs-lookup"><span data-stu-id="937eb-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="937eb-104">Этот пример сценария создает в службе приложений приложение-функции со связанными ресурсами, а затем привязывает к нему SSL-сертификат имени личного домена.</span><span class="sxs-lookup"><span data-stu-id="937eb-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="937eb-105">Для этого примера вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="937eb-105">For this sample, you need:</span></span>

* <span data-ttu-id="937eb-106">Доступ к странице конфигурации DNS вашего регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="937eb-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="937eb-107">Допустимый PFX-файл и пароль для SSL-сертификата, который будет отправлен и привязан.</span><span class="sxs-lookup"><span data-stu-id="937eb-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="937eb-108">Чтобы привязать SSL-сертификат, приложение-функция должно быть создано в плане службы приложений, а не в плане потребления.</span><span class="sxs-lookup"><span data-stu-id="937eb-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="937eb-109">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="937eb-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="937eb-110">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="937eb-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="937eb-111">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="937eb-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="937eb-112">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="937eb-112">Sample script</span></span>

<span data-ttu-id="937eb-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Привязка SSL-сертификата к веб-приложению")]</span><span class="sxs-lookup"><span data-stu-id="937eb-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="937eb-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="937eb-114">Script explanation</span></span>

<span data-ttu-id="937eb-115">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="937eb-115">This script uses the following commands.</span></span> <span data-ttu-id="937eb-116">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="937eb-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="937eb-117">Команда</span><span class="sxs-lookup"><span data-stu-id="937eb-117">Command</span></span> | <span data-ttu-id="937eb-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="937eb-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="937eb-119">az group create</span><span class="sxs-lookup"><span data-stu-id="937eb-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="937eb-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="937eb-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="937eb-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="937eb-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="937eb-122">Создает план службы приложений, необходимый для привязки SSL-сертификатов.</span><span class="sxs-lookup"><span data-stu-id="937eb-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="937eb-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="937eb-123">az functionapp create</span></span>]() | <span data-ttu-id="937eb-124">Создает приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="937eb-124">Creates a function app.</span></span> |
| [<span data-ttu-id="937eb-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="937eb-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="937eb-126">Сопоставляет личный домен с приложением-функцией.</span><span class="sxs-lookup"><span data-stu-id="937eb-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="937eb-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="937eb-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="937eb-128">Отправляет SSL-сертификат в приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="937eb-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="937eb-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="937eb-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="937eb-130">Привязывает отправленный SSL-сертификат к приложению-функции.</span><span class="sxs-lookup"><span data-stu-id="937eb-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="937eb-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="937eb-131">Next steps</span></span>

<span data-ttu-id="937eb-132">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="937eb-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="937eb-133">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure]().</span><span class="sxs-lookup"><span data-stu-id="937eb-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
