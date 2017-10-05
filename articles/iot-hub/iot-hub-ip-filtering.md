---
title: "Фильтрация подключений по протоколу IP в Центре Интернета вещей Azure | Документация Майкрософт"
description: "Сведения об использовании фильтрации IP-адресов для блокирования подключений к Центру Интернета вещей Azure с определенных IP-адресов. Вы можете блокировать подключения с отдельных IP-адресов или их диапазонов."
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
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="dd705-104">Использование фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="dd705-104">Use IP filters</span></span>

<span data-ttu-id="dd705-105">Безопасность является важным аспектом любого решения Интернета вещей на базе Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="dd705-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="dd705-106">Иногда при настройке системы безопасности необходимо явно указать IP-адреса, с которых могут подключаться устройства.</span><span class="sxs-lookup"><span data-stu-id="dd705-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="dd705-107">Функция _фильтрации IP-адресов_ позволяет настроить правила для отклонения или приема трафика с определенных IPv4-адресов.</span><span class="sxs-lookup"><span data-stu-id="dd705-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="dd705-108">Сценарии использования</span><span class="sxs-lookup"><span data-stu-id="dd705-108">When to use</span></span>

<span data-ttu-id="dd705-109">Есть два конкретных варианта применения этой функции, когда рекомендуется заблокировать конечные точки Центра Интернета вещей для определенных IP-адресов:</span><span class="sxs-lookup"><span data-stu-id="dd705-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="dd705-110">Центр Интернета вещей должен принимать трафик только из определенного диапазона IP-адресов и отклонять весь остальной трафик.</span><span class="sxs-lookup"><span data-stu-id="dd705-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="dd705-111">Допустим, что Центр Интернета вещей используется в сочетании с [Azure Express Route] для создания частных подключений между Центром Интернета вещей и локальной инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="dd705-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="dd705-112">В этом случае требуется отклонять трафик с IP-адресов, которые были определены администратором Центра Интернета вещей как подозрительные.</span><span class="sxs-lookup"><span data-stu-id="dd705-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="dd705-113">Применение правил фильтрации</span><span class="sxs-lookup"><span data-stu-id="dd705-113">How filter rules are applied</span></span>

<span data-ttu-id="dd705-114">Правила фильтрации IP-адресов применяются на уровне службы Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dd705-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="dd705-115">Поэтому они действуют для всех подключений с устройств и внутренних приложений, использующих любые поддерживаемые протоколы.</span><span class="sxs-lookup"><span data-stu-id="dd705-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="dd705-116">При попытке подключения с IP-адреса, который соответствует правилу отклонения IP-адресов в Центре Интернета вещей, пользователь получает сообщение об ошибке с кодом состояния 401 (Не авторизовано) и описанием.</span><span class="sxs-lookup"><span data-stu-id="dd705-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="dd705-117">В ответном сообщении не указывается правило фильтрации IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="dd705-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="dd705-118">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="dd705-118">Default setting</span></span>

<span data-ttu-id="dd705-119">По умолчанию раздел **Фильтрация IP-адресов** на портале для Центра Интернета вещей пуст.</span><span class="sxs-lookup"><span data-stu-id="dd705-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="dd705-120">Этот означает, что по умолчанию ваш центр принимает подключения с любых IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="dd705-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="dd705-121">То есть, такое значение параметра по умолчанию равноценно правилу, которое принимает диапазон IP-адресов 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="dd705-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![Параметры фильтрации IP-адресов по умолчанию для Центра Интернета вещей][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="dd705-123">Добавление или изменение правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="dd705-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="dd705-124">При добавлении правила фильтрации IP-адресов требуется ввести следующие значения:</span><span class="sxs-lookup"><span data-stu-id="dd705-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="dd705-125">**Название правила фильтрации IP-адресов** должно быть уникальной строкой с буквами и цифрами длиной до 128 знаков, регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="dd705-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="dd705-126">Допускаются только 7-разрядные буквы и цифры ASCII, а также `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`.</span><span class="sxs-lookup"><span data-stu-id="dd705-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="dd705-127">В качестве **действия** для правила фильтрации IP-адресов выберите **Отклонить** или **Принять**.</span><span class="sxs-lookup"><span data-stu-id="dd705-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="dd705-128">Укажите один IPv4-адрес или блок IP-адресов в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="dd705-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="dd705-129">Например, в нотации CIDR 192.168.100.0/22 обозначает диапазон из 1024 IPv4-адресов от 192.168.100.0 до 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="dd705-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Добавление правила фильтрации IP-адресов в Центр Интернета вещей][img-ip-filter-add-rule]

<span data-ttu-id="dd705-131">После сохранения правила отображается предупреждение о том, что выполняется обновление.</span><span class="sxs-lookup"><span data-stu-id="dd705-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Уведомление о сохранении правила фильтрации IP-адресов][img-ip-filter-save-new-rule]

<span data-ttu-id="dd705-133">Параметр **Добавить** становится неактивным, когда достигается максимальное число правил фильтрации IP-адресов (10).</span><span class="sxs-lookup"><span data-stu-id="dd705-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="dd705-134">Чтобы изменить существующее правило, дважды щелкните строку с этим правилом.</span><span class="sxs-lookup"><span data-stu-id="dd705-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="dd705-135">Отклонение IP-адресов может препятствовать взаимодействию других служб Azure (таких как Azure Stream Analytics, Виртуальные машины Azure или обозреватель устройств на портале) с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="dd705-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="dd705-136">Если для чтения сообщений из Центра Интернета вещей с включенной IP-фильтрацией вы используете Azure Stream Analytics (ASA), укажите в строке подключения ASA совместимые с концентратором событий имя и конечную точку.</span><span class="sxs-lookup"><span data-stu-id="dd705-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="dd705-137">Удаление правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="dd705-137">Delete an IP filter rule</span></span>

<span data-ttu-id="dd705-138">Чтобы удалить правило фильтрации IP-адресов, выберите одно или несколько правил из списка и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="dd705-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Удаление правила фильтрации IP-адресов в Центре Интернета вещей][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="dd705-140">Оценка правила фильтрации IP-адресов</span><span class="sxs-lookup"><span data-stu-id="dd705-140">IP filter rule evaluation</span></span>

<span data-ttu-id="dd705-141">Правила фильтрации IP-адресов применяются по порядку, поэтому первое правило, которое соответствует IP-адресу, определяет действие (принять или отклонить).</span><span class="sxs-lookup"><span data-stu-id="dd705-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="dd705-142">Например, если вы хотите, чтобы адреса в диапазоне 192.168.100.0/22 принимались, а все остальные отклонялись, то первым правилом в списке должно быть именно правило о приеме трафика из диапазона адресов 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="dd705-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="dd705-143">Следующим должно быть правило об отклонении всех адресов; для этого используется диапазон 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="dd705-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="dd705-144">Последовательность правил фильтрации IP-адресов в списке можно изменить. Для этого щелкните три вертикальные точки в начале строки и воспользуйтесь функцией перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="dd705-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="dd705-145">Чтобы сохранить новую последовательность, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd705-145">To save your new IP filter rule order, click **Save**.</span></span>

![Изменение порядка правил фильтрации IP-адресов в Центре Интернета вещей][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="dd705-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd705-147">Next steps</span></span>

<span data-ttu-id="dd705-148">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="dd705-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="dd705-149">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="dd705-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="dd705-150">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="dd705-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="dd705-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="dd705-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md