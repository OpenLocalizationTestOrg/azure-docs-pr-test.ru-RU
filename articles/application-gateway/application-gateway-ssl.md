---
title: "aaaConfigure SSL разгрузки классический - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Эта статья содержит инструкции, toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью hello Azure классической модели развертывания."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="e36bc-103">Настройка шлюза приложения для разгрузки SSL с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="e36bc-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e36bc-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e36bc-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="e36bc-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e36bc-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="e36bc-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e36bc-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="e36bc-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e36bc-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="e36bc-108">Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы.</span><span class="sxs-lookup"><span data-stu-id="e36bc-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="e36bc-109">Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e36bc-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e36bc-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e36bc-110">Before you begin</span></span>

1. <span data-ttu-id="e36bc-111">Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="e36bc-112">Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e36bc-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e36bc-113">Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.</span><span class="sxs-lookup"><span data-stu-id="e36bc-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="e36bc-114">Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети.</span><span class="sxs-lookup"><span data-stu-id="e36bc-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="e36bc-115">шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e36bc-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="e36bc-116">должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="e36bc-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="e36bc-117">tooconfigure SSL разгрузки на шлюза приложения, hello шагов в порядке hello:</span><span class="sxs-lookup"><span data-stu-id="e36bc-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="e36bc-118">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="e36bc-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="e36bc-119">Загрузка SSL-сертификатов</span><span class="sxs-lookup"><span data-stu-id="e36bc-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="e36bc-120">Настройка шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="e36bc-121">Набор конфигурации шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="e36bc-122">Запуск шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="e36bc-123">Проверить состояние шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="e36bc-124">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="e36bc-124">Create an application gateway</span></span>

<span data-ttu-id="e36bc-125">шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="e36bc-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="e36bc-126">Выставление счетов для шлюза hello не начинается на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="e36bc-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="e36bc-127">Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.</span><span class="sxs-lookup"><span data-stu-id="e36bc-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="e36bc-128">toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="e36bc-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="e36bc-129">В образце hello *описание*, *InstanceCount*, и *GatewaySize* являются необязательными параметрами.</span><span class="sxs-lookup"><span data-stu-id="e36bc-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="e36bc-130">Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10.</span><span class="sxs-lookup"><span data-stu-id="e36bc-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="e36bc-131">Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium.</span><span class="sxs-lookup"><span data-stu-id="e36bc-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="e36bc-132">Также доступны значения Small (Маленький) и Large (Большой).</span><span class="sxs-lookup"><span data-stu-id="e36bc-132">Small and Large are other available values.</span></span> <span data-ttu-id="e36bc-133">*Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась.</span><span class="sxs-lookup"><span data-stu-id="e36bc-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="e36bc-134">Эти значения создаются после hello шлюз находится в рабочем состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="e36bc-135">Загрузка SSL-сертификатов</span><span class="sxs-lookup"><span data-stu-id="e36bc-135">Upload SSL certificates</span></span>

<span data-ttu-id="e36bc-136">Используйте `Add-AzureApplicationGatewaySslCertificate` tooupload сертификат сервера hello в *pfx* шлюз приложений toohello формат.</span><span class="sxs-lookup"><span data-stu-id="e36bc-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="e36bc-137">Имя сертификата Hello является именем выбранные пользователем и должно быть уникальным в пределах шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="e36bc-138">Этот сертификат является ссылка tooby этим именем на все операции управления сертификата для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="e36bc-139">Это показано в следующем образце hello командлета, замените собственными значениями hello в образце hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="e36bc-140">Затем проверьте hello загрузки сертификата.</span><span class="sxs-lookup"><span data-stu-id="e36bc-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="e36bc-141">Используйте hello `Get-AzureApplicationGatewayCertificate` командлета.</span><span class="sxs-lookup"><span data-stu-id="e36bc-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="e36bc-142">Это пример hello командлета на первую строку hello, следуют hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e36bc-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="e36bc-143">Пароль сертификата Hello имеет toobe между 4 символов too12, буквы или цифры.</span><span class="sxs-lookup"><span data-stu-id="e36bc-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="e36bc-144">Специальные знаки не допускаются.</span><span class="sxs-lookup"><span data-stu-id="e36bc-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="e36bc-145">Настройка шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-145">Configure hello gateway</span></span>

<span data-ttu-id="e36bc-146">Конфигурация шлюза приложений состоит из нескольких значений.</span><span class="sxs-lookup"><span data-stu-id="e36bc-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="e36bc-147">Hello значения могут быть привязаны конфигурации hello tooconstruct вместе.</span><span class="sxs-lookup"><span data-stu-id="e36bc-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="e36bc-148">доступны следующие значения Hello:</span><span class="sxs-lookup"><span data-stu-id="e36bc-148">hello values are:</span></span>

* <span data-ttu-id="e36bc-149">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="e36bc-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="e36bc-150">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="e36bc-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="e36bc-151">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="e36bc-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e36bc-152">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="e36bc-153">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="e36bc-154">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="e36bc-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="e36bc-155">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="e36bc-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="e36bc-156">**Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="e36bc-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="e36bc-157">В настоящее время только hello *основные* правило поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e36bc-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="e36bc-158">Hello *основные* правило — распределение нагрузки с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="e36bc-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="e36bc-159">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="e36bc-159">**Additional configuration notes**</span></span>

<span data-ttu-id="e36bc-160">Для настройки сертификатов SSL, hello протокола в **HttpListener** следует изменить слишком*Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="e36bc-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="e36bc-161">Hello **SslCert** слишком добавляется элемент**HttpListener** с hello значение toohello точно такое же имя, как в hello передачи из выше разделе сертификатов SSL.</span><span class="sxs-lookup"><span data-stu-id="e36bc-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="e36bc-162">Hello интерфейсный порт должен быть обновленные too443.</span><span class="sxs-lookup"><span data-stu-id="e36bc-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="e36bc-163">**сопоставление на основе файла cookie tooenable**: шлюза приложения может быть настроенный tooensure запроса из сеанса клиента всегда является направленным toohello одной виртуальной Машины hello веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="e36bc-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="e36bc-164">Этот сценарий выполняется путем внедрения кода файла cookie сеанса, которое разрешает трафик toodirect шлюза hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e36bc-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="e36bc-165">Задайте сопоставление на основе файла cookie tooenable **CookieBasedAffinity** слишком*включено* в hello **BackendHttpSettings** элемента.</span><span class="sxs-lookup"><span data-stu-id="e36bc-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="e36bc-166">Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e36bc-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="e36bc-167">использовать конфигурацию с помощью XML-файл конфигурации tooconstruct hello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e36bc-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="e36bc-168">**Пример XML-конфигурации**</span><span class="sxs-lookup"><span data-stu-id="e36bc-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="e36bc-169">Набор конфигурации шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-169">Set hello gateway configuration</span></span>

<span data-ttu-id="e36bc-170">Затем нужно установить шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="e36bc-171">Можно использовать hello `Set-AzureApplicationGatewayConfig` командлет с объектом конфигурации или с помощью файла конфигурации XML.</span><span class="sxs-lookup"><span data-stu-id="e36bc-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="e36bc-172">Запуск шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-172">Start hello gateway</span></span>

<span data-ttu-id="e36bc-173">После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="e36bc-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="e36bc-174">Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="e36bc-175">Hello `Start-AzureApplicationGateway` командлет может занимать toofinish too15-20 минут.</span><span class="sxs-lookup"><span data-stu-id="e36bc-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="e36bc-176">Проверить состояние шлюза hello</span><span class="sxs-lookup"><span data-stu-id="e36bc-176">Verify hello gateway status</span></span>

<span data-ttu-id="e36bc-177">Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="e36bc-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="e36bc-178">Если `Start-AzureApplicationGateway` успешно hello в предыдущем шаге, *состояние* должна быть запущена, и *адреса Virtualip* и *DnsName* должны иметь допустимые записи.</span><span class="sxs-lookup"><span data-stu-id="e36bc-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="e36bc-179">Этот образец показывает, копирование, запущена и готов tootake трафик шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="e36bc-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="e36bc-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e36bc-180">Next steps</span></span>

<span data-ttu-id="e36bc-181">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="e36bc-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="e36bc-182">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="e36bc-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e36bc-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e36bc-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

