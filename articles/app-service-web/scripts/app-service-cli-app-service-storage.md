---
title: "Пример скрипта Azure CLI. Подключение веб-приложения к учетной записи хранения | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Подключение веб-приложения к учетной записи хранения"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2520eecf54b77b88d6aa1ba2e538d05e3407f3d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="5324f-103">Подключение веб-приложения к учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="5324f-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="5324f-104">В этой статье вы узнаете, как создать учетную запись хранения и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5324f-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="5324f-105">Затем вы свяжете учетную запись хранения с веб-приложением, используя параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="5324f-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5324f-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5324f-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5324f-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5324f-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5324f-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5324f-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="5324f-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5324f-109">Sample script</span></span>

<span data-ttu-id="5324f-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Служба хранилища Azure")]</span><span class="sxs-lookup"><span data-stu-id="5324f-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5324f-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5324f-111">Script explanation</span></span>

<span data-ttu-id="5324f-112">Для создания группы ресурсов, веб-приложения, учетной записи хранения и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5324f-112">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="5324f-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5324f-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5324f-114">Команда</span><span class="sxs-lookup"><span data-stu-id="5324f-114">Command</span></span> | <span data-ttu-id="5324f-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="5324f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5324f-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5324f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5324f-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5324f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5324f-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5324f-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5324f-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5324f-119">Creates an App Service plan.</span></span> <span data-ttu-id="5324f-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5324f-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5324f-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5324f-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5324f-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5324f-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5324f-123">az storage account create</span><span class="sxs-lookup"><span data-stu-id="5324f-123">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="5324f-124">Создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5324f-124">Creates a storage account.</span></span> <span data-ttu-id="5324f-125">Здесь будут храниться статичные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5324f-125">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="5324f-126">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="5324f-126">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="5324f-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="5324f-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="5324f-128">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5324f-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="5324f-129">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="5324f-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5324f-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5324f-130">Next steps</span></span>

<span data-ttu-id="5324f-131">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5324f-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5324f-132">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5324f-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
