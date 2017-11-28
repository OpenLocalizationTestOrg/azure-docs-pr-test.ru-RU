---
title: "Сброс tooreestablish шлюза Azure VPN туннелей IPsec | Документы Microsoft"
description: "В этой статье описывается сброс вашей туннелей IPsec шлюза VPN Azure tooreestablish. статья Hello относится tooVPN шлюзов в классическом hello и модели развертывания диспетчера ресурсов hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="e477a-104">Сброс VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="e477a-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="e477a-105">Сброс настроек VPN-шлюза Azure полезен при потере распределенного VPN-подключения в одном или нескольких VPN-туннелях типа "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="e477a-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="e477a-106">В этой ситуации локального VPN-устройств являются все работает правильно, но не удается tooestablish туннелей IPsec со шлюзами Azure VPN hello.</span><span class="sxs-lookup"><span data-stu-id="e477a-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="e477a-107">Эта статья поможет вам сбросить VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="e477a-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="e477a-108">Что происходит при сбросе?</span><span class="sxs-lookup"><span data-stu-id="e477a-108">What happens during a reset?</span></span>

<span data-ttu-id="e477a-109">VPN-шлюз состоит из двух экземпляров виртуальной машины (активного и резервного) с соответствующими конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="e477a-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="e477a-110">При сбросе hello шлюза будет перезагружен шлюза hello и затем повторно применяет hello между организациями tooit конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e477a-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="e477a-111">шлюз Hello сохраняет hello общедоступный IP-адрес, который уже имеет.</span><span class="sxs-lookup"><span data-stu-id="e477a-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="e477a-112">Это означает, что не нужно конфигурация маршрутизатора tooupdate hello VPN с новый общедоступный IP-адрес для шлюза Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="e477a-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="e477a-113">При использовании функции hello команда tooreset hello шлюза hello текущий активный экземпляр шлюза Azure VPN hello перезагружен немедленно.</span><span class="sxs-lookup"><span data-stu-id="e477a-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="e477a-114">При отработке отказа hello из hello активный экземпляр (перезагружается), резервный экземпляр toohello будет краткий промежуток.</span><span class="sxs-lookup"><span data-stu-id="e477a-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="e477a-115">Разрыв Hello должно быть меньше одной минуты.</span><span class="sxs-lookup"><span data-stu-id="e477a-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="e477a-116">Если подключение hello не восстанавливается после первой перезагрузки hello, проблема hello же команда снова tooreboot hello второй экземпляр виртуальной Машины (hello новый active шлюз).</span><span class="sxs-lookup"><span data-stu-id="e477a-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="e477a-117">Если дважды выполнить перезагрузку hello запрошенный tooback назад, будет немного больше времени периода перезагружаются где оба экземпляра виртуальной Машины (активные и резервные).</span><span class="sxs-lookup"><span data-stu-id="e477a-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="e477a-118">Это приведет к более длинная пауза на VPN-подключение hello вверх too2 too4 минут после перезагрузки hello toocomplete виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e477a-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="e477a-119">После двух перезагрузок Если по-прежнему возникают проблемы с подключением между организациями, создайте запрос в службу поддержки из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e477a-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="e477a-120"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e477a-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="e477a-121">Перед сбросом шлюз проверьте hello ключевые элементы, перечисленные ниже, для каждого туннеля VPN IPsec-сайтами (S2S).</span><span class="sxs-lookup"><span data-stu-id="e477a-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="e477a-122">Любые различия в элементах hello приведет к disconnect hello туннелей S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="e477a-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="e477a-123">Проверка и исправление hello конфигурации для локальной и VPN-шлюзы Azure позволяет избежать ненужных после перезагрузки и нарушений в работе для hello другие соединения работу на шлюзах hello.</span><span class="sxs-lookup"><span data-stu-id="e477a-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="e477a-124">Проверьте hello следующих элементов перед сбросом шлюза.</span><span class="sxs-lookup"><span data-stu-id="e477a-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="e477a-125">Hello Интернета IP адресов (VIP) для обоих hello VPN-шлюз Azure и hello локального VPN-шлюз настроены правильно в обе hello Azure и hello локального VPN политики.</span><span class="sxs-lookup"><span data-stu-id="e477a-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="e477a-126">Hello общий ключ должен hello же на Azure и локальных шлюзах VPN.</span><span class="sxs-lookup"><span data-stu-id="e477a-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="e477a-127">Если применить конкретной конфигурации IPsec/IKE, такие как гарантировать шифрования, хэширования алгоритмы и PFS (включить режим PFS), оба hello Azure и локальным VPN-шлюзов hello и те же конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e477a-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="e477a-128"><a name="portal"></a>Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e477a-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="e477a-129">Вы можете сбросить шлюз VPN диспетчера ресурсов с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e477a-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="e477a-130">Tooreset классический шлюза, в статье hello [PowerShell](#resetclassic) действия.</span><span class="sxs-lookup"><span data-stu-id="e477a-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="e477a-131">Модель развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="e477a-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="e477a-132">Откройте hello [портал Azure](https://portal.azure.com) и шлюз виртуальной сети toohello диспетчера ресурсов, что требуется tooreset перехода.</span><span class="sxs-lookup"><span data-stu-id="e477a-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="e477a-133">В колонке hello для hello шлюза виртуальной сети нажмите кнопку «Сброс».</span><span class="sxs-lookup"><span data-stu-id="e477a-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Колонка сброса VPN-шлюза](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="e477a-135">На hello восстановить колонку, нажмите hello **Сброс** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e477a-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="e477a-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="e477a-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="e477a-137">Модель развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="e477a-137">Resource Manager deployment model</span></span>

<span data-ttu-id="e477a-138">Здравствуйте командлет Сброс шлюза является **AzureRmVirtualNetworkGateway Сброс**.</span><span class="sxs-lookup"><span data-stu-id="e477a-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="e477a-139">Прежде чем выполнять сброс, убедитесь, что у вас есть последняя версия hello hello [командлеты PowerShell диспетчера ресурсов](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="e477a-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="e477a-140">Hello следующий пример сбрасывает шлюз виртуальной сети с именем VNet1GW в группе ресурсов TestRG1 hello:</span><span class="sxs-lookup"><span data-stu-id="e477a-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="e477a-141">Результат:</span><span class="sxs-lookup"><span data-stu-id="e477a-141">Result:</span></span>

<span data-ttu-id="e477a-142">При получении возвращают результат, можно предположить, был успешно сброшен hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="e477a-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="e477a-143">Однако нет ничего hello возвращаемого результата, который явно указывает, был успешно сброшен, hello.</span><span class="sxs-lookup"><span data-stu-id="e477a-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="e477a-144">Если требуется, чтобы toolook поближе toosee журнал hello точно шлюза hello сбрасывать произошла, эти сведения можно просмотреть в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e477a-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e477a-145">На портале hello перейдите слишком**«GatewayName» -> исправности ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="e477a-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="e477a-146"><a name="resetclassic"></a>Классическая модель развертывания</span><span class="sxs-lookup"><span data-stu-id="e477a-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="e477a-147">Здравствуйте командлет Сброс шлюза является **AzureVNetGateway Сброс**.</span><span class="sxs-lookup"><span data-stu-id="e477a-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="e477a-148">Прежде чем выполнять сброс, убедитесь, что у вас есть последняя версия hello hello [командлеты PowerShell для службы управления (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="e477a-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="e477a-149">Hello следующий пример сбрасывает hello шлюза для виртуальной сети с именем «ContosoVNet»:</span><span class="sxs-lookup"><span data-stu-id="e477a-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="e477a-150">Результат:</span><span class="sxs-lookup"><span data-stu-id="e477a-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="e477a-151"><a name="cli"></a>Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e477a-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="e477a-152">шлюз tooreset hello, используйте hello [сброс виртуальной сети — шлюз сети az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) команды.</span><span class="sxs-lookup"><span data-stu-id="e477a-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="e477a-153">Hello следующий пример сбрасывает шлюз виртуальной сети с именем VNet5GW в группе ресурсов TestRG5 hello:</span><span class="sxs-lookup"><span data-stu-id="e477a-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="e477a-154">Результат:</span><span class="sxs-lookup"><span data-stu-id="e477a-154">Result:</span></span>

<span data-ttu-id="e477a-155">При получении возвращают результат, можно предположить, был успешно сброшен hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="e477a-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="e477a-156">Однако нет ничего hello возвращаемого результата, который явно указывает, был успешно сброшен, hello.</span><span class="sxs-lookup"><span data-stu-id="e477a-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="e477a-157">Если требуется, чтобы toolook поближе toosee журнал hello точно шлюза hello сбрасывать произошла, эти сведения можно просмотреть в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e477a-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e477a-158">На портале hello перейдите слишком**«GatewayName» -> исправности ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="e477a-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
