---
title: "Создание Центра Интернета вещей Azure с помощью командлета PowerShell | Документация Майкрософт"
description: "Узнайте, как с помощью командлетов PowerShell создать Центр Интернета вещей."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="f8b39-103">Создание Центра Интернета вещей с помощью командлета New-AzureRmIotHub</span><span class="sxs-lookup"><span data-stu-id="f8b39-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="f8b39-104">Введение</span><span class="sxs-lookup"><span data-stu-id="f8b39-104">Introduction</span></span>

<span data-ttu-id="f8b39-105">Для создания Центров Интернета вещей и управления ими можно использовать командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8b39-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="f8b39-106">В этом руководстве показано, как создать Центр Интернета вещей с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8b39-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="f8b39-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8b39-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f8b39-108">В этой статье описывается использование модели развертывания на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f8b39-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="f8b39-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="f8b39-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f8b39-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f8b39-110">An active Azure account.</span></span> <br/><span data-ttu-id="f8b39-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f8b39-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="f8b39-112">[Командлеты Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="f8b39-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="f8b39-113">Подключение к подписке Azure</span><span class="sxs-lookup"><span data-stu-id="f8b39-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="f8b39-114">В командной строке PowerShell введите следующую команду, чтобы войти в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f8b39-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f8b39-115">Если у вас есть несколько подписок Azure, то при входе в Azure вы получите доступ ко всем подпискам Azure, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="f8b39-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="f8b39-116">Используйте следующую команду, чтобы просмотреть подписки Azure, доступные для использования:</span><span class="sxs-lookup"><span data-stu-id="f8b39-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="f8b39-117">Используйте следующую команду, чтобы выбрать подписку, которая будет использоваться для выполнения команд для создания Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f8b39-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="f8b39-118">Вы можете использовать имя подписки или идентификатор из выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="f8b39-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="f8b39-119">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="f8b39-119">Create resource group</span></span>

<span data-ttu-id="f8b39-120">Для развертывания Центра Интернета вещей необходима группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f8b39-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="f8b39-121">Вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="f8b39-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="f8b39-122">Чтобы узнать, где можно развернуть Центр Интернета вещей, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f8b39-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="f8b39-123">Чтобы создать группу ресурсов для Центра Интернета вещей в одном из поддерживаемых расположений, используйте указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f8b39-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="f8b39-124">В этом примере создается группа ресурсов с именем **MyIoTRG1**, размещенная в регионе **Восточная часть США**:</span><span class="sxs-lookup"><span data-stu-id="f8b39-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="f8b39-125">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f8b39-125">Create an IoT hub</span></span>

<span data-ttu-id="f8b39-126">Чтобы создать Центр Интернета вещей в группе ресурсов, созданной на предыдущем шаге, используйте указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f8b39-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="f8b39-127">В этом примере создается центр категории **S1** с именем **MyTestIoTHub**, размещенный в регионе **Восточная часть США**:</span><span class="sxs-lookup"><span data-stu-id="f8b39-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="f8b39-128">Имя Центра Интернета вещей должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="f8b39-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="f8b39-129">Для вывода списка всех Центров Интернета вещей в подписке используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f8b39-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="f8b39-130">В предыдущем примере добавляется Центр Интернета вещей уровня S1 Standard, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="f8b39-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="f8b39-131">Чтобы удалить Центр Интернета вещей, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f8b39-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="f8b39-132">Вы также можете удалить группу ресурсов и все входящие в нее ресурсы, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f8b39-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="f8b39-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8b39-133">Next steps</span></span>

<span data-ttu-id="f8b39-134">После развертывания Центра Интернета вещей с помощью командлета PowerShell вам могут понадобиться дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="f8b39-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="f8b39-135">Узнайте о других [командлетах PowerShell для работы с Центром Интернета вещей][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="f8b39-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="f8b39-136">Ознакомьтесь с возможностями [REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="f8b39-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="f8b39-137">Дополнительные сведения о разработке для Центра Интернета вещей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f8b39-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="f8b39-138">[Знакомство с пакетом SDK для устройств Azure IoT для C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="f8b39-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="f8b39-139">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="f8b39-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="f8b39-140">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="f8b39-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f8b39-141">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="f8b39-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
