---
title: "Пример скрипта Azure CLI. Мониторинг веб-приложения с помощью журналов веб-сервера | Документация Майкрософт"
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
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="5023d-103">Мониторинг веб-приложения с помощью журналов веб-сервера</span><span class="sxs-lookup"><span data-stu-id="5023d-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="5023d-104">В этом сценарии вы создадите группу ресурсов, план службы приложений, веб-приложение, а также настроите веб-приложение для включения журналов веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="5023d-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="5023d-105">Затем вы скачаете файлы журналов для просмотра.</span><span class="sxs-lookup"><span data-stu-id="5023d-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5023d-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5023d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5023d-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5023d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5023d-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5023d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5023d-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5023d-109">Sample script</span></span>

<span data-ttu-id="5023d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Мониторинг журналов")]</span><span class="sxs-lookup"><span data-stu-id="5023d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5023d-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5023d-111">Script explanation</span></span>

<span data-ttu-id="5023d-112">Для создания группы ресурсов, веб-приложений и всех связанных с ними ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5023d-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="5023d-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5023d-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5023d-114">Команда</span><span class="sxs-lookup"><span data-stu-id="5023d-114">Command</span></span> | <span data-ttu-id="5023d-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="5023d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5023d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5023d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5023d-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5023d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5023d-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5023d-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5023d-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5023d-119">Creates an App Service plan.</span></span> <span data-ttu-id="5023d-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5023d-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5023d-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5023d-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5023d-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5023d-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5023d-123">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="5023d-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="5023d-124">Настраивает журналы, в которых сохраниться веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5023d-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="5023d-125">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="5023d-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="5023d-126">Скачивает журналы веб-приложения Azure на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="5023d-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5023d-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5023d-127">Next steps</span></span>

<span data-ttu-id="5023d-128">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5023d-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5023d-129">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5023d-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
