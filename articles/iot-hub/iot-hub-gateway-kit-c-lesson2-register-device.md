---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Регистрация устройства | Документация Майкрософт"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей, облако Интернета вещей, создание устройства в Центре Интернета вещей Azure, TI SensorTag, TI BLE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="5401c-103">Создание Центра Интернета вещей Azure и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="5401c-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5401c-104">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="5401c-104">What you will do</span></span>

- <span data-ttu-id="5401c-105">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5401c-105">Create a resource group</span></span>
- <span data-ttu-id="5401c-106">Создание первого Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5401c-106">Create your first IoT hub</span></span>
- <span data-ttu-id="5401c-107">Регистрация устройства в собственном Центре Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5401c-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="5401c-108">При регистрации устройства в собственном Центре Интернета вещей служба Центра Интернета вещей Azure создает ключ для устройства, используемый для аутентификации в службе.</span><span class="sxs-lookup"><span data-stu-id="5401c-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="5401c-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5401c-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5401c-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="5401c-110">What you will learn</span></span>

<span data-ttu-id="5401c-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5401c-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="5401c-112">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5401c-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="5401c-113">Как зарегистрировать устройство в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5401c-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5401c-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5401c-114">What you need</span></span>

- <span data-ttu-id="5401c-115">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5401c-115">An active Azure subscription.</span></span> <span data-ttu-id="5401c-116">Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5401c-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="5401c-117">У вас должен быть установлен Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5401c-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="5401c-118">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="5401c-118">Create an IoT hub</span></span>

<span data-ttu-id="5401c-119">Чтобы создать Центр Интернета вещей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5401c-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="5401c-120">Войдите в свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5401c-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="5401c-121">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="5401c-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="5401c-122">Определите подписку Azure, которую необходимо использовать по умолчанию, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5401c-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="5401c-123">Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.</span><span class="sxs-lookup"><span data-stu-id="5401c-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="5401c-124">Зарегистрируйте поставщик с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="5401c-124">Register the provider by running the following command.</span></span> <span data-ttu-id="5401c-125">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="5401c-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="5401c-126">Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.</span><span class="sxs-lookup"><span data-stu-id="5401c-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="5401c-127">Создайте группу ресурсов с именем `iot-gateway` в регионе "Западная часть США", выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5401c-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="5401c-128">`westus` — это расположение, в котором создается группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5401c-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="5401c-129">Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.</span><span class="sxs-lookup"><span data-stu-id="5401c-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="5401c-130">Создайте Центр Интернета вещей в группе ресурсов `iot-gateway`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5401c-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="5401c-131">По умолчанию создается Центр Интернета вещей уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="5401c-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="5401c-132">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="5401c-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="5401c-133">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="5401c-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="5401c-134">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="5401c-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="5401c-135">Регистрация устройства в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="5401c-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="5401c-136">Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="5401c-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="5401c-137">Зарегистрируйте устройство в Центре Интернета вещей, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5401c-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="5401c-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="5401c-138">Summary</span></span>

<span data-ttu-id="5401c-139">Вы создали Центр Интернета вещей и зарегистрировали в нем логическое устройство с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="5401c-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="5401c-140">Теперь можно перейти к настройке и запуску примера приложения шлюза, используемого для отправки данных с физического устройства в Центр Интернета вещей, находящийся в облаке.</span><span class="sxs-lookup"><span data-stu-id="5401c-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5401c-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5401c-141">Next steps</span></span>
[<span data-ttu-id="5401c-142">Настройка и запуск примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="5401c-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)