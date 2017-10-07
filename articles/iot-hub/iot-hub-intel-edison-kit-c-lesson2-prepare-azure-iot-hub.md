---
title: "Connect Intel Edison (C) tooAzure IoT — Lesson 2: регистрации устройства | Документы Microsoft"
description: "Создание группы ресурсов, создать центр Azure IoT и зарегистрируйте Edison в центр Azure IoT hello с помощью hello Azure CLI."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="2fc3b-103">Создание Центра Интернета вещей и регистрация Intel Edison</span><span class="sxs-lookup"><span data-stu-id="2fc3b-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2fc3b-104">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="2fc3b-104">What you will do</span></span>
* <span data-ttu-id="2fc3b-105">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-105">Create a resource group.</span></span>
* <span data-ttu-id="2fc3b-106">Создайте концентратор Azure IoT в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="2fc3b-107">Центр Azure IoT toohello Intel Edison добавьте с помощью hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="2fc3b-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="2fc3b-108">При использовании hello Azure CLI tooadd центр IoT tooyour Edison hello службы создает ключ для tooauthenticate Edison со службой hello.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="2fc3b-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2fc3b-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2fc3b-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="2fc3b-110">What you will learn</span></span>
<span data-ttu-id="2fc3b-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-111">In this article, you will learn:</span></span>
* <span data-ttu-id="2fc3b-112">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="2fc3b-113">Как toocreate удостоверение устройства для Edison в ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2fc3b-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="2fc3b-114">What you need</span></span>
* <span data-ttu-id="2fc3b-115">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-115">An Azure account.</span></span> <span data-ttu-id="2fc3b-116">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="2fc3b-117">Необходимо иметь hello установлен Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="2fc3b-118">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="2fc3b-118">Create your IoT hub</span></span>
<span data-ttu-id="2fc3b-119">Центр Интернета вещей Azure позволяет подключать и отслеживать миллионы ресурсов Интернета вещей и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="2fc3b-120">toocreate концентратор IoT, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="2fc3b-121">Войдите в tooyour учетная запись Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="2fc3b-122">После входа отобразится список всех доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="2fc3b-123">Установить подписку по умолчанию hello требуется toouse, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="2fc3b-124">`subscription ID or name`можно найти в выходных данных hello hello `az login` или hello `az account list` команды.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="2fc3b-125">Регистрация поставщика hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="2fc3b-126">Поставщики ресурсов — это службы, предоставляющие ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="2fc3b-127">Перед развертыванием hello ресурс Azure, который hello предложения поставщика необходимо зарегистрировать поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="2fc3b-128">Создайте группу ресурсов с именем iot образца в области hello Запад США, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="2fc3b-129">`westus`— местоположение hello, создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="2fc3b-130">Если требуется toouse другое расположение, можно запустить `az account list-locations -o table` toosee все hello Azure поддерживает расположений.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="2fc3b-131">Создаете центр IoT в группе ресурсов iot образец hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="2fc3b-132">По умолчанию hello средство создает центр IoT в ценовую категорию Free hello.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="2fc3b-133">Дополнительные сведения см. на странице [Центр Интернета вещей Azure — Цены](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="2fc3b-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="2fc3b-134">имя вашего центра IoT Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="2fc3b-135">В подписке Azure можно создать только один выпуск Центра Интернета вещей категории F1.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="2fc3b-136">Регистрация устройства Edison в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="2fc3b-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="2fc3b-137">Каждое устройство, которое отправляет центр IoT tooyour сообщений и получает сообщения из вашего центра IoT должны быть зарегистрированы в уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="2fc3b-138">Зарегистрируйте устройство Edison в Центре Интернета вещей, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2fc3b-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="2fc3b-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="2fc3b-139">Summary</span></span>
<span data-ttu-id="2fc3b-140">Вы создали Центр Интернета вещей и зарегистрировали в нем устройство Edison с идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="2fc3b-141">Теперь вы готовы toolearn как toosend сообщений из центра IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="2fc3b-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fc3b-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fc3b-142">Next steps</span></span>
<span data-ttu-id="2fc3b-143">[Создание приложения Azure функции и центра IoT tooprocess и хранилище учетной записи хранилища Azure сообщения][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="2fc3b-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md