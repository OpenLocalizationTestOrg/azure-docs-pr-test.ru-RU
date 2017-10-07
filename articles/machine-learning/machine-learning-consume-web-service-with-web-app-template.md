---
title: "aaaConsume веб-службы машинного обучения с веб-приложения шаблона | Документы Microsoft"
description: "Используйте веб-шаблона приложения в Azure Marketplace tooconsume прогнозирующей веб-службы в машинном обучении Azure."
keywords: "веб-служба, ввод в эксплуатацию, REST API, машинное обучение"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="806f0-104">Использование веб-службы машинного обучения Azure с шаблоном веб-приложения</span><span class="sxs-lookup"><span data-stu-id="806f0-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="806f0-105">Один раз после разработки прогнозной модели и развернуть его как веб-службу Azure с помощью студии машинного обучения, или с помощью средств, таких как R или Python, можно открыть hello развернутых моделей с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="806f0-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="806f0-106">Существует несколько способов tooconsume hello REST API и доступа hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="806f0-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="806f0-107">Например, можно написать пользовательское приложение в C#, R, или Python, с помощью hello пример кода, созданный для вас при развертывании hello веб-службы (в hello [службы веб-портал для машины обучения](https://services.azureml.net/quickstart) или в hello мониторинга веб-службы в Студия машинного обучения).</span><span class="sxs-lookup"><span data-stu-id="806f0-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="806f0-108">Или можно использовать hello образца электронной таблицы Microsoft Excel при hello то же время.</span><span class="sxs-lookup"><span data-stu-id="806f0-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="806f0-109">Но hello tooaccess быстрее и проще всего, является веб-службу через hello веб-приложения шаблоны доступны в hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="806f0-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="806f0-110">Hello Azure Machine Learning веб-приложения шаблонов</span><span class="sxs-lookup"><span data-stu-id="806f0-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="806f0-111">Hello веб-приложения шаблоны доступны в hello Azure Marketplace можно создавать пользовательские веб-приложения, который знает входных данных веб-службы и ожидаемые результаты.</span><span class="sxs-lookup"><span data-stu-id="806f0-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="806f0-112">Все, что нужно toodo — предоставить hello web app доступа tooyour веб-службы и данных, а шаблон hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="806f0-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="806f0-113">Доступны два шаблона:</span><span class="sxs-lookup"><span data-stu-id="806f0-113">Two templates are available:</span></span>

* [<span data-ttu-id="806f0-114">шаблон веб-приложения службы «запрос — ответ» Azure ML;</span><span class="sxs-lookup"><span data-stu-id="806f0-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="806f0-115">шаблон веб-приложения службы пакетного выполнения Azure ML.</span><span class="sxs-lookup"><span data-stu-id="806f0-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="806f0-116">Каждый шаблон создает образец приложения ASP.NET, с помощью API URI hello и ключ для веб-службу и развертывает ее как tooAzure веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="806f0-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="806f0-117">шаблон запрос-ответ службы (RR) Hello создает веб-приложения, позволяющий toosend один ряд данных toohello web service tooget один результат.</span><span class="sxs-lookup"><span data-stu-id="806f0-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="806f0-118">шаблон службы пакетного выполнения (BES) Hello создает веб-приложения, который позволяет вам toosend большого количества строк данных tooget несколько результатов.</span><span class="sxs-lookup"><span data-stu-id="806f0-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="806f0-119">Без написания кода является обязательным toouse этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="806f0-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="806f0-120">Необходимо только указать hello ключ API и URI и hello шаблона построения приложение hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="806f0-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="806f0-121">ключ hello API tooget и URI запроса для веб-службы:</span><span class="sxs-lookup"><span data-stu-id="806f0-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="806f0-122">В hello [веб-портале служб](https://services.azureml.net/quickstart), веб-службу, щелкните **веб-службы** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="806f0-123">А для классической веб-службы щелкните **Classic Web Services** (Классические веб-службы).</span><span class="sxs-lookup"><span data-stu-id="806f0-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="806f0-124">Щелкните hello веб-службы требуется tooaccess.</span><span class="sxs-lookup"><span data-stu-id="806f0-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="806f0-125">Классического веб-службы щелкните конечную точку hello требуется tooaccess.</span><span class="sxs-lookup"><span data-stu-id="806f0-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="806f0-126">Нажмите кнопку **использование** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="806f0-127">Копировать hello **основной** или **вторичный ключ** и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="806f0-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="806f0-128">Если вы создаете шаблон запрос-ответ службы (RR), скопируйте hello **запрос-ответ** URI и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="806f0-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="806f0-129">При создании шаблона службы пакетного выполнения (BES), скопируйте hello **пакетных запросов** URI и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="806f0-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="806f0-130">Как toouse hello шаблон запрос-ответ службы (RR)</span><span class="sxs-lookup"><span data-stu-id="806f0-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="806f0-131">Выполните эти шаги toouse hello записей Ресурсов веб-приложения шаблона, как показано в hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="806f0-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Процесс toouse записей Ресурсов веб-шаблона][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="806f0-133">Go toohello [портал Azure](https://portal.azure.com), **входа**, нажмите кнопку **New**, поиска и выбора **веб-приложения Azure ML запрос-ответ службы**, нажмите кнопку **Создания**.</span><span class="sxs-lookup"><span data-stu-id="806f0-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="806f0-134">Присвойте веб-приложению уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="806f0-134">Give your web app a unique name.</span></span> <span data-ttu-id="806f0-135">Hello URL-адрес веб-приложения hello будет это имя, за которым следует `.azurewebsites.net.` например,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="806f0-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="806f0-136">Выберите hello подписки Azure и службы, под которыми работает веб-службу.</span><span class="sxs-lookup"><span data-stu-id="806f0-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="806f0-137">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="806f0-137">Click **Create**.</span></span>
     
     ![Создание веб-приложения][image5]

4. <span data-ttu-id="806f0-139">После завершения развертывания веб-приложения hello Azure щелкните hello **URL-адрес** hello веб-страницы параметров приложения в Azure, или введите URL-адрес hello в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="806f0-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="806f0-140">Например, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="806f0-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="806f0-141">Здравствуйте, когда веб-приложение первый выполняется он запросит hello **URL-адрес Post API** и **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="806f0-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="806f0-142">Введите значения hello, сохраненный ранее (**URI запроса** и **ключ API**соответственно).</span><span class="sxs-lookup"><span data-stu-id="806f0-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="806f0-143">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="806f0-143">Click **Submit**.</span></span>
     
     ![Введите Post URI и ключ API][image6]

6. <span data-ttu-id="806f0-145">Hello web app отображает его **веб-приложение конфигурация** страницы с помощью параметров hello текущей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="806f0-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="806f0-146">Здесь можно изменять параметры toohello, используемые веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="806f0-147">Здесь параметры hello только изменение действует для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="806f0-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="806f0-148">Он не изменяет параметры по умолчанию hello веб-службу.</span><span class="sxs-lookup"><span data-stu-id="806f0-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="806f0-149">Например, если изменения hello **описание** здесь не будет изменена hello описание, отображаемое на hello мониторинга веб-службы в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="806f0-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="806f0-150">После завершения нажмите кнопку **сохранить изменения**, а затем нажмите кнопку **Go tooHome страницы**.</span><span class="sxs-lookup"><span data-stu-id="806f0-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="806f0-151">Из hello домашней страницы, которое можно ввести значения toosend tooyour веб-службы.</span><span class="sxs-lookup"><span data-stu-id="806f0-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="806f0-152">Нажмите кнопку **отправить** после завершения и будет возвращен результат hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="806f0-153">Если требуется, чтобы tooreturn toohello **конфигурации** страницы, перейдите toohello `setting.aspx` страницы приветствия веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="806f0-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="806f0-154">Например: `http://carprediction.azurewebsites.net/setting.aspx.` запрашиваемые tooenter hello API ключ будет снова — нужно что tooaccess hello страницы и обновить параметры hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="806f0-155">Можно остановить, перезапустить или удалить веб-приложение hello в hello портал Azure, такие как веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="806f0-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="806f0-156">При условии, что он работает можно просмотреть toohello домашний веб-адрес и введите новые значения.</span><span class="sxs-lookup"><span data-stu-id="806f0-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="806f0-157">Как toouse hello шаблона службы пакетного выполнения (BES)</span><span class="sxs-lookup"><span data-stu-id="806f0-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="806f0-158">Можно использовать hello BES веб-приложения шаблона в hello таким же способом, как шаблон hello записей Ресурсов, за исключением hello веб-приложения, созданный разрешить toosubmit несколько строк данных и получать несколько результатов.</span><span class="sxs-lookup"><span data-stu-id="806f0-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="806f0-159">Hello входных значений для пакетного выполнения веб-службы могут поступать из хранилища Azure или локальный файл; Hello результаты сохраняются в контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="806f0-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="806f0-160">Таким образом, вам потребуется выполнить необходимые результаты, возвращенные веб-приложения hello hello toohold контейнер хранилища Azure, и потребуется tooget входные данные готовы.</span><span class="sxs-lookup"><span data-stu-id="806f0-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Обработать toouse BES веб-шаблона][image2]

1. <span data-ttu-id="806f0-162">Выполните hello же hello toocreate процедуры BES веб-приложения, как и для записи Ресурсов шаблона hello, за исключением go слишком[Azure ML пакетного выполнения службы веб-приложения шаблона](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES шаблона в Azure Marketplace и нажмите кнопку **Создание веб-приложения** .</span><span class="sxs-lookup"><span data-stu-id="806f0-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="806f0-163">toospecify место hello результаты, сохраненные, введите сведения о контейнере назначения hello на hello веб-приложения домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="806f0-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="806f0-164">Также укажите, где hello веб-приложения можно получить hello входных значений, либо в локальный файл или контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="806f0-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="806f0-165">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="806f0-165">Click **Submit**.</span></span>
   
    ![Сведения о хранилище][image7]

<span data-ttu-id="806f0-167">веб-приложения Hello, отображается страница с состоянием задания.</span><span class="sxs-lookup"><span data-stu-id="806f0-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="806f0-168">После завершения задания hello будет предоставляться расположение hello hello результатов в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="806f0-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="806f0-169">Также имеется возможность загрузки локального файла hello результаты tooa hello.</span><span class="sxs-lookup"><span data-stu-id="806f0-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="806f0-170">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="806f0-170">For more information</span></span>
<span data-ttu-id="806f0-171">Дополнительные сведения о toolearn...</span><span class="sxs-lookup"><span data-stu-id="806f0-171">toolearn more about...</span></span>

* <span data-ttu-id="806f0-172">Создание эксперимента машинного обучения в Студии машинного обучения — см. статью [Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="806f0-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="806f0-173">toodeploy вашей машинного обучения поэкспериментировать веб-службы. в статье [развертывание на веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="806f0-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="806f0-174">другие способы tooaccess веб-службу. в разделе [как tooconsume Azure машины обучения, веб-службы](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="806f0-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
