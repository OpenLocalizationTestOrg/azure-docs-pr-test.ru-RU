---
title: "конец aaaConfigure tooend SSL со шлюзом приложения Azure | Документы Microsoft"
description: "В этой статье описывается, как tooconfigure завершить tooend SSL со шлюзом приложений с помощью PowerShell диспетчера ресурсов Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="d0e31-103">Настройка конечного tooend SSL с помощью шлюза приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0e31-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="d0e31-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d0e31-104">Overview</span></span>

<span data-ttu-id="d0e31-105">Приложение поддерживает шлюза последний tooend шифрования трафика.</span><span class="sxs-lookup"><span data-stu-id="d0e31-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="d0e31-106">Шлюз приложений делает это путем прерывания hello соединение SSL на шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="d0e31-107">шлюз Hello затем применяет правила маршрутизации hello трафика toohello повторно шифрует пакет приветствия и переадресует hello пакетов toohello соответствующие базы данных на основе определенных правил маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="d0e31-108">Любой ответ с веб-сервера hello проходит через hello же процесс обратной toohello конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="d0e31-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="d0e31-109">Еще одна поддерживаемая шлюзом приложений функция — отключение определенных версий протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="d0e31-110">Шлюз приложений поддерживает отключение hello следующая версия протокола; **TLSv1.0**, **TLSv1.1**, и **TLSv1.2** также определение hello наборы toouse и hello порядок приоритета шифра.</span><span class="sxs-lookup"><span data-stu-id="d0e31-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="d0e31-111">Посетите toolearn Дополнительные сведения о настраиваемых параметров SSL [Общие сведения о политике SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0e31-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d0e31-112">Протоколы SSL 2.0 и SSL 3.0 отключены по умолчанию, и их нельзя включать.</span><span class="sxs-lookup"><span data-stu-id="d0e31-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="d0e31-113">Они рассматриваются как небезопасные и не может toobe при использовании шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![Изображение для сценария][scenario]

## <a name="scenario"></a><span data-ttu-id="d0e31-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="d0e31-115">Scenario</span></span>

<span data-ttu-id="d0e31-116">В этом сценарии вы узнаете toocreate шлюза приложения с помощью конечного tooend SSL с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0e31-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="d0e31-117">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="d0e31-117">This scenario will:</span></span>

* <span data-ttu-id="d0e31-118">как создать группу ресурсов **appgw-rg**;</span><span class="sxs-lookup"><span data-stu-id="d0e31-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="d0e31-119">как создать виртуальную сеть **appgwvnet** с адресным пространством 10.0.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="d0e31-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="d0e31-120">как создать две подсети, **appgwsubnet** и **appsubnet**;</span><span class="sxs-lookup"><span data-stu-id="d0e31-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="d0e31-121">Создайте небольшое приложение шлюза вспомогательные окончания tooend SSL-шифрование, ограничения версии протокола SSL и комплекты шифров.</span><span class="sxs-lookup"><span data-stu-id="d0e31-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d0e31-122">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d0e31-122">Before you begin</span></span>

<span data-ttu-id="d0e31-123">tooconfigure окончания tooend SSL со шлюзом приложений, требуется сертификат для шлюза hello и сертификаты необходимы для hello внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="d0e31-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="d0e31-124">сертификат шлюза Hello — используется tooencrypt и расшифровки hello трафик tooit с помощью протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="d0e31-125">сертификат шлюза Hello должен toobe в формате обмена личной информацией (pfx).</span><span class="sxs-lookup"><span data-stu-id="d0e31-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="d0e31-126">Этот формат позволяет для hello закрытого ключа toobe экспортированы, необходимые для hello приложения шлюза tooperform hello шифрованием/дешифрованием трафика.</span><span class="sxs-lookup"><span data-stu-id="d0e31-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="d0e31-127">Для end серверной hello шифрования SSL tooend необходимо включить в список разрешенных со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="d0e31-128">Это делается путем передачи hello сертификат с открытым toohello приложения hello серверных системах шлюза.</span><span class="sxs-lookup"><span data-stu-id="d0e31-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="d0e31-129">Это гарантирует, что этот шлюз приложения hello взаимодействует только с экземпляров известных серверной части.</span><span class="sxs-lookup"><span data-stu-id="d0e31-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="d0e31-130">Это дополнительно защищает hello tooend обмен данных.</span><span class="sxs-lookup"><span data-stu-id="d0e31-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="d0e31-131">Этот процесс описан в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d0e31-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="d0e31-132">Создание группы ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="d0e31-132">Create hello Resource Group</span></span>

<span data-ttu-id="d0e31-133">В этом разделе описывается создание группы ресурсов, содержащий шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="d0e31-134">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d0e31-134">Step 1</span></span>

<span data-ttu-id="d0e31-135">Войдите в учетную запись Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="d0e31-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d0e31-136">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d0e31-136">Step 2</span></span>

<span data-ttu-id="d0e31-137">Выберите toouse hello подписку для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="d0e31-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="d0e31-138">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d0e31-138">Step 3</span></span>

<span data-ttu-id="d0e31-139">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="d0e31-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="d0e31-140">Создание виртуальной сети и подсети для шлюза приложения hello</span><span class="sxs-lookup"><span data-stu-id="d0e31-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="d0e31-141">Hello пример создает виртуальную сеть и две подсети.</span><span class="sxs-lookup"><span data-stu-id="d0e31-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="d0e31-142">Одна подсеть — шлюз приложений используется toohold hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="d0e31-143">Hello других подсеть используется для веб-приложения hello серверных системах размещения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="d0e31-144">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d0e31-144">Step 1</span></span>

<span data-ttu-id="d0e31-145">Назначьте диапазон адресов для подсети hello использоваться для самого шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="d0e31-146">Подсети, настроенные для шлюза приложений, должны иметь соответствующий размер.</span><span class="sxs-lookup"><span data-stu-id="d0e31-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="d0e31-147">Шлюз приложений можно настроить для копирования too10 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="d0e31-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="d0e31-148">Каждый экземпляр имеет один IP-адрес из подсети hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="d0e31-149">Слишком маленький размер подсети может отрицательно сказаться на возможности масштабирования шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="d0e31-150">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d0e31-150">Step 2</span></span>

<span data-ttu-id="d0e31-151">Назначьте toobe диапазон адресов для пула адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="d0e31-152">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d0e31-152">Step 3</span></span>

<span data-ttu-id="d0e31-153">Создайте виртуальную сеть с подсетями hello, определенные в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="d0e31-154">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="d0e31-154">Step 4</span></span>

<span data-ttu-id="d0e31-155">Получить hello виртуального сетевого ресурса и подсети ресурсы toobe используется в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d0e31-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="d0e31-156">Создать общедоступный IP-адрес для интерфейса конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="d0e31-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="d0e31-157">Создание общих ресурсов toobe IP, используемая для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="d0e31-158">Этот общедоступный IP-адрес используется на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="d0e31-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="d0e31-159">Шлюз приложений не поддерживает использование hello общедоступный IP-адрес создан с метками домена.</span><span class="sxs-lookup"><span data-stu-id="d0e31-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="d0e31-160">Поддерживается только общедоступный IP-адрес с динамически создаваемой меткой домена.</span><span class="sxs-lookup"><span data-stu-id="d0e31-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="d0e31-161">Если требуется понятное DNS-имени для шлюза приложения hello, рекомендуется записать toouse запись CNAME в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="d0e31-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="d0e31-162">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="d0e31-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="d0e31-163">Перед созданием шлюза приложения hello устанавливаются все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0e31-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="d0e31-164">Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="d0e31-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="d0e31-165">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d0e31-165">Step 1</span></span>

<span data-ttu-id="d0e31-166">Создайте шлюз IP-адрес приложения, этот параметр позволяет указать, какие шлюз подсети hello приложением.</span><span class="sxs-lookup"><span data-stu-id="d0e31-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="d0e31-167">При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и направляет сетевой трафик toohello IP-адресов в пул IP-адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="d0e31-168">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d0e31-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="d0e31-169">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d0e31-169">Step 2</span></span>

<span data-ttu-id="d0e31-170">Создайте интерфейсный IP-конфигурации, этот параметр сопоставляет частные или общедоступные ip адрес toohello интерфейсную шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="d0e31-171">Привет, даст связывает hello общедоступный IP-адрес в hello предыдущих шага с hello интерфейсный IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0e31-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="d0e31-172">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d0e31-172">Step 3</span></span>

<span data-ttu-id="d0e31-173">Настройте пул IP-адресов hello серверной части с IP-адресами hello hello серверной части веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="d0e31-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="d0e31-174">Эти IP-адреса являются hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="d0e31-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="d0e31-175">Замените следующие IP адресов tooadd hello собственных конечных точек приложения IP адрес.</span><span class="sxs-lookup"><span data-stu-id="d0e31-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="d0e31-176">Полное доменное имя (FQDN) также является допустимым значением вместо IP-адрес для hello внутренних серверов с помощью параметра - BackendFqdns hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="d0e31-177">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="d0e31-177">Step 4</span></span>

<span data-ttu-id="d0e31-178">Настройте hello интерфейсный IP-порт для hello общедоступную конечную точку IP.</span><span class="sxs-lookup"><span data-stu-id="d0e31-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="d0e31-179">Это используется порт hello, конечные пользователи подключены.</span><span class="sxs-lookup"><span data-stu-id="d0e31-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="d0e31-180">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="d0e31-180">Step 5</span></span>

<span data-ttu-id="d0e31-181">Настройка hello сертификата для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="d0e31-182">Этот сертификат используется toodecrypt и повторное шифрование трафика hello для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="d0e31-183">В этом примере настраивается hello сертификат, используемый для подключения SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="d0e31-184">Hello сертификат должен toobe в формате PFX и hello пароль должен содержать от 4 too12 символов.</span><span class="sxs-lookup"><span data-stu-id="d0e31-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="d0e31-185">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="d0e31-185">Step 6</span></span>

<span data-ttu-id="d0e31-186">Создайте прослушиватель HTTP hello для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="d0e31-187">Назначьте hello интерфейсный IP-конфигурации, порта и toouse сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="d0e31-188">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="d0e31-188">Step 7</span></span>

<span data-ttu-id="d0e31-189">Отправьте сертификат hello toobe на hello SSL с включенной внутреннего пула ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d0e31-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="d0e31-190">проба по умолчанию Hello возвращает hello открытый ключ из hello **по умолчанию** SSL-привязку IP-адрес hello серверной части и сравнивает hello значение открытого ключа получит toohello значение открытого ключа здесь.</span><span class="sxs-lookup"><span data-stu-id="d0e31-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="d0e31-191">Hello извлечь открытый ключ, не обязательно сайта toowhich hello предназначен трафик, поступающий **Если** использовании заголовков узлов и SNI на внутреннем hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="d0e31-192">Если вы сомневаетесь, посетите https://127.0.0.1/ на сертификат, используемый для hello tooconfirm заканчивается обратной hello **по умолчанию** SSL-привязки.</span><span class="sxs-lookup"><span data-stu-id="d0e31-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="d0e31-193">Используйте hello открытого ключа из запроса в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="d0e31-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="d0e31-194">Если вы используете заголовки узлов и SNI на HTTPS-привязки и вы не получите ответ и сертификат из toohttps://127.0.0.1/ запрос вручную браузера на задний план hello-элементах, необходимо настроить привязку SSL по умолчанию на задний план hello-элементах.</span><span class="sxs-lookup"><span data-stu-id="d0e31-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="d0e31-195">Если это не так, зонды ошибкой и серверной части hello отсутствует в списке разрешений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="d0e31-196">сертификат Hello, делается на этом шаге, должен быть открытый ключ сертификата pfx hello на серверной hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="d0e31-197">Экспорт hello (не hello корневому сертификату) установлен на центральном сервере hello в. CER отформатировать и использовать его на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="d0e31-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="d0e31-198">Этот шаг запрещенного hello серверной со шлюзом приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="d0e31-199">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="d0e31-199">Step 8</span></span>

<span data-ttu-id="d0e31-200">Настройте hello шлюз http серверной части.</span><span class="sxs-lookup"><span data-stu-id="d0e31-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="d0e31-201">Назначение сертификата hello, переданных в предыдущих параметров http toohello шаг hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="d0e31-202">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="d0e31-202">Step 9</span></span>

<span data-ttu-id="d0e31-203">Создание маршрута правило подсистемы балансировки нагрузки, предназначенный для настройки поведения подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="d0e31-204">В этом примере создается базовое правило с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="d0e31-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="d0e31-205">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="d0e31-205">Step 10</span></span>

<span data-ttu-id="d0e31-206">Настройте размер экземпляра hello шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="d0e31-207">Доступные размеры Hello, **Стандартная\_небольшой**, **Стандартная\_Средний**, и **Стандартная\_большой**.</span><span class="sxs-lookup"><span data-stu-id="d0e31-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="d0e31-208">Ресурсы hello доступные значения: от 1 до 10.</span><span class="sxs-lookup"><span data-stu-id="d0e31-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="d0e31-209">Для тестирования можно выбрать число экземпляров, равное 1.</span><span class="sxs-lookup"><span data-stu-id="d0e31-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="d0e31-210">Очень важно, tooknow, что любой экземпляр подсчет в двух экземпляров не распространяется действие соглашения об уровне ОБСЛУЖИВАНИЯ hello и поэтому не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="d0e31-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="d0e31-211">Небольшой шлюзы, toobe, используемые для разработки тестирования и не в производственных целях.</span><span class="sxs-lookup"><span data-stu-id="d0e31-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="d0e31-212">Шаг 11</span><span class="sxs-lookup"><span data-stu-id="d0e31-212">Step 11</span></span>

<span data-ttu-id="d0e31-213">Настройка политики toobe hello SSL, использовать для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="d0e31-214">Шлюз приложений поддерживает возможность hello tooset минимальную версию для версии протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="d0e31-215">Hello следующие значения: список версий протокола, которые могут быть определены.</span><span class="sxs-lookup"><span data-stu-id="d0e31-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="d0e31-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="d0e31-216">**TLSv1_0**</span></span>
* <span data-ttu-id="d0e31-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="d0e31-217">**TLSv1_1**</span></span>
* <span data-ttu-id="d0e31-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="d0e31-218">**TLSv1_2**</span></span>

<span data-ttu-id="d0e31-219">Задает hello минимальное семейству слишком**TLSv1_2** и позволяет **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**и **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** только.</span><span class="sxs-lookup"><span data-stu-id="d0e31-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="d0e31-220">Создать hello шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="d0e31-220">Create hello Application Gateway</span></span>

<span data-ttu-id="d0e31-221">Используя все hello в предыдущих шагах, создайте hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="d0e31-222">Создание Hello hello шлюза — длительного процесса.</span><span class="sxs-lookup"><span data-stu-id="d0e31-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="d0e31-223">Ограничение версий протокола SSL на существующем шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="d0e31-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="d0e31-224">Hello описанные выше шаги, чтобы перейти по созданию приложения с конечным tooend SSL и отключение определенных версий протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="d0e31-225">Hello следующий пример отключает определенные политики SSL для существующего шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="d0e31-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="d0e31-226">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="d0e31-226">Step 1</span></span>

<span data-ttu-id="d0e31-227">Получить tooupdate шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="d0e31-228">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="d0e31-228">Step 2</span></span>

<span data-ttu-id="d0e31-229">Определите политику SSL.</span><span class="sxs-lookup"><span data-stu-id="d0e31-229">Define an SSL policy.</span></span> <span data-ttu-id="d0e31-230">В следующем примере hello, TLSv1.0 TLSv1.1 отключены и hello шифров **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, и  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** являются только hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="d0e31-231">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="d0e31-231">Step 3</span></span>

<span data-ttu-id="d0e31-232">Наконец обновление шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-232">Finally, update hello gateway.</span></span> <span data-ttu-id="d0e31-233">Это важные toonote, что последний шаг является длительных задач.</span><span class="sxs-lookup"><span data-stu-id="d0e31-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="d0e31-234">При завершении его окончания tooend SSL настраивается на шлюз приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d0e31-235">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="d0e31-235">Get application gateway DNS name</span></span>

<span data-ttu-id="d0e31-236">После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="d0e31-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="d0e31-237">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="d0e31-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d0e31-238">tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d0e31-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="d0e31-239">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0e31-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d0e31-240">toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="d0e31-241">шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="d0e31-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="d0e31-242">Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="d0e31-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="d0e31-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0e31-243">Next steps</span></span>

<span data-ttu-id="d0e31-244">Дополнительные сведения о Усиление защиты hello безопасности веб-приложений с брандмауэр веб-приложения через шлюз приложения, посетив [Обзор брандмауэра веб-приложения](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d0e31-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
