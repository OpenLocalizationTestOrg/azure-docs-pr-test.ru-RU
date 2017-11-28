---
title: "aaaCreate внутренний балансировщик нагрузки - шаблон Azure | Документы Microsoft"
description: "Узнайте, как в диспетчере ресурсов с помощью шаблона подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="9b272-103">Создайте внутренний балансировщик нагрузки с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="9b272-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b272-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="9b272-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="9b272-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b272-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="9b272-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="9b272-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="9b272-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="9b272-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9b272-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9b272-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9b272-109">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9b272-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="9b272-110">Развертывание с помощью шаблона hello щелкните toodeploy</span><span class="sxs-lookup"><span data-stu-id="9b272-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="9b272-111">шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="9b272-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="9b272-112">toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello при необходимости и следуйте инструкциям hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="9b272-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="9b272-113">Развертывание hello шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b272-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="9b272-114">toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9b272-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="9b272-115">Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="9b272-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="9b272-116">Загрузите локальном диске файл параметров tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="9b272-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="9b272-117">Измените файл hello и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="9b272-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="9b272-118">Запустите hello **New AzureRmResourceGroupDeployment** Здравствуйте, командлет toocreate группы ресурсов с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="9b272-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="9b272-119">Развертывание hello шаблона с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b272-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="9b272-120">toodeploy hello шаблона с использованием hello Azure CLI, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9b272-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="9b272-121">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="9b272-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="9b272-122">Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9b272-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="9b272-123">Вот hello ожидается выходных данных для приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="9b272-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="9b272-124">Откройте файл параметров hello, выберите его содержимое и сохраните файл tooa на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9b272-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="9b272-125">В этом примере мы сохранить файл параметров hello слишком*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="9b272-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="9b272-126">Запустите hello **создайте группу azure развертывания** toodeploy hello новый внутренней подсистемы балансировки нагрузки с помощью шаблонов hello и параметров команды файлы вы загрузили и изменить выше.</span><span class="sxs-lookup"><span data-stu-id="9b272-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="9b272-127">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="9b272-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="9b272-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b272-128">Next steps</span></span>

[<span data-ttu-id="9b272-129">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="9b272-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9b272-130">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="9b272-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

