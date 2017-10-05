---
title: "Пример развертывания сценария интерфейса командной строки Azure Service Fabric"
description: "Развертывание приложения в кластер Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="2e3e0-103">Развертывание приложения в кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2e3e0-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="2e3e0-104">Этот пример сценария копирует пакет приложения в хранилище образов кластера, регистрирует тип приложения в кластере и создает экземпляр приложения с типом приложения.</span><span class="sxs-lookup"><span data-stu-id="2e3e0-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span> <span data-ttu-id="2e3e0-105">В это же время также создаются все стандартные службы.</span><span class="sxs-lookup"><span data-stu-id="2e3e0-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="2e3e0-106">При необходимости установите [интерфейс командной строки Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e3e0-106">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="2e3e0-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2e3e0-107">Sample script</span></span>

<span data-ttu-id="2e3e0-108">[!code-sh[главный](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Развертывание приложения в кластере")]</span><span class="sxs-lookup"><span data-stu-id="2e3e0-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2e3e0-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="2e3e0-109">Clean up deployment</span></span>

<span data-ttu-id="2e3e0-110">По завершении с помощью сценария [удаления](cli-remove-application.md) можно удалить приложение.</span><span class="sxs-lookup"><span data-stu-id="2e3e0-110">When done, the [remove](cli-remove-application.md) script can be used to remove the application.</span></span> <span data-ttu-id="2e3e0-111">Сценарий удаления удаляет экземпляр приложения, отменяет регистрацию типа приложения и удаляет пакет приложения из хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="2e3e0-111">The remove script deletes the application instance, unregisters the application type, and deletes the application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e3e0-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e3e0-112">Next steps</span></span>

<span data-ttu-id="2e3e0-113">Дополнительные сведения см. в [документации интерфейса командной строки Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e3e0-113">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="2e3e0-114">Дополнительные примеры сценариев интерфейса командной строки Service Fabric для Azure Service Fabric см. в статье [Примеры сценариев Azure PowerShell](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e3e0-114">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
