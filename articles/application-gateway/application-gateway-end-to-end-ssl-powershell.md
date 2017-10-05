---
title: "Настройка сквозного режима связи SSL для шлюза приложений Azure| Документация Майкрософт"
description: "В этой статье описывается настройка сквозного режима связи SSL на шлюзе приложений с помощью PowerShell для Azure Resource Manager."
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="a1016-103">Настройка сквозного режима связи SSL для шлюза приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1016-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="a1016-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a1016-104">Overview</span></span>

<span data-ttu-id="a1016-105">Шлюз приложений поддерживает сквозное шифрование трафика.</span><span class="sxs-lookup"><span data-stu-id="a1016-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="a1016-106">Для этого шлюз приложений завершает SSL-соединение.</span><span class="sxs-lookup"><span data-stu-id="a1016-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="a1016-107">Затем шлюз применяет правила маршрутизации к трафику, повторно шифрует пакет и пересылает его в соответствующую серверную часть согласно определенным правилам маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a1016-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="a1016-108">Любой ответ веб-сервера проходит через тот же процесс на пути к пользователю.</span><span class="sxs-lookup"><span data-stu-id="a1016-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="a1016-109">Еще одна поддерживаемая шлюзом приложений функция — отключение определенных версий протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="a1016-110">Шлюз приложений поддерживает отключение следующих версий протокола: **TLSv1.0**, **TLSv1.1** и **TLSv1.2**. Также шлюз поддерживает определение комплектов шифров для использования и их приоритет.</span><span class="sxs-lookup"><span data-stu-id="a1016-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="a1016-111">Дополнительные сведения о настраиваемых параметрах SSL см. в статье [Общие сведения о политике SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1016-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a1016-112">Протоколы SSL 2.0 и SSL 3.0 отключены по умолчанию, и их нельзя включать.</span><span class="sxs-lookup"><span data-stu-id="a1016-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="a1016-113">Они считаются небезопасными и не могут использоваться со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![Изображение для сценария][scenario]

## <a name="scenario"></a><span data-ttu-id="a1016-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a1016-115">Scenario</span></span>

<span data-ttu-id="a1016-116">В этом сценарии вы узнаете, как создать шлюз приложений со сквозным режимом связи SSL с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a1016-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="a1016-117">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="a1016-117">This scenario will:</span></span>

* <span data-ttu-id="a1016-118">как создать группу ресурсов **appgw-rg**;</span><span class="sxs-lookup"><span data-stu-id="a1016-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="a1016-119">как создать виртуальную сеть **appgwvnet** с адресным пространством 10.0.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="a1016-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="a1016-120">как создать две подсети, **appgwsubnet** и **appsubnet**;</span><span class="sxs-lookup"><span data-stu-id="a1016-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="a1016-121">как создать небольшой шлюз приложений, поддерживающий сквозное шифрование SSL, который ограничивает определенные версии протокола SSL и комплекты шифров.</span><span class="sxs-lookup"><span data-stu-id="a1016-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1016-122">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a1016-122">Before you begin</span></span>

<span data-ttu-id="a1016-123">Чтобы настроить сквозной режим связи SSL для шлюза приложений, требуются сертификат для шлюза и сертификаты для внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="a1016-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="a1016-124">Сертификат шлюза используется для шифрования и расшифровки трафика, передаваемого по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="a1016-125">Сертификат шлюза должен быть представлен в формате PFX (файл обмена личной информацией).</span><span class="sxs-lookup"><span data-stu-id="a1016-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="a1016-126">Этот формат файла позволяет экспортировать закрытый ключ, необходимый шлюзу приложений для шифрования и расшифровки трафика.</span><span class="sxs-lookup"><span data-stu-id="a1016-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="a1016-127">Чтобы использовать сквозное шифрование SSL, серверная часть должна быть внесена в список разрешений с помощью шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="a1016-128">Для этого следует передать открытый сертификат серверных частей в шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="a1016-129">Это гарантирует, что шлюз приложений взаимодействует только с известными экземплярами серверной части,</span><span class="sxs-lookup"><span data-stu-id="a1016-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="a1016-130">тем самым защищая сквозной обмен данными.</span><span class="sxs-lookup"><span data-stu-id="a1016-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="a1016-131">Этот процесс описывается ниже.</span><span class="sxs-lookup"><span data-stu-id="a1016-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="a1016-132">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1016-132">Create the Resource Group</span></span>

<span data-ttu-id="a1016-133">В этом разделе описывается создание группы ресурсов, содержащей шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="a1016-134">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a1016-134">Step 1</span></span>

<span data-ttu-id="a1016-135">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a1016-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="a1016-136">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a1016-136">Step 2</span></span>

<span data-ttu-id="a1016-137">Выберите подписку для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="a1016-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="a1016-138">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a1016-138">Step 3</span></span>

<span data-ttu-id="a1016-139">Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="a1016-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="a1016-140">Создание виртуальной сети и подсети для шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1016-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="a1016-141">Следующий пример создает виртуальную сеть и две подсети.</span><span class="sxs-lookup"><span data-stu-id="a1016-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="a1016-142">Одна подсеть используется для размещения шлюза приложений,</span><span class="sxs-lookup"><span data-stu-id="a1016-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="a1016-143">а другая — для внутренних серверов, на которых размещается веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a1016-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="a1016-144">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a1016-144">Step 1</span></span>

<span data-ttu-id="a1016-145">Назначьте диапазон адресов подсети для самого шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="a1016-146">Подсети, настроенные для шлюза приложений, должны иметь соответствующий размер.</span><span class="sxs-lookup"><span data-stu-id="a1016-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="a1016-147">У шлюза приложений может быть до 10 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="a1016-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="a1016-148">Для каждого экземпляра требуется отдельный IP-адрес из подсети.</span><span class="sxs-lookup"><span data-stu-id="a1016-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="a1016-149">Слишком маленький размер подсети может отрицательно сказаться на возможности масштабирования шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="a1016-150">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a1016-150">Step 2</span></span>

<span data-ttu-id="a1016-151">Назначьте диапазон адресов для внутреннего пула адресов.</span><span class="sxs-lookup"><span data-stu-id="a1016-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="a1016-152">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a1016-152">Step 3</span></span>

<span data-ttu-id="a1016-153">Создайте виртуальную сеть с подсетями, определенными на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="a1016-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="a1016-154">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a1016-154">Step 4</span></span>

<span data-ttu-id="a1016-155">Получите ресурс виртуальной сети и ресурсы подсетей, которые будут использоваться при выполнении следующих действий.</span><span class="sxs-lookup"><span data-stu-id="a1016-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="a1016-156">Создание общедоступного IP-адреса для конфигурации интерфейсной части</span><span class="sxs-lookup"><span data-stu-id="a1016-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="a1016-157">Создайте ресурс общедоступного IP-адреса для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="a1016-158">Этот общедоступный IP-адрес используется на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="a1016-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="a1016-159">Шлюз приложений не поддерживает использование общедоступного IP-адреса, для которого метка домена была определена при создании.</span><span class="sxs-lookup"><span data-stu-id="a1016-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="a1016-160">Поддерживается только общедоступный IP-адрес с динамически создаваемой меткой домена.</span><span class="sxs-lookup"><span data-stu-id="a1016-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="a1016-161">Если для шлюза приложений требуется понятное DNS-имя, то рекомендуется использовать в качестве псевдонима запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="a1016-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="a1016-162">Создание объекта конфигурации шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1016-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="a1016-163">Перед созданием шлюза приложений необходимо настроить все элементы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a1016-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="a1016-164">В ходе следующих шагов создаются необходимые элементы конфигурации для ресурса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="a1016-165">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a1016-165">Step 1</span></span>

<span data-ttu-id="a1016-166">Создайте конфигурацию IP шлюза приложений, в которой определено, какую подсеть использует шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="a1016-167">При запуске шлюз приложений получает IP-адрес из настроенной подсети. Затем шлюз направляет сетевой трафик на IP-адреса из внутреннего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a1016-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="a1016-168">Помните, что для каждого экземпляра требуется отдельный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a1016-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="a1016-169">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a1016-169">Step 2</span></span>

<span data-ttu-id="a1016-170">Создайте конфигурацию IP внешнего интерфейса, в которой частный или общедоступный IP-адрес сопоставляется с внешним интерфейсом шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="a1016-171">На следующем шаге общедоступный IP-адрес, указанный на предыдущем шаге, будет связан конфигурацией IP внешнего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a1016-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="a1016-172">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a1016-172">Step 3</span></span>

<span data-ttu-id="a1016-173">Настройте IP-адреса внутренних веб-серверов во внутреннем пуле IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a1016-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="a1016-174">Эти IP-адреса будут использоваться для получения сетевого трафика от конечной точки с интерфейсным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="a1016-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="a1016-175">Замените приведенные ниже IP-адреса и добавьте IP-адреса конечных точек своего приложения.</span><span class="sxs-lookup"><span data-stu-id="a1016-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="a1016-176">Для внутренних серверов вместо IP-адресов можно также использовать полные доменные имена с помощью параметра -BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="a1016-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="a1016-177">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a1016-177">Step 4</span></span>

<span data-ttu-id="a1016-178">Настройте интерфейсный порт IP для конечной точки с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="a1016-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="a1016-179">Это порт, к которому подключаются пользователи.</span><span class="sxs-lookup"><span data-stu-id="a1016-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="a1016-180">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="a1016-180">Step 5</span></span>

<span data-ttu-id="a1016-181">Настройте сертификат для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="a1016-182">Этот сертификат используется для шифрования и расшифровки трафика на шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="a1016-183">Этот пример настраивает сертификат для SSL-соединения.</span><span class="sxs-lookup"><span data-stu-id="a1016-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="a1016-184">Сертификат должен быть в формате PFX, а пароль к сертификату должен содержать от 4 до 12 символов.</span><span class="sxs-lookup"><span data-stu-id="a1016-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="a1016-185">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="a1016-185">Step 6</span></span>

<span data-ttu-id="a1016-186">Создайте прослушиватель HTTP для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="a1016-187">Назначьте используемую конфигурацию IP внешнего интерфейса, порт и SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="a1016-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="a1016-188">Шаг 7</span><span class="sxs-lookup"><span data-stu-id="a1016-188">Step 7</span></span>

<span data-ttu-id="a1016-189">Передайте сертификат, который будет использоваться для ресурсов внутреннего пула, поддерживающих протокол SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="a1016-190">Проба по умолчанию получает открытый ключ из привязки SSL **по умолчанию** по IP-адресу серверной части и сравнивает полученное значение открытого ключа со значением, которое предоставляете вы.</span><span class="sxs-lookup"><span data-stu-id="a1016-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="a1016-191">**Если** на серверной части используются заголовки узлов и SNI, полученный открытый ключ не обязательно будет ключом сайта, на который направляется интернет-трафик.</span><span class="sxs-lookup"><span data-stu-id="a1016-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="a1016-192">Если вы сомневаетесь, перейдите по адресу https://127.0.0.1/ на серверных частях, чтобы проверить, какой сертификат используется для привязки SSL **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="a1016-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="a1016-193">В этом разделе используйте открытый ключ из этого запроса.</span><span class="sxs-lookup"><span data-stu-id="a1016-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="a1016-194">Если в привязках HTTPS используются заголовки узлов и SNI и вы не получаете ответ и сертификат, после того как вручную отправили в браузере запрос на адрес https://127.0.0.1/ для серверных частей, на них необходимо настроить привязку SSL по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a1016-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="a1016-195">Если этого не сделать, пробы будут завершены ошибкой и серверная часть не будет добавлена в список разрешений.</span><span class="sxs-lookup"><span data-stu-id="a1016-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="a1016-196">Сертификат, предоставленный на этом шаге, должен быть открытым ключом сертификата в формате PFX, хранящегося в серверной части.</span><span class="sxs-lookup"><span data-stu-id="a1016-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="a1016-197">Экспортируйте сертификат (не корневой) в формате CER, установленный на внутреннем сервере, и используйте его на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="a1016-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="a1016-198">Это действие добавляет серверную часть в список разрешений шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="a1016-199">Шаг 8</span><span class="sxs-lookup"><span data-stu-id="a1016-199">Step 8</span></span>

<span data-ttu-id="a1016-200">Настройте параметры HTTP серверной части шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="a1016-201">В параметрах HTTP укажите сертификат, переданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a1016-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="a1016-202">Шаг 9.</span><span class="sxs-lookup"><span data-stu-id="a1016-202">Step 9</span></span>

<span data-ttu-id="a1016-203">Создайте правило маршрутизации для балансировщика нагрузки, которое настраивает его поведение.</span><span class="sxs-lookup"><span data-stu-id="a1016-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="a1016-204">В этом примере создается базовое правило с циклическим перебором.</span><span class="sxs-lookup"><span data-stu-id="a1016-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="a1016-205">Шаг 10</span><span class="sxs-lookup"><span data-stu-id="a1016-205">Step 10</span></span>

<span data-ttu-id="a1016-206">Настройте размер экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="a1016-207">Доступные размеры: **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="a1016-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="a1016-208">Доступные значения емкости: от 1 до 10.</span><span class="sxs-lookup"><span data-stu-id="a1016-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="a1016-209">Для тестирования можно выбрать число экземпляров, равное 1.</span><span class="sxs-lookup"><span data-stu-id="a1016-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="a1016-210">Важно знать, что если указать число экземпляров менее двух, то развертывание не попадает под действие соглашения об уровне обслуживания, и поэтому это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="a1016-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="a1016-211">Мелкие шлюзы предназначены для разработки и тестирования, а не для производства.</span><span class="sxs-lookup"><span data-stu-id="a1016-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="a1016-212">Шаг 11</span><span class="sxs-lookup"><span data-stu-id="a1016-212">Step 11</span></span>

<span data-ttu-id="a1016-213">Настройте политику SSL для шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="a1016-214">Шлюз приложений поддерживает возможность установить минимальную версию для версии протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="a1016-215">Ниже приведен список значений для версий протокола, которые можно определить.</span><span class="sxs-lookup"><span data-stu-id="a1016-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="a1016-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="a1016-216">**TLSv1_0**</span></span>
* <span data-ttu-id="a1016-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="a1016-217">**TLSv1_1**</span></span>
* <span data-ttu-id="a1016-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="a1016-218">**TLSv1_2**</span></span>

<span data-ttu-id="a1016-219">Задает **TLSv1_2** в качестве минимальной версии протокола и разрешает только шифры **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** и **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**.</span><span class="sxs-lookup"><span data-stu-id="a1016-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="a1016-220">Создание шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1016-220">Create the Application Gateway</span></span>

<span data-ttu-id="a1016-221">Создайте шлюз приложений в соответствии с действиями, выполненными на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="a1016-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="a1016-222">Имейте ввиду, что создание шлюза — долгий процесс.</span><span class="sxs-lookup"><span data-stu-id="a1016-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="a1016-223">Ограничение версий протокола SSL на существующем шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="a1016-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="a1016-224">Выше было описано создание шлюза приложений со сквозным режимом связи SSL и отключение определенных версий протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="a1016-225">В следующем примере отключаются определенные политики SSL на существующем шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="a1016-226">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a1016-226">Step 1</span></span>

<span data-ttu-id="a1016-227">Получите шлюз приложений, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="a1016-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="a1016-228">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a1016-228">Step 2</span></span>

<span data-ttu-id="a1016-229">Определите политику SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-229">Define an SSL policy.</span></span> <span data-ttu-id="a1016-230">Ниже представлен пример отключения версий TLSv1.0 и TLSv1.1 и разрешения только комплектов шифров **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** и **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**.</span><span class="sxs-lookup"><span data-stu-id="a1016-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="a1016-231">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a1016-231">Step 3</span></span>

<span data-ttu-id="a1016-232">Наконец, обновите шлюз.</span><span class="sxs-lookup"><span data-stu-id="a1016-232">Finally, update the gateway.</span></span> <span data-ttu-id="a1016-233">Важно отметить, что этот последний шаг требует значительного времени.</span><span class="sxs-lookup"><span data-stu-id="a1016-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="a1016-234">По завершении на шлюзе приложений будет настроен сквозной режим связи SSL.</span><span class="sxs-lookup"><span data-stu-id="a1016-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a1016-235">Получение DNS-имени шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="a1016-235">Get application gateway DNS name</span></span>

<span data-ttu-id="a1016-236">После создания шлюза следует настроить внешний интерфейс для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="a1016-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="a1016-237">Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="a1016-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a1016-238">Чтобы гарантировать попадание пользователей на шлюз приложений, можно использовать запись CNAME, чтобы указать общедоступную конечную точку шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="a1016-239">[Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1016-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a1016-240">Получите информацию о шлюзе приложений и соответствующее IP- или DNS-имя с помощью элемента PublicIPAddress, связанного со шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="a1016-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="a1016-241">DNS-имя шлюза приложений должно использоваться для создания записи CNAME, указывающей двум веб-приложениям на это DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="a1016-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="a1016-242">Использование записи A не рекомендуется, так как виртуальный IP-адрес может измениться после перезапуска приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="a1016-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1016-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1016-243">Next steps</span></span>

<span data-ttu-id="a1016-244">Дополнительные сведения об усилении безопасности веб-приложений с помощью брандмауэра веб-приложения в шлюзе приложений см. в разделе [Обзор брандмауэра веб-приложения](application-gateway-webapplicationfirewall-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1016-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
