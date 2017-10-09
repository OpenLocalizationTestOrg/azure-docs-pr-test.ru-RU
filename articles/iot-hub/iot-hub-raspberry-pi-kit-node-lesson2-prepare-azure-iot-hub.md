---
featureFlags: usabilla
title: "Подключения Raspberry Pi (узел) tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрировать Pi в hello центра IoT реестра удостоверений с помощью Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облако raspberry pi, облачное подключение pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="1cb61-104">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1cb61-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1cb61-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="1cb61-105">What you will do</span></span>
* <span data-ttu-id="1cb61-106">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1cb61-106">Create a resource group.</span></span>
* <span data-ttu-id="1cb61-107">Создайте концентратор Azure IoT в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="1cb61-108">Добавление центра Azure IoT toohello Raspberry Pi 3 с помощью hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="1cb61-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="1cb61-109">При использовании центра IoT tooyour Pi tooadd Azure CLI hello службы создает ключ для tooauthenticate Pi со службой hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="1cb61-110">Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1cb61-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1cb61-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="1cb61-111">What you will learn</span></span>
<span data-ttu-id="1cb61-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="1cb61-112">In this article, you will learn:</span></span>
* <span data-ttu-id="1cb61-113">Как Azure CLI toouse toocreate центра IoT</span><span class="sxs-lookup"><span data-stu-id="1cb61-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="1cb61-114">Как toocreate удостоверение устройства пи в концентратор IoT</span><span class="sxs-lookup"><span data-stu-id="1cb61-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1cb61-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="1cb61-115">What you need</span></span>
* <span data-ttu-id="1cb61-116">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb61-116">An Azure account</span></span>
* <span data-ttu-id="1cb61-117">Установить Mac и Windows с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1cb61-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="1cb61-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="1cb61-118">Create your IoT hub</span></span>
<span data-ttu-id="1cb61-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="1cb61-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="1cb61-120">toocreate концентратор IoT, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1cb61-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="1cb61-121">Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1cb61-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="1cb61-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb61-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="1cb61-123">Установить подписку по умолчанию hello требуется toouse, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1cb61-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="1cb61-124">`subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.</span><span class="sxs-lookup"><span data-stu-id="1cb61-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="1cb61-125">Регистрация поставщика hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="1cb61-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="1cb61-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="1cb61-127">Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="1cb61-128">Создайте группу ресурсов с именем iot образца в области hello Запад США, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1cb61-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="1cb61-129">`westus`— местоположение hello, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1cb61-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="1cb61-130">Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.</span><span class="sxs-lookup"><span data-stu-id="1cb61-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="1cb61-131">Создаете центр IoT в группе ресурсов iot образец hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1cb61-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="1cb61-132">По умолчанию hello средство создает центр IoT в ценовую категорию Free hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="1cb61-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="1cb61-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="1cb61-134">имя вашего центра IoT Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="1cb61-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="1cb61-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="1cb61-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="1cb61-136">Регистрация устройства Pi в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="1cb61-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="1cb61-137">Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1cb61-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="1cb61-138">Будет использоваться на Pi tooregister Azure CLI и создать самозаверяющий сертификат X.509 для проверки подлинности устройства.</span><span class="sxs-lookup"><span data-stu-id="1cb61-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="1cb61-139">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="1cb61-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="1cb61-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="1cb61-140">Summary</span></span>
<span data-ttu-id="1cb61-141">Вы создали Центр Интернета вещей и зарегистрировали в этом центре устройство Pi с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="1cb61-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="1cb61-142">Теперь вы готовы toolearn как toosend сообщений из центра IoT tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="1cb61-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cb61-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1cb61-143">Next steps</span></span>
[<span data-ttu-id="1cb61-144">Создание приложения Azure функции и tooprocess учетной записи хранилища Azure и хранения сообщений концентратора IoT</span><span class="sxs-lookup"><span data-stu-id="1cb61-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

