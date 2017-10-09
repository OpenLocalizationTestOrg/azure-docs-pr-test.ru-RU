---
title: "aaaCreate центр IoT Azure с помощью шаблона (PowerShell) | Документы Microsoft"
description: "Как toouse toocreate шаблона диспетчера ресурсов Azure центр IoT с помощью PowerShell."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="115b4-103">Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="115b4-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="115b4-104">Можно использовать toocreate диспетчера ресурсов Azure и программно управлять центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="115b4-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="115b4-105">В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure центр IoT с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="115b4-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="115b4-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="115b4-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="115b4-107">В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="115b4-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="115b4-108">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="115b4-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="115b4-109">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="115b4-109">An active Azure account.</span></span> <br/><span data-ttu-id="115b4-110">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="115b4-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="115b4-111">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="115b4-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="115b4-112">статья Hello [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure] [ lnk-powershell-arm] предоставляет дополнительные сведения о том, как toouse PowerShell и диспетчера ресурсов Azure шаблоны toocreate Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="115b4-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="115b4-113">Подключение tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="115b4-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="115b4-114">В командной строке PowerShell введите hello, следующая команда toosign в tooyour подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="115b4-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="115b4-115">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="115b4-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="115b4-116">Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.</span><span class="sxs-lookup"><span data-stu-id="115b4-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="115b4-117">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="115b4-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="115b4-118">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="115b4-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="115b4-119">Можно использовать следующие команды toodiscover, где вы можете развернуть центр IoT и hello в настоящее время поддерживаемые версии API hello:</span><span class="sxs-lookup"><span data-stu-id="115b4-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="115b4-120">Создайте группы ресурсов toocontain IoT концентраторе, используя следующую команду в одном из расположений hello поддерживается для центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="115b4-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="115b4-121">В этом примере создается группа ресурсов с именем **MyIoTRG1**.</span><span class="sxs-lookup"><span data-stu-id="115b4-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="115b4-122">Отправить шаблон toocreate центра IoT</span><span class="sxs-lookup"><span data-stu-id="115b4-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="115b4-123">Используйте toocreate шаблона JSON центр IoT в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="115b4-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="115b4-124">Также можно использовать существующий концентратор IoT toomake изменения диспетчера ресурсов Azure шаблона tooan.</span><span class="sxs-lookup"><span data-stu-id="115b4-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="115b4-125">Использовать toocreate текстовый редактор, вызывается шаблона Azure Resource Manager **template.json** с hello следующие toocreate определения ресурсов Стандартная центр IoT.</span><span class="sxs-lookup"><span data-stu-id="115b4-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="115b4-126">В этом примере добавляется hello центр IoT в hello **Восток США** области, создает две группы потребителей (**cg1** и **cg2**) на конечной точке hello совместимое концентратора событий и использует hello **2016-02-03** версия API.</span><span class="sxs-lookup"><span data-stu-id="115b4-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="115b4-127">Этот шаблон также ожидает, что вы toopass имя концентратора IoT hello как параметр с именем **hubName**.</span><span class="sxs-lookup"><span data-stu-id="115b4-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="115b4-128">Текущий список расположений, которые поддерживают Центр IoT hello. в разделе [состояние Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="115b4-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="115b4-129">Сохраните файл шаблона диспетчера ресурсов Azure hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="115b4-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="115b4-130">В этом примере предполагается, что файл сохраняется в папке **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="115b4-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="115b4-131">Выполните следующие команды toodeploy hello новый концентратор IoT, передавая имя вашего центра IoT hello в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="115b4-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="115b4-132">В этом примере hello центра IoT hello называется `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="115b4-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="115b4-133">имя вашего центра IoT Hello должно быть глобально уникальным:</span><span class="sxs-lookup"><span data-stu-id="115b4-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="115b4-134">для вывода Hello hello ключи для центра IoT hello, созданный.</span><span class="sxs-lookup"><span data-stu-id="115b4-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="115b4-135">tooverify добавлено приложение hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="115b4-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="115b4-136">Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="115b4-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="115b4-137">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="115b4-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="115b4-138">Вы можете удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.</span><span class="sxs-lookup"><span data-stu-id="115b4-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="115b4-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="115b4-139">Next steps</span></span>

<span data-ttu-id="115b4-140">Теперь вы развернули центр IoT, с помощью шаблона Azure Resource Manager с помощью PowerShell, вы можете tooexplore дальнейшей:</span><span class="sxs-lookup"><span data-stu-id="115b4-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="115b4-141">Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="115b4-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="115b4-142">Чтение [Обзор диспетчера ресурсов Azure] [ lnk-azure-rm-overview] toolearn больше о возможностях hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="115b4-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="115b4-143">toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="115b4-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="115b4-144">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="115b4-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="115b4-145">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="115b4-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="115b4-146">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="115b4-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="115b4-147">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="115b4-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
