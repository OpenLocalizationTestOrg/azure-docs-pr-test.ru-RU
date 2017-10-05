---
title: "Пример сценария Azure PowerShell — создание приложения Service Fabric | Документация Майкрософт"
description: "Пример сценария Azure PowerShell — создание приложения Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="d6a3a-103">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d6a3a-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="d6a3a-104">Этот сценарий обновляет запущенный экземпляр приложения Service Fabric до версии 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="d6a3a-105">Сценарий копирует новый пакет приложения в хранилище образов кластера, регистрирует тип приложения, запускает отслеживаемое обновление и постоянно проверяет состояние обновления до завершения либо отката обновления.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="d6a3a-106">Измените параметры, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="d6a3a-107">При необходимости установите модуль PowerShell ServiceFabric вместе с [пакетом SDK для Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6a3a-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d6a3a-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d6a3a-108">Sample script</span></span>

<span data-ttu-id="d6a3a-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Обновление приложения")]</span><span class="sxs-lookup"><span data-stu-id="d6a3a-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="d6a3a-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d6a3a-110">Script explanation</span></span>

<span data-ttu-id="d6a3a-111">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-111">This script uses the following commands.</span></span> <span data-ttu-id="d6a3a-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d6a3a-113">Команда</span><span class="sxs-lookup"><span data-stu-id="d6a3a-113">Command</span></span> | <span data-ttu-id="d6a3a-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="d6a3a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6a3a-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="d6a3a-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="d6a3a-116">Возвращает все приложения в кластер Service Fabric или конкретное приложение.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="d6a3a-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="d6a3a-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="d6a3a-118">Возвращает состояние обновления приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="d6a3a-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d6a3a-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d6a3a-120">Возвращает типы приложений Service Fabric, зарегистрированные в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="d6a3a-121">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d6a3a-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d6a3a-122">Отменяет регистрацию типа приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="d6a3a-123">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="d6a3a-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="d6a3a-124">Копирует пакет приложения Service Fabric в хранилище образов.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="d6a3a-125">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d6a3a-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d6a3a-126">Регистрирует тип приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="d6a3a-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="d6a3a-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="d6a3a-128">Обновляет приложение Service Fabric до указанной версии типа приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a3a-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d6a3a-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6a3a-129">Next steps</span></span>

<span data-ttu-id="d6a3a-130">Дополнительные сведения о модуле Service Fabric PowerShell см. в [документации по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="d6a3a-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="d6a3a-131">Дополнительные примеры сценариев PowerShell для Azure Service Fabric см. в разделе [Примеры сценариев Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d6a3a-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
