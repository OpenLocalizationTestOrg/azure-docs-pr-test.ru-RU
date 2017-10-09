---
title: "Обзор интерфейса API ретрансляции aaaAzure | Документы Microsoft"
description: "Обзор доступных интерфейсов API ретранслятора Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="4550f-103">Доступные интерфейсы API ретранслятора</span><span class="sxs-lookup"><span data-stu-id="4550f-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="4550f-104">API среды выполнения</span><span class="sxs-lookup"><span data-stu-id="4550f-104">Runtime APIs</span></span>

<span data-ttu-id="4550f-105">Hello следующей таблице перечислены все клиенты в настоящее время доступна ретрансляции среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="4550f-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="4550f-106">Hello [дополнительной информацией](#additional-information) раздел содержит дополнительные сведения о состоянии hello каждой библиотеки времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="4550f-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="4550f-107">Язык или платформа</span><span class="sxs-lookup"><span data-stu-id="4550f-107">Language/Platform</span></span> | <span data-ttu-id="4550f-108">Доступная функция</span><span class="sxs-lookup"><span data-stu-id="4550f-108">Available feature</span></span> | <span data-ttu-id="4550f-109">Пакет клиента</span><span class="sxs-lookup"><span data-stu-id="4550f-109">Client package</span></span> | <span data-ttu-id="4550f-110">Репозиторий</span><span class="sxs-lookup"><span data-stu-id="4550f-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4550f-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4550f-111">.NET Standard</span></span> | <span data-ttu-id="4550f-112">через гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="4550f-112">Hybrid Connections</span></span> | [<span data-ttu-id="4550f-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="4550f-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="4550f-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="4550f-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="4550f-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4550f-115">.NET Framework</span></span> | <span data-ttu-id="4550f-116">Ретранслятор WCF</span><span class="sxs-lookup"><span data-stu-id="4550f-116">WCF Relay</span></span> | [<span data-ttu-id="4550f-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="4550f-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="4550f-118">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4550f-118">N/A</span></span> |
| <span data-ttu-id="4550f-119">Узел</span><span class="sxs-lookup"><span data-stu-id="4550f-119">Node</span></span> | <span data-ttu-id="4550f-120">через гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="4550f-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="4550f-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="4550f-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="4550f-122">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4550f-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="4550f-123">.NET</span><span class="sxs-lookup"><span data-stu-id="4550f-123">.NET</span></span>
<span data-ttu-id="4550f-124">экосистема Hello .NET имеет несколько сред выполнения, таким образом, существует несколько библиотек .NET для концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="4550f-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="4550f-125">Hello .NET стандартной библиотеки могут выполняться с помощью .NET Core или hello .NET Framework, пока hello библиотеки .NET Framework может выполняться только в среде .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4550f-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="4550f-126">Дополнительные сведения о версиях платформы .NET Framework см. в разделе [Версии платформ](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="4550f-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4550f-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4550f-127">Next steps</span></span>
<span data-ttu-id="4550f-128">toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="4550f-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="4550f-129">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="4550f-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4550f-130">Вопросы и ответы по ретранслятору</span><span class="sxs-lookup"><span data-stu-id="4550f-130">Relay FAQ</span></span>](relay-faq.md)