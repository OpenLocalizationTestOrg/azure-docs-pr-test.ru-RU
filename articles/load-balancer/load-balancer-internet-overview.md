---
title: "Общие сведения о балансировщике нагрузки, доступном в Интернете | Документация Майкрософт"
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="e5217-104">Обзор подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="e5217-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="e5217-105">Балансировщик нагрузки Azure сопоставляет общедоступный IP-адрес и номер порта для входящего трафика с частным IP-адресом и номером порта виртуальной машины и наоборот для ответного трафика из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e5217-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="e5217-106">Правила балансировки нагрузки позволяют распределить трафик определенных типов между несколькими виртуальными машинами или службами.</span><span class="sxs-lookup"><span data-stu-id="e5217-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="e5217-107">Например, можно распределить нагрузку от трафика веб-запросов на несколько веб-серверов или веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="e5217-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="e5217-108">Для облачной службы, которая содержит экземпляры веб-ролей или рабочих ролей, в определении службы (CSDEF-файле) можно определить общедоступную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="e5217-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="e5217-109">Файл *servicedefinition.csdef* содержит конфигурацию конечной точки. При наличии нескольких экземпляров роли для развертывания веб-ролей или рабочих ролей для конфигурации этой точки будет настроена подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5217-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="e5217-110">Чтобы добавить экземпляры для облачного развертывания, измените количество экземпляров в CSFG-файле конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="e5217-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="e5217-111">На следующем рисунке показана конечная точка с балансировкой нагрузки для веб-трафика, которая является общей для трех виртуальных машин на общедоступном и частном TCP-портах 80.</span><span class="sxs-lookup"><span data-stu-id="e5217-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="e5217-112">Эти три виртуальные машины находятся в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5217-112">These three virtual machines are in a load-balanced set.</span></span>

![пример общедоступной подсистемы балансировки нагрузки](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="e5217-114">Рисунок 1. Конечная точка с балансировкой нагрузки для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="e5217-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="e5217-115">Когда интернет-клиенты отправляют запросы к веб-страницам на общедоступный IP-адрес облачной службы в TCP-порт 80, Azure Load Balancer распределяет эти запросы между тремя виртуальными машинами в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5217-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="e5217-116">Дополнительные сведения об алгоритме балансировщика нагрузки см. на [странице обзора балансировщика нагрузки](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="e5217-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="e5217-117">По умолчанию Azure Load Balancer распределяет сетевой трафик между несколькими экземплярами виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5217-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="e5217-118">Вы также можете настроить сходство сеансов. Дополнительные сведения см. в разделе [Функции подсистемы балансировки нагрузки](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="e5217-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5217-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5217-119">Next steps</span></span>

<span data-ttu-id="e5217-120">Ознакомьтесь с информацией о [внутреннем балансировщике нагрузки](load-balancer-internal-overview.md), чтобы понять, какой балансировщик нагрузки лучше подходит для вашего облачного развертывания.</span><span class="sxs-lookup"><span data-stu-id="e5217-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="e5217-121">Вы также можете [приступить к созданию балансировщика нагрузки для Интернета](load-balancer-get-started-internet-arm-ps.md) и настройке типа [режима распределения](load-balancer-distribution-mode.md) для определенного поведения сетевого трафика балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5217-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="e5217-122">Если вашему приложению необходимо поддерживать подключения для серверов за балансировщиком нагрузки, можно получить дополнительные сведения о [параметрах времени ожидания простоя TCP для балансировщика нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="e5217-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="e5217-123">Вы узнаете о поведении неактивного подключения при использовании балансировщика нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="e5217-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
