---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="e8ee4-103">Репозитории реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e8ee4-103">Azure container registry repositories</span></span>

<span data-ttu-id="e8ee4-104">Реестры контейнеров Azure совместимы со множеством служб и оркестраторов.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="e8ee4-105">toomake его проще tootrack hello источника служб и агентов, из которых используется контроля доступа, мы начали использовать поле заголовка hello Docker в файле Docker.config hello.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="e8ee4-106">Просмотр репозитории в hello портала</span><span class="sxs-lookup"><span data-stu-id="e8ee4-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="e8ee4-107">заголовки ACR Hello выполните формат hello.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="e8ee4-108">Cloud: Azure, Azure Stack или другие облака для конкретной государственной организации или страны.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="e8ee4-109">Хотя в настоящее время Azure Stack и облака государственных организаций не поддерживаются, этот параметр позволяет будущую поддержку.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="e8ee4-110">Службы: имя hello службы.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-110">Service: name of hello service.</span></span>
* <span data-ttu-id="e8ee4-111">Optionalservicename: необязательный параметр для служб с subservices или toospecify SKU (пример: соответствуют веб-приложений с Azure и приложения службы или веб приложениями).</span><span class="sxs-lookup"><span data-stu-id="e8ee4-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="e8ee4-112">Услуги партнера и orchestrators, рекомендуется toouse toohelp значения определенного заголовка с нашей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="e8ee4-113">Пользователи также могут изменять значение hello передавать toohello заголовка в том случае, если такая необходимость.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="e8ee4-114">Ниже приведены значения Hello, мы хотим ACR партнеров toouse toopopulate hello «X-Meta-источник-клиент» поля.</span><span class="sxs-lookup"><span data-stu-id="e8ee4-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="e8ee4-115">Имя службы</span><span class="sxs-lookup"><span data-stu-id="e8ee4-115">Service Name</span></span>              | <span data-ttu-id="e8ee4-116">Заголовок</span><span class="sxs-lookup"><span data-stu-id="e8ee4-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="e8ee4-117">Служба контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e8ee4-117">Azure Container Service</span></span>   | <span data-ttu-id="e8ee4-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="e8ee4-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="e8ee4-119">Служба приложений — веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e8ee4-119">App Service - Web Apps</span></span>    | <span data-ttu-id="e8ee4-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="e8ee4-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="e8ee4-121">Служба приложений — Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e8ee4-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="e8ee4-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="e8ee4-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="e8ee4-123">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="e8ee4-123">Batch</span></span>                     | <span data-ttu-id="e8ee4-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="e8ee4-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="e8ee4-125">Консоль облака</span><span class="sxs-lookup"><span data-stu-id="e8ee4-125">Cloud Console</span></span>             | <span data-ttu-id="e8ee4-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="e8ee4-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="e8ee4-127">Functions</span><span class="sxs-lookup"><span data-stu-id="e8ee4-127">Functions</span></span>                 | <span data-ttu-id="e8ee4-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="e8ee4-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="e8ee4-129">Интернет вещей — Центр</span><span class="sxs-lookup"><span data-stu-id="e8ee4-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="e8ee4-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="e8ee4-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="e8ee4-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8ee4-131">HDInsight</span></span>                 | <span data-ttu-id="e8ee4-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="e8ee4-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="e8ee4-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="e8ee4-133">Jenkins</span></span>                   | <span data-ttu-id="e8ee4-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="e8ee4-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="e8ee4-135">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="e8ee4-135">Machine Learning</span></span>          | <span data-ttu-id="e8ee4-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="e8ee4-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="e8ee4-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e8ee4-137">Service Fabric</span></span>            | <span data-ttu-id="e8ee4-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="e8ee4-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="e8ee4-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="e8ee4-139">VSTS</span></span>                      | <span data-ttu-id="e8ee4-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="e8ee4-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="e8ee4-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8ee4-141">Next steps</span></span>
[<span data-ttu-id="e8ee4-142">Дополнительные сведения о реестрами и hello поддерживается служб и orchestrators</span><span class="sxs-lookup"><span data-stu-id="e8ee4-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
