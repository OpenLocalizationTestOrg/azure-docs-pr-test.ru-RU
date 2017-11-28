---
title: "Пример удаления службы структуры CLI сценария aaaAzure"
description: "Удаление приложения из кластера с помощью Azure Service Fabric CLI hello Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="46536-103">Удаление приложения из кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="46536-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="46536-104">Этот скрипт удаляет запущенный экземпляр приложения Service Fabric, отменяет регистрацию тип и версия приложения из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="46536-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="46536-105">Удаление экземпляра приложения hello также удаляет все hello выполняющихся экземпляров службы, связанное с этим приложением.</span><span class="sxs-lookup"><span data-stu-id="46536-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="46536-106">Затем файлы приложения hello удаляются из хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="46536-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="46536-107">При необходимости установите hello [службы структуры CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="46536-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="46536-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="46536-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="46536-109">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46536-109">Next steps</span></span>

<span data-ttu-id="46536-110">Дополнительные сведения см. в разделе hello [документации службы структуры CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="46536-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="46536-111">Дополнительные примеры CLI структуры службы Azure Service Fabric можно найти в hello [образцы службы структуры CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="46536-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
