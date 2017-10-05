---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 2. Регистрация устройства | Документация Майкрософт"
description: "Создание группы ресурсов и Центра Интернета вещей Azure, а также регистрация устройства Pi в Центре Интернета вещей Azure с помощью Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облако raspberry pi, облачное подключение pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="418f0-104">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="418f0-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="418f0-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="418f0-105">What you will do</span></span>
* <span data-ttu-id="418f0-106">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="418f0-106">Create a resource group.</span></span>
* <span data-ttu-id="418f0-107">Создайте Центр Интернета вещей Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="418f0-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="418f0-108">Добавьте устройство Raspberry Pi 3 в Центр Интернета вещей Azure с помощью интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="418f0-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="418f0-109">При использовании Azure CLI для добавления Pi в Центр Интернета вещей служба создает ключ для устройства Pi, чтобы выполнить в службе его аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="418f0-109">When you use the Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="418f0-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="418f0-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="418f0-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="418f0-111">What you will learn</span></span>
<span data-ttu-id="418f0-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="418f0-112">In this article, you will learn:</span></span>
* <span data-ttu-id="418f0-113">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="418f0-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="418f0-114">Создание удостоверения устройства для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="418f0-114">How to create a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="418f0-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="418f0-115">What you need</span></span>
* <span data-ttu-id="418f0-116">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="418f0-116">An Azure account</span></span>
* <span data-ttu-id="418f0-117">Компьютер под управлением Mac или Windows с установленным интерфейсом командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="418f0-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="418f0-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="418f0-118">Create your IoT hub</span></span>
<span data-ttu-id="418f0-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="418f0-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="418f0-120">Выполните следующие действия, чтобы создать Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="418f0-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="418f0-121">Войдите в свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="418f0-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="418f0-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="418f0-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="418f0-123">Укажите подписку, которую необходимо использовать по умолчанию, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="418f0-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="418f0-124">Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.</span><span class="sxs-lookup"><span data-stu-id="418f0-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="418f0-125">Зарегистрируйте поставщик с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="418f0-125">Register the provider by running the following command.</span></span> <span data-ttu-id="418f0-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="418f0-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="418f0-127">Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.</span><span class="sxs-lookup"><span data-stu-id="418f0-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="418f0-128">Создайте группу ресурсов с именем iot-sample в западном регионе США, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="418f0-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="418f0-129">`westus` — это расположение, в котором создается группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="418f0-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="418f0-130">Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.</span><span class="sxs-lookup"><span data-stu-id="418f0-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="418f0-131">Создайте Центр Интернета вещей в группе ресурсов iot-sample, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="418f0-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="418f0-132">По умолчанию создается Центр Интернета вещей уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="418f0-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="418f0-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="418f0-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="418f0-134">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="418f0-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="418f0-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="418f0-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="418f0-136">Регистрация устройства Pi в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="418f0-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="418f0-137">Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="418f0-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="418f0-138">Зарегистрируйте устройство Pi в центре, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="418f0-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="418f0-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="418f0-139">Summary</span></span>
<span data-ttu-id="418f0-140">Вы создали Центр Интернета вещей и зарегистрировали в этом центре устройство Pi с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="418f0-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="418f0-141">Теперь можно перейти к отправке сообщений с устройства Pi в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="418f0-141">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="418f0-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="418f0-142">Next steps</span></span>
<span data-ttu-id="418f0-143">[Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="418f0-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

