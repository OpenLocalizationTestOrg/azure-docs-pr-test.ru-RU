---
title: "ошибки aaaTroubleshoot Azure шлюза неверное использование шлюза приложений (502) | Документы Microsoft"
description: "Узнайте, как ошибки tootroubleshoot 502 шлюза приложения"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="a1ecd-103">Устранение ошибок "Недопустимый шлюз" в шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="a1ecd-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="a1ecd-104">Узнайте, как получение ошибки (502) Недопустимый шлюз tootroubleshoot при использовании шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="a1ecd-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a1ecd-105">Overview</span></span>

<span data-ttu-id="a1ecd-106">После настройки шлюза приложения, одна из ошибок hello, которыми может столкнуться пользователь — «ошибка сервера: 502 - веб-сервер получил недопустимый ответ играя роль шлюза или прокси-сервер».</span><span class="sxs-lookup"><span data-stu-id="a1ecd-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="a1ecd-107">Эта ошибка может возникать из-за следующих toohello основных причин:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="a1ecd-108">[серверный пул шлюза приложений Azure не настроен или пуст](#empty-backendaddresspool);</span><span class="sxs-lookup"><span data-stu-id="a1ecd-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="a1ecd-109">Ни одна из виртуальных машин hello и экземпляры в [набора масштабирования виртуальных Машин находятся в работоспособном состоянии](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="a1ecd-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="a1ecd-110">Виртуальные машины или экземпляров набора масштабирования виртуальных Машин серверной части, [пробы работоспособности по умолчанию не отвечает toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="a1ecd-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="a1ecd-111">недопустимая или неправильная [конфигурация пользовательских проб работоспособности](#problems-with-custom-health-probe.md);</span><span class="sxs-lookup"><span data-stu-id="a1ecd-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="a1ecd-112">[истекло время запроса или при его обработке возникли проблемы с подключением](#request-time-out).</span><span class="sxs-lookup"><span data-stu-id="a1ecd-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="a1ecd-113">Пустой серверный пул адресов</span><span class="sxs-lookup"><span data-stu-id="a1ecd-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="a1ecd-114">Причина:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-114">Cause</span></span>

<span data-ttu-id="a1ecd-115">Если hello шлюз приложений содержит никакие ВМ или набора масштабирования виртуальных Машин настроены в пул адресов серверной части hello, он не может направить любой запрос клиента и вызывает ошибку Недопустимый шлюз.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ecd-116">Решение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-116">Solution</span></span>

<span data-ttu-id="a1ecd-117">Убедитесь, что пул адресов серверной части hello не является пустым.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="a1ecd-118">Это можно сделать с помощью PowerShell, интерфейса командной строки или на портале.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="a1ecd-119">Hello выходные данные предшествующей командлет hello должен содержать пул адресов серверной части пустым.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="a1ecd-120">В примере ниже возвращаются два пула, в которых для серверных виртуальных машин указано полное доменное имя или IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="a1ecd-121">Здравствуйте, состояние подготовки hello BackendAddressPool должен быть «успешно».</span><span class="sxs-lookup"><span data-stu-id="a1ecd-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="a1ecd-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="a1ecd-123">Неработоспособные экземпляры в серверном пуле адресов</span><span class="sxs-lookup"><span data-stu-id="a1ecd-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="a1ecd-124">Причина:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-124">Cause</span></span>

<span data-ttu-id="a1ecd-125">Если все экземпляры hello BackendAddressPool находятся в неработоспособном состоянии, шлюз приложений не будет содержать любой запрос пользователя tooroute серверной части для.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="a1ecd-126">Это может быть случай hello при внутреннем экземпляры находятся в работоспособном состоянии, но не развернутое приложение hello требуется.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ecd-127">Решение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-127">Solution</span></span>

<span data-ttu-id="a1ecd-128">Убедитесь, что экземпляры hello находятся в работоспособном состоянии, и приложение hello настроена правильно.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="a1ecd-129">Флажок, если экземпляры внутренней hello ping может toorespond tooa из другой виртуальной Машине в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="a1ecd-130">Если общедоступная конечная точка, убедитесь в наличии обслуживания веб-приложения браузера toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="a1ecd-131">Проблемы со стандартной пробой работоспособности</span><span class="sxs-lookup"><span data-stu-id="a1ecd-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="a1ecd-132">Причина:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-132">Cause</span></span>

<span data-ttu-id="a1ecd-133">также можно часто, hello пробы работоспособности по умолчанию индикаторы ошибки 502 — не удается tooreach ВМ серверной части.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="a1ecd-134">При подготовке экземпляра шлюза приложения tooeach проверки работоспособности по умолчанию BackendAddressPool автоматически настраивается с помощью свойств hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="a1ecd-135">Пользователь не входные данные tooset необходимые проверки.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="a1ecd-136">В частности, при настройке правила балансировки нагрузки создается связь между параметром BackendHttpSetting и серверным пулом адресов.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="a1ecd-137">Проба по умолчанию настраивается для каждого из этих сопоставлений и экземпляр tooeach периодических работоспособности проверки соединений в hello BackendAddressPool на hello порт, указанный в элементе BackendHttpSetting hello инициирует шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="a1ecd-138">Ниже перечислены значения hello, связанные с пробы работоспособности по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="a1ecd-139">Свойства проверки</span><span class="sxs-lookup"><span data-stu-id="a1ecd-139">Probe property</span></span> | <span data-ttu-id="a1ecd-140">Значение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-140">Value</span></span> | <span data-ttu-id="a1ecd-141">Описание</span><span class="sxs-lookup"><span data-stu-id="a1ecd-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1ecd-142">URL-адрес проверки</span><span class="sxs-lookup"><span data-stu-id="a1ecd-142">Probe URL</span></span> |<span data-ttu-id="a1ecd-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="a1ecd-143">http://127.0.0.1/</span></span> |<span data-ttu-id="a1ecd-144">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="a1ecd-144">URL path</span></span> |
| <span data-ttu-id="a1ecd-145">Интервал</span><span class="sxs-lookup"><span data-stu-id="a1ecd-145">Interval</span></span> |<span data-ttu-id="a1ecd-146">30</span><span class="sxs-lookup"><span data-stu-id="a1ecd-146">30</span></span> |<span data-ttu-id="a1ecd-147">Интервал проверки в секундах</span><span class="sxs-lookup"><span data-stu-id="a1ecd-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="a1ecd-148">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="a1ecd-148">Time-out</span></span> |<span data-ttu-id="a1ecd-149">30</span><span class="sxs-lookup"><span data-stu-id="a1ecd-149">30</span></span> |<span data-ttu-id="a1ecd-150">Время ожидания проверки в секундах</span><span class="sxs-lookup"><span data-stu-id="a1ecd-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="a1ecd-151">Пороговое значение сбоя</span><span class="sxs-lookup"><span data-stu-id="a1ecd-151">Unhealthy threshold</span></span> |<span data-ttu-id="a1ecd-152">3</span><span class="sxs-lookup"><span data-stu-id="a1ecd-152">3</span></span> |<span data-ttu-id="a1ecd-153">Количество повторных попыток проверки.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-153">Probe retry count.</span></span> <span data-ttu-id="a1ecd-154">Hello внутренний сервер помечен после количество сбоев проверки последовательных hello достигает неработоспособности порога hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="a1ecd-155">Решение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-155">Solution</span></span>

* <span data-ttu-id="a1ecd-156">Убедитесь, что стандартный сайт настроен и ожидает передачи данных по адресу 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="a1ecd-157">Если BackendHttpSetting указывает порт, отличный от 80, сайт по умолчанию hello должно быть настроенный toolisten этого порта.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="a1ecd-158">Hello toohttp://127.0.0.1:port вызов вернет код результата HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="a1ecd-159">Это должно быть возвращено в течение времени ожидания 30 секунд hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="a1ecd-160">Убедитесь, что открыт порт настроен и что не существует правил брандмауэра или группы безопасности сети Azure, которая Блокировать входящий и исходящий трафик через порт hello настроен.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="a1ecd-161">При использовании Azure классические виртуальные машины или облачной службы с полным доменным ИМЕНЕМ или общедоступный IP-адрес, убедитесь в соответствующих hello [конечная точка](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) открыт.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="a1ecd-162">Если hello виртуальной Машины настраивается посредством Azure Resource Manager и находится за пределами виртуальной сети, где развернут шлюз приложения, hello [группы безопасности сети](../virtual-network/virtual-networks-nsg.md) должен быть настроен доступ tooallow на hello требуемого порта.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="a1ecd-163">Проблемы с пользовательскими пробами работоспособности</span><span class="sxs-lookup"><span data-stu-id="a1ecd-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="a1ecd-164">Причина:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-164">Cause</span></span>

<span data-ttu-id="a1ecd-165">Зонды работоспособности пользовательского позволяют гибко по умолчанию toohello проверки поведения.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="a1ecd-166">При использовании пользовательских зондов, прежде чем помечать hello внутреннем пуле экземпляр неработоспособен пользователей можно настроить интервал отправки проб hello, hello URL-адрес и путь tootest и сколько неудачных откликов tooaccept.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="a1ecd-167">добавлены следующие дополнительные свойства Hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="a1ecd-168">Свойства проверки</span><span class="sxs-lookup"><span data-stu-id="a1ecd-168">Probe property</span></span> | <span data-ttu-id="a1ecd-169">Описание</span><span class="sxs-lookup"><span data-stu-id="a1ecd-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1ecd-170">Имя</span><span class="sxs-lookup"><span data-stu-id="a1ecd-170">Name</span></span> |<span data-ttu-id="a1ecd-171">Имя пробы hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-171">Name of hello probe.</span></span> <span data-ttu-id="a1ecd-172">Это имя уже используется toorefer toohello проверки в серверной части параметров HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="a1ecd-173">Протокол</span><span class="sxs-lookup"><span data-stu-id="a1ecd-173">Protocol</span></span> |<span data-ttu-id="a1ecd-174">Использовать протокол проверки toosend hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="a1ecd-175">зонд Hello использует протокол hello, заданного в настройках HTTP hello серверной части</span><span class="sxs-lookup"><span data-stu-id="a1ecd-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="a1ecd-176">Узел</span><span class="sxs-lookup"><span data-stu-id="a1ecd-176">Host</span></span> |<span data-ttu-id="a1ecd-177">Зонд hello toosend имя узла.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-177">Host name toosend hello probe.</span></span> <span data-ttu-id="a1ecd-178">Применяется только тогда, когда в шлюзе приложений настроено многосайтовое подключение.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="a1ecd-179">(То есть указывается не имя узла виртуальной машины.)</span><span class="sxs-lookup"><span data-stu-id="a1ecd-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="a1ecd-180">Путь</span><span class="sxs-lookup"><span data-stu-id="a1ecd-180">Path</span></span> |<span data-ttu-id="a1ecd-181">Относительный путь проверки hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-181">Relative path of hello probe.</span></span> <span data-ttu-id="a1ecd-182">Hello допустимый путь начинается с «/».</span><span class="sxs-lookup"><span data-stu-id="a1ecd-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="a1ecd-183">зонд Hello отправляется слишком\<протокола\>://\<узла\>:\<порт\>\<путь\></span><span class="sxs-lookup"><span data-stu-id="a1ecd-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="a1ecd-184">Интервал</span><span class="sxs-lookup"><span data-stu-id="a1ecd-184">Interval</span></span> |<span data-ttu-id="a1ecd-185">Интервал проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-185">Probe interval in seconds.</span></span> <span data-ttu-id="a1ecd-186">Это hello временной интервал между двумя последовательными зонды.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="a1ecd-187">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="a1ecd-187">Time-out</span></span> |<span data-ttu-id="a1ecd-188">Время ожидания проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-188">Probe time-out in seconds.</span></span> <span data-ttu-id="a1ecd-189">Если допустимый ответ не получен в течение этого времени ожидания, пробы hello отмечен как непройденный.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="a1ecd-190">Пороговое значение сбоя</span><span class="sxs-lookup"><span data-stu-id="a1ecd-190">Unhealthy threshold</span></span> |<span data-ttu-id="a1ecd-191">Количество повторных попыток проверки.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-191">Probe retry count.</span></span> <span data-ttu-id="a1ecd-192">Hello внутренний сервер помечен после количество сбоев проверки последовательных hello достигает неработоспособности порога hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="a1ecd-193">Решение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-193">Solution</span></span>

<span data-ttu-id="a1ecd-194">Проверьте, приветствия настраиваемый проверки работоспособности настроена правильно как hello предшествующей таблице.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="a1ecd-195">Кроме того toohello выше устранения неполадок, проверьте следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="a1ecd-196">Убедитесь, что пробы hello правильно указано согласно hello [руководство](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a1ecd-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="a1ecd-197">Если шлюз приложение настраивается для одного узла, по умолчанию hello узла имя должно указываться как "127.0.0.1», если в противном случае настроена в пользовательский зонд.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="a1ecd-198">Убедитесь, что toohttp вызова: / /\<узла\>:\<порт\>\<путь\> возвращает код результата HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="a1ecd-199">Убедитесь, что интервал, время ожидания и UnhealtyThreshold в допустимых пределах hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="a1ecd-200">Если проверки с помощью HTTPS, убедитесь, что этого внутреннего сервера hello не требует SNI путем настройки сертификата fallback на самом сервере hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="a1ecd-201">Убедитесь, что интервал времени ожидания и UnhealtyThreshold в допустимых пределах hello.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="a1ecd-202">Время ожидания запроса</span><span class="sxs-lookup"><span data-stu-id="a1ecd-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="a1ecd-203">Причина:</span><span class="sxs-lookup"><span data-stu-id="a1ecd-203">Cause</span></span>

<span data-ttu-id="a1ecd-204">При получении запроса пользователя шлюз приложений применяет запрос toohello hello настроены правила и направляет его tooa пула серверной части экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="a1ecd-205">Он ожидает можно настроить интервал времени отклика от экземпляра hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="a1ecd-206">По умолчанию этот интервал составляет **30 секунд**.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="a1ecd-207">Если шлюз приложений не получает отклик от серверного приложения в течение этого времени, для пользовательского запроса отображается ошибка 502.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ecd-208">Решение</span><span class="sxs-lookup"><span data-stu-id="a1ecd-208">Solution</span></span>

<span data-ttu-id="a1ecd-209">Шлюз приложений позволяет пользователям tooconfigure этого параметра с помощью BackendHttpSetting, которой может быть, а затем применить toodifferent пулы.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="a1ecd-210">Для разных серверных пулов параметр BackendHttpSetting и время ожидания запроса можно настроить по-разному.</span><span class="sxs-lookup"><span data-stu-id="a1ecd-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="a1ecd-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1ecd-211">Next steps</span></span>

<span data-ttu-id="a1ecd-212">Если hello описанные выше шаги не решат проблему hello, откройте [обращение в службу поддержки](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="a1ecd-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

