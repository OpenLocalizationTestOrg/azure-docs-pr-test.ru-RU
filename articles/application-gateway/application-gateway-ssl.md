---
title: "Настройка разгрузки SSL для шлюза приложений Azure с помощью PowerShell (классическая модель) | Документация Майкрософт"
description: "В этой статье приводятся инструкции по созданию шлюза приложений с разгрузкой SSL с помощью классической модели развертывания Azure."
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="4d9ca-103">Настройка шлюза приложений для разгрузки SSL с помощью классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="4d9ca-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d9ca-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d9ca-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="4d9ca-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="4d9ca-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="4d9ca-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d9ca-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="4d9ca-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4d9ca-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="4d9ca-108">Шлюз приложений Azure можно настроить на завершение сеанса SSL в шлюзе, что позволит избежать выполнения дорогостоящей задачи SSL-шифрования на веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="4d9ca-109">Кроме того, разгрузка SSL упрощает процесс установки внешнего сервера и управления веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4d9ca-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4d9ca-110">Before you begin</span></span>

1. <span data-ttu-id="4d9ca-111">Установите последнюю версию командлетов Azure PowerShell, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="4d9ca-112">Последнюю версию можно загрузить и установить в разделе **Windows PowerShell** на [странице загрузок](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4d9ca-113">Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="4d9ca-114">Убедитесь, что подсеть не используется виртуальной машиной или облачным развертыванием.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="4d9ca-115">Сам шлюз приложений должен находиться в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="4d9ca-116">Для использования шлюза приложений настраиваются существующие серверы или серверы, для которых в виртуальной сети созданы конечные точки либо же назначен общедоступный или виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="4d9ca-117">Чтобы настроить разгрузку SSL в шлюзе приложений, выполните перечисленные ниже действия в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="4d9ca-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="4d9ca-118">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="4d9ca-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="4d9ca-119">Загрузка SSL-сертификатов</span><span class="sxs-lookup"><span data-stu-id="4d9ca-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="4d9ca-120">Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="4d9ca-121">Настройка конфигурации шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="4d9ca-122">Запуск шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="4d9ca-123">Проверка состояния шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="4d9ca-124">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="4d9ca-124">Create an application gateway</span></span>

<span data-ttu-id="4d9ca-125">Для создания шлюза используйте командлет `New-AzureApplicationGateway`, подставив в него свои значения.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="4d9ca-126">Выставление счетов для шлюза начинается не на данном этапе,</span><span class="sxs-lookup"><span data-stu-id="4d9ca-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="4d9ca-127">а позднее, после успешного запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="4d9ca-128">Чтобы проверить создание шлюза, используйте командлет `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="4d9ca-129">В примере параметры *Description* (Описание), *InstanceCount* (Количество экземпляров) и *GatewaySize* (Размер шлюза) являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="4d9ca-130">Значение параметра *InstanceCount* по умолчанию — 2 (максимальное значение — 10).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4d9ca-131">Значение *GatewaySize* (Размер шлюза) по умолчанию — Medium (Средний).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4d9ca-132">Также доступны значения Small (Маленький) и Large (Большой).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-132">Small and Large are other available values.</span></span> <span data-ttu-id="4d9ca-133">Параметры *VirtualIPs* и *DnsName* отображаются без значений, так как шлюз еще не запущен.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="4d9ca-134">Эти значения будут определены после запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="4d9ca-135">Загрузка SSL-сертификатов</span><span class="sxs-lookup"><span data-stu-id="4d9ca-135">Upload SSL certificates</span></span>

<span data-ttu-id="4d9ca-136">Чтобы загрузить на шлюз приложений сертификаты сервера в формате *PFX*, используйте командлет `Add-AzureApplicationGatewaySslCertificate`.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="4d9ca-137">Имя сертификата выбирается пользователем и должно быть уникальным в пределах шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="4d9ca-138">В операциях управления сертификатами в шлюзе приложений сертификат указывается по имени.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="4d9ca-139">В следующем примере приведен командлет; замените значения в нем собственными.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="4d9ca-140">Затем проверьте загрузку сертификата.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="4d9ca-141">Используйте командлет `Get-AzureApplicationGatewayCertificate` .</span><span class="sxs-lookup"><span data-stu-id="4d9ca-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="4d9ca-142">В данном примере командлет показан в первой строке, а затем выходные данные.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="4d9ca-143">Пароль сертификата должен содержать 4–12 знаков, букв или цифр.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="4d9ca-144">Специальные знаки не допускаются.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="4d9ca-145">Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-145">Configure the gateway</span></span>

<span data-ttu-id="4d9ca-146">Конфигурация шлюза приложений состоит из нескольких значений.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="4d9ca-147">Значения конфигурации могут быть взаимосвязаны.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="4d9ca-148">Доступны следующие значения.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-148">The values are:</span></span>

* <span data-ttu-id="4d9ca-149">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4d9ca-150">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4d9ca-151">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4d9ca-152">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4d9ca-153">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4d9ca-154">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4d9ca-155">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4d9ca-156">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="4d9ca-157">В настоящее время поддерживается только *основное* правило.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="4d9ca-158">*Основное* правило предусматривает циклическое распределение нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="4d9ca-159">**Дополнительные примечания по настройке конфигурации**</span><span class="sxs-lookup"><span data-stu-id="4d9ca-159">**Additional configuration notes**</span></span>

<span data-ttu-id="4d9ca-160">Чтобы настроить конфигурацию SSL-сертификатов, протокол в элементе **HttpListener** следует изменить на *Https* (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="4d9ca-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="4d9ca-161">К **HttpListener** добавляется элемент **SslCert** со значением, соответствующим имени, которое использовалось выше при передаче SSL-сертификатов.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="4d9ca-162">Внешний порт следует изменить на 443.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="4d9ca-163">**Включение сходства на основе файлов cookie**. Шлюз приложений можно настроить так, чтобы запросы от клиентского сеанса всегда направлялись на одну виртуальную машину в веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="4d9ca-164">Это делается с помощью внедрения файлов cookie сеанса, что позволяет шлюзу перенаправлять трафик соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="4d9ca-165">Чтобы включить сходство на основе файлов cookie, присвойте параметру **CookieBasedAffinity** в элементе *BackendHttpSettings* значение **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="4d9ca-166">Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="4d9ca-167">Чтобы создать конфигурацию с помощью XML-файла конфигурации, используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="4d9ca-168">**Пример XML-конфигурации**</span><span class="sxs-lookup"><span data-stu-id="4d9ca-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="4d9ca-169">Настройка конфигурации шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-169">Set the gateway configuration</span></span>

<span data-ttu-id="4d9ca-170">Теперь шлюз приложений необходимо настроить.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-170">Next, you set the application gateway.</span></span> <span data-ttu-id="4d9ca-171">Для этого можно использовать командлет `Set-AzureApplicationGatewayConfig` либо с объектом конфигурации, либо с XML-файлом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="4d9ca-172">Запуск шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-172">Start the gateway</span></span>

<span data-ttu-id="4d9ca-173">Настроенный шлюз можно запустить с помощью командлета `Start-AzureApplicationGateway` .</span><span class="sxs-lookup"><span data-stu-id="4d9ca-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="4d9ca-174">Выставление счетов для шлюза приложений начинается после запуска шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="4d9ca-175">Выполнение командлета `Start-AzureApplicationGateway`может длиться 15–20 минут.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="4d9ca-176">Проверка состояния шлюза</span><span class="sxs-lookup"><span data-stu-id="4d9ca-176">Verify the gateway status</span></span>

<span data-ttu-id="4d9ca-177">Проверить состояние шлюза можно с помощью командлета `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="4d9ca-178">Если на предыдущем этапе командлет `Start-AzureApplicationGateway` выполнен успешно, то у параметра *State* должно быть значение "Running", а у параметров *VirtualIPs* и *DnsName* — допустимые значения.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="4d9ca-179">В данном примере показан рабочий шлюз приложений, готовый к приему трафика.</span><span class="sxs-lookup"><span data-stu-id="4d9ca-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4d9ca-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d9ca-180">Next steps</span></span>

<span data-ttu-id="4d9ca-181">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="4d9ca-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4d9ca-182">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="4d9ca-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4d9ca-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4d9ca-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

