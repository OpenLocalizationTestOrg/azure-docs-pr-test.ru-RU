---
title: "Поддержка aaaHTTP/2 в Azure CDN | Документы Microsoft"
description: "Сведения о поддержке HTTP/2 и CDN."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="3fc80-103">Поддержка HTTP/2 в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3fc80-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="3fc80-104">HTTP/2 соответствует tooHTTP/1.1\ основной версии.</span><span class="sxs-lookup"><span data-stu-id="3fc80-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="3fc80-105">Он содержит быстрее веб-тестов производительности, уменьшения времени ответа и улучшенное взаимодействие с пользователем, сохраняя hello известные методы HTTP, коды состояния и семантику.</span><span class="sxs-lookup"><span data-stu-id="3fc80-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="3fc80-106">Хотя HTTP/2 спроектированный toowork HTTP и HTTPS, многие клиента веб-браузеры поддерживают только HTTP/2 через TLS.</span><span class="sxs-lookup"><span data-stu-id="3fc80-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="3fc80-107">Преимущества HTTP/2</span><span class="sxs-lookup"><span data-stu-id="3fc80-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="3fc80-108">преимущества Hello HTTP/2:</span><span class="sxs-lookup"><span data-stu-id="3fc80-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="3fc80-109">**Мультиплексирование и параллелизм**</span><span class="sxs-lookup"><span data-stu-id="3fc80-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="3fc80-110">При использовании HTTP 1.1 для выполнения нескольких запросов ресурсов требуется несколько TCP-подключений, и с каждым подключением связаны определенные затраты производительности.</span><span class="sxs-lookup"><span data-stu-id="3fc80-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="3fc80-111">HTTP/2 обеспечивает несколько toobe ресурсы, запрошенный для одного подключения TCP.</span><span class="sxs-lookup"><span data-stu-id="3fc80-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="3fc80-112">**Сжатие заголовка**</span><span class="sxs-lookup"><span data-stu-id="3fc80-112">**Header compression**</span></span>

    <span data-ttu-id="3fc80-113">Сжатие заголовков hello HTTP обслуживаются ресурсов, сети hello сокращает время значительно.</span><span class="sxs-lookup"><span data-stu-id="3fc80-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="3fc80-114">**Зависимости потоков**</span><span class="sxs-lookup"><span data-stu-id="3fc80-114">**Stream dependencies**</span></span>

    <span data-ttu-id="3fc80-115">Поток зависимости разрешить клиентским hello server toohello tooindicate, какие ресурсы имеют приоритет.</span><span class="sxs-lookup"><span data-stu-id="3fc80-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="3fc80-116">Поддержка HTTP/2 в браузерах</span><span class="sxs-lookup"><span data-stu-id="3fc80-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="3fc80-117">Все основные обозреватели hello реализована поддержка HTTP/2 в своей текущей версии.</span><span class="sxs-lookup"><span data-stu-id="3fc80-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="3fc80-118">Неподдерживаемые браузеры будут автоматически tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="3fc80-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="3fc80-119">"Обзор"</span><span class="sxs-lookup"><span data-stu-id="3fc80-119">Browser</span></span>|<span data-ttu-id="3fc80-120">Минимальная версия</span><span class="sxs-lookup"><span data-stu-id="3fc80-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="3fc80-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="3fc80-121">Microsoft Edge</span></span>| <span data-ttu-id="3fc80-122">12</span><span class="sxs-lookup"><span data-stu-id="3fc80-122">12</span></span>|
|<span data-ttu-id="3fc80-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="3fc80-123">Google Chrome</span></span>| <span data-ttu-id="3fc80-124">43</span><span class="sxs-lookup"><span data-stu-id="3fc80-124">43</span></span>|
|<span data-ttu-id="3fc80-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="3fc80-125">Mozilla Firefox</span></span>| <span data-ttu-id="3fc80-126">38</span><span class="sxs-lookup"><span data-stu-id="3fc80-126">38</span></span>|
|<span data-ttu-id="3fc80-127">Opera</span><span class="sxs-lookup"><span data-stu-id="3fc80-127">Opera</span></span>| <span data-ttu-id="3fc80-128">32</span><span class="sxs-lookup"><span data-stu-id="3fc80-128">32</span></span>|
|<span data-ttu-id="3fc80-129">Safari</span><span class="sxs-lookup"><span data-stu-id="3fc80-129">Safari</span></span>| <span data-ttu-id="3fc80-130">9</span><span class="sxs-lookup"><span data-stu-id="3fc80-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="3fc80-131">Включение HTTP/2 в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3fc80-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="3fc80-132">Сейчас поддержка HTTP/2 активна в профилях **Azure CDN от Akamai** и **Azure CDN от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="3fc80-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="3fc80-133">Никаких действий со стороны пользователей не требуется.</span><span class="sxs-lookup"><span data-stu-id="3fc80-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="3fc80-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fc80-134">Next Steps</span></span>

<span data-ttu-id="3fc80-135">toosee преимущества HTTP/2 hello в действии, в разделе [этой демонстрации из Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="3fc80-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="3fc80-136">toolearn Дополнительные сведения о HTTP/2, посетите hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="3fc80-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="3fc80-137">Домашняя страница спецификации HTTP/2</span><span class="sxs-lookup"><span data-stu-id="3fc80-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="3fc80-138">Официальная страница часто задаваемых вопросов об HTTP/2</span><span class="sxs-lookup"><span data-stu-id="3fc80-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="3fc80-139">Сведения об HTTP/2 на сайте Akamai</span><span class="sxs-lookup"><span data-stu-id="3fc80-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="3fc80-140">toolearn Дополнительные сведения о Azure CDN доступные компоненты, в разделе hello [Общие сведения о Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="3fc80-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
