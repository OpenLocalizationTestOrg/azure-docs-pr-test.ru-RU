---
featureFlags: usabilla
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 2. Регистрация устройства | Документация Майкрософт"
description: "Создание группы ресурсов и Центра Интернета вещей Azure, а также регистрация устройства Pi в реестре удостоверений Центра Интернета вещей с помощью Azure CLI."
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="b0ad1-104">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b0ad1-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b0ad1-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="b0ad1-105">What you will do</span></span>
* <span data-ttu-id="b0ad1-106">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-106">Create a resource group.</span></span>
* <span data-ttu-id="b0ad1-107">Создайте Центр Интернета вещей Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="b0ad1-108">Добавьте устройство Raspberry Pi 3 в Центр Интернета вещей Azure с помощью интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="b0ad1-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="b0ad1-109">При использовании интерфейса командной строки Azure для добавления Pi в Центр Интернета вещей служба создает ключ для устройства Pi, что выполнить в службе его аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="b0ad1-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b0ad1-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b0ad1-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="b0ad1-111">What you will learn</span></span>
<span data-ttu-id="b0ad1-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-112">In this article, you will learn:</span></span>
* <span data-ttu-id="b0ad1-113">Как использовать интерфейс командной строки Azure для создания Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="b0ad1-114">Как создать удостоверение устройства для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b0ad1-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="b0ad1-115">What you need</span></span>
* <span data-ttu-id="b0ad1-116">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-116">An Azure account</span></span>
* <span data-ttu-id="b0ad1-117">Компьютер под управлением Mac или Windows с установленным интерфейсом командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="b0ad1-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b0ad1-118">Create your IoT hub</span></span>
<span data-ttu-id="b0ad1-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="b0ad1-120">Выполните следующие действия, чтобы создать Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="b0ad1-121">Войдите в свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="b0ad1-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="b0ad1-123">Укажите подписку, которую необходимо использовать по умолчанию, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="b0ad1-124">Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="b0ad1-125">Зарегистрируйте поставщик с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-125">Register the provider by running the following command.</span></span> <span data-ttu-id="b0ad1-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="b0ad1-127">Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="b0ad1-128">Создайте группу ресурсов с именем iot-sample в западном регионе США, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="b0ad1-129">`westus` — это расположение, в котором создается группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="b0ad1-130">Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="b0ad1-131">Создайте Центр Интернета вещей в группе ресурсов iot-sample, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="b0ad1-132">По умолчанию создается Центр Интернета вещей уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="b0ad1-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="b0ad1-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="b0ad1-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="b0ad1-134">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="b0ad1-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="b0ad1-136">Регистрация устройства Pi в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b0ad1-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="b0ad1-137">Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="b0ad1-138">Регистрация устройства Pi и создание самозаверяющего сертификата X.509 для аутентификации устройства выполняется с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="b0ad1-139">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0ad1-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="b0ad1-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="b0ad1-140">Summary</span></span>
<span data-ttu-id="b0ad1-141">Вы создали Центр Интернета вещей и зарегистрировали в этом центре устройство Pi с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="b0ad1-142">Теперь можно перейти к отправке сообщений с устройства Pi в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b0ad1-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0ad1-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0ad1-143">Next steps</span></span>
<span data-ttu-id="b0ad1-144">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) (Создание приложения-функции Azure и учетной записи хранения Azure для обработки и хранения сообщений Центра Интернета вещей).</span><span class="sxs-lookup"><span data-stu-id="b0ad1-144">[Create an Azure function app and an Azure storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)</span></span>

