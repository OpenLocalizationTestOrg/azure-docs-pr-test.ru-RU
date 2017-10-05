---
title: "Репозитории реестра контейнеров Azure | Документация Майкрософт"
description: "Использование репозиториев реестра контейнеров Azure для образов Docker"
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
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="534be-103">Репозитории реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="534be-103">Azure container registry repositories</span></span>

<span data-ttu-id="534be-104">Реестры контейнеров Azure совместимы со множеством служб и оркестраторов.</span><span class="sxs-lookup"><span data-stu-id="534be-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="534be-105">Для упрощения отслеживания исходных служб и агентов, из которых используется ACR, мы начали использовать поле заголовка Docker в файле Docker.config.</span><span class="sxs-lookup"><span data-stu-id="534be-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="534be-106">Просмотр репозиториев на портале</span><span class="sxs-lookup"><span data-stu-id="534be-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="534be-107">Заголовки ACR имеют следующий формат.</span><span class="sxs-lookup"><span data-stu-id="534be-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="534be-108">Cloud: Azure, Azure Stack или другие облака для конкретной государственной организации или страны.</span><span class="sxs-lookup"><span data-stu-id="534be-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="534be-109">Хотя в настоящее время Azure Stack и облака государственных организаций не поддерживаются, этот параметр позволяет будущую поддержку.</span><span class="sxs-lookup"><span data-stu-id="534be-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="534be-110">Service: имя службы.</span><span class="sxs-lookup"><span data-stu-id="534be-110">Service: name of the service.</span></span>
* <span data-ttu-id="534be-111">Optionalservicename: необязательный параметр для служб с подчиненными службами или для указания номера SKU (пример: веб-приложения соответствуют Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="534be-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="534be-112">Партнерским службам и оркестраторам рекомендуется использовать специальные значения заголовков для помощи в нашей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="534be-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="534be-113">Пользователи также могут изменять значение, переданное в заголовке, если возникнет такая необходимость.</span><span class="sxs-lookup"><span data-stu-id="534be-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="534be-114">Ниже приведены значения, которые партнерам рекомендуется использовать для заполнения поля "X-Meta-Source-Client".</span><span class="sxs-lookup"><span data-stu-id="534be-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="534be-115">Имя службы</span><span class="sxs-lookup"><span data-stu-id="534be-115">Service Name</span></span>              | <span data-ttu-id="534be-116">Заголовок</span><span class="sxs-lookup"><span data-stu-id="534be-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="534be-117">Служба контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="534be-117">Azure Container Service</span></span>   | <span data-ttu-id="534be-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="534be-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="534be-119">Служба приложений — веб-приложения</span><span class="sxs-lookup"><span data-stu-id="534be-119">App Service - Web Apps</span></span>    | <span data-ttu-id="534be-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="534be-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="534be-121">Служба приложений — Logic Apps</span><span class="sxs-lookup"><span data-stu-id="534be-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="534be-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="534be-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="534be-123">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="534be-123">Batch</span></span>                     | <span data-ttu-id="534be-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="534be-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="534be-125">Консоль облака</span><span class="sxs-lookup"><span data-stu-id="534be-125">Cloud Console</span></span>             | <span data-ttu-id="534be-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="534be-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="534be-127">Functions</span><span class="sxs-lookup"><span data-stu-id="534be-127">Functions</span></span>                 | <span data-ttu-id="534be-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="534be-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="534be-129">Интернет вещей — Центр</span><span class="sxs-lookup"><span data-stu-id="534be-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="534be-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="534be-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="534be-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="534be-131">HDInsight</span></span>                 | <span data-ttu-id="534be-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="534be-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="534be-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="534be-133">Jenkins</span></span>                   | <span data-ttu-id="534be-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="534be-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="534be-135">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="534be-135">Machine Learning</span></span>          | <span data-ttu-id="534be-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="534be-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="534be-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="534be-137">Service Fabric</span></span>            | <span data-ttu-id="534be-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="534be-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="534be-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="534be-139">VSTS</span></span>                      | <span data-ttu-id="534be-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="534be-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="534be-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="534be-141">Next steps</span></span>
[<span data-ttu-id="534be-142">Дополнительные сведения о реестрах, поддерживаемых службах и оркестраторах</span><span class="sxs-lookup"><span data-stu-id="534be-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
