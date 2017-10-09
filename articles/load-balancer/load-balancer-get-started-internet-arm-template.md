---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет - шаблон Azure | Документы Microsoft"
description: "Узнайте, как в диспетчере ресурсов с помощью шаблона подсистемы балансировки нагрузки, toocreate из Интернета"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="b335b-103">Создание балансировщика нагрузки для Интернета с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="b335b-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b335b-104">Портал</span><span class="sxs-lookup"><span data-stu-id="b335b-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="b335b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b335b-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="b335b-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b335b-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="b335b-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="b335b-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b335b-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b335b-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="b335b-109">Вы также можете [Узнайте, как с помощью классической модели развертывания подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b335b-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="b335b-110">Развертывание с помощью шаблона hello щелкните toodeploy</span><span class="sxs-lookup"><span data-stu-id="b335b-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="b335b-111">шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="b335b-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="b335b-112">toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](http://go.microsoft.com/fwlink/?LinkId=544801), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello при необходимости и следуйте инструкциям hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="b335b-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="b335b-113">Развертывание hello шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b335b-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="b335b-114">toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b335b-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="b335b-115">Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="b335b-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="b335b-116">Запустите hello **New AzureRmResourceGroupDeployment** Здравствуйте, командлет toocreate группы ресурсов с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="b335b-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="b335b-117">Развертывание hello шаблона с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b335b-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="b335b-118">toodeploy hello шаблона с использованием hello Azure CLI, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b335b-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="b335b-119">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="b335b-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b335b-120">Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b335b-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b335b-121">Вот hello ожидается выходных данных для приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="b335b-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="b335b-122">В браузере перейдите слишком[hello шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), скопируйте содержимое hello hello json-файл и вставьте его в новый файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b335b-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="b335b-123">Для этого сценария будет копирование значений hello ниже tooa файл с именем **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="b335b-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="b335b-124">Запустите hello **создайте группу azure развертывания** командлет toodeploy hello новую подсистему балансировки загрузки с помощью шаблона hello и параметр файлы загружаются и изменить выше.</span><span class="sxs-lookup"><span data-stu-id="b335b-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="b335b-125">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="b335b-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="b335b-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b335b-126">Next steps</span></span>

[<span data-ttu-id="b335b-127">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b335b-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b335b-128">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b335b-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b335b-129">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b335b-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
