---
title: "aaaCreate, запуск или удаление шлюза приложения | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="68a44-103">Создание, запуск или удаление шлюза приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a44-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="68a44-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="68a44-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="68a44-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="68a44-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="68a44-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a44-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="68a44-107">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="68a44-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="68a44-108">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="68a44-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="68a44-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="68a44-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="68a44-110">Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="68a44-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="68a44-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="68a44-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="68a44-112">Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="68a44-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="68a44-113">В этой статье рассматриваются действия toocreate hello, Настройка, запуск и удалить шлюз приложения.</span><span class="sxs-lookup"><span data-stu-id="68a44-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="68a44-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="68a44-114">Before you begin</span></span>

1. <span data-ttu-id="68a44-115">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="68a44-116">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="68a44-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="68a44-117">При наличии существующей виртуальной сети, выберите существующую пустую подсеть или создать новую подсеть в существующей виртуальной сети для использования исключительно шлюзом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="68a44-118">Невозможно развернуть hello приложения шлюза tooa другую виртуальную сеть чем hello ресурсы предполагается toodeploy за шлюза приложения hello, если не используется пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="68a44-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="68a44-119">более посетите toolearn [Пиринг виртуальной сети](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="68a44-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="68a44-120">Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.</span><span class="sxs-lookup"><span data-stu-id="68a44-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="68a44-121">Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети.</span><span class="sxs-lookup"><span data-stu-id="68a44-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="68a44-122">шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="68a44-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="68a44-123">должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="68a44-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="68a44-124">Что такое необходимые toocreate шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="68a44-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="68a44-125">При использовании hello `New-AzureApplicationGateway` шлюза приложения hello toocreate команды, конфигурация не установлено на этом этапе и hello только что созданный ресурс настраиваются с помощью XML или объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="68a44-126">доступны следующие значения Hello:</span><span class="sxs-lookup"><span data-stu-id="68a44-126">hello values are:</span></span>

* <span data-ttu-id="68a44-127">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="68a44-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="68a44-128">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="68a44-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="68a44-129">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="68a44-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="68a44-130">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="68a44-131">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="68a44-132">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="68a44-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="68a44-133">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="68a44-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="68a44-134">**Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="68a44-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="68a44-135">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="68a44-135">Create an application gateway</span></span>

<span data-ttu-id="68a44-136">toocreate шлюза приложения:</span><span class="sxs-lookup"><span data-stu-id="68a44-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="68a44-137">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="68a44-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="68a44-138">Создайте XML-файл конфигурации или объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="68a44-139">Зафиксируйте toohello конфигурации hello созданного ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="68a44-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="68a44-140">Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="68a44-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="68a44-141">Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68a44-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Пример сценария][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="68a44-143">Создание ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="68a44-143">Create an application gateway resource</span></span>

<span data-ttu-id="68a44-144">шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="68a44-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="68a44-145">Выставление счетов для шлюза hello не начинается на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="68a44-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="68a44-146">Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.</span><span class="sxs-lookup"><span data-stu-id="68a44-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="68a44-147">Hello следующий пример создает шлюза приложения, используя виртуальную сеть с именем «testvnet1» и подсети, называется «подсеть-1»:</span><span class="sxs-lookup"><span data-stu-id="68a44-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="68a44-148">*Description*, *InstanceCount* и *GatewaySize* — необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="68a44-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="68a44-149">toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="68a44-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="68a44-150">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="68a44-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="68a44-151">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="68a44-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="68a44-152">Можно выбрать размер Small (Малый), Medium (Средний) или Large (Большой).</span><span class="sxs-lookup"><span data-stu-id="68a44-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="68a44-153">*Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась.</span><span class="sxs-lookup"><span data-stu-id="68a44-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="68a44-154">Эти отчеты создаются после hello шлюз находится в рабочем состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="68a44-155">Настройка шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="68a44-155">Configure hello application gateway</span></span>

<span data-ttu-id="68a44-156">Шлюз приложения hello можно настроить с помощью XML-индекс или объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="68a44-157">Настройка шлюза hello приложения с помощью XML</span><span class="sxs-lookup"><span data-stu-id="68a44-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="68a44-158">В следующем примере hello используйте все параметры шлюза приложения tooconfigure файла XML и зафиксировать их ресурса шлюза toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="68a44-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="68a44-159">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="68a44-159">Step 1</span></span>

<span data-ttu-id="68a44-160">Скопируйте следующий текст tooNotepad hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="68a44-161">Изменение значений hello заключено в круглые скобки hello для элементов конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="68a44-162">Сохраните hello файл с расширением .xml.</span><span class="sxs-lookup"><span data-stu-id="68a44-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68a44-163">Hello элемент протокола Http или Https с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="68a44-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="68a44-164">Hello в следующем примере показано, как toouse конфигурации файла tooset Создание шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="68a44-165">Загрузка пример Hello распределяет трафик HTTP на открытый порт 80 и отправляет сетевой трафик tooback конечный порт 80 между двумя IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="68a44-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a><span data-ttu-id="68a44-166">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="68a44-166">Step 2</span></span>

<span data-ttu-id="68a44-167">Затем задайте шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-167">Next, set hello application gateway.</span></span> <span data-ttu-id="68a44-168">Используйте hello `Set-AzureApplicationGatewayConfig` командлет с помощью файла конфигурации XML.</span><span class="sxs-lookup"><span data-stu-id="68a44-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="68a44-169">Настройка шлюза hello приложения с помощью объекта конфигурации</span><span class="sxs-lookup"><span data-stu-id="68a44-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="68a44-170">Hello в следующем примере показано, как tooconfigure hello шлюз приложений с помощью объектов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="68a44-171">Все элементы конфигурации, которые необходимо настроить отдельно и затем добавляются объект конфигурации шлюза tooan приложения.</span><span class="sxs-lookup"><span data-stu-id="68a44-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="68a44-172">После создания объекта конфигурации hello, использовать hello `Set-AzureApplicationGateway` toohello конфигурации hello toocommit команда создала ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="68a44-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="68a44-173">Перед назначением объект конфигурации tooeach значения, необходимо toodeclare объект какого типа PowerShell использует для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="68a44-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="68a44-174">Определяет, что Hello первой строки toocreate hello отдельных элементов `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` используются.</span><span class="sxs-lookup"><span data-stu-id="68a44-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="68a44-175">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="68a44-175">Step 1</span></span>

<span data-ttu-id="68a44-176">Создайте все отдельные элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-176">Create all individual configuration items.</span></span>

<span data-ttu-id="68a44-177">Создайте hello интерфейсный IP, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="68a44-178">Создайте интерфейсный порт hello, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="68a44-179">Создайте пул серверных hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="68a44-180">Определите hello IP-адресов, которые добавляются в пул серверных toohello, как показано в следующем примере hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="68a44-181">Используйте объект toohello серверной части пула tooadd hello hello $server объекта значения ($pool).</span><span class="sxs-lookup"><span data-stu-id="68a44-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="68a44-182">Создайте пул приветствия на внутреннем сервере.</span><span class="sxs-lookup"><span data-stu-id="68a44-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="68a44-183">Создайте прослушиватель hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="68a44-184">Создание правила hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="68a44-185">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="68a44-185">Step 2</span></span>

<span data-ttu-id="68a44-186">Назначьте все отдельные элементы tooan приложения шлюза конфигурации объект конфигурации ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="68a44-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="68a44-187">Добавьте hello интерфейсный IP-toohello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68a44-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="68a44-188">Добавьте конфигурацию toohello интерфейсный порт hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="68a44-189">Добавьте конфигурацию toohello пула серверных hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="68a44-190">Добавьте hello внутренней параметр toohello конфигурацию пула.</span><span class="sxs-lookup"><span data-stu-id="68a44-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="68a44-191">Добавьте конфигурацию toohello hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="68a44-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="68a44-192">Добавьте конфигурацию toohello правило hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="68a44-193">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="68a44-193">Step 3</span></span>
<span data-ttu-id="68a44-194">Зафиксировать ресурс шлюза для объекта toohello hello конфигурации приложения с помощью `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="68a44-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="68a44-195">Запуск шлюза hello</span><span class="sxs-lookup"><span data-stu-id="68a44-195">Start hello gateway</span></span>

<span data-ttu-id="68a44-196">После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="68a44-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="68a44-197">Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="68a44-198">Hello `Start-AzureApplicationGateway` командлет может занимать toofinish too15-20 минут.</span><span class="sxs-lookup"><span data-stu-id="68a44-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="68a44-199">Проверить состояние шлюза hello</span><span class="sxs-lookup"><span data-stu-id="68a44-199">Verify hello gateway status</span></span>

<span data-ttu-id="68a44-200">Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="68a44-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="68a44-201">Если `Start-AzureApplicationGateway` успешно hello в предыдущем шаге, *состояние* должна быть запущена, и *Vip* и *DnsName* должны иметь допустимые записи.</span><span class="sxs-lookup"><span data-stu-id="68a44-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="68a44-202">Hello пример шлюза приложения, активированы, запущены и готов tootake трафик, поступающий для `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="68a44-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="68a44-203">Удалить шлюз приложения hello</span><span class="sxs-lookup"><span data-stu-id="68a44-203">Delete hello application gateway</span></span>

<span data-ttu-id="68a44-204">шлюз приложения hello toodelete:</span><span class="sxs-lookup"><span data-stu-id="68a44-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="68a44-205">Используйте hello `Stop-AzureApplicationGateway` командлет toostop hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="68a44-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="68a44-206">Используйте hello `Remove-AzureApplicationGateway` командлет tooremove hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="68a44-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="68a44-207">Убедитесь, что hello шлюза был удален с помощью hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="68a44-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="68a44-208">Hello пример hello `Stop-AzureApplicationGateway` на первую строку hello, командлет следуют hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="68a44-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="68a44-209">После шлюза приложения hello в остановленном состоянии используйте hello `Remove-AzureApplicationGateway` командлет tooremove hello службы.</span><span class="sxs-lookup"><span data-stu-id="68a44-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="68a44-210">tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="68a44-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="68a44-211">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="68a44-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="68a44-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68a44-212">Next steps</span></span>

<span data-ttu-id="68a44-213">Если tooconfigure разгрузки SSL, см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="68a44-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="68a44-214">Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="68a44-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="68a44-215">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="68a44-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="68a44-216">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="68a44-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="68a44-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="68a44-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
