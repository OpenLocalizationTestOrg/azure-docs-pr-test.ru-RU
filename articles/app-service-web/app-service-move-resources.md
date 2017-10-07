---
title: "веб-приложения ресурсы aaaMove tooanother группы ресурсов"
description: "Описывает сценарии hello, где веб-приложения и службы приложений можно перемещать из одной группы ресурсов tooanother."
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
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="07306-103">Поддерживаемые конфигурации перемещения</span><span class="sxs-lookup"><span data-stu-id="07306-103">Supported Move Configurations</span></span>
<span data-ttu-id="07306-104">Можно перемещать ресурсы веб-приложения Azure с помощью hello [API переместить ресурсы ресурсов диспетчера](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="07306-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="07306-105">Azure веб-приложений в настоящее время поддерживает следующие сценарии перемещения hello:</span><span class="sxs-lookup"><span data-stu-id="07306-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="07306-106">Переместить все содержимое hello группы ресурсов (веб-приложений, планах службы приложений и сертификатов) tooanother группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="07306-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="07306-107">Hello целевая группа ресурсов не может содержать любой Microsoft.Web ресурсы в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="07306-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="07306-108">Перемещаемое отдельных web apps tooa другой группе ресурсов, по-прежнему их размещение в их текущего плана службы приложений (hello приложения службы план остается в группе ресурсов старого hello).</span><span class="sxs-lookup"><span data-stu-id="07306-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


