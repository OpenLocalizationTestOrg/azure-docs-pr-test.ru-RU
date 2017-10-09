---
title: "Подключения Arduino tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрировать Wi-Fi M0 Растушевка Adafruit в центр Azure IoT hello с помощью hello Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "подключение arduino toocloud, центр azure iot, Интернет вещей облака, центр azure iot создать устройство, arduino облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="144d9-104">Создание Центра Интернета вещей Azure и регистрация платы Adafruit Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="144d9-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="144d9-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="144d9-105">What you will do</span></span>
* <span data-ttu-id="144d9-106">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="144d9-106">Create a resource group.</span></span>
* <span data-ttu-id="144d9-107">Создайте концентратор Azure IoT в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="144d9-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="144d9-108">Добавьте концентратор Azure IoT toohello Arduino доски с помощью hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="144d9-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="144d9-109">При использовании hello Azure CLI tooadd ваш центр IoT Arduino tooyour плата hello службы создает ключ для вашей tooauthenticate плата Arduino со службой hello.</span><span class="sxs-lookup"><span data-stu-id="144d9-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="144d9-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="144d9-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="144d9-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="144d9-111">What you will learn</span></span>
<span data-ttu-id="144d9-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="144d9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="144d9-113">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="144d9-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="144d9-114">Как toocreate удостоверение устройства для вашей Arduino плата в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="144d9-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="144d9-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="144d9-115">What you need</span></span>
* <span data-ttu-id="144d9-116">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="144d9-116">An Azure account</span></span>
* <span data-ttu-id="144d9-117">Установлены на компьютере с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="144d9-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="144d9-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="144d9-118">Create your IoT hub</span></span>
<span data-ttu-id="144d9-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="144d9-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="144d9-120">toocreate концентратор IoT, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="144d9-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="144d9-121">Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="144d9-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="144d9-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="144d9-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="144d9-123">Установить подписку по умолчанию hello требуется toouse, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="144d9-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="144d9-124">`subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.</span><span class="sxs-lookup"><span data-stu-id="144d9-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="144d9-125">Регистрация поставщика hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="144d9-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="144d9-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="144d9-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="144d9-127">Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="144d9-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="144d9-128">Создайте группу ресурсов с именем iot образца в области hello Запад США, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="144d9-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="144d9-129">`westus`— местоположение hello, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="144d9-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="144d9-130">Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.</span><span class="sxs-lookup"><span data-stu-id="144d9-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="144d9-131">Создаете центр IoT в группе ресурсов iot образец hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="144d9-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="144d9-132">По умолчанию hello средство создает центр IoT в ценовую категорию Free hello.</span><span class="sxs-lookup"><span data-stu-id="144d9-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="144d9-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="144d9-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="144d9-134">имя вашего центра IoT Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="144d9-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="144d9-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="144d9-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="144d9-136">Регистрация платы Arduino в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="144d9-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="144d9-137">Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="144d9-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="144d9-138">Зарегистрируйте плату Arduino в Центре Интернета вещей, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="144d9-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="144d9-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="144d9-139">Summary</span></span>
<span data-ttu-id="144d9-140">Вы создали Центр Интернета вещей и зарегистрировали в этом центре плату Arduino с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="144d9-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="144d9-141">Вы готовы toolearn способ toosend сообщений из вашего центра IoT Arduino tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="144d9-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="144d9-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="144d9-142">Next steps</span></span>
<span data-ttu-id="144d9-143">[Создание приложения Azure функции и центра IoT tooprocess и хранилище учетной записи хранилища Azure сообщения][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="144d9-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md