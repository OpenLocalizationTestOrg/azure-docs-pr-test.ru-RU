---
title: "Пример развертывания службы структуры CLI сценария aaaAzure"
description: "Развертывание кластера Azure Service Fabric tooan приложения с помощью hello Azure Service Fabric CLI"
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="9fd2d-103">Развертывание кластера Service Fabric tooa приложения</span><span class="sxs-lookup"><span data-stu-id="9fd2d-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="9fd2d-104">Этот скрипт копирует образ хранилища кластера tooa пакет приложений, регистрирует тип приложения hello в кластере hello и создает экземпляр приложения с типом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="9fd2d-105">В это же время также создаются все стандартные службы.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="9fd2d-106">При необходимости установите hello [службы структуры CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="9fd2d-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9fd2d-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9fd2d-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9fd2d-108">Clean up deployment</span></span>

<span data-ttu-id="9fd2d-109">По завершении hello [удалить](cli-remove-application.md) сценарий может быть используется tooremove приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="9fd2d-110">сценарий удаления Hello удаляет экземпляр приложения hello, Отмена регистрации типа приложения hello и удаляет пакет приложения hello из хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fd2d-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fd2d-111">Next steps</span></span>

<span data-ttu-id="9fd2d-112">Дополнительные сведения см. в разделе hello [документации службы структуры CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="9fd2d-113">Дополнительные примеры CLI структуры службы Azure Service Fabric можно найти в hello [образцы службы структуры CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
