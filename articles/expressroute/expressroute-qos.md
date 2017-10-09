---
title: "Требования к ExpressRoute aaaQoS | Документы Microsoft"
description: "На этой странице подробно описаны требования по настройке качества обслуживания для каналов ExpressRoute и управлению им."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="8bb47-103">Требования к качеству обслуживания для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8bb47-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="8bb47-104">В Skype для бизнеса имеются различные рабочие нагрузки, требующие дифференцированного подхода к качеству обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8bb47-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="8bb47-105">Если планируется tooconsume голоса службы с помощью ExpressRoute, необходимо придерживаться toohello требованиям, описанным ниже.</span><span class="sxs-lookup"><span data-stu-id="8bb47-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="8bb47-106">Требования к QoS применяются toohello только пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8bb47-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="8bb47-107">значения DSCP Hello в вашей сетевой трафик, поступающий на Azure для общедоступного пиринга и открытого пиринга Azure будут too0 сброса.</span><span class="sxs-lookup"><span data-stu-id="8bb47-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="8bb47-108">Hello следующей таблице приведен список маркировку DSCP, используемые Скайп для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="8bb47-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="8bb47-109">См. слишком[управление QoS для Скайп для бизнеса](https://technet.microsoft.com/library/gg405409.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="8bb47-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="8bb47-110">**Класс трафика**</span><span class="sxs-lookup"><span data-stu-id="8bb47-110">**Traffic Class**</span></span> | <span data-ttu-id="8bb47-111">**Обработка (пометки DSCP)**</span><span class="sxs-lookup"><span data-stu-id="8bb47-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="8bb47-112">**Рабочие нагрузки Skype для бизнеса**</span><span class="sxs-lookup"><span data-stu-id="8bb47-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bb47-113">**Голосовая связь**</span><span class="sxs-lookup"><span data-stu-id="8bb47-113">**Voice**</span></span> |<span data-ttu-id="8bb47-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="8bb47-114">EF (46)</span></span> |<span data-ttu-id="8bb47-115">Голосовая связь Skype и Lync</span><span class="sxs-lookup"><span data-stu-id="8bb47-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="8bb47-116">**Интерактивный**</span><span class="sxs-lookup"><span data-stu-id="8bb47-116">**Interactive**</span></span> |<span data-ttu-id="8bb47-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="8bb47-117">AF41 (34)</span></span> |<span data-ttu-id="8bb47-118">Видео, VBSS</span><span class="sxs-lookup"><span data-stu-id="8bb47-118">Video, VBSS</span></span> |
| <span data-ttu-id="8bb47-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="8bb47-119">AF21 (18)</span></span> |<span data-ttu-id="8bb47-120">Совместный доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="8bb47-120">App sharing</span></span> | |
| <span data-ttu-id="8bb47-121">**По умолчанию**</span><span class="sxs-lookup"><span data-stu-id="8bb47-121">**Default**</span></span> |<span data-ttu-id="8bb47-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="8bb47-122">AF11 (10)</span></span> |<span data-ttu-id="8bb47-123">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="8bb47-123">File transfer</span></span> |
| <span data-ttu-id="8bb47-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="8bb47-124">CS0 (0)</span></span> |<span data-ttu-id="8bb47-125">Другие варианты</span><span class="sxs-lookup"><span data-stu-id="8bb47-125">Anything else</span></span> | |

* <span data-ttu-id="8bb47-126">Необходимо классифицировать hello рабочих нагрузок и пометить правильные значения DSCP hello.</span><span class="sxs-lookup"><span data-stu-id="8bb47-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="8bb47-127">Следуйте инструкциям, hello [здесь](https://technet.microsoft.com/library/gg405409.aspx) о том, как tooset маркировки DSCP в сети.</span><span class="sxs-lookup"><span data-stu-id="8bb47-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="8bb47-128">Вам необходимо настроить и поддерживать несколько очередей качества обслуживания в сети.</span><span class="sxs-lookup"><span data-stu-id="8bb47-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="8bb47-129">Голосовой должно быть автономный класс и подвергаются обработке EF hello, указанные в RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="8bb47-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="8bb47-130">Можно решить, hello очереди механизм перегрузки политику обнаружения и распределение пропускной способности каждого класса трафика.</span><span class="sxs-lookup"><span data-stu-id="8bb47-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="8bb47-131">Но hello пометки DSCP для Скайп для решения бизнес-задач, которые необходимо сохранить.</span><span class="sxs-lookup"><span data-stu-id="8bb47-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="8bb47-132">Если вы используете маркировки DSCP, не перечисленные выше, например AF31 (26), необходимо переписать это too0 значение DSCP перед отправкой пакета tooMicrosoft hello.</span><span class="sxs-lookup"><span data-stu-id="8bb47-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="8bb47-133">Корпорация Майкрософт только отправляет пакеты, отмеченные hello значение DSCP, показанное в hello над таблицей.</span><span class="sxs-lookup"><span data-stu-id="8bb47-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8bb47-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bb47-134">Next steps</span></span>
* <span data-ttu-id="8bb47-135">См. требования к toohello для [маршрутизации](expressroute-routing.md) и [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="8bb47-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="8bb47-136">См. следующие hello ссылки tooconfigure подключение ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8bb47-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="8bb47-137">Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8bb47-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="8bb47-138">Настройка маршрутизации</span><span class="sxs-lookup"><span data-stu-id="8bb47-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="8bb47-139">Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8bb47-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

