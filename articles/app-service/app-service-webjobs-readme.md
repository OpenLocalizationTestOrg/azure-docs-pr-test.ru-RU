---
title: "aaaWebJobs в службе приложений Azure"
description: "Узнайте, как проверяет toobuild toorun фона веб-заданий, взаимодействовать со службами, такими как хранилища и Service Bus и создавать запланированные задачи."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="beda0-103">Использование веб-заданий в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="beda0-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="beda0-104">В этой статье ссылки ресурсов toodocumentation о toouse веб-заданий Azure и hello Azure SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="beda0-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="beda0-105">Веб-задания Azure предоставляют простой способ toorun сценариев или программ в качестве фоновые процессы на [веб-приложений служб приложения](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="beda0-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="beda0-106">Можно загружать и запускать исполняемые файлы, например cmd, bat, exe (.NET), ps1, sh, php, py, js и jar.</span><span class="sxs-lookup"><span data-stu-id="beda0-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="beda0-107">Эти программы могут работать как веб-задания по расписанию (cron) или постоянно.</span><span class="sxs-lookup"><span data-stu-id="beda0-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="beda0-108">Hello SDK веб-заданий упрощает проще toouse хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="beda0-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="beda0-109">Hello SDK веб-задания имеет привязку и триггер систему, которая работает с хранилища больших двоичных объектов Microsoft Azure, очередей и таблиц, а также очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="beda0-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="beda0-110">Создание, развертывание веб-заданий и управление ими средствами Visual Studio не вызовет проблем.</span><span class="sxs-lookup"><span data-stu-id="beda0-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="beda0-111">Веб-задания можно создавать из шаблонов, публиковать их и управлять ими (запуск/остановка/мониторинг/jnkflrf).</span><span class="sxs-lookup"><span data-stu-id="beda0-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="beda0-112">панель мониторинга веб-заданий Hello в hello портал Azure предоставляет возможности управления, которые обеспечивают полный контроль над hello выполнение веб-заданий, включая hello возможность tooinvoke отдельные функции в веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="beda0-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="beda0-113">панель мониторинга Hello также отображает функции среды выполнения и вывода.</span><span class="sxs-lookup"><span data-stu-id="beda0-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

