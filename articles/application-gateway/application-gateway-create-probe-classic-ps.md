---
title: "aaaCreate классические пользовательский зонд - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate пользовательской проверки для шлюза приложения с помощью PowerShell в hello классической модели развертывания"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="094c9-103">Создание пользовательской проверки для шлюза приложений (классического) Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="094c9-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="094c9-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="094c9-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="094c9-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="094c9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="094c9-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="094c9-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="094c9-107">В этой статье добавьте пользовательский зонд tooan существующего приложения шлюза с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="094c9-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="094c9-108">Пользовательские зонды полезны для приложений, имеющих страницы проверки работоспособности конкретного или для приложений, которые не предоставляют успешный ответ на веб-приложения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="094c9-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="094c9-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="094c9-110">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="094c9-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="094c9-111">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="094c9-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="094c9-112">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="094c9-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="094c9-113">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="094c9-113">Create an application gateway</span></span>

<span data-ttu-id="094c9-114">toocreate шлюза приложения:</span><span class="sxs-lookup"><span data-stu-id="094c9-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="094c9-115">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="094c9-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="094c9-116">Создайте XML-файл конфигурации или объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="094c9-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="094c9-117">Зафиксируйте toohello конфигурации hello созданного ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="094c9-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="094c9-118">Создание ресурса шлюза приложений с пользовательской пробой</span><span class="sxs-lookup"><span data-stu-id="094c9-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="094c9-119">шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="094c9-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="094c9-120">Выставление счетов для шлюза hello не начинается на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="094c9-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="094c9-121">Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.</span><span class="sxs-lookup"><span data-stu-id="094c9-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="094c9-122">Hello следующий пример создает шлюза приложения, используя виртуальную сеть с именем «testvnet1» и подсети, называется «подсеть-1».</span><span class="sxs-lookup"><span data-stu-id="094c9-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="094c9-123">toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="094c9-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="094c9-124">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="094c9-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="094c9-125">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="094c9-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="094c9-126">Можно выбрать значения Small, Medium или Large.</span><span class="sxs-lookup"><span data-stu-id="094c9-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="094c9-127">*Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась.</span><span class="sxs-lookup"><span data-stu-id="094c9-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="094c9-128">Эти значения создаются после hello шлюз находится в рабочем состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="094c9-129">Настройка шлюза приложений с помощью XML-файла</span><span class="sxs-lookup"><span data-stu-id="094c9-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="094c9-130">В следующем примере hello используйте все параметры шлюза приложения tooconfigure файла XML и зафиксировать их ресурса шлюза toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="094c9-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="094c9-131">Скопируйте следующий текст tooNotepad hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="094c9-132">Изменение значений hello заключено в круглые скобки hello для элементов конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="094c9-133">Сохраните hello файл с расширением .xml.</span><span class="sxs-lookup"><span data-stu-id="094c9-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="094c9-134">Hello следующем примере показано, как toouse tooset файл конфигурации вверх tooload шлюза приложения hello найти баланс между HTTP-трафика на открытый порт 80 и отправлять tooback конечный порт 80 между двумя IP-адресами с помощью пользовательский зонд сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="094c9-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="094c9-135">Hello элемент протокола Http или Https с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="094c9-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="094c9-136">Новый элемент конфигурации \<проверки\> добавляется tooconfigure пользовательские зонды.</span><span class="sxs-lookup"><span data-stu-id="094c9-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="094c9-137">используются следующие параметры конфигурации Hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="094c9-138">Параметр</span><span class="sxs-lookup"><span data-stu-id="094c9-138">Parameter</span></span>|<span data-ttu-id="094c9-139">Описание</span><span class="sxs-lookup"><span data-stu-id="094c9-139">Description</span></span>|
|---|---|
|<span data-ttu-id="094c9-140">**Имя**</span><span class="sxs-lookup"><span data-stu-id="094c9-140">**Name**</span></span> |<span data-ttu-id="094c9-141">Имя пользовательской пробы.</span><span class="sxs-lookup"><span data-stu-id="094c9-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="094c9-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="094c9-142">* **Protocol**</span></span> | <span data-ttu-id="094c9-143">Используемый протокол (возможные значения: HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="094c9-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="094c9-144">**Host** и **Path**</span><span class="sxs-lookup"><span data-stu-id="094c9-144">**Host** and **Path**</span></span> | <span data-ttu-id="094c9-145">Полный путь к URL-адрес, вызываемая hello приложения шлюза toodetermine hello работоспособности экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="094c9-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="094c9-146">Например если у вас http://contoso.com/ веб-сайта можно настроить пользовательский зонд hello для «http://contoso.com/path/custompath.htm» для проверки проверяет toohave успешного ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="094c9-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="094c9-147">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="094c9-147">**Interval**</span></span> | <span data-ttu-id="094c9-148">Настраивает hello выборки интервала проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="094c9-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="094c9-149">**Время ожидания**</span><span class="sxs-lookup"><span data-stu-id="094c9-149">**Timeout**</span></span> | <span data-ttu-id="094c9-150">Определяет время ожидания проверки hello для проверки ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="094c9-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="094c9-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="094c9-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="094c9-152">Здравствуйте, количество неудачных откликов HTTP необходимости tooflag hello внутренней экземпляр как *неработоспособное*.</span><span class="sxs-lookup"><span data-stu-id="094c9-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="094c9-153">Имя пробы Hello упоминается в hello \<BackendHttpSettings\> tooassign конфигурации серверной части пул использует пользовательский зонд параметры.</span><span class="sxs-lookup"><span data-stu-id="094c9-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="094c9-154">Добавление шлюза пользовательский зонд tooan существующего приложения</span><span class="sxs-lookup"><span data-stu-id="094c9-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="094c9-155">Изменение hello текущую конфигурацию шлюза приложения состоит из трех действий: получение hello текущего файла конфигурации XML, изменения toohave пользовательский зонд и настройки шлюза приложения hello hello новыми параметрами XML.</span><span class="sxs-lookup"><span data-stu-id="094c9-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="094c9-156">Получить hello XML-файл с помощью `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="094c9-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="094c9-157">Этот командлет экспортирует hello конфигурации XML toobe изменить tooadd параметр пробы.</span><span class="sxs-lookup"><span data-stu-id="094c9-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="094c9-158">Привет открыть XML-файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="094c9-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="094c9-159">Добавьте раздел `<probe>` после `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="094c9-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="094c9-160">В разделе backendHttpSettings hello hello XML добавьте имя пробы hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="094c9-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="094c9-161">Сохраните hello XML-файл.</span><span class="sxs-lookup"><span data-stu-id="094c9-161">Save hello XML file.</span></span>

1. <span data-ttu-id="094c9-162">Обновление конфигурации шлюза приложения hello hello новый XML-файл с помощью `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="094c9-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="094c9-163">Этот командлет обновляет шлюз приложения hello новую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="094c9-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="094c9-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="094c9-164">Next steps</span></span>

<span data-ttu-id="094c9-165">Если tooconfigure разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="094c9-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="094c9-166">Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="094c9-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

