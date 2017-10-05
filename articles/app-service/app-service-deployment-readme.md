---
title: "Развертывание приложений в службе приложений Azure"
description: "Узнайте, как развертывать приложения для работы службы приложений"
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
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="368b7-104">Общие сведения о развертывании службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="368b7-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="368b7-105">Служба приложений Azure предоставляет широкий, интегрированный набор функций для создания эффективных и гибких рабочих процессов развертывания.</span><span class="sxs-lookup"><span data-stu-id="368b7-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="368b7-106">При развертывании приложений можно использовать такие возможности, как непрерывная интеграция, публикация из локальной системы управления версиями, WebDeploy и FTP.</span><span class="sxs-lookup"><span data-stu-id="368b7-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="368b7-107">Рекомендуемый метод развертывания рабочих приложений — переключение областей развертывания.</span><span class="sxs-lookup"><span data-stu-id="368b7-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="368b7-108">Слоты развертывания представляют собой промежуточные среды и среды развертывания, связанные с рабочими приложениями.</span><span class="sxs-lookup"><span data-stu-id="368b7-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="368b7-109">Слоты развертывания можно настраивать и направлять на веб-трафик, требующий проверки, а трафик по запросу переключать на развертывание в рабочей среде без какого-либо простоя и автоматического прогрева.</span><span class="sxs-lookup"><span data-stu-id="368b7-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="368b7-110">Этапы рабочего процесса развертывания легко автоматизируются с помощью таких систем, как служба управления выпусками Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="368b7-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="368b7-111">Это обеспечивает координацию с другими ресурсами решения (например хранилищем данных), а также повторяемость и репликацию в различных единицах развертывания.</span><span class="sxs-lookup"><span data-stu-id="368b7-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

