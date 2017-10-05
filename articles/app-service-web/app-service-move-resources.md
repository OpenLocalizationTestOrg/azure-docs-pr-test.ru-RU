---
title: "Перемещение ресурсов веб-приложений в другую группу ресурсов."
description: "Описываются сценарии, в которых вы можете перемещать веб-приложения и службы приложений из одной группы ресурсов в другую."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="d4ccf-103">Поддерживаемые конфигурации перемещения</span><span class="sxs-lookup"><span data-stu-id="d4ccf-103">Supported Move Configurations</span></span>
<span data-ttu-id="d4ccf-104">Ресурсы веб-приложений Azure можно перемещать с помощью [API перемещения ресурсов Resource Manager](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d4ccf-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="d4ccf-105">Веб-приложения Azure в настоящее время поддерживают следующие сценарии перемещения.</span><span class="sxs-lookup"><span data-stu-id="d4ccf-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="d4ccf-106">Перемещение всего содержимого группы ресурсов (веб-приложений, планов обслуживания приложений и сертификатов) в другую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4ccf-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="d4ccf-107">В этом сценарии конечная группа ресурсов не может содержать никаких ресурсов Microsoft.Web.</span><span class="sxs-lookup"><span data-stu-id="d4ccf-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="d4ccf-108">Перемещение отдельных веб-приложений в другую группу ресурсов с сохранением их размещения в текущем плане службы приложений (план службы приложений остается в старой группе ресурсов).</span><span class="sxs-lookup"><span data-stu-id="d4ccf-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


