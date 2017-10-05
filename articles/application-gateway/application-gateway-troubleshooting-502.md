---
title: "Устранение ошибок \"Недопустимый шлюз (502)\" шлюза приложений Azure | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как устранять ошибки 502 шлюза приложений."
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="b63b7-103">Устранение ошибок "Недопустимый шлюз" в шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="b63b7-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="b63b7-104">В этой статье приведены сведения об устранении ошибок "Недопустимый шлюз (502)" шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="b63b7-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="b63b7-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b63b7-105">Overview</span></span>

<span data-ttu-id="b63b7-106">После настройки шлюза приложений может появиться сообщение об ошибке "Ошибка сервера 502: веб-сервер, выполняющий роль шлюза или прокси-сервера, получил недопустимый ответ".</span><span class="sxs-lookup"><span data-stu-id="b63b7-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="b63b7-107">Такая ошибка происходит по следующим причинам:</span><span class="sxs-lookup"><span data-stu-id="b63b7-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="b63b7-108">[серверный пул шлюза приложений Azure не настроен или пуст](#empty-backendaddresspool);</span><span class="sxs-lookup"><span data-stu-id="b63b7-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="b63b7-109">в [наборе масштабирования виртуальных машин нет работоспособных](#unhealthy-instances-in-backendaddresspool) экземпляров или виртуальных машин;</span><span class="sxs-lookup"><span data-stu-id="b63b7-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="b63b7-110">серверные виртуальные машины или экземпляры набора масштабирования виртуальных машин [не отвечают на стандартную пробу работоспособности](#problems-with-default-health-probe.md);</span><span class="sxs-lookup"><span data-stu-id="b63b7-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="b63b7-111">недопустимая или неправильная [конфигурация пользовательских проб работоспособности](#problems-with-custom-health-probe.md);</span><span class="sxs-lookup"><span data-stu-id="b63b7-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="b63b7-112">[истекло время запроса или при его обработке возникли проблемы с подключением](#request-time-out).</span><span class="sxs-lookup"><span data-stu-id="b63b7-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="b63b7-113">Пустой серверный пул адресов</span><span class="sxs-lookup"><span data-stu-id="b63b7-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="b63b7-114">Причина:</span><span class="sxs-lookup"><span data-stu-id="b63b7-114">Cause</span></span>

<span data-ttu-id="b63b7-115">Если для шлюза приложений в серверном пуле адресов не настроены виртуальные машины или масштабируемый набор виртуальных машин, шлюз не сможет отправлять запросы клиентов, выдавая ошибку недопустимого шлюза.</span><span class="sxs-lookup"><span data-stu-id="b63b7-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="b63b7-116">Решение</span><span class="sxs-lookup"><span data-stu-id="b63b7-116">Solution</span></span>

<span data-ttu-id="b63b7-117">Убедитесь, что серверный пул адресов не пуст.</span><span class="sxs-lookup"><span data-stu-id="b63b7-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="b63b7-118">Это можно сделать с помощью PowerShell, интерфейса командной строки или на портале.</span><span class="sxs-lookup"><span data-stu-id="b63b7-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="b63b7-119">Выходные данные командлета, приведенного выше, должны содержать непустой серверный пул адресов.</span><span class="sxs-lookup"><span data-stu-id="b63b7-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="b63b7-120">В примере ниже возвращаются два пула, в которых для серверных виртуальных машин указано полное доменное имя или IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b63b7-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="b63b7-121">Состояние подготовки серверного пула адресов должно быть "Выполнено".</span><span class="sxs-lookup"><span data-stu-id="b63b7-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="b63b7-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="b63b7-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="b63b7-123">Неработоспособные экземпляры в серверном пуле адресов</span><span class="sxs-lookup"><span data-stu-id="b63b7-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="b63b7-124">Причина:</span><span class="sxs-lookup"><span data-stu-id="b63b7-124">Cause</span></span>

<span data-ttu-id="b63b7-125">Если неработоспособными являются все экземпляры серверного пула адресов, шлюзу приложений некуда отправлять запросы пользователей.</span><span class="sxs-lookup"><span data-stu-id="b63b7-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="b63b7-126">То же самое происходит, когда серверные экземпляры работоспособны, но в них не развернуто требуемое приложение.</span><span class="sxs-lookup"><span data-stu-id="b63b7-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="b63b7-127">Решение</span><span class="sxs-lookup"><span data-stu-id="b63b7-127">Solution</span></span>

<span data-ttu-id="b63b7-128">Сделайте экземпляры работоспособными и правильно настройте приложение.</span><span class="sxs-lookup"><span data-stu-id="b63b7-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="b63b7-129">Проверьте, могут ли серверные экземпляры отвечать на запрос при проверке связи от другой виртуальной машины в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b63b7-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="b63b7-130">Если настроена общая конечная точка, убедитесь, что запрос браузера к веб-приложению подлежит обслуживанию.</span><span class="sxs-lookup"><span data-stu-id="b63b7-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="b63b7-131">Проблемы со стандартной пробой работоспособности</span><span class="sxs-lookup"><span data-stu-id="b63b7-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="b63b7-132">Причина:</span><span class="sxs-lookup"><span data-stu-id="b63b7-132">Cause</span></span>

<span data-ttu-id="b63b7-133">Ошибки 502 часто указывают на то, что стандартная проба работоспособности не может связаться с виртуальными машинами серверной части.</span><span class="sxs-lookup"><span data-stu-id="b63b7-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="b63b7-134">Подготовленный экземпляр шлюза приложений автоматически настраивает стандартную пробу работоспособности для каждого серверного пула адресов. Для этого он использует свойства параметра BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="b63b7-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="b63b7-135">Пользователю ничего не нужно вводить для настройки этой пробы.</span><span class="sxs-lookup"><span data-stu-id="b63b7-135">No user input is required to set this probe.</span></span> <span data-ttu-id="b63b7-136">В частности, при настройке правила балансировки нагрузки создается связь между параметром BackendHttpSetting и серверным пулом адресов.</span><span class="sxs-lookup"><span data-stu-id="b63b7-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="b63b7-137">Стандартная проба настраивается для каждой такой связи. Шлюз приложений периодически проверяет работоспособность каждого экземпляра в серверном пуле адресов. Для этого он подключается к нужным экземплярам, пользуясь портом, заданным в параметре BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="b63b7-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="b63b7-138">Ниже приведены значения, связанные со стандартной пробой работоспособности.</span><span class="sxs-lookup"><span data-stu-id="b63b7-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="b63b7-139">Свойства проверки</span><span class="sxs-lookup"><span data-stu-id="b63b7-139">Probe property</span></span> | <span data-ttu-id="b63b7-140">Значение</span><span class="sxs-lookup"><span data-stu-id="b63b7-140">Value</span></span> | <span data-ttu-id="b63b7-141">Описание</span><span class="sxs-lookup"><span data-stu-id="b63b7-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b63b7-142">URL-адрес проверки</span><span class="sxs-lookup"><span data-stu-id="b63b7-142">Probe URL</span></span> |<span data-ttu-id="b63b7-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="b63b7-143">http://127.0.0.1/</span></span> |<span data-ttu-id="b63b7-144">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b63b7-144">URL path</span></span> |
| <span data-ttu-id="b63b7-145">Интервал</span><span class="sxs-lookup"><span data-stu-id="b63b7-145">Interval</span></span> |<span data-ttu-id="b63b7-146">30</span><span class="sxs-lookup"><span data-stu-id="b63b7-146">30</span></span> |<span data-ttu-id="b63b7-147">Интервал проверки в секундах</span><span class="sxs-lookup"><span data-stu-id="b63b7-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="b63b7-148">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="b63b7-148">Time-out</span></span> |<span data-ttu-id="b63b7-149">30</span><span class="sxs-lookup"><span data-stu-id="b63b7-149">30</span></span> |<span data-ttu-id="b63b7-150">Время ожидания проверки в секундах</span><span class="sxs-lookup"><span data-stu-id="b63b7-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="b63b7-151">Пороговое значение сбоя</span><span class="sxs-lookup"><span data-stu-id="b63b7-151">Unhealthy threshold</span></span> |<span data-ttu-id="b63b7-152">3</span><span class="sxs-lookup"><span data-stu-id="b63b7-152">3</span></span> |<span data-ttu-id="b63b7-153">Количество повторных попыток проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-153">Probe retry count.</span></span> <span data-ttu-id="b63b7-154">Сервер внутреннего пула считается неисправным, когда количество повторных неудачных попыток проверки достигает порогового значения сбоя.</span><span class="sxs-lookup"><span data-stu-id="b63b7-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="b63b7-155">Решение</span><span class="sxs-lookup"><span data-stu-id="b63b7-155">Solution</span></span>

* <span data-ttu-id="b63b7-156">Убедитесь, что стандартный сайт настроен и ожидает передачи данных по адресу 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="b63b7-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="b63b7-157">Если в параметре BackendHttpSetting задан порт, отличный от 80, на стандартном сайте нужно настроить ожидание передачи данных через этот порт.</span><span class="sxs-lookup"><span data-stu-id="b63b7-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="b63b7-158">Вызов к http://127.0.0.1:port должен вернуть HTTP-код результата 200</span><span class="sxs-lookup"><span data-stu-id="b63b7-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="b63b7-159">(в течении 30-секундного периода ожидания).</span><span class="sxs-lookup"><span data-stu-id="b63b7-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="b63b7-160">Откройте настроенный порт и удалите правила брандмауэра и группы безопасности сети Azure. Иначе они будут блокировать входящий и исходящий трафик через настроенный порт.</span><span class="sxs-lookup"><span data-stu-id="b63b7-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="b63b7-161">Если классические виртуальные машины Azure или облачная служба используются с полным доменным именем или общедоступным IP-адресом, откройте соответствующую [конечную точку](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="b63b7-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="b63b7-162">Если виртуальная машина настроена с помощью Azure Resource Manager и находится за пределами виртуальной сети, в которой развернут шлюз приложений, настройте в [группе безопасности сети](../virtual-network/virtual-networks-nsg.md) доступ через нужный порт.</span><span class="sxs-lookup"><span data-stu-id="b63b7-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="b63b7-163">Проблемы с пользовательскими пробами работоспособности</span><span class="sxs-lookup"><span data-stu-id="b63b7-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="b63b7-164">Причина:</span><span class="sxs-lookup"><span data-stu-id="b63b7-164">Cause</span></span>

<span data-ttu-id="b63b7-165">Пользовательские пробы работоспособности более гибкие по сравнению со стандартными.</span><span class="sxs-lookup"><span data-stu-id="b63b7-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="b63b7-166">Для пользовательских проб можно настроить интервал, URL-адрес и путь к ним (для тестирования), а также число неудачных откликов, после которых экземпляр пула внутренних серверов будет считаться неработоспособным.</span><span class="sxs-lookup"><span data-stu-id="b63b7-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="b63b7-167">Добавляются приведенные ниже дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="b63b7-167">The following additional properties are added.</span></span>

| <span data-ttu-id="b63b7-168">Свойства проверки</span><span class="sxs-lookup"><span data-stu-id="b63b7-168">Probe property</span></span> | <span data-ttu-id="b63b7-169">Описание</span><span class="sxs-lookup"><span data-stu-id="b63b7-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b63b7-170">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="b63b7-170">Name</span></span> |<span data-ttu-id="b63b7-171">Имя проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-171">Name of the probe.</span></span> <span data-ttu-id="b63b7-172">Это имя используется для указания проверки в параметрах HTTP внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="b63b7-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="b63b7-173">Протокол</span><span class="sxs-lookup"><span data-stu-id="b63b7-173">Protocol</span></span> |<span data-ttu-id="b63b7-174">Протокол, используемый для проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-174">Protocol used to send the probe.</span></span> <span data-ttu-id="b63b7-175">Проба использует протокол, определенный в параметрах HTTP серверной части.</span><span class="sxs-lookup"><span data-stu-id="b63b7-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="b63b7-176">Узел</span><span class="sxs-lookup"><span data-stu-id="b63b7-176">Host</span></span> |<span data-ttu-id="b63b7-177">Имя узла для проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-177">Host name to send the probe.</span></span> <span data-ttu-id="b63b7-178">Применяется только тогда, когда в шлюзе приложений настроено многосайтовое подключение.</span><span class="sxs-lookup"><span data-stu-id="b63b7-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="b63b7-179">(То есть указывается не имя узла виртуальной машины.)</span><span class="sxs-lookup"><span data-stu-id="b63b7-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="b63b7-180">Путь</span><span class="sxs-lookup"><span data-stu-id="b63b7-180">Path</span></span> |<span data-ttu-id="b63b7-181">Относительный путь проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-181">Relative path of the probe.</span></span> <span data-ttu-id="b63b7-182">Путь должен начинаться с "/".</span><span class="sxs-lookup"><span data-stu-id="b63b7-182">The valid path starts from '/'.</span></span> <span data-ttu-id="b63b7-183">Проба отправляется по адресу \<протокол\>://\<узел\>:\<порт\>\<путь\>.</span><span class="sxs-lookup"><span data-stu-id="b63b7-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="b63b7-184">Интервал</span><span class="sxs-lookup"><span data-stu-id="b63b7-184">Interval</span></span> |<span data-ttu-id="b63b7-185">Интервал проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="b63b7-185">Probe interval in seconds.</span></span> <span data-ttu-id="b63b7-186">Интервал времени между двумя последовательными проверками.</span><span class="sxs-lookup"><span data-stu-id="b63b7-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="b63b7-187">Время ожидания</span><span class="sxs-lookup"><span data-stu-id="b63b7-187">Time-out</span></span> |<span data-ttu-id="b63b7-188">Время ожидания проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="b63b7-188">Probe time-out in seconds.</span></span> <span data-ttu-id="b63b7-189">Если ответ о работоспособности не получен в течение этого времени ожидания, то проба считается неудачной.</span><span class="sxs-lookup"><span data-stu-id="b63b7-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="b63b7-190">Пороговое значение сбоя</span><span class="sxs-lookup"><span data-stu-id="b63b7-190">Unhealthy threshold</span></span> |<span data-ttu-id="b63b7-191">Количество повторных попыток проверки.</span><span class="sxs-lookup"><span data-stu-id="b63b7-191">Probe retry count.</span></span> <span data-ttu-id="b63b7-192">Сервер внутреннего пула считается неисправным, когда количество повторных неудачных попыток проверки достигает порогового значения сбоя.</span><span class="sxs-lookup"><span data-stu-id="b63b7-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="b63b7-193">Решение</span><span class="sxs-lookup"><span data-stu-id="b63b7-193">Solution</span></span>

<span data-ttu-id="b63b7-194">Настройте пользовательскую пробу производительности правильно, как описано в таблице выше.</span><span class="sxs-lookup"><span data-stu-id="b63b7-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="b63b7-195">Кроме действий по устранению неполадок, описанных выше, требуется соблюдение следующих условий:</span><span class="sxs-lookup"><span data-stu-id="b63b7-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="b63b7-196">проба указана правильно, согласно [руководству](application-gateway-create-probe-ps.md);</span><span class="sxs-lookup"><span data-stu-id="b63b7-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="b63b7-197">если шлюз приложений настроен для одного сайта, нужно указать стандартное имя узла 127.0.0.1, если только другое имя не задано в пользовательской пробе;</span><span class="sxs-lookup"><span data-stu-id="b63b7-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="b63b7-198">Убедитесь, что вызов к http://\<узел\>:\<порт\>\<путь\> возвращает HTTP-код результата 200.</span><span class="sxs-lookup"><span data-stu-id="b63b7-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="b63b7-199">значения "Интервал", "Время ожидания" и "Порог работоспособности" должны находиться в допустимом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="b63b7-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="b63b7-200">При использовании зонда HTTPS убедитесь, что внутренний сервер не требует SNI путем настройки резервного сертификата.</span><span class="sxs-lookup"><span data-stu-id="b63b7-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="b63b7-201">Убедитесь, что значения "Интервал", "Время ожидания" и "Порог работоспособности" находятся в допустимом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="b63b7-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="b63b7-202">Время ожидания запроса</span><span class="sxs-lookup"><span data-stu-id="b63b7-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="b63b7-203">Причина:</span><span class="sxs-lookup"><span data-stu-id="b63b7-203">Cause</span></span>

<span data-ttu-id="b63b7-204">При получении запроса пользователя шлюз приложений применяет настроенные правила к запросу и направляет его экземпляру серверного пула.</span><span class="sxs-lookup"><span data-stu-id="b63b7-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="b63b7-205">Затем в течение указанного интервала он ожидает отклик от серверного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b63b7-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="b63b7-206">По умолчанию этот интервал составляет **30 секунд**.</span><span class="sxs-lookup"><span data-stu-id="b63b7-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="b63b7-207">Если шлюз приложений не получает отклик от серверного приложения в течение этого времени, для пользовательского запроса отображается ошибка 502.</span><span class="sxs-lookup"><span data-stu-id="b63b7-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="b63b7-208">Решение</span><span class="sxs-lookup"><span data-stu-id="b63b7-208">Solution</span></span>

<span data-ttu-id="b63b7-209">Шлюз приложений позволяет пользователям настроить этот параметр с помощью параметра BackendHttpSetting, который затем можно применить к разным пулам.</span><span class="sxs-lookup"><span data-stu-id="b63b7-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="b63b7-210">Для разных серверных пулов параметр BackendHttpSetting и время ожидания запроса можно настроить по-разному.</span><span class="sxs-lookup"><span data-stu-id="b63b7-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="b63b7-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b63b7-211">Next steps</span></span>

<span data-ttu-id="b63b7-212">Если описанные выше шаги не устранят проблему, отправьте [запрос в службу поддержки](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="b63b7-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

