---
title: "Использование веб-службы Машинного обучения Azure с шаблоном веб-приложения | Документация Майкрософт"
description: "Использование шаблона веб-приложения в Azure Marketplace для использования прогнозной веб-службы в машинном обучении Azure."
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
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="f2e61-104">Использование веб-службы машинного обучения Azure с шаблоном веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f2e61-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="f2e61-105">Разработав прогнозную модель и развернув ее в виде веб-службы Azure при помощи Студии машинного обучения или таких средств, как R или Python, вы можете обращаться к рабочей модели с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f2e61-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="f2e61-106">Существует несколько способов использования REST API и доступа к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="f2e61-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="f2e61-107">Например, можно создать приложение в C#, R или Python, используя образец кода, созданного при развертывании веб-службы (доступен на [портале веб-служб машинного обучения](https://services.azureml.net/quickstart) или на панели мониторинга веб-службы в Студии машинного обучения).</span><span class="sxs-lookup"><span data-stu-id="f2e61-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="f2e61-108">Кроме того, можно использовать одновременно созданный для вас образец книги Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="f2e61-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="f2e61-109">Но самым быстрым и легким способом доступа к веб-службе является доступ через шаблоны веб-приложений, доступные в [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="f2e61-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="f2e61-110">Шаблоны веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="f2e61-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="f2e61-111">С помощью шаблонов веб-служб, доступных в Azure Marketplace, можно создать пользовательское веб-приложение, которое «знает» входные данные вашей веб-службы и ожидаемые результаты.</span><span class="sxs-lookup"><span data-stu-id="f2e61-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="f2e61-112">Вам нужно всего лишь предоставить веб-приложению доступ к веб-службе и данным, а шаблон выполнит все остальные действия.</span><span class="sxs-lookup"><span data-stu-id="f2e61-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="f2e61-113">Доступны два шаблона:</span><span class="sxs-lookup"><span data-stu-id="f2e61-113">Two templates are available:</span></span>

* [<span data-ttu-id="f2e61-114">шаблон веб-приложения службы «запрос — ответ» Azure ML;</span><span class="sxs-lookup"><span data-stu-id="f2e61-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="f2e61-115">шаблон веб-приложения службы пакетного выполнения Azure ML.</span><span class="sxs-lookup"><span data-stu-id="f2e61-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="f2e61-116">Каждый шаблон создает образец приложения ASP.NET, используя URI API и ключ для вашей веб-службы, и развертывает его как веб-сайт в Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e61-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="f2e61-117">Шаблон службы «запрос — ответ» (RRS) создает веб-приложение, которое позволяет отправлять одну строку данных в веб-службу для получения одного результата.</span><span class="sxs-lookup"><span data-stu-id="f2e61-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="f2e61-118">Шаблон службы пакетного выполнения (BES) создает веб-приложение, которое позволяет отправлять несколько строк данных, чтобы получить несколько результатов.</span><span class="sxs-lookup"><span data-stu-id="f2e61-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="f2e61-119">Для использования этих шаблонов не требуется создавать код.</span><span class="sxs-lookup"><span data-stu-id="f2e61-119">No coding is required to use these templates.</span></span> <span data-ttu-id="f2e61-120">Вы просто предоставляете ключ API и универсальный код ресурса (URI), а шаблон создается в приложении.</span><span class="sxs-lookup"><span data-stu-id="f2e61-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="f2e61-121">Чтобы получить ключ API и URI запроса для веб-службы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f2e61-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="f2e61-122">Для новой веб-службы на [портале веб-служб](https://services.azureml.net/quickstart) в верхнем меню щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="f2e61-123">А для классической веб-службы щелкните **Classic Web Services** (Классические веб-службы).</span><span class="sxs-lookup"><span data-stu-id="f2e61-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="f2e61-124">Щелкните веб-службу, к которой необходимо получить доступ.</span><span class="sxs-lookup"><span data-stu-id="f2e61-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="f2e61-125">Для классической веб-службы щелкните конечную точку, к которой необходимо получить доступ.</span><span class="sxs-lookup"><span data-stu-id="f2e61-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="f2e61-126">В верхней части экрана щелкните **Consume** (Использовать).</span><span class="sxs-lookup"><span data-stu-id="f2e61-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="f2e61-127">Скопируйте и сохраните значение первичного (**Primary**) или вторичного ключа (**Secondary Key**).</span><span class="sxs-lookup"><span data-stu-id="f2e61-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="f2e61-128">При создании шаблона службы "запрос-ответ" (RRS) скопируйте универсальный код ресурса (URI) **Request-Response** (Запрос-ответ) и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="f2e61-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="f2e61-129">При создании шаблона службы пакетного выполнения (BES) скопируйте универсальный код ресурса (URI) **Batch Requests** (Пакетные запросы) и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="f2e61-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="f2e61-130">Использование шаблона службы «запрос-ответ» (RRS)</span><span class="sxs-lookup"><span data-stu-id="f2e61-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="f2e61-131">Выполните эти действия, чтобы использовать шаблон веб-приложения RRS, как показано на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="f2e61-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Использование веб-шаблона RRS][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="f2e61-133">Откройте [портал Azure](https://portal.azure.com), выполните **вход**, щелкните **Создать**, найдите и выберите **Azure ML Request-Response Service Web App** (Веб-приложение службы "запрос-ответ" Azure ML), а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="f2e61-134">Присвойте веб-приложению уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="f2e61-134">Give your web app a unique name.</span></span> <span data-ttu-id="f2e61-135">URL-адресом веб-приложения будет это имя с текстом `.azurewebsites.net.`. Например: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f2e61-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="f2e61-136">Выберите подписку Azure и службы, с которыми работает ваша веб-служба.</span><span class="sxs-lookup"><span data-stu-id="f2e61-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="f2e61-137">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-137">Click **Create**.</span></span>
     
     ![Создать веб-приложение][image5]

4. <span data-ttu-id="f2e61-139">Когда служба Azure завершит развертывание веб-приложения, щелкните **URL-адрес** на странице параметров веб-приложения в Azure или введите URL-адрес в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="f2e61-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="f2e61-140">Например, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f2e61-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="f2e61-141">При первом запуске веб-приложение запросит ввести значения в поля **API Post URL** (URL-адрес записи API) и **Ключ API**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="f2e61-142">Введите значения, которые были сохранены ранее (**URI запроса** и **Ключ API** соответственно).</span><span class="sxs-lookup"><span data-stu-id="f2e61-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="f2e61-143">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="f2e61-143">Click **Submit**.</span></span>
     
     ![Введите Post URI и ключ API][image6]

6. <span data-ttu-id="f2e61-145">Веб-приложение отобразит страницу **Конфигурация веб-приложения** с текущими параметрами веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f2e61-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="f2e61-146">Здесь можно вносить изменения в параметры, используемые веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="f2e61-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f2e61-147">Изменение этих параметров влияет только на параметры этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f2e61-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="f2e61-148">Это не изменяет параметры веб-службы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f2e61-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="f2e61-149">Например, если изменить параметр **Описание** , описание, отображаемое на панели мониторинга веб-службы в Студии машинного обучения, не изменится.</span><span class="sxs-lookup"><span data-stu-id="f2e61-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="f2e61-150">Когда все будет готово, нажмите кнопку **Сохранить изменения**, а затем щелкните **На домашнюю страницу**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="f2e61-151">На домашней странице можно ввести значения для отправки в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="f2e61-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="f2e61-152">Закончив, нажмите кнопку **Отправить** и получите результат.</span><span class="sxs-lookup"><span data-stu-id="f2e61-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="f2e61-153">Если вы хотите вернуться на страницу **Конфигурация**, перейдите на страницу `setting.aspx` веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f2e61-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="f2e61-154">Например: `http://carprediction.azurewebsites.net/setting.aspx.`. Вам будет предложено ввести ключ API снова, чтобы получить доступ к странице и обновить параметры.</span><span class="sxs-lookup"><span data-stu-id="f2e61-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="f2e61-155">Можно остановить, перезапустить или удалить веб-приложения на портале Azure, как любое другое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f2e61-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="f2e61-156">При условии что приложение работает, можно перейти к домашнему веб-адресу и ввести новые значения.</span><span class="sxs-lookup"><span data-stu-id="f2e61-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="f2e61-157">Использование шаблона службы пакетного выполнения (BES)</span><span class="sxs-lookup"><span data-stu-id="f2e61-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="f2e61-158">Шаблон веб-приложения BES можно использовать так же, как и шаблон RRS. Исключение состоит только в том, что создаваемое веб-приложение позволит передавать несколько строк данных и получать несколько результатов.</span><span class="sxs-lookup"><span data-stu-id="f2e61-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="f2e61-159">Источником входных значений для веб-службы пакетного выполнения может быть хранилище Azure или локальный файл. Результаты хранятся в контейнере хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e61-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="f2e61-160">Таким образом, вам потребуется контейнер хранилища Azure для хранения результатов, возвращаемых веб-приложением. Вам также нужно будет подготовить входные данные.</span><span class="sxs-lookup"><span data-stu-id="f2e61-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Использование веб-шаблона BES][image2]

1. <span data-ttu-id="f2e61-162">Чтобы создать веб-приложение BES, выполните ту же процедуру, что и для шаблона RRS, кроме таких действий: перейдите по ссылке [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) (Шаблон веб-приложения службы пакетного выполнения Azure ML), чтобы открыть шаблон BES в Azure Marketplace, а затем нажмите кнопку **Создать веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="f2e61-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="f2e61-163">Чтобы указать, куда следует сохранить результаты, введите сведения о целевом контейнере на домашней странице веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f2e61-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="f2e61-164">Кроме того, укажите источник входных значений для веб-приложения: локальный файл или контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e61-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="f2e61-165">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="f2e61-165">Click **Submit**.</span></span>
   
    ![Сведения о хранилище][image7]

<span data-ttu-id="f2e61-167">Веб-приложение отобразит страницу с состоянием задания.</span><span class="sxs-lookup"><span data-stu-id="f2e61-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="f2e61-168">После завершения задания будет указано расположение результатов в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e61-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="f2e61-169">Результаты также можно загрузить в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="f2e61-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="f2e61-170">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="f2e61-170">For more information</span></span>
<span data-ttu-id="f2e61-171">Дополнительная информация.</span><span class="sxs-lookup"><span data-stu-id="f2e61-171">To learn more about...</span></span>

* <span data-ttu-id="f2e61-172">Создание эксперимента машинного обучения в Студии машинного обучения — см. статью [Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="f2e61-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="f2e61-173">Развертывание эксперимента машинного обучения в качестве веб-службы — см. статью [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f2e61-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="f2e61-174">Сведения о других способах доступа к веб-службе см. статье [Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="f2e61-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
