---
title: "Создание пользовательской пробы для шлюза приложений Azure с помощью PowerShell (классическая модель) | Документация Майкрософт"
description: "Узнайте, как создавать пользовательские проверки для шлюза приложений с помощью PowerShell в классической модели развертывания."
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="b90e3-103">Создание пользовательской проверки для шлюза приложений (классического) Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b90e3-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b90e3-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b90e3-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="b90e3-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b90e3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="b90e3-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b90e3-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="b90e3-107">Следуя инструкциям этой статьи вы добавите пользовательскую пробу в имеющийся шлюз приложений с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b90e3-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="b90e3-108">Пользовательские пробы полезны в приложениях с конкретной страницей проверки работоспособности или приложениях, не предоставляющих успешный ответ веб-приложению по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b90e3-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b90e3-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b90e3-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b90e3-110">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b90e3-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b90e3-111">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b90e3-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b90e3-112">Узнайте, как [выполнить эти действия с помощью модели Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b90e3-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="b90e3-113">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="b90e3-113">Create an application gateway</span></span>

<span data-ttu-id="b90e3-114">Создание шлюза приложений:</span><span class="sxs-lookup"><span data-stu-id="b90e3-114">To create an application gateway:</span></span>

1. <span data-ttu-id="b90e3-115">Создайте ресурс шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="b90e3-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="b90e3-116">Создайте XML-файл конфигурации или объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b90e3-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="b90e3-117">Применить конфигурацию к созданному ресурсу шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="b90e3-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="b90e3-118">Создание ресурса шлюза приложений с пользовательской пробой</span><span class="sxs-lookup"><span data-stu-id="b90e3-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="b90e3-119">Для создания шлюза используйте командлет `New-AzureApplicationGateway`, подставив в него свои значения.</span><span class="sxs-lookup"><span data-stu-id="b90e3-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="b90e3-120">Выставление счетов для шлюза начинается не на данном этапе,</span><span class="sxs-lookup"><span data-stu-id="b90e3-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="b90e3-121">а позднее, после успешного запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="b90e3-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="b90e3-122">В следующем примере создается шлюз приложений с использованием виртуальной сети testvnet1 и подсети subnet-1.</span><span class="sxs-lookup"><span data-stu-id="b90e3-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="b90e3-123">Чтобы проверить создание шлюза, используйте командлет `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="b90e3-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="b90e3-124">Значение параметра *InstanceCount* по умолчанию — 2 (максимальное значение — 10).</span><span class="sxs-lookup"><span data-stu-id="b90e3-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="b90e3-125">По умолчанию для параметра *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="b90e3-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="b90e3-126">Можно выбрать значения Small, Medium или Large.</span><span class="sxs-lookup"><span data-stu-id="b90e3-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="b90e3-127">Параметры *VirtualIPs* и *DnsName* отображаются без значений, так как шлюз еще не запущен.</span><span class="sxs-lookup"><span data-stu-id="b90e3-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="b90e3-128">Эти значения будут определены после запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="b90e3-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="b90e3-129">Настройка шлюза приложений с помощью XML-файла</span><span class="sxs-lookup"><span data-stu-id="b90e3-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="b90e3-130">В следующем примере все параметры шлюза приложений настраиваются и применяются к ресурсу шлюза приложений при помощи XML-файла.</span><span class="sxs-lookup"><span data-stu-id="b90e3-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="b90e3-131">Скопируйте следующий текст в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="b90e3-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="b90e3-132">Измените значения в скобках для элементов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b90e3-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="b90e3-133">Сохраните файл с расширением XML.</span><span class="sxs-lookup"><span data-stu-id="b90e3-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="b90e3-134">В приведенном ниже примере показано, как использовать файл конфигурации, чтобы настроить шлюз приложений для балансировки нагрузки HTTP-трафика на общем порте 80 и направления сетевого трафика на внутренний порт 80 между двумя IP-адресами с помощью пользовательской проверки.</span><span class="sxs-lookup"><span data-stu-id="b90e3-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b90e3-135">В элементе протокола HTTP или HTTPS учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="b90e3-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="b90e3-136">Новый элемент конфигурации \<Probe\> добавляется для настройки пользовательских проверок работоспособности.</span><span class="sxs-lookup"><span data-stu-id="b90e3-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="b90e3-137">Используются следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b90e3-137">The configuration parameters are:</span></span>

|<span data-ttu-id="b90e3-138">Параметр</span><span class="sxs-lookup"><span data-stu-id="b90e3-138">Parameter</span></span>|<span data-ttu-id="b90e3-139">Описание</span><span class="sxs-lookup"><span data-stu-id="b90e3-139">Description</span></span>|
|---|---|
|<span data-ttu-id="b90e3-140">**Имя**</span><span class="sxs-lookup"><span data-stu-id="b90e3-140">**Name**</span></span> |<span data-ttu-id="b90e3-141">Имя пользовательской пробы.</span><span class="sxs-lookup"><span data-stu-id="b90e3-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="b90e3-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="b90e3-142">* **Protocol**</span></span> | <span data-ttu-id="b90e3-143">Используемый протокол (возможные значения: HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="b90e3-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="b90e3-144">**Host** и **Path**</span><span class="sxs-lookup"><span data-stu-id="b90e3-144">**Host** and **Path**</span></span> | <span data-ttu-id="b90e3-145">Полный путь URL-адреса, который вызывается шлюзом приложений для определения работоспособности экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b90e3-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="b90e3-146">Например, если у вас есть веб-сайт http://contoso.com/, пользовательскую пробу работоспособности для получения успешного ответа HTTP можно настроить в формате http://contoso.com/path/custompath.htm.</span><span class="sxs-lookup"><span data-stu-id="b90e3-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="b90e3-147">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="b90e3-147">**Interval**</span></span> | <span data-ttu-id="b90e3-148">Задает интервал между пробами в секундах.</span><span class="sxs-lookup"><span data-stu-id="b90e3-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="b90e3-149">**Время ожидания**</span><span class="sxs-lookup"><span data-stu-id="b90e3-149">**Timeout**</span></span> | <span data-ttu-id="b90e3-150">Определяет время ожидания для проверки ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="b90e3-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="b90e3-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="b90e3-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="b90e3-152">Количество неудачных ответов HTTP, по достижении которого серверный экземпляр считается *неработоспособным*.</span><span class="sxs-lookup"><span data-stu-id="b90e3-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="b90e3-153">Имя пробы указывается в конфигурации \<BackendHttpSettings\> для назначения пула серверной части, который будет использовать параметры пользовательской пробы.</span><span class="sxs-lookup"><span data-stu-id="b90e3-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="b90e3-154">Добавление пользовательской пробы в имеющийся шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="b90e3-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="b90e3-155">Изменение текущей конфигурации шлюза приложений состоит из трех шагов: получение XML-файла конфигурации, внесение изменений для пользовательской проверки и настройка шлюза приложений с использованием новых параметров XML.</span><span class="sxs-lookup"><span data-stu-id="b90e3-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="b90e3-156">Получите XML-файл с помощью командлета `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="b90e3-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="b90e3-157">Он экспортирует XML-файл конфигурации, который нужно изменить, чтобы добавить параметры пробы.</span><span class="sxs-lookup"><span data-stu-id="b90e3-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="b90e3-158">Откройте XML-файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="b90e3-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="b90e3-159">Добавьте раздел `<probe>` после `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="b90e3-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="b90e3-160">В разделе backendHttpSettings XML-файла добавьте имя пробы, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b90e3-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="b90e3-161">Сохраните XML-файл.</span><span class="sxs-lookup"><span data-stu-id="b90e3-161">Save the XML file.</span></span>

1. <span data-ttu-id="b90e3-162">Обновите конфигурацию шлюза приложения с помощью нового XML-файла, используя командлет `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="b90e3-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="b90e3-163">Он обновит шлюз приложений с учетом новой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b90e3-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="b90e3-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b90e3-164">Next steps</span></span>

<span data-ttu-id="b90e3-165">Указания по настройке разгрузки SSL см. в статье о [настройке шлюза приложений для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b90e3-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="b90e3-166">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="b90e3-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

