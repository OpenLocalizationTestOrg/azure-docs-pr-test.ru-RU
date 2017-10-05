---
title: "Подключение компьютера к виртуальной сети Azure с помощью соединения типа \"точка — сеть\" и проверки подлинности на основе сертификата, используя PowerShell | Документация Майкрософт"
description: "Безопасно подключайте компьютер к виртуальной сети Azure, создав подключение типа \"точка — сеть\" через VPN-шлюз с помощью проверки подлинности на основе сертификата безопасности. Эта статья посвящена модели развертывания Resource Manager. Кроме того, в ней используется PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 2e072ada13b8c742fe7f2e14737c9376f7677906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="e2017-104">Настройка подключения типа "точка — сеть" к виртуальной сети с помощью проверки подлинности на основе сертификата, используя PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2017-104">Configure a Point-to-Site connection to a VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="e2017-105">В этой статье показано, как создать виртуальную сеть с подключением типа "точка — сеть" в модели развертывания Resource Manager с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2017-105">This article shows you how to create a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e2017-106">В этой конфигурации для проверки подлинности подключающегося клиента используются сертификаты.</span><span class="sxs-lookup"><span data-stu-id="e2017-106">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="e2017-107">Эту конфигурацию также можно создать с помощью разных средств или моделей развертывания, выбрав вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="e2017-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2017-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e2017-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e2017-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2017-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="e2017-110">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="e2017-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="e2017-111">VPN-шлюз типа "точка — сеть" (P2S) позволяет создать безопасное подключение к виртуальной сети с отдельного клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="e2017-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="e2017-112">VPN-подключения типа "точка — сеть" (P2S) эффективны для подключения к виртуальной сети из удаленного расположения, например, если вы дома или на конференции.</span><span class="sxs-lookup"><span data-stu-id="e2017-112">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="e2017-113">Такая конфигурация также эффективна для использования вместо VPN-подключения типа "сеть — сеть" при наличии небольшого количества клиентов, которым требуется подключение к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-113">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span>

<span data-ttu-id="e2017-114">Подключение типа "точка — сеть" (P2S) использует протокол Secure Socket Tunneling Protocol (SSTP), то есть VPN-протокол на основе SSL.</span><span class="sxs-lookup"><span data-stu-id="e2017-114">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="e2017-115">VPN-подключение типа P2S сначала устанавливается с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="e2017-115">A P2S VPN connection is established by starting it from the client computer.</span></span>

![Схема соединения компьютера с виртуальной сетью Azure через подключение типа "точка — сеть"](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="e2017-117">Для проверки подлинности подключений типа "точка — сеть" на основе сертификатов необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="e2017-117">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="e2017-118">VPN-шлюз с маршрутизацией на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="e2017-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="e2017-119">Открытый ключ (CER-файл) для корневого сертификата, импортированный в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-119">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="e2017-120">Сразу после передачи сертификат считается доверенным сертификатом и используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e2017-120">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="e2017-121">Сертификат клиента создается из корневого сертификата и устанавливается на каждом клиентском компьютере, подключающемся к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-121">A client certificate that is generated from the root certificate and installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="e2017-122">Этот сертификат используется для проверки подлинности клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="e2017-123">Пакет конфигурации VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-123">A VPN client configuration package.</span></span> <span data-ttu-id="e2017-124">Пакет конфигурации VPN-клиента содержит информацию, необходимую для клиента, чтобы подключиться к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-124">The VPN client configuration package contains the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="e2017-125">Пакет настраивает имеющийся клиент VPN, встроенный в операционной системе Windows.</span><span class="sxs-lookup"><span data-stu-id="e2017-125">The package configures the existing VPN client that is native to the Windows operating system.</span></span> <span data-ttu-id="e2017-126">Необходимо настроить каждый клиент, подключающийся с использованием пакета конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2017-126">Each client that connects must be configured using the configuration package.</span></span>

<span data-ttu-id="e2017-127">Для подключения типа "точка — сеть" не требуется VPN-устройство или локальный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e2017-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="e2017-128">Для создания VPN-подключения используется протокол SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="e2017-128">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="e2017-129">На стороне сервера поддерживается SSTP версии 1.0, 1.1 и 1.2.</span><span class="sxs-lookup"><span data-stu-id="e2017-129">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="e2017-130">Какую версию использовать, решает клиент.</span><span class="sxs-lookup"><span data-stu-id="e2017-130">The client decides which version to use.</span></span> <span data-ttu-id="e2017-131">Для Windows 8.1 и более поздних версий по умолчанию используется SSTP версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="e2017-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="e2017-132">Дополнительные сведения о подключениях типа "точка — сеть" см. в разделе [Часто задаваемые вопросы о подключениях типа "точка — сеть"](#faq) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e2017-132">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="e2017-133">Подготовка</span><span class="sxs-lookup"><span data-stu-id="e2017-133">Before beginning</span></span>

* <span data-ttu-id="e2017-134">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="e2017-135">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e2017-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="e2017-136">Установите последнюю версию командлетов PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2017-136">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e2017-137">Дополнительные сведения об установке командлетов PowerShell см. в статье [Overview of Azure PowerShell](/powershell/azure/overview) (Обзор Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="e2017-137">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="e2017-138"><a name="example"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="e2017-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="e2017-139">Эти примеры значений можно использовать для создания тестовой среды или анализа примеров из этой стать.</span><span class="sxs-lookup"><span data-stu-id="e2017-139">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="e2017-140">Переменные присваиваются в части [1](#declare) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e2017-140">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="e2017-141">Вы можете использовать эти пошаговые инструкции, используя указанные в них значения, или же изменить значения в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="e2017-141">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

* <span data-ttu-id="e2017-142">**Имя: VNet1**.</span><span class="sxs-lookup"><span data-stu-id="e2017-142">**Name: VNet1**</span></span>
* <span data-ttu-id="e2017-143">**Адресное пространство: 192.168.0.0/16** и **10.254.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="e2017-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="e2017-144">Чтобы продемонстрировать, что эта конфигурация будет работать с несколькими адресными пространствами, в этом примере мы используем несколько адресных пространств.</span><span class="sxs-lookup"><span data-stu-id="e2017-144">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="e2017-145">Однако это необязательно для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2017-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="e2017-146">**Имя подсети: FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="e2017-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="e2017-147">**Диапазон адресов подсети: 192.168.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="e2017-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="e2017-148">**Имя подсети: BackEnd.**</span><span class="sxs-lookup"><span data-stu-id="e2017-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="e2017-149">**Диапазон адресов подсети: 10.254.1.0/24.**</span><span class="sxs-lookup"><span data-stu-id="e2017-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="e2017-150">**Имя подсети: GatewaySubnet.**</span><span class="sxs-lookup"><span data-stu-id="e2017-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="e2017-151">Имя подсети *GatewaySubnet* обязательно для работы VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="e2017-151">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="e2017-152">**Диапазон адресов подсети шлюза: 192.168.200.0/24.**</span><span class="sxs-lookup"><span data-stu-id="e2017-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="e2017-153">**Пул адресов VPN-клиента: 172.16.201.0/24.**</span><span class="sxs-lookup"><span data-stu-id="e2017-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="e2017-154">VPN-клиенты, подключающиеся к виртуальной сети с помощью этого подключения типа "точка — сеть", получают IP-адреса из пула адресов VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-154">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="e2017-155">**Подписка**. Если у вас есть несколько подписок, убедитесь, что используется правильная.</span><span class="sxs-lookup"><span data-stu-id="e2017-155">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="e2017-156">**Группа ресурсов: TestRG**.</span><span class="sxs-lookup"><span data-stu-id="e2017-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="e2017-157">**Расположение: восточная часть США**.</span><span class="sxs-lookup"><span data-stu-id="e2017-157">**Location: East US**</span></span>
* <span data-ttu-id="e2017-158">**DNS-сервер: IP-адрес** DNS-сервера, который нужно использовать для разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="e2017-158">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="e2017-159">**Имя шлюза: Vnet1GW**.</span><span class="sxs-lookup"><span data-stu-id="e2017-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="e2017-160">**Имя общедоступного IP-адреса: VNet1GWPIP**.</span><span class="sxs-lookup"><span data-stu-id="e2017-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="e2017-161">**Тип VPN: RouteBased.**</span><span class="sxs-lookup"><span data-stu-id="e2017-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="e2017-162"><a name="declare"></a>1. Вход и настройка переменных</span><span class="sxs-lookup"><span data-stu-id="e2017-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="e2017-163">В этом разделе мы выполним вход и объявим значения для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2017-163">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="e2017-164">Объявленные значения используются в примерах скриптов.</span><span class="sxs-lookup"><span data-stu-id="e2017-164">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="e2017-165">Измените значения в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="e2017-165">Change the values to reflect your own environment.</span></span> <span data-ttu-id="e2017-166">Также можно использовать объявленные значения и выполнить эти шаги в качестве упражнения.</span><span class="sxs-lookup"><span data-stu-id="e2017-166">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="e2017-167">Откройте консоль PowerShell с повышенными привилегиями и войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-167">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="e2017-168">Командлет запрашивает учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="e2017-168">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="e2017-169">После выполнения входа он скачивает параметры учетной записи, чтобы они были доступны в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2017-169">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="e2017-170">Получите список подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="e2017-171">Укажите подписку, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="e2017-171">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="e2017-172">Объявите переменные, которые вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="e2017-172">Declare the variables that you want to use.</span></span> <span data-ttu-id="e2017-173">Используйте следующий пример, подставив собственные значения в соответствующих параметрах.</span><span class="sxs-lookup"><span data-stu-id="e2017-173">Use the following sample, substituting the values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="e2017-174"><a name="ConfigureVNet"></a>2. Настройка шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e2017-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="e2017-175">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e2017-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="e2017-176">Создайте конфигурации подсети для виртуальной сети, присвоив им имена *FrontEnd*, *BackEnd* и *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="e2017-176">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="e2017-177">Эти префиксы должны быть частью объявленного адресного пространства виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-177">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="e2017-178">Создание виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-178">Create the virtual network.</span></span>

  <span data-ttu-id="e2017-179">В этом примере DNS-сервер можно не использовать.</span><span class="sxs-lookup"><span data-stu-id="e2017-179">In this example, the DNS server is optional.</span></span> <span data-ttu-id="e2017-180">Если указать значение, DNS-сервер не создается.</span><span class="sxs-lookup"><span data-stu-id="e2017-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="e2017-181">Необходимо указать IP-адрес DNS-сервера, который может разрешать имена для ресурсов, к которым вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="e2017-181">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="e2017-182">В этом примере мы использовали частный IP-адрес, но, скорее всего, это не IP-адрес DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="e2017-182">For this example, we used a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="e2017-183">Подставьте собственные значения.</span><span class="sxs-lookup"><span data-stu-id="e2017-183">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="e2017-184">Укажите переменные для созданной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-184">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="e2017-185">VPN-шлюз должен иметь общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e2017-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="e2017-186">Сначала запросите ресурс IP-адреса, а затем укажите его при создании шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-186">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="e2017-187">IP-адрес динамически назначается ресурсу при создании VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="e2017-187">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="e2017-188">В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e2017-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="e2017-189">Вы не можете запросить назначение статического общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e2017-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="e2017-190">Однако это не означает, что IP-адрес изменяется после назначения VPN-шлюзу.</span><span class="sxs-lookup"><span data-stu-id="e2017-190">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="e2017-191">Общедоступный IP-адрес изменяется только после удаления и повторного создания шлюза.</span><span class="sxs-lookup"><span data-stu-id="e2017-191">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="e2017-192">При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.</span><span class="sxs-lookup"><span data-stu-id="e2017-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="e2017-193">Запросите динамически назначенный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e2017-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="e2017-194"><a name="creategateway"></a>3. Создание VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="e2017-194"><a name="creategateway"></a>3. Create the VPN gateway</span></span>

<span data-ttu-id="e2017-195">Настройте и создайте шлюз для своей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-195">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="e2017-196">У параметра *-GatewayType* должно быть значение **Vpn**, а у параметра *-VpnType* — **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="e2017-196">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="e2017-197">Создание VPN-шлюза может занять до 45 минут в зависимости от выбранного [номера SKU шлюза](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="e2017-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="e2017-198"><a name="addresspool"></a>4. Добавление пула адресов VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-198"><a name="addresspool"></a>4. Add the VPN client address pool</span></span>

<span data-ttu-id="e2017-199">По завершении создания сетевого VPN-шлюза можно добавить пул адресов клиента VPN.</span><span class="sxs-lookup"><span data-stu-id="e2017-199">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="e2017-200">Пул адресов VPN-клиента представляет собой диапазон, из которого VPN-клиенты будут получать IP-адреса при подключении.</span><span class="sxs-lookup"><span data-stu-id="e2017-200">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="e2017-201">Используйте диапазон частных IP-адресов, который не пересекается с локальным расположением, из которого выполнено подключение, или с виртуальной сетью, к которой вы хотите подключиться.</span><span class="sxs-lookup"><span data-stu-id="e2017-201">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="e2017-202">В этом примере пул адресов VPN-клиента объявляется как [переменная](#declare) на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="e2017-202">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="e2017-203"><a name="Certificates"></a>5. Создайте сертификаты.</span><span class="sxs-lookup"><span data-stu-id="e2017-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="e2017-204">Сертификаты используются в Azure для проверки подлинности VPN-клиентов в VPN-подключениях типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="e2017-204">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="e2017-205">Необходимо отправить сведения об открытом ключе корневого сертификата в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-205">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="e2017-206">После этого открытый ключ считается доверенным.</span><span class="sxs-lookup"><span data-stu-id="e2017-206">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="e2017-207">Сертификаты клиентов должны создаваться из доверенного корневого сертификата, а затем устанавливаться на каждом клиентском компьютере в хранилище сертификатов Certificates-Current User/Personal.</span><span class="sxs-lookup"><span data-stu-id="e2017-207">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="e2017-208">Сертификат используется для проверки подлинности клиента, когда он инициирует подключение к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-208">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="e2017-209">Используемые самозаверяющие сертификаты должны быть созданы с помощью определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="e2017-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="e2017-210">Чтобы создать самозаверяющий сертификат, см. инструкции по [PowerShell и Windows 10](vpn-gateway-certificates-point-to-site.md). Если у вас нет Windows 10, вы можете использовать [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="e2017-210">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="e2017-211">Во время создания самозаверяющих корневых сертификатов и сертификатов клиента обязательно следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="e2017-211">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="e2017-212">В противном случае создаваемые сертификаты не будут совместимы с подключениями типа "точка — сеть", и вы получите сообщение об ошибке подключения.</span><span class="sxs-lookup"><span data-stu-id="e2017-212">Otherwise, the certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="e2017-213"><a name="cer"></a>1. Получение CER-файла для корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="e2017-213"><a name="cer"></a>1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="e2017-214"><a name="generate"></a>2. Создание сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="e2017-215"><a name="upload"></a>6. Отправка сведений об открытом ключе корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="e2017-215"><a name="upload"></a>6. Upload the root certificate public key information</span></span>

<span data-ttu-id="e2017-216">Убедитесь, что создание VPN-шлюза завершено.</span><span class="sxs-lookup"><span data-stu-id="e2017-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="e2017-217">После создания шлюза вы можете передать CER-файл (который содержит сведения об открытом ключе) для доверенного корневого сертификата в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-217">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="e2017-218">После отправки CER-файла Azure сможет использовать его для проверки подлинности клиентов, на которых установлен клиентский сертификат, созданный из доверенного корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="e2017-218">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="e2017-219">При необходимости позже можно отправить дополнительные файлы доверенных корневых сертификатов (не более 20).</span><span class="sxs-lookup"><span data-stu-id="e2017-219">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="e2017-220">Объявите переменную для имени сертификата, заменив существующее значение собственным.</span><span class="sxs-lookup"><span data-stu-id="e2017-220">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="e2017-221">Добавьте собственный путь к файлу, а затем выполните командлеты.</span><span class="sxs-lookup"><span data-stu-id="e2017-221">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="e2017-222">Отправьте сведения об открытом ключе в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-222">Upload the public key information to Azure.</span></span> <span data-ttu-id="e2017-223">После отправки сведений о сертификате Azure рассматривает его как доверенный корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e2017-223">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="e2017-224"><a name="clientconfig"></a>7. Скачивание пакета конфигурации VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-224"><a name="clientconfig"></a>7. Download the VPN client configuration package</span></span>

<span data-ttu-id="e2017-225">Чтобы подключиться к виртуальной сети, создав подключение типа "точка — сеть" через VPN-шлюз, каждому клиенту необходимо установить пакет конфигурации клиента, настраивающий собственный клиент VPN с помощью параметров и файлов, необходимых для подключения к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-225">To connect to a VNet using a Point-to-Site VPN, each client must install a client configuration package that configures the native VPN client with the settings and files that are necessary to connect to the virtual network.</span></span> <span data-ttu-id="e2017-226">Пакет конфигурации VPN-клиента настраивает собственный клиент Windows VPN и не устанавливает новые или другие клиенты VPN.</span><span class="sxs-lookup"><span data-stu-id="e2017-226">The VPN client configuration package configures the native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="e2017-227">На каждом клиентском компьютере можно использовать один и тот же пакет конфигурации VPN-клиента при условии, что его версия соответствует архитектуре клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-227">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="e2017-228">Список поддерживаемых клиентских операционных систем см. в разделе [Часто задаваемые вопросы о подключениях типа "точка — сеть"](#faq) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e2017-228">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="e2017-229">После создания шлюза можно создать и скачать пакет конфигурации клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-229">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="e2017-230">В этом примере будет скачан пакет для 64-разрядных клиентов.</span><span class="sxs-lookup"><span data-stu-id="e2017-230">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="e2017-231">Чтобы скачать 32-разрядный клиент, замените Amd64 на x86.</span><span class="sxs-lookup"><span data-stu-id="e2017-231">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="e2017-232">Пакет для VPN-клиента также можно скачать на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-232">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="e2017-233">Скопируйте и вставьте эту ссылку в веб-браузер (без кавычек), чтобы скачать пакет.</span><span class="sxs-lookup"><span data-stu-id="e2017-233">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the quotes surrounding the link.</span></span> 
3. <span data-ttu-id="e2017-234">Скачайте и установите пакет на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="e2017-234">Download and install the package on the client computer.</span></span> <span data-ttu-id="e2017-235">При появлении всплывающего окна SmartScreen щелкните **Дополнительно**, а затем выберите **Выполнить в любом случае**.</span><span class="sxs-lookup"><span data-stu-id="e2017-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="e2017-236">Вы также можете сохранить пакет для установки на других клиентских компьютерах.</span><span class="sxs-lookup"><span data-stu-id="e2017-236">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="e2017-237">На клиентском компьютере перейдите в раздел **Параметры сети** и щелкните **VPN**.</span><span class="sxs-lookup"><span data-stu-id="e2017-237">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="e2017-238">Для VPN-подключения отображается имя виртуальной сети, к которой оно устанавливается.</span><span class="sxs-lookup"><span data-stu-id="e2017-238">The VPN connection shows the name of the virtual network that it connects to.</span></span>

## <span data-ttu-id="e2017-239"><a name="clientcertificate"></a>8. Установка экспортированного сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="e2017-240">Если вы хотите создать подключение типа "точка — сеть" на клиентском компьютере, отличном от того, который использовался для создания сертификатов клиентов, необходимо установить сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-240">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="e2017-241">При установке сертификата клиента потребуется пароль, созданный при экспорте сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-241">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="e2017-242">Обычно для этого нужно просто дважды щелкнуть сертификат и установить его.</span><span class="sxs-lookup"><span data-stu-id="e2017-242">Typically, it is just a matter of double-clicking the certificate and installing it.</span></span>

<span data-ttu-id="e2017-243">Убедитесь, что сертификат клиента был экспортирован как PFX-файл вместе со всей цепочкой сертификатов (это значение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="e2017-243">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="e2017-244">В противном случае данные корневого сертификата будут отсутствовать на клиентском компьютере и клиент не сможет пройти проверку должным образом.</span><span class="sxs-lookup"><span data-stu-id="e2017-244">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> <span data-ttu-id="e2017-245">Дополнительные сведения см. в разделе [Установка экспортированного сертификата клиента](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="e2017-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="e2017-246"><a name="connect"></a>9. Подключение к Azure</span><span class="sxs-lookup"><span data-stu-id="e2017-246"><a name="connect"></a>9. Connect to Azure</span></span>

1. <span data-ttu-id="e2017-247">Чтобы подключиться к виртуальной сети, откройте VPN-подключения на клиентском компьютере и найдите созданное VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="e2017-247">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="e2017-248">Его имя совпадает с названием вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-248">It is named the same name as your virtual network.</span></span> <span data-ttu-id="e2017-249">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e2017-249">Click **Connect**.</span></span> <span data-ttu-id="e2017-250">Может появиться всплывающее сообщение об использовании сертификата.</span><span class="sxs-lookup"><span data-stu-id="e2017-250">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="e2017-251">В таком случае щелкните **Продолжить**, чтобы использовать более высокий уровень привилегий.</span><span class="sxs-lookup"><span data-stu-id="e2017-251">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="e2017-252">На странице состояния **подключения** щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="e2017-252">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="e2017-253">Если появится окно **Выбор сертификата**, убедитесь в том, что отображается сертификат клиента, с помощью которого вы хотите подключиться к сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-253">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="e2017-254">Если окно не появится, выберите нужный сертификат в раскрывающемся списке и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e2017-254">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![Подключение VPN-клиента к Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="e2017-256">Теперь подключение установлено.</span><span class="sxs-lookup"><span data-stu-id="e2017-256">Your connection is established.</span></span>

  ![Подключение установлено](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="e2017-258">Устранение неполадок подключения P2S</span><span class="sxs-lookup"><span data-stu-id="e2017-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="e2017-259"><a name="verify"></a>10. Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="e2017-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="e2017-260">Чтобы проверить, активно ли VPN-подключение, откройте окно командной строки от имени администратора и выполните команду *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="e2017-260">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="e2017-261">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="e2017-261">View the results.</span></span> <span data-ttu-id="e2017-262">Обратите внимание, что полученный вами IP-адрес — это один из адресов в пуле адресов VPN-клиента подключения "точка–cеть", указанном в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2017-262">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="e2017-263">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="e2017-263">The results are similar to this example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="e2017-264"><a name="connectVM"></a>Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="e2017-264"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="e2017-265"><a name="addremovecert"></a>Добавление и удаление корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="e2017-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="e2017-266">Вы можете добавлять доверенные корневые сертификаты в Azure, а также удалять их из Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="e2017-267">При удалении корневого сертификата клиенты, использующие цифровой сертификат, созданный из этого корневого сертификата, не смогут пройти проверку подлинности и поэтому не смогут подключиться.</span><span class="sxs-lookup"><span data-stu-id="e2017-267">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="e2017-268">Чтобы клиенты могли проходить аутентификацию и подключаться, необходимо установить новый сертификат клиента, созданный на основе корневого сертификата, который является доверенным для Azure (то есть он передан в Azure).</span><span class="sxs-lookup"><span data-stu-id="e2017-268">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="e2017-269"><a name="addtrustedroot"></a>Добавление доверенного корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="e2017-269"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="e2017-270">В Azure можно добавить до 20 CER-файлов корневых сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e2017-270">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="e2017-271">Ниже описано, как добавить корневой сертификат:</span><span class="sxs-lookup"><span data-stu-id="e2017-271">The following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="e2017-272"><a name="certmethod1"></a>Метод 1</span><span class="sxs-lookup"><span data-stu-id="e2017-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="e2017-273">Это наиболее эффективный способ отправить корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e2017-273">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="e2017-274">Подготовьте CER-файл для отправки:</span><span class="sxs-lookup"><span data-stu-id="e2017-274">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="e2017-275">Отправьте файл.</span><span class="sxs-lookup"><span data-stu-id="e2017-275">Upload the file.</span></span> <span data-ttu-id="e2017-276">Вы можете отправить только один файл за раз.</span><span class="sxs-lookup"><span data-stu-id="e2017-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="e2017-277">Убедитесь, что файл сертификата загружен:</span><span class="sxs-lookup"><span data-stu-id="e2017-277">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="e2017-278"><a name="certmethod2"></a>Метод 2</span><span class="sxs-lookup"><span data-stu-id="e2017-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="e2017-279">Этот метод имеет больше шагов, чем метод 1, но результат тот же.</span><span class="sxs-lookup"><span data-stu-id="e2017-279">This method is has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="e2017-280">Он включен при необходимости просмотра данных сертификата.</span><span class="sxs-lookup"><span data-stu-id="e2017-280">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="e2017-281">Создайте корневой сертификат и подготовьте его к добавлению в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2017-281">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="e2017-282">Экспортируйте открытый ключ как CER-файл X.509 в кодировке Base-64 и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="e2017-282">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="e2017-283">Скопируйте значения, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e2017-283">Copy the values, as shown in the following example:</span></span>

  ![на основе сертификата.](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="e2017-285">При копировании данных сертификата обязательно скопируйте текст как одну непрерывную строку без символов возврата каретки и перевода строки.</span><span class="sxs-lookup"><span data-stu-id="e2017-285">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="e2017-286">Может потребоваться изменить параметры представления в текстовом редакторе, чтобы показать символы или показать все знаки и просмотреть символы возврата каретки и перевода строки.</span><span class="sxs-lookup"><span data-stu-id="e2017-286">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="e2017-287">Укажите имя сертификата и сведения о ключе как значения переменных.</span><span class="sxs-lookup"><span data-stu-id="e2017-287">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="e2017-288">Подставьте собственные значения, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e2017-288">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="e2017-289">Добавьте новый корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e2017-289">Add the new root certificate.</span></span> <span data-ttu-id="e2017-290">Можно добавлять только один сертификат за раз.</span><span class="sxs-lookup"><span data-stu-id="e2017-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="e2017-291">Чтобы проверить, добавлен ли новый сертификат должным образом, воспользуйтесь приведенным ниже примером.</span><span class="sxs-lookup"><span data-stu-id="e2017-291">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="e2017-292"><a name="removerootcert"></a>Удалите корневой сертификат</span><span class="sxs-lookup"><span data-stu-id="e2017-292"><a name="removerootcert"></a>To remove a root certificate</span></span>

1. <span data-ttu-id="e2017-293">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="e2017-293">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="e2017-294">Удалите сертификат.</span><span class="sxs-lookup"><span data-stu-id="e2017-294">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="e2017-295">Используйте приведенный ниже пример, чтобы убедиться, что сертификат успешно удален.</span><span class="sxs-lookup"><span data-stu-id="e2017-295">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="e2017-296"><a name="revoke"></a>Отзыв сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="e2017-297">Можно отозвать сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-297">You can revoke client certificates.</span></span> <span data-ttu-id="e2017-298">Список отзыва сертификатов позволяет выборочно запрещать подключение типа "точка-сеть" на основе отдельных сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-298">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="e2017-299">Эта процедура отличается от удаления доверенного корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="e2017-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="e2017-300">При удалении доверенного корневого сертификата (CER-файл) из Azure будет запрещен доступ для всех сертификатов клиента, созданных на основе отозванного корневого сертификата или подписанных им.</span><span class="sxs-lookup"><span data-stu-id="e2017-300">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="e2017-301">Отзыв сертификата клиента, а не корневого сертификата, позволяет по-прежнему использовать другие сертификаты, созданные на основе корневого сертификата, для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e2017-301">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="e2017-302">Обычно корневой сертификат используется для управления доступом на уровнях группы или организации, а отозванный сертификат клиента — для точного контроля доступа для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e2017-302">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="e2017-303"><a name="revokeclientcert"></a>Отзыв сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-303"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

1. <span data-ttu-id="e2017-304">Получите отпечаток сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-304">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="e2017-305">Дополнительные сведения см. в статье [Практическое руководство. Извлечение отпечатка сертификата](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2017-305">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="e2017-306">Скопируйте данные в текстовый редактор и удалите все пробелы, чтобы предоставить отпечаток в виде непрерывной строки.</span><span class="sxs-lookup"><span data-stu-id="e2017-306">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="e2017-307">Далее эта строка будет объявлена в качестве переменной.</span><span class="sxs-lookup"><span data-stu-id="e2017-307">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="e2017-308">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="e2017-308">Declare the variables.</span></span> <span data-ttu-id="e2017-309">Обязательно объявите отпечаток, полученный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="e2017-309">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="e2017-310">Добавьте отпечаток в список отозванных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e2017-310">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="e2017-311">После добавления отпечатка отобразится Succeeded.</span><span class="sxs-lookup"><span data-stu-id="e2017-311">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="e2017-312">Убедитесь, что отпечаток добавлен в список отзыва сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e2017-312">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="e2017-313">Теперь сертификат нельзя использовать для подключения.</span><span class="sxs-lookup"><span data-stu-id="e2017-313">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="e2017-314">Клиенты, пытающиеся подключиться с помощью этого сертификата, получат сообщение, что он недействителен.</span><span class="sxs-lookup"><span data-stu-id="e2017-314">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <span data-ttu-id="e2017-315"><a name="reinstateclientcert"></a>Возобновление сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="e2017-315"><a name="reinstateclientcert"></a>To reinstate a client certificate</span></span>

<span data-ttu-id="e2017-316">Можно возобновить использование сертификата клиента, удалив отпечаток из списка отозванных сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="e2017-316">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="e2017-317">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="e2017-317">Declare the variables.</span></span> <span data-ttu-id="e2017-318">Обязательно объявите правильный отпечаток сертификата, который требуется возобновить.</span><span class="sxs-lookup"><span data-stu-id="e2017-318">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="e2017-319">Удалите отпечаток сертификата из списка отзыва сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e2017-319">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="e2017-320">Проверьте, удален ли отпечаток из списка отозванных отпечатков.</span><span class="sxs-lookup"><span data-stu-id="e2017-320">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="e2017-321"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="e2017-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e2017-322">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2017-322">Next steps</span></span>
<span data-ttu-id="e2017-323">Установив подключение, можно добавить виртуальные машины в виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="e2017-323">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="e2017-324">Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="e2017-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="e2017-325">Дополнительные сведения о сетях и виртуальных машинах см. в статье [Azure и Linux: обзор сетей виртуальных машин](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2017-325">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>