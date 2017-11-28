---
title: "Образец скрипта CLI - маршрутизацию трафика для обеспечения высокой доступности приложений aaaAzure | Документы Microsoft"
description: "Пример скрипта Azure CLI. Маршрутизация трафика для обеспечения высокой доступности приложений."
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="00d3a-103">Маршрутизация трафика для обеспечения высокой доступности приложений</span><span class="sxs-lookup"><span data-stu-id="00d3a-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="00d3a-104">Этот скрипт создает группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="00d3a-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="00d3a-105">Диспетчер трафика направляет трафик toohello приложения в одной области, как основной регион hello и дополнительный регион toohello при недоступности приложения hello в основном регионе hello.</span><span class="sxs-lookup"><span data-stu-id="00d3a-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="00d3a-106">Перед выполнением сценария hello, необходимо изменить hello MyWebApp, MyWebAppL1 и MyWebAppL2 значения toounique значения в пределах Azure.</span><span class="sxs-lookup"><span data-stu-id="00d3a-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="00d3a-107">После выполнения сценария hello, можно открыть приложение hello в основной регион hello с mywebapp.trafficmanager.net hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="00d3a-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="00d3a-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="00d3a-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="00d3a-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="00d3a-109">Clean up deployment</span></span> 

<span data-ttu-id="00d3a-110">После выполнения сценария образец hello hello команда может быть группы ресурсов используется tooremove hello, приложение служб приложений и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="00d3a-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="00d3a-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="00d3a-111">Script explanation</span></span>

<span data-ttu-id="00d3a-112">Этот скрипт использует следующие команды toocreate группы ресурсов, веб-приложения, профиль диспетчера трафика hello и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="00d3a-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="00d3a-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="00d3a-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="00d3a-114">Команда</span><span class="sxs-lookup"><span data-stu-id="00d3a-114">Command</span></span> | <span data-ttu-id="00d3a-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="00d3a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="00d3a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="00d3a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="00d3a-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="00d3a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="00d3a-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="00d3a-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="00d3a-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="00d3a-119">Creates an App Service plan.</span></span> <span data-ttu-id="00d3a-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="00d3a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="00d3a-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="00d3a-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="00d3a-122">Создает веб-приложение Azure в течение hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="00d3a-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="00d3a-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="00d3a-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="00d3a-124">Создает профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="00d3a-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="00d3a-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="00d3a-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="00d3a-126">Добавляет конечную точку tooan профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="00d3a-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="00d3a-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00d3a-127">Next steps</span></span>

<span data-ttu-id="00d3a-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="00d3a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="00d3a-129">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [сеть Azure документации](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="00d3a-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
