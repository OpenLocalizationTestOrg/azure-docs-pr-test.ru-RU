---
title: "aaaRetrain новый машинного обучения Azure веб-службы с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения моделей и обновления hello web service toouse hello вновь обученной модели в машинном обучении Azure с помощью командлетов PowerShell для управления обучения машины hello."
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
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="6fa5d-103">Обучение с помощью командлетов PowerShell для управления обучения машины hello новый диспетчер ресурсов на основе веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="6fa5d-104">При веб-службу, обучение, следует обновить hello прогнозной модели веб-служб определения tooreference hello новый обучения.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6fa5d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6fa5d-105">Prerequisites</span></span>
<span data-ttu-id="6fa5d-106">Необходимо настроить обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="6fa5d-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6fa5d-107">Hello прогнозной эксперимента необходимо развернуть как диспетчера ресурсов Azure (новая) на основе веб-службе машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="6fa5d-108">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="6fa5d-109">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="6fa5d-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="6fa5d-110">Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6fa5d-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="6fa5d-111">Этот процесс требует, что вы установили hello командлеты обучения машины Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="6fa5d-112">Установка командлетов машинного обучения hello подробнее hello [обучения командлеты Azure машины](https://msdn.microsoft.com/library/azure/mt767952.aspx) ссылку на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="6fa5d-113">Скопированный hello следующую информацию из hello переподготовки выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6fa5d-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="6fa5d-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="6fa5d-114">BaseLocation</span></span>
* <span data-ttu-id="6fa5d-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="6fa5d-115">RelativeLocation</span></span>

<span data-ttu-id="6fa5d-116">Hello выполнить действия, являются:</span><span class="sxs-lookup"><span data-stu-id="6fa5d-116">hello steps you take are:</span></span>

1. <span data-ttu-id="6fa5d-117">Войдите в tooyour учетной записи диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="6fa5d-118">Получить определение hello веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-118">Get hello web service definition</span></span>
3. <span data-ttu-id="6fa5d-119">Экспорт hello определение веб-службы как JSON</span><span class="sxs-lookup"><span data-stu-id="6fa5d-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="6fa5d-120">Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="6fa5d-121">Импортировать hello JSON в определении веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="6fa5d-122">Обновить hello веб-службы с помощью нового определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="6fa5d-123">Войдите в tooyour учетной записи диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="6fa5d-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="6fa5d-124">Необходимо сначала войти в учетную запись Azure с hello среды PowerShell, с помощью hello tooyour [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="6fa5d-125">Получить hello определение веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="6fa5d-126">Затем следует получить hello веб-службы путем вызова hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="6fa5d-127">Hello определение веб-службы имеет внутреннее представление hello обученной модели hello веб-службы и не может быть непосредственно изменен.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="6fa5d-128">Убедитесь, что при получении hello определение веб-службы для прогнозирования эксперимента и не эксперимента обучения.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="6fa5d-129">toodetermine hello группу ресурсов с именем существующей веб-службе, используйте командлет Get-AzureRmMlWebService hello без параметров toodisplay hello веб-служб в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="6fa5d-130">Найдите hello веб-службы, а затем найдите на идентификатор его web service.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="6fa5d-131">Hello имя группы ресурсов hello — hello четвертый элемент в качестве идентификатора hello сразу после hello *resourceGroups* элемента.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="6fa5d-132">В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="6fa5d-133">Кроме того toodetermine hello группу ресурсов с именем существующей веб-службы в журнал на портале веб-службы Microsoft Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="6fa5d-134">Выберите веб-службу hello.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-134">Select hello web service.</span></span> <span data-ttu-id="6fa5d-135">Имя группы ресурсов Hello — пятый элемент hello hello и URL-адрес веб-службы hello, сразу после hello *resourceGroups* элемента.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="6fa5d-136">В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="6fa5d-137">Экспорт hello определение веб-службы как JSON</span><span class="sxs-lookup"><span data-stu-id="6fa5d-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="6fa5d-138">toomodify hello определения toohello Обучение модели toouse вновь Здравствуйте обученной модели, необходимо сначала использовать hello [AzureRmMlWebService экспорта](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport командлет его tooa формат JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="6fa5d-139">Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="6fa5d-140">В средствах hello найдите hello [обученной модели], обновление hello *uri* значение в hello *locationInfo* узел с hello URI большого двоичного объекта ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="6fa5d-141">Hello URI создается путем объединения hello *BaseLocation* и hello *RelativeLocation* из вывода hello hello BES повторную вызова.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="6fa5d-142">Это обновляет hello путь tooreference hello новой обученной модели.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="6fa5d-143">Импортировать hello JSON в определении веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="6fa5d-144">Необходимо использовать hello [AzureRmMlWebService импорта](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert командлет измененного JSON-файл обратно в определение веб-службы, которые можно использовать tooupdate hello определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="6fa5d-145">Обновить hello веб-службы с помощью нового определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="6fa5d-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="6fa5d-146">Наконец, можно использовать [AzureRmMlWebService обновление](https://msdn.microsoft.com/library/azure/mt767922.aspx) hello tooupdate командлет определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="6fa5d-147">Сводка</span><span class="sxs-lookup"><span data-stu-id="6fa5d-147">Summary</span></span>
<span data-ttu-id="6fa5d-148">С помощью командлетов управления PowerShell обучения машины hello, нужно обновить hello обученной модели прогнозирования Включение сценариях, например веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="6fa5d-149">Периодическое переобучение модели с использованием новых данных.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="6fa5d-150">Распределение toocustomers модели с целью hello. Однако обучение модели hello, используя свои собственные данные.</span><span class="sxs-lookup"><span data-stu-id="6fa5d-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

