---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 2. Регистрация устройства | Документация Майкрософт"
description: "Создайте группу ресурсов и Центр Интернета вещей Azure, а также зарегистрируйте в нем устройство Edison с помощью Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="f030d-103">Создание Центра Интернета вещей и регистрация Intel Edison</span><span class="sxs-lookup"><span data-stu-id="f030d-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f030d-104">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f030d-104">What you will do</span></span>
* <span data-ttu-id="f030d-105">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f030d-105">Create a resource group.</span></span>
* <span data-ttu-id="f030d-106">Создайте Центр Интернета вещей Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f030d-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="f030d-107">Добавьте устройство Intel Edison в Центр Интернета вещей Azure с помощью интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f030d-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="f030d-108">При использовании Azure CLI для добавления устройства Edison в Центр Интернета вещей служба создает ключ для устройства Edison, чтобы аутентифицировать его в службе.</span><span class="sxs-lookup"><span data-stu-id="f030d-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="f030d-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f030d-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f030d-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f030d-110">What you will learn</span></span>
<span data-ttu-id="f030d-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f030d-111">In this article, you will learn:</span></span>
* <span data-ttu-id="f030d-112">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f030d-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="f030d-113">Как создать удостоверения устройства для устройства Edison в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f030d-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f030d-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f030d-114">What you need</span></span>
* <span data-ttu-id="f030d-115">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f030d-115">An Azure account.</span></span> <span data-ttu-id="f030d-116">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f030d-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="f030d-117">У вас должен быть установлен Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f030d-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="f030d-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f030d-118">Create your IoT hub</span></span>
<span data-ttu-id="f030d-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="f030d-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="f030d-120">Выполните следующие действия, чтобы создать Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="f030d-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="f030d-121">Войдите в свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f030d-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="f030d-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="f030d-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="f030d-123">Укажите подписку, которую необходимо использовать по умолчанию, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f030d-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="f030d-124">Значение `subscription ID or name` можно найти в выходных данных команды `az login` или `az account list`.</span><span class="sxs-lookup"><span data-stu-id="f030d-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="f030d-125">Зарегистрируйте поставщик с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="f030d-125">Register the provider by running the following command.</span></span> <span data-ttu-id="f030d-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="f030d-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="f030d-127">Поставщик следует регистрировать перед развертыванием ресурса Azure, предлагаемого поставщиком.</span><span class="sxs-lookup"><span data-stu-id="f030d-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="f030d-128">Создайте группу ресурсов с именем iot-sample в западном регионе США, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f030d-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="f030d-129">`westus` — это расположение, в котором создается группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f030d-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="f030d-130">Чтобы использовать другое расположение, выполните команду `az account list-locations -o table` и просмотрите все расположения, поддерживаемые Azure.</span><span class="sxs-lookup"><span data-stu-id="f030d-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="f030d-131">Создайте Центр Интернета вещей в группе ресурсов iot-sample, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f030d-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="f030d-132">По умолчанию создается Центр Интернета вещей уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="f030d-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="f030d-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="f030d-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="f030d-134">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="f030d-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="f030d-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="f030d-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="f030d-136">Регистрация устройства Edison в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f030d-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="f030d-137">Каждое устройство, которое отправляет сообщения в ваш Центр Интернета вещей и получает сообщения из него, должно быть зарегистрировано с использованием уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="f030d-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="f030d-138">Зарегистрируйте устройство Edison в Центре Интернета вещей, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f030d-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="f030d-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="f030d-139">Summary</span></span>
<span data-ttu-id="f030d-140">Вы создали Центр Интернета вещей и зарегистрировали в нем устройство Edison с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="f030d-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="f030d-141">Теперь можно перейти к отправке сообщений с устройства Edison в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f030d-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f030d-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f030d-142">Next steps</span></span>
<span data-ttu-id="f030d-143">[Создание приложения-функции Azure и учетной записи хранения Azure][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="f030d-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md