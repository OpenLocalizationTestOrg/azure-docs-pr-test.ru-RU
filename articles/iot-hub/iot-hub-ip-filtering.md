---
title: "фильтры соединения IP концентратора IoT aaaAzure | Документы Microsoft"
description: "Как toouse по IP-адресам tooblock соединений из определенного диапазона IP-адресов для tooyour центр Azure IoT. Вы можете блокировать подключения с отдельных IP-адресов или их диапазонов."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="a1353-104">Использование фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a1353-104">Use IP filters</span></span>

<span data-ttu-id="a1353-105">Безопасность является важным аспектом любого решения Интернета вещей на базе Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="a1353-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="a1353-106">Иногда требуется tooexplicitly указать hello IP-адресов, из которых устройства могут подключаться как часть конфигурации безопасности.</span><span class="sxs-lookup"><span data-stu-id="a1353-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="a1353-107">Hello _IP-фильтра_ дают возможность tooconfigure правила для отклонения или прием трафика с определенных адресов IPv4.</span><span class="sxs-lookup"><span data-stu-id="a1353-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="a1353-108">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="a1353-108">When toouse</span></span>

<span data-ttu-id="a1353-109">Существует два конкретных вариантов использования при конечные точки центра IoT hello tooblock полезны для определенных IP-адресов:</span><span class="sxs-lookup"><span data-stu-id="a1353-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="a1353-110">Центр Интернета вещей должен принимать трафик только из определенного диапазона IP-адресов и отклонять весь остальной трафик.</span><span class="sxs-lookup"><span data-stu-id="a1353-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="a1353-111">Например, вы используете концентратор IoT с [Azure Express Route] toocreate частные подключения между центр IoT и локальной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a1353-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="a1353-112">Необходимо tooreject трафика с IP-адресов, которые определены как подозрительные администратором концентратора IoT hello.</span><span class="sxs-lookup"><span data-stu-id="a1353-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="a1353-113">Применение правил фильтрации</span><span class="sxs-lookup"><span data-stu-id="a1353-113">How filter rules are applied</span></span>

<span data-ttu-id="a1353-114">правила фильтрации IP Hello применяются на hello центра IoT уровня обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a1353-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="a1353-115">Таким образом правил фильтрации IP hello применяются tooall подключения с устройств и приложений серверной части, используя любой поддерживаемый протокол.</span><span class="sxs-lookup"><span data-stu-id="a1353-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="a1353-116">При попытке подключения с IP-адреса, который соответствует правилу отклонения IP-адресов в Центре Интернета вещей, пользователь получает сообщение об ошибке с кодом состояния 401 (Не авторизовано) и описанием.</span><span class="sxs-lookup"><span data-stu-id="a1353-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="a1353-117">ответное сообщение Hello не упоминал hello IP правило.</span><span class="sxs-lookup"><span data-stu-id="a1353-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="a1353-118">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a1353-118">Default setting</span></span>

<span data-ttu-id="a1353-119">По умолчанию hello **IP-фильтра** сетки hello портала для центр IoT является пустым.</span><span class="sxs-lookup"><span data-stu-id="a1353-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="a1353-120">Этот означает, что по умолчанию ваш центр принимает подключения с любых IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a1353-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="a1353-121">Этот параметр по умолчанию — эквивалент tooa правило, которое принимает hello 0.0.0.0/0 IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a1353-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Параметры фильтрации IP-адресов по умолчанию для Центра Интернета вещей][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="a1353-123">Добавление или изменение правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a1353-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="a1353-124">При добавлении правила фильтра IP появится для hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a1353-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="a1353-125">**Имя правила фильтрации IP** , должно быть строкой уникальный, без учета регистра, буквенно-цифровое копирование too128 символов.</span><span class="sxs-lookup"><span data-stu-id="a1353-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="a1353-126">Только hello ASCII 7-разрядных буквы, цифры и `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` принимаются.</span><span class="sxs-lookup"><span data-stu-id="a1353-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="a1353-127">Выберите **Отклонить** или **принимать** как hello **действие** правила фильтрации сообщений hello IP.</span><span class="sxs-lookup"><span data-stu-id="a1353-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="a1353-128">Укажите один IPv4-адрес или блок IP-адресов в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="a1353-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="a1353-129">Например, в CIDR нотации 192.168.100.0/22 представляет hello 1024 IPv4-адреса из 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="a1353-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Добавление центра IoT tooan правило фильтра IP][img-ip-filter-add-rule]

<span data-ttu-id="a1353-131">После сохранения правила hello, вы увидите оповещение, уведомляющее о том, что выполняется обновление hello.</span><span class="sxs-lookup"><span data-stu-id="a1353-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Уведомление о сохранении правила фильтрации IP-адресов][img-ip-filter-save-new-rule]

<span data-ttu-id="a1353-133">Hello **добавить** параметр отключен, при достижении hello максимум десять правил фильтра IP.</span><span class="sxs-lookup"><span data-stu-id="a1353-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="a1353-134">Можно изменить существующее правило, дважды щелкнув строку hello, которая содержит правило hello.</span><span class="sxs-lookup"><span data-stu-id="a1353-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="a1353-135">Отклонение IP адресов можно запретить другим службам Azure (Azure Stream Analytics, виртуальные машины Azure или hello обозреватель устройств на портале hello) взаимодействует с центром IoT hello.</span><span class="sxs-lookup"><span data-stu-id="a1353-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="a1353-136">При использовании сообщения tooread Azure Stream Analytics (ASA) из центра IoT с включена фильтрация IP-адресов, используйте hello концентратора событий-совместимое имя и ваш центр IoT конечной точки в hello ASA строки подключения.</span><span class="sxs-lookup"><span data-stu-id="a1353-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="a1353-137">Удаление правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a1353-137">Delete an IP filter rule</span></span>

<span data-ttu-id="a1353-138">toodelete правило фильтра IP выберите одно или несколько правил в сетке hello и щелкните **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a1353-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Удаление правила фильтрации IP-адресов в Центре Интернета вещей][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="a1353-140">Оценка правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a1353-140">IP filter rule evaluation</span></span>

<span data-ttu-id="a1353-141">Правила фильтрации IP применяются в определенном порядке и hello первое правило, IP-адрес соответствует hello определяет hello принять или отклонить действие.</span><span class="sxs-lookup"><span data-stu-id="a1353-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="a1353-142">Например tooaccept адреса в диапазоне 192.168.100.0/22 hello и Отклонить все остальное, hello первого правила в сетке hello должен принимать 192.168.100.0/22 диапазона адресов hello.</span><span class="sxs-lookup"><span data-stu-id="a1353-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="a1353-143">с помощью диапазона 0.0.0.0/0 hello следующего правила Hello Отклонить все адреса.</span><span class="sxs-lookup"><span data-stu-id="a1353-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="a1353-144">Можно изменить порядок hello правил фильтра IP в сетке hello, щелкнув hello вертикальное многоточие в начале строки hello и с помощью перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="a1353-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="a1353-145">Фильтрация на новый IP-адрес toosave порядку правил, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a1353-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Изменение порядка hello правил фильтрации IP концентратора IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="a1353-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1353-147">Next steps</span></span>

<span data-ttu-id="a1353-148">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="a1353-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="a1353-149">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="a1353-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="a1353-150">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="a1353-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md