---
title: "Повторное обучение новой веб-службы машинного обучения Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как с помощью командлетов управления PowerShell для машинного обучения осуществить программное переобучение модели и обновить веб-службу так, чтобы она использовала заново обученную модель в машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="e5b7a-103">Переобучение нового экземпляра Resource Manager с помощью командлетов PowerShell для управления машинным обучением</span><span class="sxs-lookup"><span data-stu-id="e5b7a-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="e5b7a-104">При переобучении новой веб-службы следует обновить определение прогнозной веб-службы, чтобы оно ссылалось на новую обученную модель.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e5b7a-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e5b7a-105">Prerequisites</span></span>
<span data-ttu-id="e5b7a-106">Необходимо настроить обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="e5b7a-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e5b7a-107">Прогнозный эксперимент развернут в виде веб-службы машинного обучения на основе Azure Resource Manager (новой веб-службы).</span><span class="sxs-lookup"><span data-stu-id="e5b7a-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="e5b7a-108">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="e5b7a-109">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e5b7a-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e5b7a-110">Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e5b7a-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="e5b7a-111">Для этого процесса требуется установить командлеты Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="e5b7a-112">Сведения по установке командлетов службы машинного обучения Azure см. по [этой ссылке](https://msdn.microsoft.com/library/azure/mt767952.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="e5b7a-113">Вы скопировали из выходных данных переобучения следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e5b7a-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="e5b7a-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="e5b7a-114">BaseLocation</span></span>
* <span data-ttu-id="e5b7a-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="e5b7a-115">RelativeLocation</span></span>

<span data-ttu-id="e5b7a-116">Теперь необходимо выполнить следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e5b7a-116">The steps you take are:</span></span>

1. <span data-ttu-id="e5b7a-117">Войти в учетную запись Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="e5b7a-118">Получить определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-118">Get the web service definition</span></span>
3. <span data-ttu-id="e5b7a-119">Экспортировать определение веб-службы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="e5b7a-120">Обновить ссылку на большой двоичный объект ilearner в JSON.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="e5b7a-121">Импортировать JSON в определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="e5b7a-122">Обновить веб-службу с помощью нового определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="e5b7a-123">Вход в учетную запись Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e5b7a-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="e5b7a-124">Сначала войдите в учетную запись Azure в среде PowerShell с помощью командлета [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e5b7a-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="e5b7a-125">Получить определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-125">Get the Web Service Definition</span></span>
<span data-ttu-id="e5b7a-126">Затем получите сведения о веб-службе, вызвав командлет [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e5b7a-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="e5b7a-127">Определение веб-службы — это внутреннее представление обученной модели веб-службы, которое нельзя изменить напрямую.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="e5b7a-128">Убедитесь, что извлекается определение веб-службы для прогнозного, а не обучающего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="e5b7a-129">Для определения имени группы ресурсов существующей веб-службы выполните командлет Get-AzureRmMlWebService без каких-либо параметров, чтобы отобразились веб-службы в подписке.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="e5b7a-130">Найдите необходимую веб-службу и посмотрите ее идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="e5b7a-131">Имя группы ресурсов — это четвертый элемент в идентификаторе, который следует сразу за элементом *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="e5b7a-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="e5b7a-132">В следующем примере имя группы ресурсов — Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="e5b7a-133">Кроме того, для определения имени группы ресурсов существующей веб-службы можно войти на портал веб-служб Машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e5b7a-134">Затем выбрать веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-134">Select the web service.</span></span> <span data-ttu-id="e5b7a-135">Имя группы ресурсов — это пятый элемент в URL-адресе веб-службы, который следует сразу за элементом *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="e5b7a-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="e5b7a-136">В следующем примере имя группы ресурсов — Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="e5b7a-137">Экспортировать определение веб-службы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="e5b7a-138">Чтобы изменить определение обученной модели для использования новой обученной модели, необходимо сначала воспользоваться командлетом [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) и экспортировать его в файл в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="e5b7a-139">Обновить ссылку на большой двоичный объект ilearner в JSON.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="e5b7a-140">В ресурсах-контейнерах найдите элемент [trained model], обновите значение *uri* в узле *locationInfo*, заменив его универсальным кодом ресурса (URI) BLOB-объекта ilearner.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="e5b7a-141">URI формируется в результате объединения параметров *BaseLocation* и *RelativeLocation* из выходных данных вызова переобучения BES.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="e5b7a-142">При этом обновляется путь к новой обученной модели.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="e5b7a-143">Импортировать JSON в определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="e5b7a-144">Воспользуйтесь командлетом [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) для преобразования измененного JSON-файла обратно в определение веб-службы, которое можно использовать для обновления определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="e5b7a-145">Обновить веб-службу с помощью нового определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="e5b7a-146">Наконец, воспользуйтесь командлетом [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) для обновления определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="e5b7a-147">Сводка</span><span class="sxs-lookup"><span data-stu-id="e5b7a-147">Summary</span></span>
<span data-ttu-id="e5b7a-148">С помощью командлетов управления PowerShell Машинного обучения можно обновить обученную модель прогнозной веб-службы, что позволяет выполнять следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="e5b7a-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="e5b7a-149">Периодическое переобучение модели с использованием новых данных.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="e5b7a-150">Распределение модели клиентам, чтобы они могли переобучить ее с использованием собственных данных.</span><span class="sxs-lookup"><span data-stu-id="e5b7a-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

