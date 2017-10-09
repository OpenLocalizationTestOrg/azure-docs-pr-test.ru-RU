---
title: "Метод маршрутизации, с помощью диспетчера трафика Azure трафика aaaConfigure Взвешенное циклического | Документы Microsoft"
description: "В этой статье объясняется, как tooload балансировки трафика, циклический перебор в диспетчере трафика"
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="d712a-103">Настроить метод маршрутизации трафика hello со смещением в диспетчере трафика</span><span class="sxs-lookup"><span data-stu-id="d712a-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="d712a-104">Общий шаблон маршрутизации метод трафика — tooprovide набор идентичных конечных точек, то есть облачных служб и веб-сайтов и отправки трафика tooeach в циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="d712a-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="d712a-105">следующие шаги Hello структуры как tooconfigure данный тип метод маршрутизации трафика.</span><span class="sxs-lookup"><span data-stu-id="d712a-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="d712a-106">Веб-сайты Azure уже обеспечивают балансировку нагрузки с циклическим перебором для веб-сайтов в центре данных (регионе).</span><span class="sxs-lookup"><span data-stu-id="d712a-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="d712a-107">Диспетчер трафика позволяет метод маршрутизации трафика циклическое toospecify для веб-сайтов в разных центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d712a-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="d712a-108">Метод маршрутизации трафика tooconfigure hello со смещением</span><span class="sxs-lookup"><span data-stu-id="d712a-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="d712a-109">В браузере вход toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d712a-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d712a-110">Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии на один месяц](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d712a-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="d712a-111">В строке поиска hello портала, поиск hello **профилей диспетчера трафика** и щелкните имя профиля hello нужного метода маршрутизации hello tooconfigure для.</span><span class="sxs-lookup"><span data-stu-id="d712a-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="d712a-112">В hello **профиль диспетчера трафика** колонки, убедитесь, что оба hello облачных служб и веб-сайтов, которые должны tooinclude в конфигурации присутствуют.</span><span class="sxs-lookup"><span data-stu-id="d712a-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="d712a-113">В hello **параметры** щелкните **конфигурации**и в hello **конфигурации** колонке завершения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d712a-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="d712a-114">Для **параметры метода маршрутизации трафика**, убедитесь, что метод маршрутизации трафика hello **Взвешенное**.</span><span class="sxs-lookup"><span data-stu-id="d712a-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="d712a-115">Если это не так, нажмите кнопку **Взвешенное** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="d712a-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="d712a-116">Набор hello **монитора параметры конечной точки** одинаков для всех каждой конечной точки в этот профиль, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d712a-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="d712a-117">Выберите hello соответствующие **протокола**и укажите hello **порт** номер.</span><span class="sxs-lookup"><span data-stu-id="d712a-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="d712a-118">В поле **Путь** введите косую черту */*.</span><span class="sxs-lookup"><span data-stu-id="d712a-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="d712a-119">toomonitor конечных точек, необходимо указать путь и имя файла.</span><span class="sxs-lookup"><span data-stu-id="d712a-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="d712a-120">A косая черта «/» является допустимой записью для относительного пути hello и означает, что файл hello находится в корневом каталоге hello (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="d712a-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="d712a-121">В начале hello страницы приветствия, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d712a-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="d712a-122">Тестировать hello изменения в конфигурации следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d712a-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="d712a-123">В строке поиска hello портала найдите имя профиля диспетчера трафика hello и нажмите кнопку hello профиля диспетчера трафика в результатах hello, hello отображается.</span><span class="sxs-lookup"><span data-stu-id="d712a-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="d712a-124">В hello **диспетчера трафика** колонки, установите флажок **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d712a-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="d712a-125">Hello **профиль диспетчера трафика** колонке отображает hello DNS-имя только что созданный профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="d712a-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="d712a-126">Это может использоваться любой клиентов (например, перейдя в веб-браузере tooit) tooget Маршрутизация toohello правого конечной точкой что определяется тип маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="d712a-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="d712a-127">В этом случае все запросы направляются к каждой конечной точке методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="d712a-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="d712a-128">После работы вашего профиля диспетчера трафика измените запись DNS hello на ваш заслуживающий доверия сервер toopoint DNS домена имя toohello диспетчера трафика доменного имени вашей компании.</span><span class="sxs-lookup"><span data-stu-id="d712a-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Настройка метода взвешенной маршрутизации трафика с помощью диспетчера трафика][1]

## <a name="next-steps"></a><span data-ttu-id="d712a-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d712a-130">Next steps</span></span>

- <span data-ttu-id="d712a-131">Узнайте больше о [методе маршрутизации по приоритету](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d712a-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="d712a-132">Узнайте больше о [методе маршрутизации по производительности](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d712a-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="d712a-133">Узнайте о [методе географической маршрутизации](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d712a-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="d712a-134">Узнайте, каким образом слишком[проверить параметры диспетчера трафика](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d712a-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
