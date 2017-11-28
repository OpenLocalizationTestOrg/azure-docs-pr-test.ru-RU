---
title: "Пример сценария PowerShell - aaaAzure развертывание кластера tooa приложения | Документы Microsoft"
description: "Сценарий Azure PowerShell пример: развертывание кластера Service Fabric tooa приложения."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="3ea88-103">Развертывание кластера Service Fabric tooa приложения</span><span class="sxs-lookup"><span data-stu-id="3ea88-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="3ea88-104">Этот скрипт копирует образ хранилища кластера tooa пакет приложений, регистрирует тип приложения hello в кластере hello и создает экземпляр приложения с типом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3ea88-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="3ea88-105">Если все службы по умолчанию были определены в манифесте приложения hello объекта тип целевого приложения hello, эти службы создаются в данный момент.</span><span class="sxs-lookup"><span data-stu-id="3ea88-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="3ea88-106">При необходимости настройте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="3ea88-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="3ea88-107">При необходимости установите модуля Service Fabric PowerShell hello с hello [пакет Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3ea88-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3ea88-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3ea88-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3ea88-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="3ea88-109">Clean up deployment</span></span> 

<span data-ttu-id="3ea88-110">После выполнения сценария образец hello hello скрипта в [удалить приложение](service-fabric-powershell-remove-application.md) может быть tooremove используется экземпляр приложения hello, отменена регистрация типа приложения hello и удалить пакет приложения hello из хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="3ea88-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="3ea88-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3ea88-111">Script explanation</span></span>

<span data-ttu-id="3ea88-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="3ea88-112">This script uses hello following commands.</span></span> <span data-ttu-id="3ea88-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3ea88-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3ea88-114">Команда</span><span class="sxs-lookup"><span data-stu-id="3ea88-114">Command</span></span> | <span data-ttu-id="3ea88-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="3ea88-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ea88-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="3ea88-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="3ea88-117">Скопируйте образ хранилища кластера toohello пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="3ea88-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="3ea88-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="3ea88-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="3ea88-119">Регистрирует тип и версия приложения на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="3ea88-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="3ea88-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="3ea88-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="3ea88-121">Создает приложение на основе зарегистрированного типа приложения.</span><span class="sxs-lookup"><span data-stu-id="3ea88-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ea88-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ea88-122">Next steps</span></span>

<span data-ttu-id="3ea88-123">Дополнительные сведения о модуля Service Fabric PowerShell hello см. в разделе [документация по Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="3ea88-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="3ea88-124">Дополнительные примеры Powershell для Azure Service Fabric можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3ea88-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
