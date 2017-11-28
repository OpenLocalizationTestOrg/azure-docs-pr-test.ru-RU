---
title: "Подключение компьютера tooan виртуальной сети Azure, с помощью точки сайтами и сертификат проверки подлинности: PowerShell | Документы Microsoft"
description: "Безопасное подключение виртуальной сети компьютера tooyour путем создания подключения шлюза VPN точки сайтами с использованием проверки подлинности сертификата. В этой статье относится модели развертывания диспетчера ресурсов toohello и использует PowerShell."
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
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="6c06e-104">Настройка tooa подключение точка-сайт виртуальной сети с использованием проверки подлинности сертификата: PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c06e-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="6c06e-105">В этой статье показано, как toocreate виртуальную сеть с подключением точки сайтами в развертывании диспетчера ресурсов hello модели с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c06e-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="6c06e-106">В этой конфигурации используется hello tooauthenticate сертификаты подключения клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="6c06e-107">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="6c06e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c06e-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6c06e-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="6c06e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c06e-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="6c06e-110">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="6c06e-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="6c06e-111">Шлюз VPN точки сайтами (P2S) позволяет создавать tooyour безопасное подключение виртуальной сети из отдельных клиентских компьютерах.</span><span class="sxs-lookup"><span data-stu-id="6c06e-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="6c06e-112">Точка-сеть VPN-подключений полезны в тех случаях, когда требуется tooconnect tooyour виртуальной сети из удаленного расположения, например, при путем дистанционного доступа из дома или конференц-связи.</span><span class="sxs-lookup"><span data-stu-id="6c06e-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="6c06e-113">P2S VPN также является решение toouse вместо VPN сайтами, при наличии только несколько клиентов, которым требуется tooconnect tooa виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="6c06e-114">Использует P2S hello Secure Socket туннелирование протокола (SSTP), протокол VPN на основе SSL.</span><span class="sxs-lookup"><span data-stu-id="6c06e-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="6c06e-115">P2S VPN-подключения, запустите его из hello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="6c06e-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Подключение компьютера tooan виртуальной сети Azure - схема соединений точка-сеть](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="6c06e-117">Сертификат точки сайтами проверки подлинности подключений требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6c06e-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="6c06e-118">VPN-шлюз с маршрутизацией на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="6c06e-119">Hello открытый ключ (CER-файл) для корневого сертификата, являющегося отправленного tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="6c06e-120">После передачи сертификата hello, он считается доверенных сертификатов и используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6c06e-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="6c06e-121">Сертификат клиента, который создается из корневого сертификата hello и установлена на каждом клиентском компьютере, к которому будут подключаться toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="6c06e-122">Этот сертификат используется для проверки подлинности клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="6c06e-123">Пакет конфигурации VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-123">A VPN client configuration package.</span></span> <span data-ttu-id="6c06e-124">пакет конфигурации VPN-клиента Hello содержит hello сведения, необходимые для hello клиента tooconnect toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="6c06e-125">пакет Hello настраивает hello существующего VPN-клиента, имеет собственный toohello операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="6c06e-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="6c06e-126">Каждый клиент, который подключается должен быть настроен с использованием hello конфигурации пакета.</span><span class="sxs-lookup"><span data-stu-id="6c06e-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="6c06e-127">Для подключения типа "точка — сеть" не требуется VPN-устройство или локальный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6c06e-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="6c06e-128">Hello VPN-подключения создается на основе SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="6c06e-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="6c06e-129">На серверной стороне hello мы поддерживаем SSTP версии 1.0, 1.1 и 1.2.</span><span class="sxs-lookup"><span data-stu-id="6c06e-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="6c06e-130">Hello клиент решает, какие версии toouse.</span><span class="sxs-lookup"><span data-stu-id="6c06e-130">hello client decides which version toouse.</span></span> <span data-ttu-id="6c06e-131">Для Windows 8.1 и более поздних версий по умолчанию используется SSTP версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="6c06e-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="6c06e-132">Дополнительные сведения о подключениях точки сайтами см. в разделе hello [точки сайтами часто задаваемые вопросы о](#faq) в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6c06e-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="6c06e-133">Подготовка</span><span class="sxs-lookup"><span data-stu-id="6c06e-133">Before beginning</span></span>

* <span data-ttu-id="6c06e-134">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="6c06e-135">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="6c06e-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="6c06e-136">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6c06e-137">Дополнительные сведения об установке командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c06e-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="6c06e-138"><a name="example"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="6c06e-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="6c06e-139">Можно использовать toocreate значения пример hello тестовой среде, или ссылаться значения toothese toobetter понять hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6c06e-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="6c06e-140">Мы устанавливаем hello переменные в разделе [1](#declare) hello статьи.</span><span class="sxs-lookup"><span data-stu-id="6c06e-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="6c06e-141">Можно использовать шаги hello как пошаговое руководство и использовать hello значения, не изменяя их или изменить их tooreflect вашей среде.</span><span class="sxs-lookup"><span data-stu-id="6c06e-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="6c06e-142">**Имя: VNet1**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-142">**Name: VNet1**</span></span>
* <span data-ttu-id="6c06e-143">**Адресное пространство: 192.168.0.0/16** и **10.254.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="6c06e-144">В этом примере мы используем несколько tooillustrate пространства адресов, такая конфигурация работает с несколько адресных пространств.</span><span class="sxs-lookup"><span data-stu-id="6c06e-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="6c06e-145">Однако это необязательно для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c06e-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="6c06e-146">**Имя подсети: FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="6c06e-147">**Диапазон адресов подсети: 192.168.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="6c06e-148">**Имя подсети: BackEnd.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="6c06e-149">**Диапазон адресов подсети: 10.254.1.0/24.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="6c06e-150">**Имя подсети: GatewaySubnet.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="6c06e-151">Имя подсети Hello *GatewaySubnet* является обязательным для toowork шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="6c06e-152">**Диапазон адресов подсети шлюза: 192.168.200.0/24.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="6c06e-153">**Пул адресов VPN-клиента: 172.16.201.0/24.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="6c06e-154">VPN-клиенты, подключающиеся toohello виртуальной сети с помощью этого соединения точка-сеть получать IP-адрес из пула адресов VPN-клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="6c06e-155">**Подписки:** при наличии более чем одной подписке, убедитесь, что вы используете hello правильный выбор.</span><span class="sxs-lookup"><span data-stu-id="6c06e-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="6c06e-156">**Группа ресурсов: TestRG**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="6c06e-157">**Расположение: восточная часть США**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-157">**Location: East US**</span></span>
* <span data-ttu-id="6c06e-158">**DNS-сервера: IP-адрес** hello DNS-сервера требуется toouse для разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="6c06e-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="6c06e-159">**Имя шлюза: Vnet1GW**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="6c06e-160">**Имя общедоступного IP-адреса: VNet1GWPIP**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="6c06e-161">**Тип VPN: RouteBased.**</span><span class="sxs-lookup"><span data-stu-id="6c06e-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="6c06e-162"><a name="declare"></a>1. Вход и настройка переменных</span><span class="sxs-lookup"><span data-stu-id="6c06e-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="6c06e-163">В этом разделе вход и объявления hello значения, используемые для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c06e-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="6c06e-164">Привет, объявленные значения используются в скриптах образец hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="6c06e-165">Измените значения tooreflect hello собственной среде.</span><span class="sxs-lookup"><span data-stu-id="6c06e-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="6c06e-166">Также можно использовать значения объявлены hello и проходят этапы hello в качестве упражнения.</span><span class="sxs-lookup"><span data-stu-id="6c06e-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="6c06e-167">Откройте консоль PowerShell с повышенными привилегиями и выполните вход в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="6c06e-168">Этот командлет запросит учетные данные входа hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="6c06e-169">После входа в систему, он загружает параметры учетной записи, чтобы они были доступны tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c06e-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="6c06e-170">Получите список подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="6c06e-171">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="6c06e-172">Объявления переменных hello, которое следует toouse.</span><span class="sxs-lookup"><span data-stu-id="6c06e-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="6c06e-173">Здравствуйте, используйте следующий пример, заменив значения hello лично, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="6c06e-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

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

## <span data-ttu-id="6c06e-174"><a name="ConfigureVNet"></a>2. Настройка шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="6c06e-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="6c06e-175">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="6c06e-176">Создайте hello конфигурации подсети виртуальной сети hello, именование их *переднего плана*, *серверной*, и *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="6c06e-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="6c06e-177">Эти префиксы должна входить в адресное пространство виртуальной сети, объявленного hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="6c06e-178">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-178">Create hello virtual network.</span></span>

  <span data-ttu-id="6c06e-179">В этом примере hello DNS-сервер является необязательным.</span><span class="sxs-lookup"><span data-stu-id="6c06e-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="6c06e-180">Если указать значение, DNS-сервер не создается.</span><span class="sxs-lookup"><span data-stu-id="6c06e-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="6c06e-181">Hello IP-адрес сервера DNS, указываемое должен быть DNS-сервера, которые позволяют устранить hello имен для ресурсов hello, которому вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="6c06e-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="6c06e-182">В этом примере мы использовали частный IP-адрес, но скорее всего, что это не hello IP-адрес DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6c06e-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="6c06e-183">Быть убедиться, что toouse собственные значения.</span><span class="sxs-lookup"><span data-stu-id="6c06e-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="6c06e-184">Укажите переменные hello для hello виртуальной сети, которую вы создали.</span><span class="sxs-lookup"><span data-stu-id="6c06e-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="6c06e-185">VPN-шлюз должен иметь общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6c06e-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="6c06e-186">Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="6c06e-187">Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="6c06e-188">В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="6c06e-189">Вы не можете запросить назначение статического общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="6c06e-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="6c06e-190">Однако это не значит, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="6c06e-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="6c06e-191">только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново.</span><span class="sxs-lookup"><span data-stu-id="6c06e-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="6c06e-192">При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.</span><span class="sxs-lookup"><span data-stu-id="6c06e-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="6c06e-193">Запросите динамически назначенный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6c06e-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="6c06e-194"><a name="creategateway"></a>3. Создание шлюза VPN hello</span><span class="sxs-lookup"><span data-stu-id="6c06e-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="6c06e-195">Настройте и создайте hello шлюз виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="6c06e-196">Hello *- тип шлюза* должно быть **Vpn** и hello *- VpnType* должно быть **routebased**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="6c06e-197">VPN-шлюза может занять toocomplete too45 минут, в зависимости от hello [номер sku шлюза](vpn-gateway-about-vpn-gateway-settings.md) выбора.</span><span class="sxs-lookup"><span data-stu-id="6c06e-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="6c06e-198"><a name="addresspool"></a>4. Добавление пула адресов клиента VPN hello</span><span class="sxs-lookup"><span data-stu-id="6c06e-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="6c06e-199">По завершении создания hello VPN-шлюз можно добавить пул адресов клиента VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="6c06e-200">Hello пула адресов VPN-клиента — диапазон hello, из которого hello VPN-клиентам получать IP-адрес при подключении.</span><span class="sxs-lookup"><span data-stu-id="6c06e-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="6c06e-201">Используйте диапазон частных IP-адресов, не перекрывающийся с hello в локальное расположение, подключение из, или виртуальной сети, требуется tooconnect для hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="6c06e-202">В этом примере объявляется hello пула адресов VPN-клиента, как [переменной](#declare) на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="6c06e-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="6c06e-203"><a name="Certificates"></a>5. Создайте сертификаты.</span><span class="sxs-lookup"><span data-stu-id="6c06e-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="6c06e-204">Сертификаты используются VPN-клиентами Azure tooauthenticate точка-сеть виртуальных частных сетей.</span><span class="sxs-lookup"><span data-stu-id="6c06e-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="6c06e-205">Необходимо отправить hello сведения об открытом ключе для hello корневого сертификата tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="6c06e-206">рассматривается как «доверять» Hello открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="6c06e-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="6c06e-207">Клиентские сертификаты необходимо сгенерированных hello доверенный корневой сертификат, а затем устанавливается на каждом клиентском компьютере, в хранилище сертификатов Сертификаты-текущий пользователь/персональные hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="6c06e-208">сертификат Hello при используется tooauthenticate hello клиент инициирует соединение toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="6c06e-209">Используемые самозаверяющие сертификаты должны быть созданы с помощью определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="6c06e-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="6c06e-210">Можно создать самозаверяющий сертификат, с помощью инструкции hello [PowerShell и Windows 10](vpn-gateway-certificates-point-to-site.md), или, если у вас нет Windows 10, можно использовать [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="6c06e-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="6c06e-211">Очень важно следовать hello действия в инструкциях hello при создании самозаверяющие корневые сертификаты и сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="6c06e-212">В противном случае hello сертификаты, создаваемые будет несовместим с подключениями P2S и возникнет ошибка соединения.</span><span class="sxs-lookup"><span data-stu-id="6c06e-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="6c06e-213"><a name="cer"></a>1. Получить hello CER-файл для корневого сертификата hello</span><span class="sxs-lookup"><span data-stu-id="6c06e-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="6c06e-214"><a name="generate"></a>2. Создание сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="6c06e-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="6c06e-215"><a name="upload"></a>6. Отправка hello корневого сертификата сведений открытого ключа</span><span class="sxs-lookup"><span data-stu-id="6c06e-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="6c06e-216">Убедитесь, что создание VPN-шлюза завершено.</span><span class="sxs-lookup"><span data-stu-id="6c06e-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="6c06e-217">После ее завершения, можно загрузить hello CER-файл (который содержит сведения об открытом ключе hello) для tooAzure доверенного корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="6c06e-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="6c06e-218">После загрузки файла a.cer Azure можно использовать tooauthenticate клиенты, на которых установлен сертификат клиента, созданные из hello доверенный корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c06e-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="6c06e-219">При необходимости можно передать файлы сертификатов доверенных корневых - копирование всего tooa 20 – более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="6c06e-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="6c06e-220">Объявите переменную hello для имени сертификата, заменив значение hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="6c06e-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="6c06e-221">Замените собственными hello путь к файлу, а затем запустите командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="6c06e-222">Отправьте сведения об открытом ключе tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="6c06e-223">После загрузки сведений о сертификате hello Azure считает, что это toobe с доверенным корневым сертификатом.</span><span class="sxs-lookup"><span data-stu-id="6c06e-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="6c06e-224"><a name="clientconfig"></a>7. Загрузите пакет конфигурации VPN-клиента hello</span><span class="sxs-lookup"><span data-stu-id="6c06e-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="6c06e-225">tooa tooconnect виртуальной сети с помощью VPN-Подключение точка-сеть, каждому клиенту необходимо установить пакет конфигурации клиента, который настраивает hello собственного клиента VPN с использованием параметров hello и файлы, необходимые tooconnect toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="6c06e-226">пакет конфигурации VPN-клиента Hello настраивает клиент Windows VPN hello, не устанавливает новые или другие VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="6c06e-227">Можно использовать hello пакета же Настройка VPN-клиента на каждом клиентском компьютере, при условии, что версия hello соответствует hello архитектуры для клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="6c06e-228">Hello список клиентских операционных систем, поддерживаемых см hello [точки сайтами соединения часто задаваемые вопросы о](#faq) в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6c06e-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="6c06e-229">После создания шлюза hello можно создать и загрузить пакет конфигурации клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="6c06e-230">В этом примере загружает hello пакет для 64-разрядных клиентах.</span><span class="sxs-lookup"><span data-stu-id="6c06e-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="6c06e-231">Если требуется 32-разрядного клиента toodownload hello, «Amd64» замените «x86".</span><span class="sxs-lookup"><span data-stu-id="6c06e-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="6c06e-232">Можно также загрузить hello VPN-клиента с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="6c06e-233">Скопируйте и вставьте ссылку hello, возвращается tooa веб-браузера toodownload hello пакета, позаботится tooremove hello кавычки вокруг hello ссылку.</span><span class="sxs-lookup"><span data-stu-id="6c06e-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="6c06e-234">Загрузить и установить на клиентском компьютере hello hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="6c06e-235">При появлении всплывающего окна SmartScreen щелкните **Дополнительно**, а затем выберите **Выполнить в любом случае**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="6c06e-236">Можно также сохранить пакет tooinstall hello на других клиентских компьютерах.</span><span class="sxs-lookup"><span data-stu-id="6c06e-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="6c06e-237">На клиентском компьютере hello перейдите слишком**параметры сети** и нажмите кнопку **VPN**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="6c06e-238">Hello VPN-подключение отображается hello hello виртуальной сети, он подключается.</span><span class="sxs-lookup"><span data-stu-id="6c06e-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="6c06e-239"><a name="clientcertificate"></a>8. Установка экспортированного сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="6c06e-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="6c06e-240">Подключение toocreate P2S на клиентском компьютере, отличном от hello один использовалась toogenerate hello клиентские сертификаты, необходимые tooinstall сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="6c06e-241">При установке сертификата клиента, необходимо hello пароль, созданный при экспорте сертификата клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="6c06e-242">Как правило это лишь дважды щелкнув сертификат hello и его установки.</span><span class="sxs-lookup"><span data-stu-id="6c06e-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="6c06e-243">Убедитесь, что сертификат клиента hello был экспортирован как PFX-файла вместе с hello всей цепочки сертификатов (он по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="6c06e-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="6c06e-244">В противном случае сведения о сертификате корневого hello отсутствует на клиентском компьютере hello и hello клиента не будет возможности tooauthenticate должным образом.</span><span class="sxs-lookup"><span data-stu-id="6c06e-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="6c06e-245">Дополнительные сведения см. в разделе [Установка экспортированного сертификата клиента](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="6c06e-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="6c06e-246"><a name="connect"></a>9. Подключение tooAzure</span><span class="sxs-lookup"><span data-stu-id="6c06e-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="6c06e-247">tooyour tooconnect виртуальной сети, на клиентском компьютере hello, перейдите tooVPN соединения и найдите созданное подключение VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="6c06e-248">Он называется hello точно такое же имя вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6c06e-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="6c06e-249">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-249">Click **Connect**.</span></span> <span data-ttu-id="6c06e-250">Появится всплывающее сообщение может оказаться, что означает toousing hello сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c06e-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="6c06e-251">Нажмите кнопку **Продолжить** toouse с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="6c06e-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="6c06e-252">На hello **подключения** страница «состояние», нажмите кнопку **Connect** toostart hello соединения.</span><span class="sxs-lookup"><span data-stu-id="6c06e-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="6c06e-253">Если вы видите **Выбор сертификата** экране, убедитесь, что hello отображается именно сертификат клиента hello один нужных toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6c06e-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="6c06e-254">Если это не так, используйте правильный сертификат hello tooselect hello стрелку раскрывающегося списка и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6c06e-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN-клиент подключается tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="6c06e-256">Теперь подключение установлено.</span><span class="sxs-lookup"><span data-stu-id="6c06e-256">Your connection is established.</span></span>

  ![Подключение установлено](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="6c06e-258">Устранение неполадок подключения P2S</span><span class="sxs-lookup"><span data-stu-id="6c06e-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="6c06e-259"><a name="verify"></a>10. Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="6c06e-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="6c06e-260">tooverify, что VPN-подключение активно, откройте командную строку с повышенными привилегиями и выполните *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="6c06e-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="6c06e-261">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-261">View hello results.</span></span> <span data-ttu-id="6c06e-262">Обратите внимание, что hello IP-адрес, который вы получили одно hello адресов в пул адресов клиента VPN hello точки сайтами, указанное в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c06e-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="6c06e-263">результаты Hello, аналогичный пример toothis:</span><span class="sxs-lookup"><span data-stu-id="6c06e-263">hello results are similar toothis example:</span></span>

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

## <span data-ttu-id="6c06e-264"><a name="connectVM"></a>Подключение tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6c06e-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="6c06e-265"><a name="addremovecert"></a>Добавление и удаление корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="6c06e-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="6c06e-266">Вы можете добавлять доверенные корневые сертификаты в Azure, а также удалять их из Azure.</span><span class="sxs-lookup"><span data-stu-id="6c06e-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="6c06e-267">При удалении корневого сертификата, клиенты, имеющие сертификат, сформированный из hello корневой сертификат не может проверить подлинность и не будет возможности tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6c06e-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="6c06e-268">Tooauthenticate клиента и подключения, необходимо tooinstall нового сертификата клиента, созданный из корневой сертификат, является доверенным tooAzure (переданный).</span><span class="sxs-lookup"><span data-stu-id="6c06e-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="6c06e-269"><a name="addtrustedroot"></a>tooadd доверенный корневой сертификат</span><span class="sxs-lookup"><span data-stu-id="6c06e-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="6c06e-270">Добавляются файлы .cer tooAzure для too20 корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="6c06e-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="6c06e-271">Hello описанных ниже действий можно добавить корневой сертификат:</span><span class="sxs-lookup"><span data-stu-id="6c06e-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="6c06e-272"><a name="certmethod1"></a>Метод 1</span><span class="sxs-lookup"><span data-stu-id="6c06e-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="6c06e-273">Это hello наиболее эффективный метод tooupload корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c06e-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="6c06e-274">Подготовка tooupload файл .cer hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="6c06e-275">Отправьте файл hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-275">Upload hello file.</span></span> <span data-ttu-id="6c06e-276">Вы можете отправить только один файл за раз.</span><span class="sxs-lookup"><span data-stu-id="6c06e-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="6c06e-277">загрузить этот файл сертификата hello tooverify:</span><span class="sxs-lookup"><span data-stu-id="6c06e-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="6c06e-278"><a name="certmethod2"></a>Метод 2</span><span class="sxs-lookup"><span data-stu-id="6c06e-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="6c06e-279">Этот метод имеет несколько шагов, чем метод 1, но есть hello того же результата.</span><span class="sxs-lookup"><span data-stu-id="6c06e-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="6c06e-280">Он включен, при необходимости данные сертификата tooview hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="6c06e-281">Создание и подготовка hello tooAzure tooadd на новый корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c06e-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="6c06e-282">Экспорт открытого ключа hello как Base64-кодировке X.509 (. (CER) и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="6c06e-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="6c06e-283">Скопируйте значения hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="6c06e-283">Copy hello values, as shown in hello following example:</span></span>

  ![на основе сертификата.](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="6c06e-285">При копировании данных сертификата hello, сделать, необходимо скопировать текст hello в виде одной непрерывной строки без возврата каретки и перевода строки.</span><span class="sxs-lookup"><span data-stu-id="6c06e-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="6c06e-286">Может потребоваться toomodify представления на too'Show редактор текста hello символа/Показать возвращает все символы toosee hello каретки и перевода строки.</span><span class="sxs-lookup"><span data-stu-id="6c06e-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="6c06e-287">Укажите имя сертификата hello и сведения о ключе как переменная.</span><span class="sxs-lookup"><span data-stu-id="6c06e-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="6c06e-288">Замените сведения hello собственный, как показано в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6c06e-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="6c06e-289">Добавьте новый корневой сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-289">Add hello new root certificate.</span></span> <span data-ttu-id="6c06e-290">Можно добавлять только один сертификат за раз.</span><span class="sxs-lookup"><span data-stu-id="6c06e-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="6c06e-291">Можно проверить, что новый сертификат hello был правильно добавлен, используя следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="6c06e-292"><a name="removerootcert"></a>tooremove корневой сертификат</span><span class="sxs-lookup"><span data-stu-id="6c06e-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="6c06e-293">Объявления переменных hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="6c06e-294">Удалите сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="6c06e-295">Hello используйте следующий пример tooverify, hello сертификат был успешно удален.</span><span class="sxs-lookup"><span data-stu-id="6c06e-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="6c06e-296"><a name="revoke"></a>Отзыв сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="6c06e-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="6c06e-297">Можно отозвать сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="6c06e-297">You can revoke client certificates.</span></span> <span data-ttu-id="6c06e-298">список отзыва позволяет tooselectively сертификатов Hello запрещать подключение точка-сеть на основе отдельных клиентских сертификатов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="6c06e-299">Эта процедура отличается от удаления доверенного корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="6c06e-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="6c06e-300">При удалении .cer доверенного корневого сертификата из Azure, он отменяет hello доступ для всех клиентских сертификатов создан и подписан сертификатом корневого отозванных hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="6c06e-301">Отзыва сертификата клиента, а не hello корневого сертификата, позволяет hello другие сертификаты, которые были созданы из hello toobe на toocontinue корневой сертификат для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6c06e-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="6c06e-302">Hello распространенной практикой является toouse hello корневой сертификат toomanage доступа на уровнях команда или организация, при использовании отозванных сертификатов клиентов для детальное управление доступом для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="6c06e-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="6c06e-303"><a name="revokeclientcert"></a>toorevoke сертификат клиента</span><span class="sxs-lookup"><span data-stu-id="6c06e-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="6c06e-304">Получить отпечаток сертификата клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="6c06e-305">Дополнительные сведения см. в разделе [как tooretrieve hello отпечаток сертификата](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c06e-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="6c06e-306">Скопируйте hello сведения tooa текстовом редакторе и удалите все пробелы, чтобы оно было непрерывной строки.</span><span class="sxs-lookup"><span data-stu-id="6c06e-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="6c06e-307">Эта строка объявляется как переменная приветствия при следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="6c06e-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="6c06e-308">Объявления переменных hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-308">Declare hello variables.</span></span> <span data-ttu-id="6c06e-309">Убедитесь, что отпечаток hello toodeclare, полученным в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="6c06e-310">Добавьте hello отпечаток toohello список отозванных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="6c06e-311">Вы видите «Succeeded» при добавлении отпечаток hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="6c06e-312">Проверьте, что отпечаток hello Добавление toohello список отзыва сертификатов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="6c06e-313">После добавления hello отпечаток сертификата hello больше не может быть используется tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6c06e-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="6c06e-314">Клиенты, пытающиеся tooconnect, с помощью этого сертификата сообщение о том, что этот сертификат hello больше не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="6c06e-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="6c06e-315"><a name="reinstateclientcert"></a>tooreinstate сертификат клиента</span><span class="sxs-lookup"><span data-stu-id="6c06e-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="6c06e-316">Ее можно возобновить сертификат клиента, удалив hello отпечаток из hello список отозванных сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="6c06e-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="6c06e-317">Объявления переменных hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-317">Declare hello variables.</span></span> <span data-ttu-id="6c06e-318">Убедитесь, что объявления hello правильный отпечаток для hello сертификат, который tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="6c06e-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="6c06e-319">Удалите hello отпечаток сертификата из списка отзыва сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="6c06e-320">Проверьте, если отпечаток hello удаляется из списка отозванных hello.</span><span class="sxs-lookup"><span data-stu-id="6c06e-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="6c06e-321"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="6c06e-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6c06e-322">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c06e-322">Next steps</span></span>
<span data-ttu-id="6c06e-323">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="6c06e-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="6c06e-324">Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="6c06e-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="6c06e-325">toounderstand Дополнительные сведения о сети и виртуальные машины в разделе [обзор сети Azure и виртуальных Машин Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c06e-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
