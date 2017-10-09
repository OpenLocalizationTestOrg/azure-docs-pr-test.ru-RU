---
title: "aaaCreate центр IoT с помощью Azure CLI (azure.js) | Документы Microsoft"
description: "Как toocreate концентратора Azure IoT с помощью hello кросс платформенных Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="d40fe-103">Создать центр IoT с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d40fe-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="d40fe-104">Введение</span><span class="sxs-lookup"><span data-stu-id="d40fe-104">Introduction</span></span>

<span data-ttu-id="d40fe-105">Можно использовать toocreate Azure CLI (azure.js) и программно управлять центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d40fe-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="d40fe-106">В этой статье показано, как toouse hello Azure CLI (azure.js) toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d40fe-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="d40fe-107">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="d40fe-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="d40fe-108">Azure CLI (azure.js) — hello CLI для классического hello и моделями развертывания ресурсов управления как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d40fe-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="d40fe-109">[2.0 Azure CLI (az.py)](iot-hub-create-using-cli.md) -hello следующего поколения CLI для модели развертывания hello ресурса управления.</span><span class="sxs-lookup"><span data-stu-id="d40fe-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="d40fe-110">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d40fe-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d40fe-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d40fe-111">An active Azure account.</span></span> <span data-ttu-id="d40fe-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d40fe-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d40fe-113">[Интерфейс командной строки Azure 0.10.4][lnk-CLI-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d40fe-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="d40fe-114">Если уже hello Azure CLI установлен, можно проверить hello текущей версии hello командной строки с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d40fe-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="d40fe-115">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d40fe-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d40fe-116">Hello Azure CLI должен находиться в режиме диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="d40fe-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="d40fe-117">Настройка учетной записи и подписки Azure</span><span class="sxs-lookup"><span data-stu-id="d40fe-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="d40fe-118">В командной строке hello входа, введя следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="d40fe-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="d40fe-119">Используйте hello предлагаемые веб-браузер и tooauthenticate кода.</span><span class="sxs-lookup"><span data-stu-id="d40fe-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="d40fe-120">Если у вас несколько подписок Azure, подключение tooAzure предоставляет вам доступ tooall hello подписок Azure, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="d40fe-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="d40fe-121">Можно просмотреть hello подписок Azure и определить, какой из них по умолчанию hello, с помощью команды hello:</span><span class="sxs-lookup"><span data-stu-id="d40fe-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="d40fe-122">контекст hello подписки tooset из которой требуется rest hello toorun hello команд с помощью:</span><span class="sxs-lookup"><span data-stu-id="d40fe-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="d40fe-123">Создайте группу ресурсов с именем **exampleResourceGroup**, если она не создана:</span><span class="sxs-lookup"><span data-stu-id="d40fe-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="d40fe-124">статья Hello [использовать toomanage Azure CLI hello Azure ресурсов и групп ресурсов] [ lnk-CLI-arm] предоставляет дополнительные сведения о том, как toouse hello Azure CLI toomanage Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d40fe-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="d40fe-125">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="d40fe-125">Create an IoT Hub</span></span>

<span data-ttu-id="d40fe-126">Ниже перечислены необходимые параметры:</span><span class="sxs-lookup"><span data-stu-id="d40fe-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="d40fe-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="d40fe-127">**resource-group**.</span></span> <span data-ttu-id="d40fe-128">Имя группы ресурсов Hello.</span><span class="sxs-lookup"><span data-stu-id="d40fe-128">hello resource group name.</span></span> <span data-ttu-id="d40fe-129">Формат Hello — без учета регистра алфавитно-цифровой символ подчеркивания и дефиса, длина 1-64.</span><span class="sxs-lookup"><span data-stu-id="d40fe-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="d40fe-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="d40fe-130">**name**.</span></span> <span data-ttu-id="d40fe-131">Имя Hello hello IoT hub toobe создан.</span><span class="sxs-lookup"><span data-stu-id="d40fe-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="d40fe-132">Формат Hello — без учета регистра алфавитно-цифровой символ подчеркивания и дефиса, длиной 3 50.</span><span class="sxs-lookup"><span data-stu-id="d40fe-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="d40fe-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="d40fe-133">**location**.</span></span> <span data-ttu-id="d40fe-134">Hello местоположение (регион/центра обработки данных azure) tooprovision hello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d40fe-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="d40fe-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="d40fe-135">**sku-name**.</span></span> <span data-ttu-id="d40fe-136">Имя Hello hello SKU, один из: [F1, S1, S2 и S3].</span><span class="sxs-lookup"><span data-stu-id="d40fe-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="d40fe-137">См. последний полный список hello, toohello странице цен для центра IoT.</span><span class="sxs-lookup"><span data-stu-id="d40fe-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="d40fe-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="d40fe-138">**units**.</span></span> <span data-ttu-id="d40fe-139">Hello число подготовленных единиц.</span><span class="sxs-lookup"><span data-stu-id="d40fe-139">hello number of provisioned units.</span></span> <span data-ttu-id="d40fe-140">Диапазон: F1 [1]; S1, S2 [1–200]; S3 [1–10].</span><span class="sxs-lookup"><span data-stu-id="d40fe-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="d40fe-141">Единицы центра IoT основаны на общее число сообщений номер count и hello устройств будет tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d40fe-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="d40fe-142">toosee все Здравствуйте, параметры, доступные для создания, можно использовать команду hello справки в командной строке:</span><span class="sxs-lookup"><span data-stu-id="d40fe-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="d40fe-143">Краткий пример: вызывается центра IoT toocreate **exampleIoTHubName** в группе ресурсов hello **exampleResourceGroup**, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d40fe-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="d40fe-144">Эта команда интерфейса командной строки Azure создает стандартный центр Интернета вещей S1, за который взимается плата.</span><span class="sxs-lookup"><span data-stu-id="d40fe-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="d40fe-145">Вы можете удалить центр IoT hello **exampleIoTHubName** , используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d40fe-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="d40fe-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d40fe-146">Next steps</span></span>

<span data-ttu-id="d40fe-147">toolearn Дополнительные сведения о разработке приложений для центра IoT см. в следующей статьей hello:</span><span class="sxs-lookup"><span data-stu-id="d40fe-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="d40fe-148">[Пакеты SDK для Центра Интернета вещей][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="d40fe-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="d40fe-149">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="d40fe-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d40fe-150">[С помощью hello Azure портала toomanage центра IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="d40fe-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
