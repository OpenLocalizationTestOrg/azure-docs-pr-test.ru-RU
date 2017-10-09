---
title: "Центр IoT Azure с помощью командлета PowerShell aaaCreate | Документы Microsoft"
description: "Как toouse toocreate командлет PowerShell центра IoT."
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
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="3a0a6-103">Создать центр IoT с помощью командлета New-AzureRmIotHub hello</span><span class="sxs-lookup"><span data-stu-id="3a0a6-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="3a0a6-104">Введение</span><span class="sxs-lookup"><span data-stu-id="3a0a6-104">Introduction</span></span>

<span data-ttu-id="3a0a6-105">Можно использовать toocreate командлетов Azure PowerShell и управление центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="3a0a6-106">В этом учебнике показано как toocreate центр IoT с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3a0a6-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3a0a6-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3a0a6-108">В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="3a0a6-109">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="3a0a6-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-110">An active Azure account.</span></span> <br/><span data-ttu-id="3a0a6-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="3a0a6-112">[Командлеты Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="3a0a6-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="3a0a6-113">Подключение tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="3a0a6-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="3a0a6-114">В командной строке PowerShell введите hello, следующая команда toosign в tooyour подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3a0a6-115">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="3a0a6-116">Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="3a0a6-117">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="3a0a6-118">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="3a0a6-119">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="3a0a6-119">Create resource group</span></span>

<span data-ttu-id="3a0a6-120">Необходимо toodeploy группы ресурсов центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="3a0a6-121">Вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="3a0a6-122">Можно использовать hello следующих команда toodiscover hello расположения, где можно развернуть центр IoT.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="3a0a6-123">toocreate группу ресурсов для вашего центра IoT в одном из расположений hello поддерживается для центра IoT, hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="3a0a6-124">Этот пример создает группу ресурсов под названием **MyIoTRG1** в hello **Восток США** области:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="3a0a6-125">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="3a0a6-125">Create an IoT hub</span></span>

<span data-ttu-id="3a0a6-126">toocreate центр IoT в группе ресурсов hello, созданный на предыдущем шаге hello, hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="3a0a6-127">В этом примере создается **S1** концентратора вызывается **MyTestIoTHub** в hello **Восток США** области:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="3a0a6-128">Hello имя центра IoT hello должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="3a0a6-129">Можно перечислить все центры IoT hello в подписке, используя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="3a0a6-130">Hello предыдущего примера добавляет S1 Стандартная центр IoT для которого взимается плата.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="3a0a6-131">Можно удалить центр IoT hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="3a0a6-132">Кроме того можно удалить группу ресурсов и Здравствуйте, все ресурсы, которые он содержит, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="3a0a6-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a0a6-133">Next steps</span></span>

<span data-ttu-id="3a0a6-134">Теперь развертывания с помощью командлета PowerShell центра IoT вы можете дополнительно tooexplore:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="3a0a6-135">Узнайте о других [командлетах PowerShell для работы с Центром Интернета вещей][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="3a0a6-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="3a0a6-136">Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="3a0a6-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="3a0a6-137">toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3a0a6-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="3a0a6-138">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="3a0a6-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="3a0a6-139">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="3a0a6-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="3a0a6-140">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="3a0a6-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3a0a6-141">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="3a0a6-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
