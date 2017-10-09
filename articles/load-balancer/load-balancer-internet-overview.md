---
title: "Обзор подсистемы балансировки нагрузки с выходом aaaInternet | Документы Microsoft"
description: "Обзор подсистемы балансировки нагрузки, доступной в Интернете, и ее функций. Информация о принципе работы подсистемы балансировки нагрузки с виртуальными машинами и облачными службами в Azure."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="6a442-104">Обзор подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="6a442-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="6a442-105">Подсистема балансировки нагрузки Azure сопоставляет hello открытый IP адрес и номер порта входящего трафика toohello частного IP адрес и номер порта hello виртуальной машины и наоборот hello ответного трафика от виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="6a442-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="6a442-106">Правила балансировки нагрузки позволяют toodistribute определенных типов трафика между несколькими виртуальные машины или службы.</span><span class="sxs-lookup"><span data-stu-id="6a442-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="6a442-107">Например можно распределить hello нагрузки трафика веб-запросов по нескольким веб-серверам или веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="6a442-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="6a442-108">Для облачной службы, которая содержит экземпляры веб-ролей или рабочих ролей можно определить общедоступной конечной точки в файле определения службы(.csdef) hello службы.</span><span class="sxs-lookup"><span data-stu-id="6a442-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="6a442-109">Hello *servicedefinition.csdef* файл содержит конфигурацию конечной точки hello и при наличии нескольких экземпляров роли для рабочих и веб-развертывания роли балансировки нагрузки hello будет настроен для него.</span><span class="sxs-lookup"><span data-stu-id="6a442-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="6a442-110">Hello способом tooadd экземпляров tooyour облачного развертывания является изменение hello число экземпляров на файл конфигурации службы hello (.csfg).</span><span class="sxs-lookup"><span data-stu-id="6a442-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="6a442-111">Hello на этом рисунке показано к конечной точке с балансировкой нагрузки для веб-трафик, который разделяется между тремя виртуальными машинами для hello открытого и закрытого TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="6a442-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="6a442-112">Эти три виртуальные машины находятся в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a442-112">These three virtual machines are in a load-balanced set.</span></span>

![пример общедоступной подсистемы балансировки нагрузки](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="6a442-114">Рисунок 1. Конечная точка с балансировкой нагрузки для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="6a442-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="6a442-115">Если Интернет-клиент отправляет запросы веб-страниц toohello общедоступный IP-адрес облачной службы hello на TCP-порт 80, hello подсистемы балансировки нагрузки Azure распределяет запросы hello между hello три виртуальные машины в наборе балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="6a442-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="6a442-116">Дополнительные сведения об алгоритмах балансировки нагрузки см. в разделе hello [страница обзора подсистемы балансировки нагрузки](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="6a442-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="6a442-117">По умолчанию Azure Load Balancer распределяет сетевой трафик между несколькими экземплярами виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6a442-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="6a442-118">Вы также можете настроить сходство сеансов. Дополнительные сведения см. в разделе [Функции подсистемы балансировки нагрузки](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="6a442-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a442-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a442-119">Next steps</span></span>

<span data-ttu-id="6a442-120">Дополнительные сведения о [внутренняя Подсистема балансировки нагрузки](load-balancer-internal-overview.md) toobetter понять, какие подсистемы балансировки нагрузки лучше подойдет для развертывания облака.</span><span class="sxs-lookup"><span data-stu-id="6a442-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="6a442-121">Вы также можете [приступить к созданию балансировщика нагрузки для Интернета](load-balancer-get-started-internet-arm-ps.md) и настройке типа [режима распределения](load-balancer-distribution-mode.md) для определенного поведения сетевого трафика балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6a442-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="6a442-122">Если приложению tookeep подключений проверки активности для серверов в подсистему балансировки нагрузки, можно понять больше о [простоя параметры времени ожидания TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="6a442-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="6a442-123">Это поможет toolearn о поведении простоя подключения при использовании подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="6a442-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
