---
title: "Поддержка HTTP/2 в Azure CDN | Документы Майкрософт"
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
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="1c226-103">Поддержка HTTP/2 в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1c226-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="1c226-104">HTTP/2 является основной версии для HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="1c226-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="1c226-105">Он содержит быстрее веб-тестов производительности, уменьшения времени ответа и улучшенное взаимодействие с пользователем, сохраняя известные методы HTTP, коды состояния и семантику.</span><span class="sxs-lookup"><span data-stu-id="1c226-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="1c226-106">Хотя HTTP/2 предназначен для работы с HTTP и HTTPS, многие клиентские веб-браузеры поддерживают только HTTP/2 через TLS.</span><span class="sxs-lookup"><span data-stu-id="1c226-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="1c226-107">Преимущества HTTP/2</span><span class="sxs-lookup"><span data-stu-id="1c226-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="1c226-108">Преимущества HTTP/2 перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="1c226-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="1c226-109">**Мультиплексирование и параллелизм**</span><span class="sxs-lookup"><span data-stu-id="1c226-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="1c226-110">При использовании HTTP 1.1 для выполнения нескольких запросов ресурсов требуется несколько TCP-подключений, и с каждым подключением связаны определенные затраты производительности.</span><span class="sxs-lookup"><span data-stu-id="1c226-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="1c226-111">HTTP/2 позволяет запрашивать несколько ресурсов через одно TCP-подключение.</span><span class="sxs-lookup"><span data-stu-id="1c226-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="1c226-112">**Сжатие заголовка**</span><span class="sxs-lookup"><span data-stu-id="1c226-112">**Header compression**</span></span>

    <span data-ttu-id="1c226-113">Благодаря сжатию HTTP-заголовков для обслуживаемых ресурсов значительно уменьшается время в сети.</span><span class="sxs-lookup"><span data-stu-id="1c226-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="1c226-114">**Зависимости потоков**</span><span class="sxs-lookup"><span data-stu-id="1c226-114">**Stream dependencies**</span></span>

    <span data-ttu-id="1c226-115">Зависимости потоков позволяют клиенту указывать серверу, какие из ресурсов имеют приоритет.</span><span class="sxs-lookup"><span data-stu-id="1c226-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="1c226-116">Поддержка HTTP/2 в браузерах</span><span class="sxs-lookup"><span data-stu-id="1c226-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="1c226-117">Во всех текущих версиях основных браузеров реализована поддержка HTTP/2.</span><span class="sxs-lookup"><span data-stu-id="1c226-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="1c226-118">Неподдерживаемые браузеры будет автоматически использовать HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="1c226-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="1c226-119">"Обзор"</span><span class="sxs-lookup"><span data-stu-id="1c226-119">Browser</span></span>|<span data-ttu-id="1c226-120">Минимальная версия</span><span class="sxs-lookup"><span data-stu-id="1c226-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="1c226-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="1c226-121">Microsoft Edge</span></span>| <span data-ttu-id="1c226-122">12</span><span class="sxs-lookup"><span data-stu-id="1c226-122">12</span></span>|
|<span data-ttu-id="1c226-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="1c226-123">Google Chrome</span></span>| <span data-ttu-id="1c226-124">43</span><span class="sxs-lookup"><span data-stu-id="1c226-124">43</span></span>|
|<span data-ttu-id="1c226-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="1c226-125">Mozilla Firefox</span></span>| <span data-ttu-id="1c226-126">38</span><span class="sxs-lookup"><span data-stu-id="1c226-126">38</span></span>|
|<span data-ttu-id="1c226-127">Opera</span><span class="sxs-lookup"><span data-stu-id="1c226-127">Opera</span></span>| <span data-ttu-id="1c226-128">32</span><span class="sxs-lookup"><span data-stu-id="1c226-128">32</span></span>|
|<span data-ttu-id="1c226-129">Safari</span><span class="sxs-lookup"><span data-stu-id="1c226-129">Safari</span></span>| <span data-ttu-id="1c226-130">9</span><span class="sxs-lookup"><span data-stu-id="1c226-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="1c226-131">Включение HTTP/2 в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1c226-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="1c226-132">Сейчас поддержка HTTP/2 активна в профилях **Azure CDN от Akamai** и **Azure CDN от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="1c226-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="1c226-133">Никаких действий со стороны пользователей не требуется.</span><span class="sxs-lookup"><span data-stu-id="1c226-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="1c226-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c226-134">Next Steps</span></span>

<span data-ttu-id="1c226-135">Преимущества HTTP/2 в действии представлены в [этой демонстрации от Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="1c226-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="1c226-136">Дополнительные сведения о HTTP/2 см. в следующих ресурсах.</span><span class="sxs-lookup"><span data-stu-id="1c226-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="1c226-137">Домашняя страница спецификации HTTP/2</span><span class="sxs-lookup"><span data-stu-id="1c226-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="1c226-138">Официальная страница часто задаваемых вопросов об HTTP/2</span><span class="sxs-lookup"><span data-stu-id="1c226-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="1c226-139">Сведения об HTTP/2 на сайте Akamai</span><span class="sxs-lookup"><span data-stu-id="1c226-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="1c226-140">Дополнительные сведения о доступных функциях Azure CDN см. в статье [Общие сведения о сети доставки содержимого (CDN) Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="1c226-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>