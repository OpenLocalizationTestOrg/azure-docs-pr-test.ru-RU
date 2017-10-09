---
title: "aaaCreate центр IoT с помощью Azure CLI (az.py) | Документы Microsoft"
description: "Как toocreate концентратора Azure IoT с помощью hello кросс платформенных Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="6ae03-103">Создать центр IoT с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="6ae03-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="6ae03-104">Введение</span><span class="sxs-lookup"><span data-stu-id="6ae03-104">Introduction</span></span>

<span data-ttu-id="6ae03-105">Можно использовать toocreate Azure CLI 2.0 (az.py) и программно управлять центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6ae03-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6ae03-106">В этой статье показано, как toouse hello Azure CLI 2.0 (az.py) toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="6ae03-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="6ae03-107">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="6ae03-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="6ae03-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) — hello CLI для hello классический и ресурсов развертывания модели управления.</span><span class="sxs-lookup"><span data-stu-id="6ae03-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="6ae03-109">Azure CLI 2.0 (az.py) - hello следующего поколения CLI для управления развертывания ресурсов hello модели, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6ae03-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="6ae03-110">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6ae03-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6ae03-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6ae03-111">An active Azure account.</span></span> <span data-ttu-id="6ae03-112">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6ae03-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6ae03-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="6ae03-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="6ae03-114">Выполнение входа и установка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="6ae03-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="6ae03-115">Войдите в tooyour учетная запись Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="6ae03-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="6ae03-116">Hello командной строки, выполнив hello [входа команда][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="6ae03-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="6ae03-117">Выполните инструкции tooauthenticate hello, с помощью кода hello и войдите в tooyour учетная запись Azure через веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="6ae03-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="6ae03-118">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello Azure учетные записи, связанные с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="6ae03-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="6ae03-119">Используйте следующие hello [toolist команда hello учетных записей Azure] [ lnk-az-account-command] для toouse вы:</span><span class="sxs-lookup"><span data-stu-id="6ae03-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="6ae03-120">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="6ae03-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="6ae03-121">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="6ae03-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="6ae03-122">Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6ae03-122">Create an IoT Hub</span></span>

<span data-ttu-id="6ae03-123">Используйте hello Azure CLI toocreate группы ресурсов, а затем добавьте центра IoT.</span><span class="sxs-lookup"><span data-stu-id="6ae03-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="6ae03-124">Создайте Центр Интернета вещей в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6ae03-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="6ae03-125">Использовать существующую группу ресурсов, либо выполнить следующие hello [toocreate команда группу ресурсов][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="6ae03-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="6ae03-126">Hello предыдущего примера создает группы ресурсов hello в hello расположение Запад США.</span><span class="sxs-lookup"><span data-stu-id="6ae03-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="6ae03-127">Можно просмотреть список доступных расположений, выполнив команду hello `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="6ae03-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="6ae03-128">Запустите следующие hello [toocreate команда центра IoT] [ lnk-az-iot-command] в группе ресурсов, с помощью глобальное уникальное имя для вашего центра IoT:</span><span class="sxs-lookup"><span data-stu-id="6ae03-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="6ae03-129">Предыдущая команда Hello создает центр IoT в ценовой категории, для которой выставляются hello S1.</span><span class="sxs-lookup"><span data-stu-id="6ae03-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="6ae03-130">Дополнительные сведения см. на странице с [ценами на Центр Интернета вещей Azure][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="6ae03-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="6ae03-131">Удаление Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6ae03-131">Remove an IoT Hub</span></span>

<span data-ttu-id="6ae03-132">Можно также использовать hello Azure CLI[удалить конкретный ресурс][lnk-az-resource-command], например центр IoT или удалить группу ресурсов и его ресурсам, включая все центры IoT.</span><span class="sxs-lookup"><span data-stu-id="6ae03-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="6ae03-133">toodelete центр IoT запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ae03-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="6ae03-134">toodelete группу ресурсов и всех его ресурсов, выполнения hello следующих команд:</span><span class="sxs-lookup"><span data-stu-id="6ae03-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="6ae03-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ae03-135">Next steps</span></span>
<span data-ttu-id="6ae03-136">toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="6ae03-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="6ae03-137">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6ae03-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="6ae03-138">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="6ae03-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6ae03-139">[С помощью hello Azure портала toomanage центра IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="6ae03-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
