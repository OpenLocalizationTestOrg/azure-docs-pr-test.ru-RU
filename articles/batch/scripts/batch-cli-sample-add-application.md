---
title: "Пример сценария CLI - aaaAzure добавить приложение в пакете | Документы Microsoft"
description: "Пример сценария Azure CLI для добавления приложения в пакетную службу."
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="29f49-103">Добавление приложений tooAzure пакета с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="29f49-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="29f49-104">Этот сценарий демонстрирует, как tooset приложения для использования в пуле пакетной службы Azure или задачи.</span><span class="sxs-lookup"><span data-stu-id="29f49-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="29f49-105">tooset приложения, пакета исполняемого файла, вместе с зависимостями, в ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="29f49-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="29f49-106">В данный пример hello исполняемый архив файл будет назван "my-приложения-exe.zip".</span><span class="sxs-lookup"><span data-stu-id="29f49-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29f49-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="29f49-107">Prerequisites</span></span>

- <span data-ttu-id="29f49-108">Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.</span><span class="sxs-lookup"><span data-stu-id="29f49-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="29f49-109">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="29f49-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="29f49-110">В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.</span><span class="sxs-lookup"><span data-stu-id="29f49-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="29f49-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="29f49-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="29f49-112">Очистка приложения</span><span class="sxs-lookup"><span data-stu-id="29f49-112">Clean up application</span></span>

<span data-ttu-id="29f49-113">После запуска hello выше пример сценария, запустите следующие команды tooremove hello приложения и все его отправленное приложение пакетов.</span><span class="sxs-lookup"><span data-stu-id="29f49-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="29f49-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="29f49-114">Script explanation</span></span>

<span data-ttu-id="29f49-115">Этот скрипт использует следующие команды toocreate hello приложения и отправка пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="29f49-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="29f49-116">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="29f49-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="29f49-117">Команда</span><span class="sxs-lookup"><span data-stu-id="29f49-117">Command</span></span> | <span data-ttu-id="29f49-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="29f49-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="29f49-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="29f49-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="29f49-120">Создает приложение.</span><span class="sxs-lookup"><span data-stu-id="29f49-120">Creates an application.</span></span>  |
| [<span data-ttu-id="29f49-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="29f49-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="29f49-122">Обновляет свойства приложения.</span><span class="sxs-lookup"><span data-stu-id="29f49-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="29f49-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="29f49-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="29f49-124">Добавляет toohello пакета приложения указанного приложения.</span><span class="sxs-lookup"><span data-stu-id="29f49-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="29f49-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29f49-125">Next steps</span></span>

<span data-ttu-id="29f49-126">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29f49-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="29f49-127">Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="29f49-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
