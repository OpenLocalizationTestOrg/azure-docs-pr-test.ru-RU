---
title: "tooend окончания aaaEnabling SSL для шлюза приложения Azure | Документы Microsoft"
description: "Эта страница Обзор hello шлюза приложения конечным tooend поддержки SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="6ce64-103">Общие сведения о конечных tooend SSL со шлюзом приложений</span><span class="sxs-lookup"><span data-stu-id="6ce64-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="6ce64-104">Шлюз приложений поддерживает завершения запросов SSL на шлюз hello после трафика обычно передаются в незашифрованном виде toohello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="6ce64-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="6ce64-105">Эта функция позволяет toobe серверы web unburdened от дорогостоящих издержки шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="6ce64-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="6ce64-106">Однако для некоторых клиентов незашифрованный обмен данными toohello внутренним серверам не приемлемый вариант.</span><span class="sxs-lookup"><span data-stu-id="6ce64-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="6ce64-107">Незашифрованный обмен информацией может быть вызвано toosecurity требования, требования соответствия, или приложение hello может принимать только безопасное соединение.</span><span class="sxs-lookup"><span data-stu-id="6ce64-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="6ce64-108">Для таких приложений приложения шлюз поддерживает tooend окончания SSL шифрования.</span><span class="sxs-lookup"><span data-stu-id="6ce64-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="6ce64-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="6ce64-109">Overview</span></span>

<span data-ttu-id="6ce64-110">Конец tooend SSL позволяет toosecurely передачи конфиденциальных данных серверной части toohello зашифрованы по-прежнему преимуществами hello преимущества балансировать нагрузку уровня 7 шлюз, который приложение предоставляет.</span><span class="sxs-lookup"><span data-stu-id="6ce64-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="6ce64-111">Некоторые из этих функций, сходство сеансов на основе файлов cookie, маршрутизация на основе URL-адреса, поддержку для маршрутизации на основе сайтов или возможности tooinject - перенаправленных - X * заголовки.</span><span class="sxs-lookup"><span data-stu-id="6ce64-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="6ce64-112">Если режиме обмен данными SSL tooend end, шлюз приложений завершает hello SSL-сеансов в шлюз hello и расшифровывает пользовательский трафик.</span><span class="sxs-lookup"><span data-stu-id="6ce64-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="6ce64-113">Затем она применяет правила tooselect hello настроен экземпляр tooroute соответствующих серверных пула трафик к.</span><span class="sxs-lookup"><span data-stu-id="6ce64-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="6ce64-114">Шлюз приложений затем инициирует новый внутреннему серверу toohello SSL подключение и повторно шифрует данные с помощью сертификата открытого ключа сервера hello базы данных перед их передачей серверной toohello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="6ce64-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="6ce64-115">Конец tooend, протокол SSL включен, установив параметр протокола в tooHTTPS BackendHTTPSetting, которое затем применить tooa внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="6ce64-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="6ce64-116">Сертификат tooallow безопасного взаимодействия должны быть настроены каждого сервера базы данных в пуле внутренних hello с tooend end, протокол SSL включен.</span><span class="sxs-lookup"><span data-stu-id="6ce64-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![сценарий tooend ssl][1]

<span data-ttu-id="6ce64-118">В этом примере запросы с использованием TLS1.2 являются серверы перенаправленное toobackend в Pool1 с помощью tooend окончания SSL.</span><span class="sxs-lookup"><span data-stu-id="6ce64-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="6ce64-119">Завершить tooend SSL и список утвержденных сертификатов</span><span class="sxs-lookup"><span data-stu-id="6ce64-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="6ce64-120">Шлюз приложений взаимодействует только с экземплярами известных серверной части, сертификат которых имеет входят их со шлюзом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6ce64-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="6ce64-121">Список утвержденных tooenable сертификатов, необходимо передать открытый ключ hello внутреннего сервера сертификатов toohello использование шлюза приложений (не hello корневого сертификата).</span><span class="sxs-lookup"><span data-stu-id="6ce64-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="6ce64-122">Затем разрешены серверных системах tooknown а входят только подключения.</span><span class="sxs-lookup"><span data-stu-id="6ce64-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="6ce64-123">Осталось серверных системах Hello приводит к ошибке шлюза.</span><span class="sxs-lookup"><span data-stu-id="6ce64-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="6ce64-124">Самозаверяющие сертификаты предназначены только для тестирования и не рекомендуются для рабочих нагрузок в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6ce64-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="6ce64-125">Такие сертификаты имеют входят toobe со шлюзом приложения hello, как описано в предыдущих шагах, прежде чем можно будет использовать hello.</span><span class="sxs-lookup"><span data-stu-id="6ce64-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ce64-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ce64-126">Next steps</span></span>

<span data-ttu-id="6ce64-127">После изучения tooend окончания SSL, go слишком[включить tooend окончания SSL на использование шлюза приложений](application-gateway-end-to-end-ssl-powershell.md) toocreate шлюза приложения с помощью завершить tooend SSL.</span><span class="sxs-lookup"><span data-stu-id="6ce64-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
