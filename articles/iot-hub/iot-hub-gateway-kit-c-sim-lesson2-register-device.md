---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Регистрация устройства | Документация Майкрософт"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей, облако Интернета вещей, создание устройства в Центре Интернета вещей Azure, TI SensorTag, TI BLE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="7e2e5-103">Создание Центра Интернета вещей Azure и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="7e2e5-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7e2e5-104">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="7e2e5-104">What you will do</span></span>

- <span data-ttu-id="7e2e5-105">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7e2e5-105">Create a resource group</span></span>
- <span data-ttu-id="7e2e5-106">Создание первого Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-106">Create your first IoT hub</span></span>
- <span data-ttu-id="7e2e5-107">Регистрация устройства в концентратор IoT с использованием hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="7e2e5-108">При регистрации устройства в концентратор IoT, hello Azure IoT Hub service создает ключ для tooauthenticate toouse вашего устройства с помощью службы hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="7e2e5-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7e2e5-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7e2e5-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="7e2e5-110">What you will learn</span></span>

<span data-ttu-id="7e2e5-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7e2e5-112">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="7e2e5-113">Как tooregister устройства в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7e2e5-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="7e2e5-114">What you need</span></span>

- <span data-ttu-id="7e2e5-115">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-115">An active Azure subscription.</span></span> <span data-ttu-id="7e2e5-116">Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="7e2e5-117">Необходимо иметь hello установлен Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="7e2e5-118">Создание центра IoT</span><span class="sxs-lookup"><span data-stu-id="7e2e5-118">Create an IoT hub</span></span>

<span data-ttu-id="7e2e5-119">toocreate центра IoT, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7e2e5-120">Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7e2e5-121">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7e2e5-122">Значение по умолчанию hello подписки Azure, требуется toouse, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7e2e5-123">`subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="7e2e5-124">Регистрация поставщика hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="7e2e5-125">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7e2e5-126">Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="7e2e5-127">Создание группы ресурсов с именем `iot-gateway` в регионе hello Запад США, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="7e2e5-128">`westus`— местоположение hello, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="7e2e5-129">Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="7e2e5-130">Создать центр IoT в hello `iot-gateway` группы ресурсов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="7e2e5-131">По умолчанию hello средство создает центр IoT в ценовую категорию Free hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="7e2e5-132">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7e2e5-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="7e2e5-133">имя вашего центра IoT Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="7e2e5-134">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="7e2e5-135">Регистрация устройства в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="7e2e5-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="7e2e5-136">Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="7e2e5-137">Зарегистрируйте устройство в Центре Интернета вещей, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e2e5-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="7e2e5-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="7e2e5-138">Summary</span></span>

<span data-ttu-id="7e2e5-139">Вы создали Центр Интернета вещей и зарегистрировали в нем логическое устройство с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="7e2e5-140">Теперь вы готовы toolearn об облачных tooconfigure и запустите приложение toosend шлюза образец данных из концентратор IoT tooyour физическое устройство hello.</span><span class="sxs-lookup"><span data-stu-id="7e2e5-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e2e5-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e2e5-141">Next steps</span></span>
<span data-ttu-id="7e2e5-142">[Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md) (Настройка и запуск примера приложения отправки в облако для имитации устройства)</span><span class="sxs-lookup"><span data-stu-id="7e2e5-142">[Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>