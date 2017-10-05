---
title: "Сброс VPN-шлюза Azure для повторного установления туннелей IPsec | Документация Майкрософт"
description: "В этой статье описывается, как выполнить сброс настроек VPN-шлюза Azure для повторного установления туннелей IPsec. Инструкции в этой статье применимы к VPN-шлюзам, созданным как на базе классической модели развертывания, так и на базе модели развертывания с помощью Resource Manager."
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
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="97af7-104">Сброс VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="97af7-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="97af7-105">Сброс настроек VPN-шлюза Azure полезен при потере распределенного VPN-подключения в одном или нескольких VPN-туннелях типа "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="97af7-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="97af7-106">В этой ситуации все локальные VPN-устройства работают правильно, но не могут взаимодействовать с VPN-шлюзами Azure через туннели IPsec.</span><span class="sxs-lookup"><span data-stu-id="97af7-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="97af7-107">Эта статья поможет вам сбросить VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="97af7-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="97af7-108">Что происходит при сбросе?</span><span class="sxs-lookup"><span data-stu-id="97af7-108">What happens during a reset?</span></span>

<span data-ttu-id="97af7-109">VPN-шлюз состоит из двух экземпляров виртуальной машины (активного и резервного) с соответствующими конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="97af7-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="97af7-110">Во время сброса настроек шлюза он перезагружает шлюз и повторно применяет на нем конфигурации распределенного подключения.</span><span class="sxs-lookup"><span data-stu-id="97af7-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="97af7-111">Шлюз сохранит имеющийся общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="97af7-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="97af7-112">Это означает, что вам не нужно указывать в конфигурации VPN-маршрутизатора новый общедоступный IP-адрес VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="97af7-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="97af7-113">Выполнение команды сброса шлюза влечет за собой немедленную перезагрузку текущего активного экземпляра VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="97af7-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="97af7-114">Переход от активного (перезагружаемого) экземпляра к резервному при отработке отказа сопровождается небольшой паузой.</span><span class="sxs-lookup"><span data-stu-id="97af7-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="97af7-115">Пауза не должна превышать одну минуту.</span><span class="sxs-lookup"><span data-stu-id="97af7-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="97af7-116">Если после первой перезагрузки соединение не восстановится, выполните эту же команду еще раз, чтобы перезагрузить второй экземпляр виртуальной машины (новый активный шлюз).</span><span class="sxs-lookup"><span data-stu-id="97af7-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="97af7-117">Если необходимо выполнить две последовательные перезагрузки (обоих экземпляров виртуальных машин — активного и резервного), это займет немного больше времени.</span><span class="sxs-lookup"><span data-stu-id="97af7-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="97af7-118">В таком случае пауза при установке VPN-подключения увеличится до 2–4 минут. Длительность паузы определяется скоростью перезагрузки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="97af7-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="97af7-119">Если после двух перезагрузок проблема с распределенным подключением не решится, отправьте запрос в службу поддержки на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="97af7-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="97af7-120"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="97af7-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="97af7-121">Перед сбросом настроек шлюза проверьте ключевые условия для каждого VPN-туннеля IPsec типа S2S, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="97af7-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="97af7-122">Если какое-то из условий не выполняется, подключение через VPN-туннели типа S2S не будет работать.</span><span class="sxs-lookup"><span data-stu-id="97af7-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="97af7-123">Проверка и исправление конфигурации для локальных VPN-шлюзов и VPN-шлюзов Azure избавляет от ненужных перезагрузок, а другие рабочие подключения через шлюзы — от сбоев.</span><span class="sxs-lookup"><span data-stu-id="97af7-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="97af7-124">Перед сбросом настроек шлюза проверьте следующие условия.</span><span class="sxs-lookup"><span data-stu-id="97af7-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="97af7-125">IP-адреса в Интернете (VIP) для VPN-шлюза Azure и локального VPN-шлюза должны быть настроены правильно в политиках Azure и локальных политиках VPN.</span><span class="sxs-lookup"><span data-stu-id="97af7-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="97af7-126">Общий ключ должен быть одинаковым для VPN-шлюза Azure и локального VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="97af7-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="97af7-127">Если применяется определенная конфигурация IPsec/IKE, например шифрование, алгоритмы хэширования и режим безопасной пересылки (PFS), задайте для VPN-шлюза Azure и локального VPN-шлюза одинаковые настройки.</span><span class="sxs-lookup"><span data-stu-id="97af7-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="97af7-128"><a name="portal"></a>Портал Azure</span><span class="sxs-lookup"><span data-stu-id="97af7-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="97af7-129">Сбросить настройки VPN-шлюза Resource Manager можно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="97af7-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="97af7-130">Если необходимо сбросить настройки классического шлюза, ознакомьтесь с [этим разделом](#resetclassic).</span><span class="sxs-lookup"><span data-stu-id="97af7-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="97af7-131">Модель развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="97af7-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="97af7-132">Откройте [портал Azure](https://portal.azure.com) и перейдите к шлюзу виртуальной сети Resource Manager, настройки которого необходимо сбросить.</span><span class="sxs-lookup"><span data-stu-id="97af7-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="97af7-133">В колонке для шлюза виртуальной сети щелкните "Сброс".</span><span class="sxs-lookup"><span data-stu-id="97af7-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Колонка сброса VPN-шлюза](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="97af7-135">В колонке "Сброс" нажмите кнопку **Сброс**.</span><span class="sxs-lookup"><span data-stu-id="97af7-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="97af7-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="97af7-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="97af7-137">Модель развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="97af7-137">Resource Manager deployment model</span></span>

<span data-ttu-id="97af7-138">Командлет сброса шлюза — **Reset-AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="97af7-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="97af7-139">Перед выполнением сброса убедитесь, что у вас установлена последняя версия командлетов [PowerShell для Azure Resource Manager](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="97af7-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="97af7-140">В следующем примере выполняется сброс шлюза виртуальной сети с именем VNet1GW в группе ресурсов TestRG1:</span><span class="sxs-lookup"><span data-stu-id="97af7-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="97af7-141">Результат:</span><span class="sxs-lookup"><span data-stu-id="97af7-141">Result:</span></span>

<span data-ttu-id="97af7-142">Вывод результата подразумевает успешное выполнение сброса шлюза.</span><span class="sxs-lookup"><span data-stu-id="97af7-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="97af7-143">Тем не менее никакие данные в возвращаемом результате не указывают явно на то, что сброс выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="97af7-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="97af7-144">Если вам требуется проверить журнал, чтобы узнать точное время сброса шлюза, эти сведения можно просмотреть на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97af7-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="97af7-145">На портале перейдите в раздел **ИмяШлюза -> Работоспособность ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="97af7-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="97af7-146"><a name="resetclassic"></a>Классическая модель развертывания</span><span class="sxs-lookup"><span data-stu-id="97af7-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="97af7-147">Командлет сброса шлюза — **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="97af7-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="97af7-148">Перед выполнением сброса убедитесь, что у вас установлена последняя версия командлетов [PowerShell для управления службами](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="97af7-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="97af7-149">В следующем примере выполняется сброс шлюза для виртуальной сети с именем ContosoVNet:</span><span class="sxs-lookup"><span data-stu-id="97af7-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="97af7-150">Результат:</span><span class="sxs-lookup"><span data-stu-id="97af7-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="97af7-151"><a name="cli"></a>Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="97af7-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="97af7-152">Чтобы сбросить шлюз, используйте команду [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset).</span><span class="sxs-lookup"><span data-stu-id="97af7-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="97af7-153">В следующем примере выполняется сброс шлюза виртуальной сети с именем VNet5GW в группе ресурсов TestRG5:</span><span class="sxs-lookup"><span data-stu-id="97af7-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="97af7-154">Результат:</span><span class="sxs-lookup"><span data-stu-id="97af7-154">Result:</span></span>

<span data-ttu-id="97af7-155">Вывод результата подразумевает успешное выполнение сброса шлюза.</span><span class="sxs-lookup"><span data-stu-id="97af7-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="97af7-156">Тем не менее никакие данные в возвращаемом результате не указывают явно на то, что сброс выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="97af7-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="97af7-157">Если вам требуется проверить журнал, чтобы узнать точное время сброса шлюза, эти сведения можно просмотреть на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97af7-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="97af7-158">На портале перейдите в раздел **ИмяШлюза -> Работоспособность ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="97af7-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>