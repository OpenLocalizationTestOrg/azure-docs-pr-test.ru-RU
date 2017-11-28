---
title: "tooAzure aaaDeploying приложений служб приложений"
description: "Узнайте, как работают приложения tooDeploy tooApp службы"
keywords: "служба приложений, служба приложений azure, развертывание"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="b23ff-104">Общие сведения о развертывании службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b23ff-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="b23ff-105">Служба приложений Azure предоставляет многофункциональный и toosupport, создание рабочих процессов развертывания мощный и гибкий набор интеграции функций.</span><span class="sxs-lookup"><span data-stu-id="b23ff-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="b23ff-106">При развертывании приложений можно использовать такие возможности, как непрерывная интеграция, публикация из локальной системы управления версиями, WebDeploy и FTP.</span><span class="sxs-lookup"><span data-stu-id="b23ff-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="b23ff-107">Hello рекомендуемые метод для рабочего развертывания приложения является переключения слотов развертывания.</span><span class="sxs-lookup"><span data-stu-id="b23ff-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="b23ff-108">Слоты развертывания представляют собой промежуточные среды и среды развертывания, связанные с рабочими приложениями.</span><span class="sxs-lookup"><span data-stu-id="b23ff-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="b23ff-109">Слоты развертывания можно настроить и применить веб-трафик для проверки и трафика можно переключать по запросу для развертывания tooproduction с простой и автоматизировать прогрева.</span><span class="sxs-lookup"><span data-stu-id="b23ff-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="b23ff-110">посредством release management продуктов, таких как Visual Studio Release Management можно легко автоматизировать Hello действия рабочего процесса развертывания.</span><span class="sxs-lookup"><span data-stu-id="b23ff-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="b23ff-111">Это обеспечивает координацию с другими ресурсами решения (например хранилищем данных), а также повторяемость и репликацию в различных единицах развертывания.</span><span class="sxs-lookup"><span data-stu-id="b23ff-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

