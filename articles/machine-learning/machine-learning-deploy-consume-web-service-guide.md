---
title: "Развертывание и использование веб-служб машинного обучения Azure | Документация Майкрософт"
description: "Ресурсы для развертывания и использования веб-служб."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="e25a1-103">Развертывание и использование веб-служб Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e25a1-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="e25a1-104">Рабочие процессы машинного обучения toodeploy машинного обучения Azure и модели можно использовать как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e25a1-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="e25a1-105">Эти веб-службы затем можно использовать toocall hello машинного обучения моделей из приложений через hello Internet toodo прогнозов в реальном времени или в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="e25a1-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="e25a1-106">Поскольку категории RESTful hello веб-служб, их можно вызывать из различных языков программирования и платформах, например .NET и Java и из приложений, таких как Excel.</span><span class="sxs-lookup"><span data-stu-id="e25a1-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="e25a1-107">Hello далее разделах содержатся ссылки toowalkthroughs, кода и документации toohelp приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="e25a1-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="e25a1-108">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="e25a1-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="e25a1-109">С помощью Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e25a1-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="e25a1-110">Портал веб-службы Microsoft Azure Machine Learning hello и студии машинного обучения поможет вам развернуть и управлять веб-службы без написания кода.</span><span class="sxs-lookup"><span data-stu-id="e25a1-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="e25a1-111">Hello следующие ссылки предоставляют общие сведения о том, как toodeploy веб-службу:</span><span class="sxs-lookup"><span data-stu-id="e25a1-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="e25a1-112">Общие сведения о том, как toodeploy новую веб-службу, которая основана на Azure Resource Manager отображается [развернуть веб-службу](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e25a1-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="e25a1-113">Пошаговые инструкции о том, как toodeploy веб-службы, в разделе [развертывания веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e25a1-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="e25a1-114">Полное Пошаговое руководство о том, как toocreate и развернуть веб-службы см. в разделе [шаг 1 пошагового руководства: Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="e25a1-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="e25a1-115">Конкретные примеры развертывания веб-службы см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e25a1-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="e25a1-116">Пошаговое руководство шаг 5: Развертывание веб-службы машинного обучения Azure hello</span><span class="sxs-lookup"><span data-stu-id="e25a1-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="e25a1-117">Как toodeploy веб-сайт службы toomultiple областей</span><span class="sxs-lookup"><span data-stu-id="e25a1-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="e25a1-118">С помощью интерфейсов API поставщика ресурсов веб-служб (интерфейсов API Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e25a1-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="e25a1-119">поставщик ресурсов Hello машинного обучения Azure для веб-служб обеспечивает развертывания и управления веб-служб с помощью вызовов REST API.</span><span class="sxs-lookup"><span data-stu-id="e25a1-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="e25a1-120">Дополнительные сведения см. в статье [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) (Веб-служба машинного обучения (REST)).</span><span class="sxs-lookup"><span data-stu-id="e25a1-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="e25a1-121">С помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25a1-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="e25a1-122">Поставщик ресурсов Машинного обучения Azure для веб-служб позволяет развертывать веб-службы и управлять ими с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e25a1-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="e25a1-123">командлеты hello toouse, необходимо сначала войти в учетную запись Azure из среды PowerShell hello tooyour с помощью hello [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="e25a1-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="e25a1-124">Если вы не знакомы с как toocall PowerShell команды основаны на диспетчера ресурсов см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="e25a1-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="e25a1-125">tooexport вашей прогнозной поэкспериментировать, используйте [этот пример кода](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="e25a1-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="e25a1-126">После создания файла .exe hello из кода hello, можно ввести:</span><span class="sxs-lookup"><span data-stu-id="e25a1-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="e25a1-127">Запуск приложения hello создает JSON шаблона веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e25a1-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="e25a1-128">шаблон toodeploy hello toouse веб-службы, необходимо добавить hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e25a1-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="e25a1-129">Имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e25a1-129">Storage account name and key</span></span>

    <span data-ttu-id="e25a1-130">Имя учетной записи хранения hello и ключ можно получить из любой hello [портал Azure](https://portal.azure.com/) или hello [классический портал Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e25a1-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="e25a1-131">Идентификатор плана предложения.</span><span class="sxs-lookup"><span data-stu-id="e25a1-131">Commitment plan ID</span></span>

    <span data-ttu-id="e25a1-132">Можно получить идентификатор плана hello hello [веб-службы Azure Machine Learning](https://services.azureml.net) портала, войдя в систему и выбрать имя плана.</span><span class="sxs-lookup"><span data-stu-id="e25a1-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="e25a1-133">Добавить шаблон toohello JSON как дочерние элементы hello *свойства* узел на hello же уровня как hello *MachineLearningWorkspace* узла.</span><span class="sxs-lookup"><span data-stu-id="e25a1-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="e25a1-134">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="e25a1-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="e25a1-135">См. следующие статьи hello и образцы кода для получения дополнительных сведений:</span><span class="sxs-lookup"><span data-stu-id="e25a1-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="e25a1-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) (Командлеты Машинного обучения Azure) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="e25a1-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="e25a1-137">Пример [пошагового руководства](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="e25a1-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="e25a1-138">Использование hello веб-служб</span><span class="sxs-lookup"><span data-stu-id="e25a1-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="e25a1-139">Из hello Azure машины обучения веб-интерфейса служб (тестирования)</span><span class="sxs-lookup"><span data-stu-id="e25a1-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="e25a1-140">Можно проверить веб-службу из веб-службы Azure Machine Learning портала hello.</span><span class="sxs-lookup"><span data-stu-id="e25a1-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e25a1-141">Сюда входят тестирование службы hello запрос-ответ (RR) и интерфейсы службы пакетного выполнения (BES).</span><span class="sxs-lookup"><span data-stu-id="e25a1-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="e25a1-142">Развертывание новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="e25a1-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="e25a1-143">Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e25a1-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="e25a1-144">Пошаговое руководство шаг 5: Развертывание веб-службы машинного обучения Azure hello</span><span class="sxs-lookup"><span data-stu-id="e25a1-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="e25a1-145">Из Excel</span><span class="sxs-lookup"><span data-stu-id="e25a1-145">From Excel</span></span>
<span data-ttu-id="e25a1-146">Можно загрузить шаблон Excel, использующего hello веб-службы:</span><span class="sxs-lookup"><span data-stu-id="e25a1-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="e25a1-147">Использование веб-службы Машинного обучения Azure в Excel</span><span class="sxs-lookup"><span data-stu-id="e25a1-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="e25a1-148">Надстройка Excel для веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e25a1-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="e25a1-149">Из клиента на основе REST</span><span class="sxs-lookup"><span data-stu-id="e25a1-149">From a REST-based client</span></span>
<span data-ttu-id="e25a1-150">Веб-службы Машинного обучения Azure представляют собой интерфейсы API RESTful.</span><span class="sxs-lookup"><span data-stu-id="e25a1-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="e25a1-151">Можно использовать эти API-интерфейсы из различных платформ, таких как .NET, Python, R, Java, т. д. hello **использование** страницы веб-службы на hello [портал веб-службы Microsoft Azure Machine Learning](https://services.azureml.net) образец код, который поможет вам приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="e25a1-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="e25a1-152">Дополнительные сведения см. в разделе [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e25a1-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
