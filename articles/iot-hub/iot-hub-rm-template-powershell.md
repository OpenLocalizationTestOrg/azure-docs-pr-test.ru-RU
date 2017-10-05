---
title: "Создание Центра Интернета вещей Azure с помощью шаблона (PowerShell) | Документация Майкрософт"
description: "Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager и PowerShell."
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="379d5-103">Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="379d5-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="379d5-104">Диспетчер ресурсов Azure можно использовать для создания Центров Интернета вещей Azure программным способом и управления ими.</span><span class="sxs-lookup"><span data-stu-id="379d5-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="379d5-105">В этом учебнике показано, как использовать шаблон Azure Resource Manager для создания Центра Интернета вещей с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="379d5-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="379d5-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="379d5-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="379d5-107">В этой статье описывается использование модели развертывания на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="379d5-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="379d5-108">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="379d5-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="379d5-109">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="379d5-109">An active Azure account.</span></span> <br/><span data-ttu-id="379d5-110">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="379d5-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="379d5-111">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="379d5-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="379d5-112">Дополнительные сведения об использовании PowerShell и шаблонов Azure Resource Manager для создания ресурсов Azure см. в статье [Управление ресурсами с помощью Azure PowerShell и Resource Manager][lnk-powershell-arm].</span><span class="sxs-lookup"><span data-stu-id="379d5-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="379d5-113">Подключение к подписке Azure</span><span class="sxs-lookup"><span data-stu-id="379d5-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="379d5-114">В командной строке PowerShell введите следующую команду, чтобы войти в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="379d5-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="379d5-115">Если у вас есть несколько подписок Azure, то при входе в Azure вы получите доступ ко всем подпискам Azure, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="379d5-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="379d5-116">Используйте следующую команду, чтобы просмотреть подписки Azure, доступные для использования:</span><span class="sxs-lookup"><span data-stu-id="379d5-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="379d5-117">Используйте следующую команду, чтобы выбрать подписку, которая будет использоваться для выполнения команд для создания Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="379d5-118">Вы можете использовать имя подписки или идентификатор из выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="379d5-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="379d5-119">Чтобы узнать, где можно развернуть Центр Интернета вещей, и ознакомиться с текущими поддерживаемыми версиями API, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="379d5-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="379d5-120">Создайте группу ресурсов для хранения Центра Интернета вещей, используя указанную ниже команду в одном из поддерживаемых расположений для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="379d5-121">В этом примере создается группа ресурсов с именем **MyIoTRG1**.</span><span class="sxs-lookup"><span data-stu-id="379d5-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="379d5-122">Отправка шаблона для создания Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="379d5-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="379d5-123">Используйте шаблон JSON для создания Центра Интернета вещей в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="379d5-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="379d5-124">Можно также использовать шаблон Azure Resource Manager для изменения существующего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="379d5-125">Используйте текстовый редактор, чтобы создать шаблон Azure Resource Manager с именем **template.json** с помощью следующего определения ресурса для создания стандартного Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="379d5-126">В этом примере в регион **Восточная часть США** добавляется Центр Интернета вещей, создаются две группы потребителей (**cg1** и **cg2**) для конечной точки, совместимой с концентраторами событий, и используется версия API **2016-02-03**.</span><span class="sxs-lookup"><span data-stu-id="379d5-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="379d5-127">При использовании этого шаблона нужно передать имя Центра Интернета вещей в качестве параметра с именем **hubName**.</span><span class="sxs-lookup"><span data-stu-id="379d5-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="379d5-128">Текущий список расположений, которые поддерживают Центр Интернета вещей, указан на странице [Состояние Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="379d5-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="379d5-129">Сохраните файл шаблона Azure Resource Manager на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="379d5-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="379d5-130">В этом примере предполагается, что файл сохраняется в папке **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="379d5-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="379d5-131">Выполните следующую команду, чтобы развернуть новый Центр Интернета вещей, передав в качестве параметра имя Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="379d5-132">В этом примере имя Центра Интернета вещей — `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="379d5-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="379d5-133">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="379d5-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="379d5-134">В выходных данных отображаются ключи для созданного Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="379d5-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="379d5-135">Чтобы убедиться, что в приложение добавлен новый Центр Интернета вещей, посетите [портал Azure][lnk-azure-portal] и просмотрите список ресурсов.</span><span class="sxs-lookup"><span data-stu-id="379d5-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="379d5-136">Вы также можете воспользоваться командлетом PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="379d5-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="379d5-137">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="379d5-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="379d5-138">Когда закончите, Центр Интернета вещей можно удалить через [портал Azure][lnk-azure-portal] или с помощью командлета PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="379d5-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="379d5-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="379d5-139">Next steps</span></span>

<span data-ttu-id="379d5-140">После развертывания Центра Интернета вещей с использованием шаблона Azure Resource Manager и PowerShell вас могут заинтересовать следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="379d5-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="379d5-141">Ознакомьтесь с возможностями [REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="379d5-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="379d5-142">Сведения о возможностях Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="379d5-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="379d5-143">Дополнительные сведения о разработке для Центра Интернета вещей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="379d5-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="379d5-144">[Знакомство с пакетом SDK для устройств Azure IoT для C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="379d5-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="379d5-145">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="379d5-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="379d5-146">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="379d5-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="379d5-147">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="379d5-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
