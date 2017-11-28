---
title: "Образец скрипта PowerShell - удалить приложение из кластера aaaAzure | Документы Microsoft"
description: "Пример сценария Azure PowerShell — удаление приложения из кластера Service Fabric."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="e8991-103">Удаление приложения из кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e8991-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="e8991-104">Этот скрипт удаляет запущенный экземпляр приложения Service Fabric, отменяет регистрацию тип и версия приложения из кластера hello и удаляет пакет приложения hello из хранилища образов кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e8991-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="e8991-105">Удаление экземпляра приложения hello также удаляет все hello выполняющихся экземпляров службы, связанное с этим приложением.</span><span class="sxs-lookup"><span data-stu-id="e8991-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="e8991-106">При необходимости настройте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="e8991-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="e8991-107">При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8991-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e8991-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e8991-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="e8991-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e8991-109">Script explanation</span></span>

<span data-ttu-id="e8991-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e8991-110">This script uses hello following commands.</span></span> <span data-ttu-id="e8991-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="e8991-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8991-112">Команда</span><span class="sxs-lookup"><span data-stu-id="e8991-112">Command</span></span> | <span data-ttu-id="e8991-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8991-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8991-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="e8991-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="e8991-115">Удаляет запущенный экземпляр приложения Service Fabric из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e8991-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="e8991-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="e8991-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="e8991-117">Отменяет регистрацию Service Fabric тип и версия приложения из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e8991-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="e8991-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="e8991-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="e8991-119">Удаляет пакет Service Fabric приложения из хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="e8991-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="e8991-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8991-120">Next steps</span></span>

<span data-ttu-id="e8991-121">Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="e8991-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="e8991-122">Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e8991-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
