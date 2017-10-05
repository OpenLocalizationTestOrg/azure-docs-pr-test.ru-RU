---
title: "Использование шлюза приложения Azure с внутренней подсистемой балансировки нагрузки | Документация Майкрософт"
description: "Данная страница содержит инструкции по настройке шлюза приложений Azure с конечной точкой с внутренней балансировкой нагрузки."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="5b128-103">Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)</span><span class="sxs-lookup"><span data-stu-id="5b128-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b128-104">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b128-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="5b128-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5b128-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="5b128-106">Шлюз приложений можно настроить на использование виртуального IP-адреса с выходом в Интернет или с внутренней конечной точкой без выхода в Интернет, которая называется также конечной точкой внутренней подсистемы балансировщика нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="5b128-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="5b128-107">Настройка шлюза с внутренним балансировщиком нагрузки подходит для внутренних бизнес-приложений без доступа в Интернет.</span><span class="sxs-lookup"><span data-stu-id="5b128-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="5b128-108">Кроме того, этот вариант конфигурации можно использовать для служб и уровней многоуровневого приложения, размещенного в периметре безопасности без доступа к Интернету, но требующего циклического перебора нагрузки, закрепления сеансов или завершения SSL-запросов.</span><span class="sxs-lookup"><span data-stu-id="5b128-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="5b128-109">В этой статье приводятся пошаговые инструкции по настройке шлюза приложений с использованием внутреннего балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5b128-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b128-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5b128-110">Before you begin</span></span>

1. <span data-ttu-id="5b128-111">Используя установщик веб-платформы, установите последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b128-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="5b128-112">Вы можете скачать ее в разделе **Windows PowerShell** на [странице загрузки](https://azure.microsoft.com/downloads/), а затем установить.</span><span class="sxs-lookup"><span data-stu-id="5b128-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5b128-113">Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.</span><span class="sxs-lookup"><span data-stu-id="5b128-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="5b128-114">Убедитесь, что у вас есть внутренние серверы в виртуальной сети или с назначенным общедоступным IP или виртуальным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="5b128-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="5b128-115">Чтобы создать шлюз приложений, выполните следующие действия в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="5b128-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="5b128-116">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="5b128-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="5b128-117">Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="5b128-118">Настройка конфигурации шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="5b128-119">Запуск шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="5b128-120">Проверка шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="5b128-121">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="5b128-121">Create an application gateway:</span></span>

<span data-ttu-id="5b128-122">**Чтобы создать шлюз**, используйте командлет `New-AzureApplicationGateway`, подставив в него свои значения.</span><span class="sxs-lookup"><span data-stu-id="5b128-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="5b128-123">Обратите внимание, что выставление счетов для шлюза начинается не на данном этапе,</span><span class="sxs-lookup"><span data-stu-id="5b128-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="5b128-124">а позднее, после успешного запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="5b128-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="5b128-125">**Чтобы проверить** создание шлюза, используйте командлет `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="5b128-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="5b128-126">В примере параметры *Description*, *InstanceCount* и *GatewaySize* являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="5b128-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="5b128-127">Значение параметра *InstanceCount* по умолчанию — 2 (максимальное значение — 10).</span><span class="sxs-lookup"><span data-stu-id="5b128-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5b128-128">Значение *GatewaySize* (Размер шлюза) по умолчанию — Medium (Средний).</span><span class="sxs-lookup"><span data-stu-id="5b128-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5b128-129">Также доступны значения Small (Маленький) и Large (Большой).</span><span class="sxs-lookup"><span data-stu-id="5b128-129">Small and Large are other available values.</span></span> <span data-ttu-id="5b128-130">Параметры *Vip* и *DnsName* отображаются без значений, так как шлюз еще не запущен.</span><span class="sxs-lookup"><span data-stu-id="5b128-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="5b128-131">Эти значения будут заданы после его запуска.</span><span class="sxs-lookup"><span data-stu-id="5b128-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="5b128-132">Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-132">Configure the gateway</span></span>
<span data-ttu-id="5b128-133">Конфигурация шлюза приложений состоит из нескольких значений.</span><span class="sxs-lookup"><span data-stu-id="5b128-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="5b128-134">Значения конфигурации могут быть взаимосвязаны.</span><span class="sxs-lookup"><span data-stu-id="5b128-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="5b128-135">Доступны следующие значения.</span><span class="sxs-lookup"><span data-stu-id="5b128-135">The values are:</span></span>

* <span data-ttu-id="5b128-136">**Пул внутренних серверов:** список IP-адресов для внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="5b128-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="5b128-137">Указываемые IP-адреса должны относиться к подсети виртуальной сети или представлять собой общедоступные IP или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5b128-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="5b128-138">**Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="5b128-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5b128-139">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="5b128-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="5b128-140">**Внешний порт:** общий порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="5b128-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="5b128-141">Трафик поступает в этот порт, а затем перенаправляется на один из внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="5b128-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="5b128-142">**Прослушиватель:** прослушиватель имеет внешний порт, протокол (Http или Https; регистр имеет значение) и имя SSL-сертификата (если настраивается разгрузка SSL).</span><span class="sxs-lookup"><span data-stu-id="5b128-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="5b128-143">**Правило:** правило связывает прослушиватель и пул внутренних серверов и определяет, в какой пул внутренних серверов должен направляться трафик, попадающий в определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="5b128-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="5b128-144">В настоящее время поддерживается только *основное* правило.</span><span class="sxs-lookup"><span data-stu-id="5b128-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="5b128-145">*Основное* правило предусматривает циклическое распределение нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5b128-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="5b128-146">Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b128-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="5b128-147">Чтобы создать конфигурацию с помощью XML-файла конфигурации, используйте приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="5b128-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="5b128-148">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="5b128-148">Note the following:</span></span>

* <span data-ttu-id="5b128-149">Элемент *FrontendIPConfiguration* (IP-конфигурация внешнего интерфейса) описывает данные ILB, которые относятся к настройке шлюза приложений с использованием ILB.</span><span class="sxs-lookup"><span data-stu-id="5b128-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="5b128-150">Параметр *Type* (Тип) IP-адреса внутреннего интерфейса должен иметь значение Private (Частный).</span><span class="sxs-lookup"><span data-stu-id="5b128-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="5b128-151">Элементу *StaticIPAddress* должен быть присвоен необходимый внутренний IP-адрес, по которому шлюз получает трафик.</span><span class="sxs-lookup"><span data-stu-id="5b128-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="5b128-152">Обратите внимание, что элемент *StaticIPAddress* (Статический IP-адрес) не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="5b128-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="5b128-153">Если он не задан, выбирается доступный внутренний IP-адрес из развернутой подсети.</span><span class="sxs-lookup"><span data-stu-id="5b128-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="5b128-154">Значение элемента *Name* в параметре *FrontendIPConfiguration* используется в элементе *FrontendIP* параметра HTTPListener для ссылки на параметр FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="5b128-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="5b128-155">**Пример XML-конфигурации**</span><span class="sxs-lookup"><span data-stu-id="5b128-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="5b128-156">Настройка конфигурации шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-156">Set the gateway configuration</span></span>
<span data-ttu-id="5b128-157">Теперь шлюз приложений необходимо настроить.</span><span class="sxs-lookup"><span data-stu-id="5b128-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="5b128-158">Для этого можно использовать командлет `Set-AzureApplicationGatewayConfig` с объектом конфигурации или с XML-файлом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b128-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="5b128-159">Запуск шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-159">Start the gateway</span></span>

<span data-ttu-id="5b128-160">Настроенный шлюз можно запустить с помощью командлета `Start-AzureApplicationGateway` .</span><span class="sxs-lookup"><span data-stu-id="5b128-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="5b128-161">Выставление счетов для шлюза приложений начинается после запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="5b128-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="5b128-162">`Start-AzureApplicationGateway` занимает до 15–20 минут.</span><span class="sxs-lookup"><span data-stu-id="5b128-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="5b128-163">Проверка состояния шлюза</span><span class="sxs-lookup"><span data-stu-id="5b128-163">Verify the gateway status</span></span>

<span data-ttu-id="5b128-164">Проверить состояние шлюза можно с помощью командлета `Get-AzureApplicationGateway` .</span><span class="sxs-lookup"><span data-stu-id="5b128-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="5b128-165">Если на предыдущем этапе командлет `Start-AzureApplicationGateway` выполнен успешно, у параметра State должно быть значение *Running*, а у параметров Vip и DnsName — допустимые значения.</span><span class="sxs-lookup"><span data-stu-id="5b128-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="5b128-166">В данном примере командлет показан в первой строке, а затем выходные данные.</span><span class="sxs-lookup"><span data-stu-id="5b128-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="5b128-167">В этом примере шлюз запущен и готов принимать трафик.</span><span class="sxs-lookup"><span data-stu-id="5b128-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="5b128-168">В данном примере шлюз приложений настроен для приема трафика в заданной конечной точке внутреннего балансировщика нагрузки 10.0.0.10.</span><span class="sxs-lookup"><span data-stu-id="5b128-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="5b128-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b128-169">Next steps</span></span>
<span data-ttu-id="5b128-170">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="5b128-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5b128-171">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="5b128-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5b128-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5b128-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

