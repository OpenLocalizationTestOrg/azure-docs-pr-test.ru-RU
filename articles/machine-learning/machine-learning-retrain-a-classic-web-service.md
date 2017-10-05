---
title: "Переобучение классической веб-службы | Документация Майкрософт"
description: "Узнайте о том, как осуществить программное переобучение модели и обновить веб-службу так, чтобы она использовала переобученную модель при задействовании функций машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="8f2e4-103">Переобучение классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="8f2e4-103">Retrain a Classic web service</span></span>
<span data-ttu-id="8f2e4-104">Развернутая прогнозная веб-служба является конечной точкой оценки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="8f2e4-105">Конечные точки по умолчанию синхронизируются с исходными экспериментами по обучению и оценке, поэтому обученную модель конечной точки по умолчанию нельзя заменить.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="8f2e4-106">Чтобы переобучить веб-службу, необходимо добавить в нее новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8f2e4-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8f2e4-107">Prerequisites</span></span>
<span data-ttu-id="8f2e4-108">Вы уже настроили обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8f2e4-109">Прогнозный эксперимент развернут в виде классической веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="8f2e4-110">Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="8f2e4-111">Добавление новой конечной точки</span><span class="sxs-lookup"><span data-stu-id="8f2e4-111">Add a new Endpoint</span></span>
<span data-ttu-id="8f2e4-112">Прогнозная веб-служба, которую вы развернули, содержит конечную точку по умолчанию, синхронизированную с исходной обученной моделью обучающего и оценивающего экспериментов.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="8f2e4-113">Чтобы обновить веб-службу с помощью новой обученной модели, необходимо создать конечную точку оценки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="8f2e4-114">Чтобы создать конечную точку оценки, в прогнозной веб-службе, которую можно обновить с помощью обученной модели, выполните действия ниже.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="8f2e4-115">Важно добавить конечную точку к прогнозной веб-службе, а не к обучающей.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="8f2e4-116">Если вы правильно установили обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="8f2e4-117">Имя прогнозной веб-службы должно заканчиваться на [predictive exp.].</span><span class="sxs-lookup"><span data-stu-id="8f2e4-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="8f2e4-118">Существует три способа добавления новой конечной точки в веб-службу:</span><span class="sxs-lookup"><span data-stu-id="8f2e4-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="8f2e4-119">Программным образом</span><span class="sxs-lookup"><span data-stu-id="8f2e4-119">Programmatically</span></span>
2. <span data-ttu-id="8f2e4-120">С помощью портала веб-служб Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8f2e4-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="8f2e4-121">Использование классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="8f2e4-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="8f2e4-122">Добавление конечной точки программно</span><span class="sxs-lookup"><span data-stu-id="8f2e4-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="8f2e4-123">Конечные точки оценки можно добавить с помощью примера кода, приведенного в этом [репозитории GitHub](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="8f2e4-124">Добавление конечной точки с помощью портала веб-служб Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8f2e4-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="8f2e4-125">В Студии машинного обучения в левой области навигации щелкните "Web Services" (Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="8f2e4-126">В нижней части панели мониторинга веб-служб щелкните **Manage endpoints preview**(Управление конечными точками (предварительная версия)).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="8f2e4-127">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-127">Click **Add**.</span></span>
4. <span data-ttu-id="8f2e4-128">Введите имя и описание новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="8f2e4-129">Выберите уровень ведения журнала и укажите, включать ли образцы данных.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="8f2e4-130">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="8f2e4-131">Добавление конечной точки с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="8f2e4-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="8f2e4-132">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8f2e4-133">В меню слева щелкните **Машинное обучение**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="8f2e4-134">В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="8f2e4-135">В поле "Имя" щелкните **Модель ценза [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="8f2e4-136">В нижней части страницы щелкните **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="8f2e4-137">Дополнительные сведения о добавлении конечных точек см. в статье [Создание конечных точек](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="8f2e4-138">Обновление обученной модели добавленной конечной точки</span><span class="sxs-lookup"><span data-stu-id="8f2e4-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="8f2e4-139">Чтобы завершить процесс переобучения, необходимо обновить обученную модель добавленной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="8f2e4-140">Если вы добавили новую конечную точку с помощью классического портала Azure, щелкните имя новой конечной точки на портале, а затем — ссылку **Обновить ресурс**, чтобы получить URL-адрес, необходимый для обновления модели конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="8f2e4-141">При добавлении конечной точки с помощью примера кода он также включает расположение URL-адреса справки, заданного в свойстве *HelpLocationURL* в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="8f2e4-142">Чтобы извлечь URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="8f2e4-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="8f2e4-143">Скопируйте и вставьте этот URL-адрес в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="8f2e4-144">Щелкните ссылку "Обновить ресурс".</span><span class="sxs-lookup"><span data-stu-id="8f2e4-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="8f2e4-145">Скопируйте URL-адрес POST запроса PATCH.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="8f2e4-146">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2e4-146">For example:</span></span>
   
     <span data-ttu-id="8f2e4-147">URL-адрес запроса PATCH: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="8f2e4-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="8f2e4-148">Теперь обученную модель можно использовать для обновления созданной конечной точки оценки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="8f2e4-149">В следующем примере кода показано, как использовать параметры *BaseLocation*, *RelativeLocation*, *SasBlobToken* и URL-адрес исправления для обновления конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="8f2e4-150">Параметры *apiKey* и *endpointUrl* для этого вызова можно получить на панели мониторинга конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="8f2e4-151">Значение параметра *Имя* в *ресурсах* должно соответствовать имени ресурса сохраненной обученной модели в прогнозном эксперименте.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="8f2e4-152">Чтобы получить имя ресурса:</span><span class="sxs-lookup"><span data-stu-id="8f2e4-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="8f2e4-153">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8f2e4-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8f2e4-154">В меню слева щелкните **Машинное обучение**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="8f2e4-155">В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="8f2e4-156">В поле "Имя" щелкните **Модель ценза [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="8f2e4-157">Щелкните новую добавленную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="8f2e4-158">На панели мониторинга конечной точки щелкните **Обновить ресурс**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="8f2e4-159">На странице документации по API обновления ресурсов для веб-службы можно найти **имя ресурса** в разделе **обновляемых ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="8f2e4-160">Если срок действия маркера SAS истекает до завершения обновления конечной точки, необходимо выполнить операцию GET с использованием идентификатора задания, чтобы получить новый маркер.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="8f2e4-161">Если код выполнен успешно, новая конечная точка начнет использовать переобученную модель примерно через 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="8f2e4-162">Сводка</span><span class="sxs-lookup"><span data-stu-id="8f2e4-162">Summary</span></span>
<span data-ttu-id="8f2e4-163">Используя интерфейсы API переобучения, можно обновить обученную модель прогнозной веб-службы, что позволяет выполнять следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="8f2e4-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="8f2e4-164">Периодическое переобучение модели с использованием новых данных.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="8f2e4-165">Распределение модели клиентам, чтобы они могли переобучить ее с использованием собственных данных.</span><span class="sxs-lookup"><span data-stu-id="8f2e4-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f2e4-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f2e4-166">Next steps</span></span>
[<span data-ttu-id="8f2e4-167">Устранение неполадок при повторном обучении классической веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="8f2e4-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

