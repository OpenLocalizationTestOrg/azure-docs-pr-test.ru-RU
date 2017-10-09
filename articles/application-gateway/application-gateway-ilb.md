---
title: "Шлюз приложения Azure с внутренним балансировщиком нагрузки aaaUsing | Документы Microsoft"
description: "На этой странице представлены инструкции tooconfigure шлюза приложения Azure с конечной точкой внутренней балансировки нагрузки"
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
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="e13b5-103">Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)</span><span class="sxs-lookup"><span data-stu-id="e13b5-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e13b5-104">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13b5-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="e13b5-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e13b5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="e13b5-106">Шлюз приложений можно настроить виртуальный IP-адрес с выходом в Интернет или с toohello внутренняя конечная точка не предоставляется Интернет, также известные как внутренняя Подсистема балансировки нагрузки (ILB) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="e13b5-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="e13b5-107">Настройка шлюза hello с ILB полезен для toointernet внутренних бизнес-приложений, в не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="e13b5-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="e13b5-108">Также полезно для служб или уровней в многоуровневое приложение, в которой располагается в toointernet не предоставляется границу безопасности, но по-прежнему требуется распределение нагрузки циклического перебора, stickiness сеанса или завершение запросов SSL.</span><span class="sxs-lookup"><span data-stu-id="e13b5-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="e13b5-109">В этой статье рассматриваются действия hello tooconfigure шлюза приложения с ILB.</span><span class="sxs-lookup"><span data-stu-id="e13b5-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e13b5-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e13b5-110">Before you begin</span></span>

1. <span data-ttu-id="e13b5-111">Установите последнюю версию hello установщика веб-платформы с помощью командлетов Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="e13b5-112">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницы загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e13b5-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e13b5-113">Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.</span><span class="sxs-lookup"><span data-stu-id="e13b5-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="e13b5-114">Проверьте наличие внутренних серверов в виртуальной сети hello или открытый IP/VIP-адрес, назначенный.</span><span class="sxs-lookup"><span data-stu-id="e13b5-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="e13b5-115">toocreate шлюза приложения, выполните следующие шаги в порядке hello hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="e13b5-116">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="e13b5-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="e13b5-117">Настройка шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="e13b5-118">Набор конфигурации шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="e13b5-119">Запуск шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="e13b5-120">Проверка шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="e13b5-121">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="e13b5-121">Create an application gateway:</span></span>

<span data-ttu-id="e13b5-122">**шлюз hello toocreate**, использовать hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="e13b5-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="e13b5-123">Обратите внимание, что выставления счетов для hello шлюза не запущен на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="e13b5-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="e13b5-124">Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.</span><span class="sxs-lookup"><span data-stu-id="e13b5-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

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

<span data-ttu-id="e13b5-125">**toovalidate** hello шлюз был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="e13b5-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="e13b5-126">В образце hello *описание*, *InstanceCount*, и *GatewaySize* являются необязательными параметрами.</span><span class="sxs-lookup"><span data-stu-id="e13b5-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="e13b5-127">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="e13b5-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="e13b5-128">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="e13b5-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="e13b5-129">Также доступны значения Small (Маленький) и Large (Большой).</span><span class="sxs-lookup"><span data-stu-id="e13b5-129">Small and Large are other available values.</span></span> <span data-ttu-id="e13b5-130">*Виртуальный IP-адрес* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась.</span><span class="sxs-lookup"><span data-stu-id="e13b5-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="e13b5-131">Эти отчеты создаются после hello шлюз находится в рабочем состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-131">These are created once hello gateway is in hello running state.</span></span> 

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

## <a name="configure-hello-gateway"></a><span data-ttu-id="e13b5-132">Настройка шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-132">Configure hello gateway</span></span>
<span data-ttu-id="e13b5-133">Конфигурация шлюза приложений состоит из нескольких значений.</span><span class="sxs-lookup"><span data-stu-id="e13b5-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="e13b5-134">Hello значения могут быть привязаны конфигурации hello tooconstruct вместе.</span><span class="sxs-lookup"><span data-stu-id="e13b5-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="e13b5-135">доступны следующие значения Hello:</span><span class="sxs-lookup"><span data-stu-id="e13b5-135">hello values are:</span></span>

* <span data-ttu-id="e13b5-136">**Внутренний пул сервера:** hello список IP-адресов hello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="e13b5-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="e13b5-137">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="e13b5-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="e13b5-138">**Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="e13b5-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e13b5-139">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="e13b5-140">**Интерфейсный порт:** этой цели используется порт hello открытый порт открыт для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="e13b5-141">Трафик обращений к этому порту и затем получает перенаправленный tooone hello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="e13b5-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="e13b5-142">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, они зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="e13b5-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="e13b5-143">**Правило:** правило hello привязывает прослушивателя hello и hello внутреннего сервера пула и определяет, какой трафик hello внутреннего пула сервера должен быть расширенный toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="e13b5-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="e13b5-144">В настоящее время только hello *основные* правило поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e13b5-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="e13b5-145">Hello *основные* правило — распределение нагрузки с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="e13b5-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="e13b5-146">Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e13b5-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="e13b5-147">tooconstruct конфигурацию с помощью XML-файл конфигурации, используйте hello примера ниже.</span><span class="sxs-lookup"><span data-stu-id="e13b5-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="e13b5-148">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e13b5-148">Note hello following:</span></span>

* <span data-ttu-id="e13b5-149">Hello *FrontendIPConfigurations* описывает hello ILB сведения относятся только к настройке шлюза приложения с ILB.</span><span class="sxs-lookup"><span data-stu-id="e13b5-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="e13b5-150">Hello интерфейсных IP-адресов *тип* должно быть установлено too'Private "</span><span class="sxs-lookup"><span data-stu-id="e13b5-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="e13b5-151">Hello *StaticIPAddress* должно быть установлено toohello требуемого внутренний IP-адрес на какие hello шлюз получает трафик.</span><span class="sxs-lookup"><span data-stu-id="e13b5-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="e13b5-152">Обратите внимание, что hello *StaticIPAddress* элемент является необязательным.</span><span class="sxs-lookup"><span data-stu-id="e13b5-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="e13b5-153">В противном случае выбирается набор, доступный внутренний IP-адрес из подсети развернут hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="e13b5-154">Здравствуйте, значение hello *имя* элемент, указанный в *FrontendIPConfiguration* должны использоваться в hello HTTPListener в *FrontendIP* toohello toorefer элемент FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="e13b5-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="e13b5-155">**Пример XML-конфигурации**</span><span class="sxs-lookup"><span data-stu-id="e13b5-155">**Configuration XML sample**</span></span>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="e13b5-156">Набор конфигурации шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-156">Set hello gateway configuration</span></span>
<span data-ttu-id="e13b5-157">Затем можно задать шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="e13b5-158">Можно использовать hello `Set-AzureApplicationGatewayConfig` командлет с помощью объекта конфигурации или с помощью файла конфигурации XML.</span><span class="sxs-lookup"><span data-stu-id="e13b5-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-hello-gateway"></a><span data-ttu-id="e13b5-159">Запуск шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-159">Start hello gateway</span></span>

<span data-ttu-id="e13b5-160">После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="e13b5-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="e13b5-161">Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="e13b5-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="e13b5-162">Hello `Start-AzureApplicationGateway` командлет может занимать toocomplete too15-20 минут.</span><span class="sxs-lookup"><span data-stu-id="e13b5-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
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

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="e13b5-163">Проверить состояние шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e13b5-163">Verify hello gateway status</span></span>

<span data-ttu-id="e13b5-164">Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза.</span><span class="sxs-lookup"><span data-stu-id="e13b5-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="e13b5-165">Если `Start-AzureApplicationGateway` успешно в предыдущем шаге hello hello состояние должно быть *под управлением*, hello виртуальных IP-адресов и DnsName должны иметь допустимые записи.</span><span class="sxs-lookup"><span data-stu-id="e13b5-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="e13b5-166">Это пример hello командлета на первую строку hello, следуют hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e13b5-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="e13b5-167">В этом образце hello шлюз запущен и готов tootake трафика.</span><span class="sxs-lookup"><span data-stu-id="e13b5-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="e13b5-168">шлюз приложения Hello настроен tooaccept трафика в hello конечной точке ILB 10.0.0.10 настроен в этом примере.</span><span class="sxs-lookup"><span data-stu-id="e13b5-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e13b5-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e13b5-169">Next steps</span></span>
<span data-ttu-id="e13b5-170">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="e13b5-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="e13b5-171">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="e13b5-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e13b5-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e13b5-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

