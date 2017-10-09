---
title: "Это функция Azure, которая подключается tooan хранилища Azure aaaCreate | Документы Microsoft"
description: "Сценарий Azure CLI пример — создание это функция Azure, которая подключается tooan хранилища Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="e95dd-103">Интеграция приложения-функции в учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e95dd-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="e95dd-104">Этот пример скрипта создает приложение-функцию и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e95dd-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e95dd-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e95dd-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e95dd-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e95dd-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e95dd-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e95dd-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e95dd-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e95dd-108">Sample script</span></span>

<span data-ttu-id="e95dd-109">Этот образец создает приложение Azure функции и добавляет hello хранилища tooan приложения настроек подключения.</span><span class="sxs-lookup"><span data-stu-id="e95dd-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="e95dd-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="e95dd-110">Clean up deployment</span></span>

<span data-ttu-id="e95dd-111">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, приложение служб приложений и все связанные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e95dd-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e95dd-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e95dd-112">Script explanation</span></span>

<span data-ttu-id="e95dd-113">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e95dd-113">This script uses hello following commands.</span></span> <span data-ttu-id="e95dd-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="e95dd-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e95dd-115">Команда</span><span class="sxs-lookup"><span data-stu-id="e95dd-115">Command</span></span> | <span data-ttu-id="e95dd-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="e95dd-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e95dd-117">az login</span><span class="sxs-lookup"><span data-stu-id="e95dd-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="e95dd-118">TooAzure входа.</span><span class="sxs-lookup"><span data-stu-id="e95dd-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="e95dd-119">az group create</span><span class="sxs-lookup"><span data-stu-id="e95dd-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e95dd-120">Создайте группу ресурсов с расположением.</span><span class="sxs-lookup"><span data-stu-id="e95dd-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="e95dd-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="e95dd-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="e95dd-122">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e95dd-122">Create a storage account</span></span> |
| [<span data-ttu-id="e95dd-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="e95dd-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="e95dd-124">Создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="e95dd-124">Create a new function app</span></span> |
| [<span data-ttu-id="e95dd-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="e95dd-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="e95dd-126">Очистка</span><span class="sxs-lookup"><span data-stu-id="e95dd-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e95dd-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e95dd-127">Next steps</span></span>

<span data-ttu-id="e95dd-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e95dd-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e95dd-129">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e95dd-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
