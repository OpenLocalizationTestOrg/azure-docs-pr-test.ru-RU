---
title: "Настройка маршрутизации для канала Azure ExpressRoute с помощью интерфейса командной строки | Документация Майкрософт"
description: "Эта статья поможет вам создать и подготовить частный пиринг, общедоступный пиринг или пиринг Microsoft для канала ExpressRoute. а также показано, как проверить состояние, обновить или удалить пиринги для канала."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="d70e5-104">Создание и изменение маршрутизации для канала ExpressRoute с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="d70e5-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="d70e5-105">Эта статья поможет вам создать конфигурацию для канала ExpressRoute и управлять ею в модели развертывания с помощью Azure Resource Manager, используя интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="d70e5-106">Вы также сможете проверить состояние, обновить, удалить и отозвать пиринги для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="d70e5-107">Если вы хотите использовать для работы с каналом другой метод, выберите подходящую статью из списка ниже.</span><span class="sxs-lookup"><span data-stu-id="d70e5-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d70e5-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="d70e5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d70e5-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="d70e5-110">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="d70e5-111">Видео — частный пиринг</span><span class="sxs-lookup"><span data-stu-id="d70e5-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d70e5-112">Видео — общедоступный пиринг</span><span class="sxs-lookup"><span data-stu-id="d70e5-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d70e5-113">Видео — пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d70e5-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="d70e5-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="d70e5-115">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="d70e5-115">Configuration prerequisites</span></span>

* <span data-ttu-id="d70e5-116">Перед началом работы установите последнюю версию команд интерфейса командной строки (версию 2.0 или более позднюю).</span><span class="sxs-lookup"><span data-stu-id="d70e5-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="d70e5-117">Сведения об установке команд интерфейса командной строки см. в статье [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Установка Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="d70e5-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="d70e5-118">Не забудьте изучить страницы с описанием [предварительных требований](expressroute-prerequisites.md), [требований к маршрутизации](expressroute-routing.md) и [рабочих процессов](expressroute-workflows.md), прежде чем приступать к настройке.</span><span class="sxs-lookup"><span data-stu-id="d70e5-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="d70e5-119">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d70e5-120">Приступая к работе, [создайте канал ExpressRoute](howto-circuit-cli.md) ; он должен быть затем включен на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="d70e5-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d70e5-121">Для выполнения команд, описанных в статье, должен быть подготовлен и включен канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="d70e5-122">Эти инструкции распространяются только на каналы от поставщиков, предоставляющих услуги подключения второго уровня.</span><span class="sxs-lookup"><span data-stu-id="d70e5-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="d70e5-123">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="d70e5-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="d70e5-124">Для каждого канала ExpressRoute можно настроить один, два или все три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="d70e5-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="d70e5-125">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="d70e5-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="d70e5-126">главное, выполнять их конфигурацию по очереди.</span><span class="sxs-lookup"><span data-stu-id="d70e5-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="d70e5-127">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-127">Azure private peering</span></span>

<span data-ttu-id="d70e5-128">Этот раздел поможет вам создать, получить, обновить и (или) удалить конфигурацию частного пиринга Azure для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="d70e5-129">Создание частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-129">To create Azure private peering</span></span>

1. <span data-ttu-id="d70e5-130">Установите последнюю версию Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d70e5-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="d70e5-131">Используйте последнюю версию интерфейса командной строки (CLI) Azure.* Прежде чем начинать настройку, изучите [предварительные условия](expressroute-prerequisites.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d70e5-132">Выберите подписку, необходимую для создания канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d70e5-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d70e5-133">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="d70e5-134">Выполните инструкции по созданию [канала ExpressRoute](howto-circuit-cli.md). Поставщик услуг подключения должен подготовить его.</span><span class="sxs-lookup"><span data-stu-id="d70e5-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="d70e5-135">Если поставщик услуг подключения оказывает услуги третьего уровня, он может включить для вас частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="d70e5-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="d70e5-136">В этом случае инструкции в следующих разделах выполнять не нужно.</span><span class="sxs-lookup"><span data-stu-id="d70e5-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d70e5-137">Если же поставщик услуг подключения не берет на себя управление маршрутизацией, выполните приведенные ниже инструкции для настройки конфигурации после создания канала.</span><span class="sxs-lookup"><span data-stu-id="d70e5-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="d70e5-138">Убедитесь, что канал ExpressRoute подготовлен и включен.</span><span class="sxs-lookup"><span data-stu-id="d70e5-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d70e5-139">Используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="d70e5-140">Ответ будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="d70e5-140">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="d70e5-141">Настройте для канала частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="d70e5-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="d70e5-142">Прежде чем продолжить, убедитесь в наличии следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d70e5-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="d70e5-143">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d70e5-144">Эта подсеть не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d70e5-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d70e5-145">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d70e5-146">Эта подсеть не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d70e5-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d70e5-147">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d70e5-148">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="d70e5-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d70e5-149">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-149">AS number for peering.</span></span> <span data-ttu-id="d70e5-150">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d70e5-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="d70e5-151">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="d70e5-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="d70e5-152">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="d70e5-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="d70e5-153">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="d70e5-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="d70e5-154">Чтобы настроить для канала частный пиринг Azure, выполните код из следующего примера:</span><span class="sxs-lookup"><span data-stu-id="d70e5-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="d70e5-155">Если вы решили использовать MD5-хэш, используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d70e5-156">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="d70e5-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="d70e5-157">Просмотр сведений о частном пиринге Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-157">To view Azure private peering details</span></span>

<span data-ttu-id="d70e5-158">Для получения сведений о конфигурации можно использовать следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="d70e5-159">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="d70e5-159">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="d70e5-160">Обновление конфигурации частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="d70e5-161">С помощью следующего примера можно обновить любую часть конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d70e5-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="d70e5-162">В приведенном ниже примере значение идентификатора виртуальной локальной сети для канала изменяется со 100 на 500.</span><span class="sxs-lookup"><span data-stu-id="d70e5-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="d70e5-163">Удаление частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-163">To delete Azure private peering</span></span>

<span data-ttu-id="d70e5-164">Для удаления конфигурации пиринга выполните следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="d70e5-165">Перед выполнением этого кода отсоедините от канала ExpressRoute все виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="d70e5-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="d70e5-166">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-166">Azure public peering</span></span>

<span data-ttu-id="d70e5-167">Этот раздел поможет создать, получить, обновить и (или) удалить конфигурацию общедоступного пиринга Azure для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="d70e5-168">Создание общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-168">To create Azure public peering</span></span>

1. <span data-ttu-id="d70e5-169">Установите последнюю версию Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d70e5-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="d70e5-170">Используйте последнюю версию интерфейса командной строки (CLI) Azure.* Прежде чем начинать настройку, изучите [предварительные условия](expressroute-prerequisites.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d70e5-171">Выберите подписку, для которой будете создавать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d70e5-172">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="d70e5-173">Выполните инструкции по созданию [канала ExpressRoute](howto-circuit-cli.md). Поставщик услуг подключения должен подготовить его.</span><span class="sxs-lookup"><span data-stu-id="d70e5-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="d70e5-174">Если ваш поставщик услуг подключения оказывает услуги третьего уровня, попросите его включить для вас частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="d70e5-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="d70e5-175">В этом случае инструкции в следующих разделах выполнять не нужно.</span><span class="sxs-lookup"><span data-stu-id="d70e5-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d70e5-176">Если же поставщик услуг подключения не берет на себя управление маршрутизацией, выполните приведенные ниже инструкции для настройки конфигурации после создания канала.</span><span class="sxs-lookup"><span data-stu-id="d70e5-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="d70e5-177">Убедитесь, что канал ExpressRoute подготовлен и включен.</span><span class="sxs-lookup"><span data-stu-id="d70e5-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="d70e5-178">Используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="d70e5-179">Ответ будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="d70e5-179">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="d70e5-180">Настройте для канала общедоступный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="d70e5-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="d70e5-181">Прежде чем продолжить, убедитесь, что у вас есть следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="d70e5-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="d70e5-182">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d70e5-183">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="d70e5-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d70e5-184">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d70e5-185">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="d70e5-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d70e5-186">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d70e5-187">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="d70e5-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d70e5-188">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-188">AS number for peering.</span></span> <span data-ttu-id="d70e5-189">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d70e5-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d70e5-190">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="d70e5-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="d70e5-191">Чтобы настроить для канала общедоступный пиринг Azure, выполните код из следующего примера:</span><span class="sxs-lookup"><span data-stu-id="d70e5-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="d70e5-192">Если вы решили использовать MD5-хэш, используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d70e5-193">Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.</span><span class="sxs-lookup"><span data-stu-id="d70e5-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="d70e5-194">Просмотр сведений об общедоступном пиринге Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-194">To view Azure public peering details</span></span>

<span data-ttu-id="d70e5-195">Для получения сведений о конфигурации можно использовать следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="d70e5-196">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="d70e5-196">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="d70e5-197">Обновление конфигурации общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="d70e5-198">С помощью следующего примера можно обновить любую часть конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d70e5-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="d70e5-199">В приведенном ниже примере значение идентификатора виртуальной локальной сети для канала изменяется с 200 на 600.</span><span class="sxs-lookup"><span data-stu-id="d70e5-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="d70e5-200">Удаление общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="d70e5-200">To delete Azure public peering</span></span>

<span data-ttu-id="d70e5-201">Для удаления конфигурации пиринга выполните следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="d70e5-202">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-202">Microsoft peering</span></span>

<span data-ttu-id="d70e5-203">Этот раздел поможет создать, получить, обновить и (или) удалить конфигурацию пиринга Майкрософт для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d70e5-204">Пиринг Майкрософт для каналов ExpressRoute, которые были настроены до 1 августа 2017 г., позволяет объявлять все префиксы служб, даже если фильтры маршрутов не определены.</span><span class="sxs-lookup"><span data-stu-id="d70e5-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="d70e5-205">Пиринг Майкрософт для каналов ExpressRoute, настроенных 1 августа 2017 г. или позднее, не будет объявлять префиксы, пока к каналу не будет присоединен фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d70e5-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="d70e5-206">Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="d70e5-207">Создание пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="d70e5-208">Установите последнюю версию Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d70e5-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="d70e5-209">Используйте последнюю версию интерфейса командной строки (CLI) Azure.* Прежде чем начинать настройку, изучите [предварительные условия](expressroute-prerequisites.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d70e5-210">Выберите подписку, для которой будете создавать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d70e5-211">Создайте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70e5-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="d70e5-212">Выполните инструкции по созданию [канала ExpressRoute](howto-circuit-cli.md). Поставщик услуг подключения должен подготовить его.</span><span class="sxs-lookup"><span data-stu-id="d70e5-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="d70e5-213">Если поставщик услуг подключения оказывает услуги третьего уровня, он может включить для вас частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="d70e5-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="d70e5-214">В этом случае инструкции в следующих разделах выполнять не нужно.</span><span class="sxs-lookup"><span data-stu-id="d70e5-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d70e5-215">Если же поставщик услуг подключения не берет на себя управление маршрутизацией, выполните приведенные ниже инструкции для настройки конфигурации после создания канала.</span><span class="sxs-lookup"><span data-stu-id="d70e5-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="d70e5-216">Убедитесь, что канал ExpressRoute подготовлен и включен.</span><span class="sxs-lookup"><span data-stu-id="d70e5-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d70e5-217">Используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d70e5-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="d70e5-218">Ответ будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="d70e5-218">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="d70e5-219">Настройте пиринг Майкрософт для этого канала.</span><span class="sxs-lookup"><span data-stu-id="d70e5-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="d70e5-220">Перед началом работы убедитесь, что у вас есть следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d70e5-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="d70e5-221">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d70e5-222">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="d70e5-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d70e5-223">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="d70e5-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d70e5-224">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="d70e5-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d70e5-225">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d70e5-226">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="d70e5-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d70e5-227">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="d70e5-227">AS number for peering.</span></span> <span data-ttu-id="d70e5-228">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="d70e5-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d70e5-229">Объявленные префиксы: необходимо предоставить список всех префиксов, которые вы планируете объявить во время сеанса BGP.</span><span class="sxs-lookup"><span data-stu-id="d70e5-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="d70e5-230">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="d70e5-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="d70e5-231">Если вы планируете отправить набор префиксов, их можно оформить в виде списка, разделенного запятыми.</span><span class="sxs-lookup"><span data-stu-id="d70e5-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="d70e5-232">Эти префиксы должны быть зарегистрированы в RIR/IRR на ваше имя.</span><span class="sxs-lookup"><span data-stu-id="d70e5-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="d70e5-233">**Необязательно.** ASN клиента: для объявления префиксов, не зарегистрированных с номером AS для пиринга, можно указать номер AS, с которым они зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="d70e5-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="d70e5-234">Имя реестра маршрутизации: можно указать RIR/IRR, в котором зарегистрированы номер AS и префиксы.</span><span class="sxs-lookup"><span data-stu-id="d70e5-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="d70e5-235">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="d70e5-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="d70e5-236">Чтобы настроить пиринг Майкрософт для своего канала, выполните следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="d70e5-237">Получение сведений о пиринге Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-237">To get Microsoft peering details</span></span>

<span data-ttu-id="d70e5-238">Для получения сведений о конфигурации можно использовать следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="d70e5-239">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="d70e5-239">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="d70e5-240">Обновление конфигурации пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="d70e5-241">Вы можете обновить любую часть конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d70e5-241">You can update any part of the configuration.</span></span> <span data-ttu-id="d70e5-242">Следующий пример кода изменяет объявленные для канала префиксы с 123.1.0.0/24 на 124.1.0.0/24:</span><span class="sxs-lookup"><span data-stu-id="d70e5-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="d70e5-243">Удаление пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d70e5-243">To delete Microsoft peering</span></span>

<span data-ttu-id="d70e5-244">Для удаления конфигурации пиринга выполните следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d70e5-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="d70e5-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d70e5-245">Next steps</span></span>

<span data-ttu-id="d70e5-246">Следующий шаг — [связывание виртуальной сети с каналом ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="d70e5-247">Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="d70e5-248">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="d70e5-249">Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d70e5-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>