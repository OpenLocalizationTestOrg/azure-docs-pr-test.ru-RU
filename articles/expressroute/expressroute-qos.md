---
title: "Требования к качеству обслуживания для ExpressRoute | Документация Майкрософт"
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
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="8ab8e-103">Требования к качеству обслуживания для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ab8e-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="8ab8e-104">В Skype для бизнеса имеются различные рабочие нагрузки, требующие дифференцированного подхода к качеству обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="8ab8e-105">Если вы планируете использовать голосовые службы с помощью ExpressRoute, то необходимо соблюдать указанные ниже требования.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="8ab8e-106">Требования к качеству обслуживания применяются только к пирингу Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="8ab8e-107">Значения DSCP в сетевом трафике, полученном через общедоступный или частный пиринг Azure, будут сброшены до "0".</span><span class="sxs-lookup"><span data-stu-id="8ab8e-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="8ab8e-108">В таблице ниже перечислены пометки DSCP, используемые в Skype для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="8ab8e-109">Дополнительные сведения см. в статье [Управление качеством обслуживания для Skype для бизнеса](https://technet.microsoft.com/library/gg405409.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ab8e-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="8ab8e-110">**Класс трафика**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-110">**Traffic Class**</span></span> | <span data-ttu-id="8ab8e-111">**Обработка (пометки DSCP)**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="8ab8e-112">**Рабочие нагрузки Skype для бизнеса**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ab8e-113">**Голосовая связь**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-113">**Voice**</span></span> |<span data-ttu-id="8ab8e-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="8ab8e-114">EF (46)</span></span> |<span data-ttu-id="8ab8e-115">Голосовая связь Skype и Lync</span><span class="sxs-lookup"><span data-stu-id="8ab8e-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="8ab8e-116">**Интерактивный**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-116">**Interactive**</span></span> |<span data-ttu-id="8ab8e-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="8ab8e-117">AF41 (34)</span></span> |<span data-ttu-id="8ab8e-118">Видео, VBSS</span><span class="sxs-lookup"><span data-stu-id="8ab8e-118">Video, VBSS</span></span> |
| <span data-ttu-id="8ab8e-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="8ab8e-119">AF21 (18)</span></span> |<span data-ttu-id="8ab8e-120">Совместный доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="8ab8e-120">App sharing</span></span> | |
| <span data-ttu-id="8ab8e-121">**По умолчанию**</span><span class="sxs-lookup"><span data-stu-id="8ab8e-121">**Default**</span></span> |<span data-ttu-id="8ab8e-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="8ab8e-122">AF11 (10)</span></span> |<span data-ttu-id="8ab8e-123">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="8ab8e-123">File transfer</span></span> |
| <span data-ttu-id="8ab8e-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="8ab8e-124">CS0 (0)</span></span> |<span data-ttu-id="8ab8e-125">Другие варианты</span><span class="sxs-lookup"><span data-stu-id="8ab8e-125">Anything else</span></span> | |

* <span data-ttu-id="8ab8e-126">Вам необходимо классифицировать рабочие нагрузки и пометить правильные значения DSCP.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="8ab8e-127">Следуйте указанным [здесь](https://technet.microsoft.com/library/gg405409.aspx) инструкциям по настройке пометок DSCP в сети.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="8ab8e-128">Вам необходимо настроить и поддерживать несколько очередей качества обслуживания в сети.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="8ab8e-129">Голосовая связь должна быть изолированным классом и использовать обработку EF согласно документу RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="8ab8e-130">Вы можете решить, какие механизм очередей, политику обнаружения перегрузки и пропускную способность использовать для каждого класса трафика.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="8ab8e-131">Тем не менее необходимо сохранить пометки DSCP для рабочих нагрузок Skype для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="8ab8e-132">Если вы используете пометки DSCP, которых нет в списке выше, например AF31 (26), то перед отправкой пакета в корпорацию Майкрософт необходимо перезаписать это значение DSCP и сделать его равным 0.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="8ab8e-133">Корпорация Майкрософт отправляет только те пакеты, которые помечены значениями DSCP, указанными в таблице выше.</span><span class="sxs-lookup"><span data-stu-id="8ab8e-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8ab8e-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ab8e-134">Next steps</span></span>
* <span data-ttu-id="8ab8e-135">См. сведения о требованиях для [маршрутизации](expressroute-routing.md) и [преобразования сетевых адресов (NAT)](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="8ab8e-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="8ab8e-136">Чтобы настроить подключение ExpressRoute, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="8ab8e-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="8ab8e-137">Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ab8e-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="8ab8e-138">Настройка маршрутизации</span><span class="sxs-lookup"><span data-stu-id="8ab8e-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="8ab8e-139">Связывание виртуальной сети с каналом ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ab8e-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

