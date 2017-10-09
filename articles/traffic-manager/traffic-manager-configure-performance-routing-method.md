---
title: "Метод маршрутизации, с помощью диспетчера трафика Azure трафика производительности aaaConfigure | Документы Microsoft"
description: "В этой статье объясняется, как tooconfigure tooroute диспетчера трафика трафику toohello конечной точки с минимальной задержкой"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="6be23-103">Настроить метод маршрутизации трафика производительности hello</span><span class="sxs-lookup"><span data-stu-id="6be23-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="6be23-104">Hello метод маршрутизации трафика производительности позволяет конечной точке toohello трафика toodirect с минимальной задержкой hello из hello клиентской сети.</span><span class="sxs-lookup"><span data-stu-id="6be23-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="6be23-105">Как правило hello центра обработки данных с минимальной задержкой hello является физически ближайшим hello.</span><span class="sxs-lookup"><span data-stu-id="6be23-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="6be23-106">Этот метод маршрутизации трафика не учитывает изменения в конфигурации или загрузке сети в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="6be23-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="6be23-107">Метод маршрутизации tooconfigure производительности</span><span class="sxs-lookup"><span data-stu-id="6be23-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="6be23-108">В браузере вход toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6be23-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="6be23-109">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии на один месяц](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6be23-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="6be23-110">В строке поиска hello портала, поиск hello **профилей диспетчера трафика** и щелкните имя профиля hello нужного метода маршрутизации hello tooconfigure для.</span><span class="sxs-lookup"><span data-stu-id="6be23-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="6be23-111">В hello **профиль диспетчера трафика** колонки, убедитесь, что оба hello облачных служб и веб-сайтов, которые должны tooinclude в конфигурации присутствуют.</span><span class="sxs-lookup"><span data-stu-id="6be23-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="6be23-112">В hello **параметры** щелкните **конфигурации**и в hello **конфигурации** колонке завершения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6be23-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="6be23-113">В **параметрах метода маршрутизации трафика** в качестве **метода маршрутизации** выберите **Производительность**.</span><span class="sxs-lookup"><span data-stu-id="6be23-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="6be23-114">Набор hello **монитора параметры конечной точки** одинаков для всех каждой конечной точки в этот профиль, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="6be23-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="6be23-115">Выберите hello соответствующие **протокола**и укажите hello **порт** номер.</span><span class="sxs-lookup"><span data-stu-id="6be23-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="6be23-116">В поле **Путь** введите косую черту */*.</span><span class="sxs-lookup"><span data-stu-id="6be23-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="6be23-117">toomonitor конечных точек, необходимо указать путь и имя файла.</span><span class="sxs-lookup"><span data-stu-id="6be23-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="6be23-118">A косая черта «/» является допустимой записью для относительного пути hello и означает, что файл hello находится в корневом каталоге hello (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="6be23-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="6be23-119">В начале hello страницы приветствия, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6be23-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="6be23-120">Тестировать hello изменения в конфигурации следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6be23-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="6be23-121">В строке поиска hello портала найдите имя профиля диспетчера трафика hello и нажмите кнопку hello профиля диспетчера трафика в результатах hello, hello отображается.</span><span class="sxs-lookup"><span data-stu-id="6be23-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="6be23-122">В hello **диспетчера трафика** колонки, установите флажок **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="6be23-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="6be23-123">Hello **профиль диспетчера трафика** колонке отображает hello DNS-имя только что созданный профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="6be23-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="6be23-124">Это может использоваться любой клиентов (например, перейдя в веб-браузере tooit) tooget Маршрутизация toohello правого конечной точкой что определяется тип маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="6be23-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="6be23-125">В этом случае все запросы являются перенаправленное toohello конечной точке с минимальной задержкой hello из hello клиентской сети.</span><span class="sxs-lookup"><span data-stu-id="6be23-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="6be23-126">После работы вашего профиля диспетчера трафика измените запись DNS hello на ваш заслуживающий доверия сервер toopoint DNS домена имя toohello диспетчера трафика доменного имени вашей компании.</span><span class="sxs-lookup"><span data-stu-id="6be23-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Настройка метода маршрутизации трафика по производительности с помощью диспетчера трафика][1]

## <a name="next-steps"></a><span data-ttu-id="6be23-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6be23-128">Next steps</span></span>

- <span data-ttu-id="6be23-129">Узнайте о [методе взвешенной маршрутизации трафика](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="6be23-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="6be23-130">Узнайте о [методе маршрутизации по приоритету](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="6be23-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="6be23-131">Узнайте о [методе географической маршрутизации](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="6be23-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="6be23-132">Узнайте, каким образом слишком[проверить параметры диспетчера трафика](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6be23-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png