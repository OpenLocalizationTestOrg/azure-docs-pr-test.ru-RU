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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="0e3aa-103">Развертывание и использование веб-служб Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="0e3aa-104">Машинное обучение Azure позволяет развертывать рабочие процессы и модели машинного обучения в качестве веб-служб.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="0e3aa-105">Затем эти веб-службы можно использовать для вызова моделей машинного обучения из приложений в Интернете, чтобы делать прогнозы в режиме реального времени или в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="0e3aa-106">Так как это веб-службы RESTful, их можно вызывать, используя различные языки программирования и платформы, например .NET и Java, а также приложения, например Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="0e3aa-107">В следующих разделах представлены ссылки на пошаговые инструкции, код и документацию, которые помогут вам приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="0e3aa-108">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="0e3aa-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="0e3aa-109">С помощью Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="0e3aa-110">На портале Студии машинного обучения и веб-служб Машинного обучения Microsoft Azure можно развернуть веб-службы, а также управлять ими без написания кода.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="0e3aa-111">В статьях по следующим ссылкам содержатся общие сведения о процессе развертывания новой веб-службы:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="0e3aa-112">Общие сведения о развертывании новой веб-службы на основе Azure Resource Manager см. в статье [Развертывание новой веб-службы](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="0e3aa-113">Пошаговое руководство по развертыванию веб-службы см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="0e3aa-114">Полное пошаговое руководство по созданию и развертыванию веб-службы см. в статье [Шаг 1. Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="0e3aa-115">Конкретные примеры развертывания веб-службы см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="0e3aa-116">Шаг 5. Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="0e3aa-117">Развертывание веб-службы в нескольких регионах</span><span class="sxs-lookup"><span data-stu-id="0e3aa-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="0e3aa-118">С помощью интерфейсов API поставщика ресурсов веб-служб (интерфейсов API Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="0e3aa-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="0e3aa-119">Поставщик ресурсов Машинного обучения Azure для веб-служб позволяет развертывать веб-службы и управлять ими с помощью вызовов REST API.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="0e3aa-120">Дополнительные сведения см. в статье [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) (Веб-служба машинного обучения (REST)).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="0e3aa-121">С помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e3aa-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="0e3aa-122">Поставщик ресурсов Машинного обучения Azure для веб-служб позволяет развертывать веб-службы и управлять ими с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="0e3aa-123">Для использования командлетов необходимо сначала войти в учетную запись Azure в среде PowerShell с помощью командлета [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="0e3aa-124">Если вы не знакомы с вызовом команд PowerShell на основе Resource Manager, см. статью [Использование Azure PowerShell с Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="0e3aa-125">Чтобы экспортировать прогнозный эксперимент, используйте [этот пример кода](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="0e3aa-126">После создания EXE-файла из кода можно ввести следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="0e3aa-127">При запуске приложения создается шаблон JSON веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="0e3aa-128">Чтобы использовать шаблон для развертывания веб-службы, необходимо добавить следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="0e3aa-129">Имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-129">Storage account name and key</span></span>

    <span data-ttu-id="0e3aa-130">Их можно получить на [портале Azure](https://portal.azure.com/) или на [классическом портале Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="0e3aa-131">Идентификатор плана предложения.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-131">Commitment plan ID</span></span>

    <span data-ttu-id="0e3aa-132">Идентификатор плана можно получить на портале [веб-служб машинного обучения Azure](https://services.azureml.net). Для этого необходимо войти на портал и щелкнуть имя плана.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="0e3aa-133">Добавьте их в шаблон JSON в качестве дочерних элементов узла *Properties* на том же уровне, где находится узел *MachineLearningWorkspace*.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="0e3aa-134">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="0e3aa-135">Дополнительные сведения см. в следующих статьях и примерах кода:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="0e3aa-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) (Командлеты Машинного обучения Azure) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="0e3aa-137">Пример [пошагового руководства](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="0e3aa-138">Использование веб-служб</span><span class="sxs-lookup"><span data-stu-id="0e3aa-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="0e3aa-139">Через пользовательский интерфейс веб-служб Машинного обучения Azure (тестирование)</span><span class="sxs-lookup"><span data-stu-id="0e3aa-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="0e3aa-140">Веб-службу можно проверить на портале веб-служб Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="0e3aa-141">Эта проверка включает в себя тестирование интерфейсов службы запрос-ответ (RRS) и службы пакетного выполнения (BES).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="0e3aa-142">Развертывание новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="0e3aa-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="0e3aa-143">Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="0e3aa-144">Шаг 5. Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="0e3aa-145">Из Excel</span><span class="sxs-lookup"><span data-stu-id="0e3aa-145">From Excel</span></span>
<span data-ttu-id="0e3aa-146">Вы можете скачать шаблон Excel, который использует веб-службу:</span><span class="sxs-lookup"><span data-stu-id="0e3aa-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="0e3aa-147">Использование веб-службы Машинного обучения Azure в Excel</span><span class="sxs-lookup"><span data-stu-id="0e3aa-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="0e3aa-148">Надстройка Excel для веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0e3aa-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="0e3aa-149">Из клиента на основе REST</span><span class="sxs-lookup"><span data-stu-id="0e3aa-149">From a REST-based client</span></span>
<span data-ttu-id="0e3aa-150">Веб-службы Машинного обучения Azure представляют собой интерфейсы API RESTful.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="0e3aa-151">Их можно использовать на различных платформах, например .NET, Python, R, Java и т. д. На странице **Consume** (Использование) для веб-службы на [портале веб-служб машинного обучения Microsoft Azure](https://services.azureml.net) размещен пример кода, позволяющий приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="0e3aa-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="0e3aa-152">Дополнительные сведения см. в статье [Как использовать веб-службу машинного обучения Azure, развернутую из эксперимента машинного обучения](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="0e3aa-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
