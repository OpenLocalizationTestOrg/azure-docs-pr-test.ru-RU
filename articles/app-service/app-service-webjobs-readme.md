---
title: "Веб-задания в службе приложений Azure"
description: "Узнайте, как создавать веб-задания для выполнения фоновых тестов, взаимодействия с такими службами, как хранилище и служебная шина, а также создания плановых задач."
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
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="f1a4d-103">Использование веб-заданий в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="f1a4d-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="f1a4d-104">В данной статье содержатся ссылки на документацию о том, как применять веб-задания Azure и пакет SDK веб-заданий Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="f1a4d-105">Веб-задания Azure предоставляют простой способ запуска скриптов и программ в виде фоновых процессов [веб-приложений службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f1a4d-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f1a4d-106">Можно загружать и запускать исполняемые файлы, например cmd, bat, exe (.NET), ps1, sh, php, py, js и jar.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="f1a4d-107">Эти программы могут работать как веб-задания по расписанию (cron) или постоянно.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="f1a4d-108">Пакет SDK веб-заданий упрощает использование хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="f1a4d-109">Пакет SDK веб-заданий имеет систему привязки и запуска, которая работает совместно с хранилищем Microsoft Azure для BLOB-объектов, очередей и таблиц, а также очередей служебной шины.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="f1a4d-110">Создание, развертывание веб-заданий и управление ими средствами Visual Studio не вызовет проблем.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="f1a4d-111">Веб-задания можно создавать из шаблонов, публиковать их и управлять ими (запуск/остановка/мониторинг/jnkflrf).</span><span class="sxs-lookup"><span data-stu-id="f1a4d-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="f1a4d-112">Панель мониторинга веб-заданий на портале Azure предоставляет широкие возможности управления и полный контроль над выполнением веб-заданий, включая возможность вызова отдельных функций в рамках самого веб-задания.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="f1a4d-113">Информационная панель также показывает состояние исполняемой среды и записи журнала.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

