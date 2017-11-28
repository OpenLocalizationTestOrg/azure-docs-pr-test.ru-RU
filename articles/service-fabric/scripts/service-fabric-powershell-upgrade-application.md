---
title: "Пример сценария PowerShell - aaaAzure обновление приложения Service Fabric | Документы Microsoft"
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
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="c4fa7-103">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c4fa7-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="c4fa7-104">Этот скрипт обновляет выполняющегося экземпляра tooversion Service Fabric приложения 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="c4fa7-105">Hello скрипт копирует hello новое приложение toohello кластера изображения хранилище пакетов, регистрирует тип приложения hello, запустит отслеживаемых обновление и постоянно проверяет состояние обновления hello до завершения обновления hello, либо откатывается назад.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="c4fa7-106">При необходимости настройте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="c4fa7-107">При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4fa7-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c4fa7-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c4fa7-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="c4fa7-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c4fa7-109">Script explanation</span></span>

<span data-ttu-id="c4fa7-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-110">This script uses hello following commands.</span></span> <span data-ttu-id="c4fa7-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4fa7-112">Команда</span><span class="sxs-lookup"><span data-stu-id="c4fa7-112">Command</span></span> | <span data-ttu-id="c4fa7-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="c4fa7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4fa7-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="c4fa7-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="c4fa7-115">Возвращает все приложения hello в кластер Service Fabric hello или конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="c4fa7-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="c4fa7-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="c4fa7-117">Возвращает состояние hello обновления приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="c4fa7-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c4fa7-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c4fa7-119">Возвращает типы приложения Service Fabric hello, зарегистрированные в кластере Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="c4fa7-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c4fa7-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c4fa7-121">Отменяет регистрацию типа приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="c4fa7-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="c4fa7-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="c4fa7-123">Копирует образ toohello пакета приложения Service Fabric хранилище.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="c4fa7-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c4fa7-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="c4fa7-125">Регистрирует тип приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="c4fa7-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="c4fa7-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="c4fa7-127">Обновление версии типа приложения toohello Service Fabric указанного приложения.</span><span class="sxs-lookup"><span data-stu-id="c4fa7-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c4fa7-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4fa7-128">Next steps</span></span>

<span data-ttu-id="c4fa7-129">Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c4fa7-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="c4fa7-130">Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4fa7-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
