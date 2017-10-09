---
title: "Обзор интерфейса API концентраторов событий aaaAzure | Документы Microsoft"
description: "Обзор доступных интерфейсов API концентраторов событий Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="65c74-103">Доступные интерфейсы API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="65c74-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="65c74-104">API среды выполнения</span><span class="sxs-lookup"><span data-stu-id="65c74-104">Runtime APIs</span></span>

<span data-ttu-id="65c74-105">Hello ниже приводится описание всех доступных в данный момент клиентов концентраторов событий Azure времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="65c74-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="65c74-106">Хотя некоторые из этих библиотек также содержат функциональные возможности ограниченные возможности управления, есть также [определенных библиотек](#management-apis) выделенного toomanagement операций.</span><span class="sxs-lookup"><span data-stu-id="65c74-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="65c74-107">основной темой Hello эти библиотеки является toosend и получение сообщений из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="65c74-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="65c74-108">В разделе [дополнительной информацией](#additional-information) для получения дополнительных сведений о hello текущее состояние каждого библиотеки времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="65c74-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="65c74-109">Язык или платформа</span><span class="sxs-lookup"><span data-stu-id="65c74-109">Language/Platform</span></span> | <span data-ttu-id="65c74-110">Пакет клиента</span><span class="sxs-lookup"><span data-stu-id="65c74-110">Client package</span></span> | <span data-ttu-id="65c74-111">Пакет EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="65c74-111">EventProcessorHost package</span></span> | <span data-ttu-id="65c74-112">Репозиторий</span><span class="sxs-lookup"><span data-stu-id="65c74-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65c74-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="65c74-113">.NET Standard</span></span> | [<span data-ttu-id="65c74-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="65c74-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="65c74-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="65c74-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="65c74-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="65c74-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="65c74-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="65c74-117">.NET Framework</span></span> | [<span data-ttu-id="65c74-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="65c74-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="65c74-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="65c74-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="65c74-120">Недоступно</span><span class="sxs-lookup"><span data-stu-id="65c74-120">N/A</span></span> |
| <span data-ttu-id="65c74-121">Java</span><span class="sxs-lookup"><span data-stu-id="65c74-121">Java</span></span> | [<span data-ttu-id="65c74-122">Maven</span><span class="sxs-lookup"><span data-stu-id="65c74-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="65c74-123">Maven</span><span class="sxs-lookup"><span data-stu-id="65c74-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="65c74-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="65c74-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="65c74-125">Узел</span><span class="sxs-lookup"><span data-stu-id="65c74-125">Node</span></span> | [<span data-ttu-id="65c74-126">NPM</span><span class="sxs-lookup"><span data-stu-id="65c74-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="65c74-127">Недоступно</span><span class="sxs-lookup"><span data-stu-id="65c74-127">N/A</span></span> | [<span data-ttu-id="65c74-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="65c74-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="65c74-129">C</span><span class="sxs-lookup"><span data-stu-id="65c74-129">C</span></span> | <span data-ttu-id="65c74-130">Недоступно</span><span class="sxs-lookup"><span data-stu-id="65c74-130">N/A</span></span> | <span data-ttu-id="65c74-131">Недоступно</span><span class="sxs-lookup"><span data-stu-id="65c74-131">N/A</span></span> | [<span data-ttu-id="65c74-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="65c74-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="65c74-133">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="65c74-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="65c74-134">.NET</span><span class="sxs-lookup"><span data-stu-id="65c74-134">.NET</span></span>
<span data-ttu-id="65c74-135">экосистема Hello .NET имеет несколько сред выполнения, таким образом, существует несколько библиотек .NET для концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="65c74-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="65c74-136">Hello .NET стандартной библиотеки могут выполняться с помощью .NET Core или hello .NET Framework, пока hello библиотеки .NET Framework может выполняться только в среде .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="65c74-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="65c74-137">Дополнительные сведения о версиях платформы .NET Framework см. в разделе [Версии платформ](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="65c74-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="65c74-138">Узел</span><span class="sxs-lookup"><span data-stu-id="65c74-138">Node</span></span>

<span data-ttu-id="65c74-139">Библиотека Node.js Hello в настоящее время находится в предварительной версии и поддерживаются как части проекта с сотрудниками корпорации Майкрософт и внешних участников.</span><span class="sxs-lookup"><span data-stu-id="65c74-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="65c74-140">Все добавляемые материалы, включая исходный код, принимаются и проверяются.</span><span class="sxs-lookup"><span data-stu-id="65c74-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="65c74-141">API управления</span><span class="sxs-lookup"><span data-stu-id="65c74-141">Management APIs</span></span>

<span data-ttu-id="65c74-142">Hello ниже приведен список всех доступных в настоящее время управления определенных библиотек.</span><span class="sxs-lookup"><span data-stu-id="65c74-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="65c74-143">Ни один из этих библиотек содержат операций среды выполнения и являются единственной целью hello управления сущностями концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="65c74-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="65c74-144">Язык или платформа</span><span class="sxs-lookup"><span data-stu-id="65c74-144">Language/Platform</span></span> | <span data-ttu-id="65c74-145">Пакет управления</span><span class="sxs-lookup"><span data-stu-id="65c74-145">Management package</span></span> | <span data-ttu-id="65c74-146">Репозиторий</span><span class="sxs-lookup"><span data-stu-id="65c74-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65c74-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="65c74-147">.NET Standard</span></span> | [<span data-ttu-id="65c74-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="65c74-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="65c74-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="65c74-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="65c74-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65c74-150">Next steps</span></span>
<span data-ttu-id="65c74-151">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="65c74-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="65c74-152">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="65c74-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="65c74-153">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="65c74-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="65c74-154">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="65c74-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)