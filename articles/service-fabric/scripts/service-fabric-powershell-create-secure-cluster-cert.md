---
title: "Пример сценария PowerShell - aaaAzure создание кластера Service Fabric | Документы Microsoft"
description: "Пример сценария Azure PowerShell — создание кластера Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="397c9-103">Создание кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="397c9-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="397c9-104">В этом примере сценария создается кластер Service Fabric из пяти узлов, защищенный с помощью сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="397c9-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="397c9-105">Hello команда создает самозаверяющий сертификат и передает его tooa нового ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="397c9-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="397c9-106">сертификат Hello также является скопированный tooa локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="397c9-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="397c9-107">Набор hello *-OS* параметр toochoose hello версии Windows или Linux, работающей на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="397c9-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="397c9-108">При необходимости настройте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="397c9-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="397c9-109">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview) , а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="397c9-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="397c9-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="397c9-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="397c9-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="397c9-111">Clean up deployment</span></span> 

<span data-ttu-id="397c9-112">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello, кластера и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="397c9-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="397c9-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="397c9-113">Script explanation</span></span>

<span data-ttu-id="397c9-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="397c9-114">This script uses hello following commands.</span></span> <span data-ttu-id="397c9-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="397c9-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="397c9-116">Команда</span><span class="sxs-lookup"><span data-stu-id="397c9-116">Command</span></span> | <span data-ttu-id="397c9-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="397c9-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="397c9-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="397c9-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="397c9-119">Создает кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="397c9-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="397c9-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="397c9-120">Next steps</span></span>

<span data-ttu-id="397c9-121">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="397c9-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="397c9-122">Дополнительные примеры Azure Service Fabric Azure Powershell можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="397c9-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
