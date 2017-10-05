---
title: "Обзор API концентраторов событий Azure | Документация Майкрософт"
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
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="e66e1-103">Доступные интерфейсы API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="e66e1-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="e66e1-104">API среды выполнения</span><span class="sxs-lookup"><span data-stu-id="e66e1-104">Runtime APIs</span></span>

<span data-ttu-id="e66e1-105">Ниже приведено описание всех доступных в настоящее время клиентов в среде выполнения для концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="e66e1-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="e66e1-106">Хотя некоторые из этих библиотек включают в себя ограниченные функции управления, также существуют [специальные библиотеки](#management-apis), предназначенные для операций управления.</span><span class="sxs-lookup"><span data-stu-id="e66e1-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="e66e1-107">Основной задачей этих библиотек является отправка сообщений в концентратор событий и получение их из него.</span><span class="sxs-lookup"><span data-stu-id="e66e1-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="e66e1-108">Ознакомьтесь с разделом [Дополнительная информация](#additional-information), чтобы узнать больше о текущем состоянии каждой библиотеки среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="e66e1-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="e66e1-109">Язык или платформа</span><span class="sxs-lookup"><span data-stu-id="e66e1-109">Language/Platform</span></span> | <span data-ttu-id="e66e1-110">Пакет клиента</span><span class="sxs-lookup"><span data-stu-id="e66e1-110">Client package</span></span> | <span data-ttu-id="e66e1-111">Пакет EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e66e1-111">EventProcessorHost package</span></span> | <span data-ttu-id="e66e1-112">Репозиторий</span><span class="sxs-lookup"><span data-stu-id="e66e1-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e66e1-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="e66e1-113">.NET Standard</span></span> | [<span data-ttu-id="e66e1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="e66e1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="e66e1-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="e66e1-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="e66e1-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="e66e1-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="e66e1-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="e66e1-117">.NET Framework</span></span> | [<span data-ttu-id="e66e1-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="e66e1-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="e66e1-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="e66e1-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="e66e1-120">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e66e1-120">N/A</span></span> |
| <span data-ttu-id="e66e1-121">Java</span><span class="sxs-lookup"><span data-stu-id="e66e1-121">Java</span></span> | [<span data-ttu-id="e66e1-122">Maven</span><span class="sxs-lookup"><span data-stu-id="e66e1-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="e66e1-123">Maven</span><span class="sxs-lookup"><span data-stu-id="e66e1-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="e66e1-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="e66e1-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="e66e1-125">Узел</span><span class="sxs-lookup"><span data-stu-id="e66e1-125">Node</span></span> | [<span data-ttu-id="e66e1-126">NPM</span><span class="sxs-lookup"><span data-stu-id="e66e1-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="e66e1-127">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e66e1-127">N/A</span></span> | [<span data-ttu-id="e66e1-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="e66e1-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="e66e1-129">C</span><span class="sxs-lookup"><span data-stu-id="e66e1-129">C</span></span> | <span data-ttu-id="e66e1-130">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e66e1-130">N/A</span></span> | <span data-ttu-id="e66e1-131">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e66e1-131">N/A</span></span> | [<span data-ttu-id="e66e1-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="e66e1-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="e66e1-133">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e66e1-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="e66e1-134">.NET</span><span class="sxs-lookup"><span data-stu-id="e66e1-134">.NET</span></span>
<span data-ttu-id="e66e1-135">В экосистеме .NET существует несколько сред выполнения, поэтому для концентраторов событий используется несколько библиотек .NET.</span><span class="sxs-lookup"><span data-stu-id="e66e1-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="e66e1-136">Библиотеку .NET Standard можно запустить с помощью .NET Core или .NET Framework, а библиотеку .NET Framework можно запустить только в среде .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e66e1-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="e66e1-137">Дополнительные сведения о версиях платформы .NET Framework см. в разделе [Версии платформ](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="e66e1-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="e66e1-138">Узел</span><span class="sxs-lookup"><span data-stu-id="e66e1-138">Node</span></span>

<span data-ttu-id="e66e1-139">В настоящее время доступна предварительная версия библиотеки Node.js. Она поддерживается как параллельный проект сотрудниками корпорации Майкрософт и внешними соавторами.</span><span class="sxs-lookup"><span data-stu-id="e66e1-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="e66e1-140">Все добавляемые материалы, включая исходный код, принимаются и проверяются.</span><span class="sxs-lookup"><span data-stu-id="e66e1-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="e66e1-141">API управления</span><span class="sxs-lookup"><span data-stu-id="e66e1-141">Management APIs</span></span>

<span data-ttu-id="e66e1-142">Ниже приведен список всех доступных специальных библиотеки, предназначенных для операций управления.</span><span class="sxs-lookup"><span data-stu-id="e66e1-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="e66e1-143">Ни одна из этих библиотек не содержит операций среды выполнения. Они предназначены только для управления сущностями концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="e66e1-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="e66e1-144">Язык или платформа</span><span class="sxs-lookup"><span data-stu-id="e66e1-144">Language/Platform</span></span> | <span data-ttu-id="e66e1-145">Пакет управления</span><span class="sxs-lookup"><span data-stu-id="e66e1-145">Management package</span></span> | <span data-ttu-id="e66e1-146">Репозиторий</span><span class="sxs-lookup"><span data-stu-id="e66e1-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e66e1-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="e66e1-147">.NET Standard</span></span> | [<span data-ttu-id="e66e1-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="e66e1-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="e66e1-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="e66e1-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="e66e1-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e66e1-150">Next steps</span></span>
<span data-ttu-id="e66e1-151">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="e66e1-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e66e1-152">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="e66e1-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e66e1-153">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="e66e1-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e66e1-154">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="e66e1-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)