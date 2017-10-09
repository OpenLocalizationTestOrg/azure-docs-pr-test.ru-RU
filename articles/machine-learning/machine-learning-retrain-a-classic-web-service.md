---
title: "aaaRetrain классического веб-службы | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения модели и обновление hello web service toouse hello вновь обученной модели в машинном обучении Azure."
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="3adfc-103">Переобучение классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="3adfc-103">Retrain a Classic web service</span></span>
<span data-ttu-id="3adfc-104">Hello прогнозной веб-службы, развертываемые — оценки конечной точки по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="3adfc-105">Конечные точки по умолчанию сохраняются в соответствии с hello исходного обучения и оценки экспериментов и поэтому hello обученной модели для конечной точки по умолчанию hello не может быть заменен.</span><span class="sxs-lookup"><span data-stu-id="3adfc-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="3adfc-106">tooretrain hello веб-службы, необходимо добавить новую конечную точку веб-службу toohello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3adfc-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3adfc-107">Prerequisites</span></span>
<span data-ttu-id="3adfc-108">Вы уже настроили обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="3adfc-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3adfc-109">Hello прогнозной эксперимента необходимо развернуть как классический машинного обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3adfc-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="3adfc-110">Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3adfc-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="3adfc-111">Добавление новой конечной точки</span><span class="sxs-lookup"><span data-stu-id="3adfc-111">Add a new Endpoint</span></span>
<span data-ttu-id="3adfc-112">Hello прогнозной веб-службы, который был развернут содержит оценки конечную точку, которая синхронизируется с исходной обучения hello и оценки экспериментов обученной модели по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3adfc-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="3adfc-113">tooupdate вашей toowith новый обученной модели службы web необходимо создать новую конечную точку для оценки.</span><span class="sxs-lookup"><span data-stu-id="3adfc-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="3adfc-114">toocreate новой конечной точки оценки, на hello прогнозной веб-службы, которая может быть обновлена с помощью обученной модели hello:</span><span class="sxs-lookup"><span data-stu-id="3adfc-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="3adfc-115">Убедитесь, что вы добавляете toohello hello конечную точку прогнозируемого веб-службы, hello обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3adfc-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="3adfc-116">Если вы правильно установили обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3adfc-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="3adfc-117">Hello прогнозной веб-службы должно заканчиваться «[прогнозной exp.]».</span><span class="sxs-lookup"><span data-stu-id="3adfc-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="3adfc-118">Существует три способа, в которых можно добавить новую конечную точку веб-службу tooa:</span><span class="sxs-lookup"><span data-stu-id="3adfc-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="3adfc-119">Программным образом</span><span class="sxs-lookup"><span data-stu-id="3adfc-119">Programmatically</span></span>
2. <span data-ttu-id="3adfc-120">С помощью портала hello веб-службы Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3adfc-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="3adfc-121">Hello используйте классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="3adfc-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="3adfc-122">Добавление конечной точки программно</span><span class="sxs-lookup"><span data-stu-id="3adfc-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="3adfc-123">Можно добавить оценки конечные точки, использующие hello кода примера, приведенного в этом [репозитории github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="3adfc-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="3adfc-124">Использование портала tooadd веб-службы Microsoft Azure hello конечной точки</span><span class="sxs-lookup"><span data-stu-id="3adfc-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="3adfc-125">В студии машинного обучения на столбце hello навигации слева, нажмите кнопку веб-служб.</span><span class="sxs-lookup"><span data-stu-id="3adfc-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="3adfc-126">Внизу hello hello мониторинга веб-службы, нажмите кнопку **Управление конечными точками preview**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="3adfc-127">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-127">Click **Add**.</span></span>
4. <span data-ttu-id="3adfc-128">Введите имя и описание для новой конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="3adfc-129">Выберите уровень ведения журнала hello и включена ли образец данных.</span><span class="sxs-lookup"><span data-stu-id="3adfc-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="3adfc-130">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="3adfc-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="3adfc-131">Использовать hello Azure классического портала tooadd конечной точки</span><span class="sxs-lookup"><span data-stu-id="3adfc-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="3adfc-132">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3adfc-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3adfc-133">В левом меню hello, щелкните **машинного обучения**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="3adfc-134">В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="3adfc-135">В поле "Имя" щелкните **Модель ценза [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="3adfc-136">Внизу hello страницы приветствия щелкните **добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="3adfc-137">Дополнительные сведения о добавлении конечных точек см. в статье [Создание конечных точек](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="3adfc-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="3adfc-138">Обновление hello добавлены обученной модели конечной точки</span><span class="sxs-lookup"><span data-stu-id="3adfc-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="3adfc-139">Цикл процесса toocomplete hello, необходимо обновить hello обученной модели hello новую конечную точку, которая была добавлена.</span><span class="sxs-lookup"><span data-stu-id="3adfc-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="3adfc-140">Если вы добавили hello новую конечную точку, с помощью классического портала Azure hello, можно щелкнуть hello новое имя конечной точки на портале hello, затем hello **UpdateResource** hello tooget URL-адрес, потребовалось бы модели tooupdate hello конечной точки ссылки.</span><span class="sxs-lookup"><span data-stu-id="3adfc-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="3adfc-141">Если вы добавили hello конечной точки с использованием примера кода hello, в нем расположение определяется hello URL-адрес справки hello *HelpLocationURL* значение в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="3adfc-142">tooretrieve hello путь URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="3adfc-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="3adfc-143">Скопируйте и вставьте hello URL-адрес в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="3adfc-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="3adfc-144">Щелкните ссылку hello обновления ресурса.</span><span class="sxs-lookup"><span data-stu-id="3adfc-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="3adfc-145">Скопируйте hello POST URL-адрес запроса PATCH hello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="3adfc-146">Например:</span><span class="sxs-lookup"><span data-stu-id="3adfc-146">For example:</span></span>
   
     <span data-ttu-id="3adfc-147">URL-адрес запроса PATCH: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="3adfc-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="3adfc-148">Теперь можно использовать hello обученной модели tooupdate hello оценки конечную точку, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="3adfc-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="3adfc-149">Следующий образец кода Hello показано, как toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*и конечная точка hello tooupdate ИСПРАВЛЕНИЯ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3adfc-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="3adfc-150">Hello *apiKey* и hello *endpointUrl* для hello вызов может быть получен из панели мониторинга конечной точки.</span><span class="sxs-lookup"><span data-stu-id="3adfc-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="3adfc-151">Здравствуйте, значение hello *имя* параметр в *ресурсы* должен hello соответствия ресурсов с именем hello сохранен обученной модели в эксперименте прогнозной hello.</span><span class="sxs-lookup"><span data-stu-id="3adfc-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="3adfc-152">hello tooget имя ресурса:</span><span class="sxs-lookup"><span data-stu-id="3adfc-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="3adfc-153">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3adfc-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3adfc-154">В левом меню hello, щелкните **машинного обучения**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="3adfc-155">В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="3adfc-156">В поле "Имя" щелкните **Модель ценза [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="3adfc-157">Щелкните новую конечную точку hello, добавленными.</span><span class="sxs-lookup"><span data-stu-id="3adfc-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="3adfc-158">На панели мониторинга endpoint hello, нажмите кнопку **обновления ресурса**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="3adfc-159">На странице документации по API обновление ресурсов hello hello веб-службы, можно найти hello **имя ресурса** под **обновляемых ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="3adfc-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="3adfc-160">Если срок действия токена SAS истекает до завершения обновления hello конечной точки, необходимо выполнить GET с ИД задания hello tooobtain новый маркер.</span><span class="sxs-lookup"><span data-stu-id="3adfc-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="3adfc-161">После успешного выполнения кода hello hello новую конечную точку следует начать использовать hello повторное Обучение модели приблизительно через 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="3adfc-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="3adfc-162">Сводка</span><span class="sxs-lookup"><span data-stu-id="3adfc-162">Summary</span></span>
<span data-ttu-id="3adfc-163">С помощью API-интерфейсы переподготовки "hello", вы можете обновить hello обученной модели прогнозирования Включение сценариев, таких как веб-службы:</span><span class="sxs-lookup"><span data-stu-id="3adfc-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="3adfc-164">Периодическое переобучение модели с использованием новых данных.</span><span class="sxs-lookup"><span data-stu-id="3adfc-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="3adfc-165">Распределение toocustomers модели с целью hello. Однако обучение модели hello, используя свои собственные данные.</span><span class="sxs-lookup"><span data-stu-id="3adfc-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3adfc-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3adfc-166">Next steps</span></span>
[<span data-ttu-id="3adfc-167">Устранение неполадок hello переподготовки классического веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="3adfc-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

