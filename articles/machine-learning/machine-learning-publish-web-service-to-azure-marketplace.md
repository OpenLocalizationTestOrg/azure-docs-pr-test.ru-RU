---
title: "Публикация веб-службы машинного обучения в Azure Marketplace (устаревшая версия) | Документация Майкрософт"
description: "Сведения о публикации веб-службы машинного обучения Azure в Azure Marketplace (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="dc6de-103">Публикация веб-службы машинного обучения Azure в Azure Marketplace (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="dc6de-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="dc6de-104">Работа DataMarket и служб данных прекращается. Начиная с 31 марта 2017 г. имеющиеся подписки выводятся из эксплуатации и будут отменены.</span><span class="sxs-lookup"><span data-stu-id="dc6de-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="dc6de-105">Поэтому мы не рекомендуем использовать эту статью.</span><span class="sxs-lookup"><span data-stu-id="dc6de-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="dc6de-106">В качестве альтернативы вы можете публиковать свои эксперименты машинного обучения в [коллекции Cortana Intelligence](https://gallery.cortanaintelligence.com/) и поделиться ими с сообществом, занимающимся анализом данных.</span><span class="sxs-lookup"><span data-stu-id="dc6de-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="dc6de-107">Дополнительные сведения см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="dc6de-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="dc6de-108">Azure Marketplace предоставляет возможность публикации веб-служб машинного обучения Azure как платных или бесплатных служб для внешних клиентов.</span><span class="sxs-lookup"><span data-stu-id="dc6de-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="dc6de-109">В этой статье приводится обзор процесса публикации со ссылками на руководства для начала работы.</span><span class="sxs-lookup"><span data-stu-id="dc6de-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="dc6de-110">С помощью этой процедуры можно разрешить другим разработчикам использовать веб-службы в их приложениях.</span><span class="sxs-lookup"><span data-stu-id="dc6de-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="dc6de-111">Обзор процесса публикации</span><span class="sxs-lookup"><span data-stu-id="dc6de-111">Overview of the publishing process</span></span>
<span data-ttu-id="dc6de-112">Чтобы опубликовать веб-службу Машинного обучения Azure в Azure Marketplace, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dc6de-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="dc6de-113">Создайте и опубликуйте службу машинного обучения типа «запрос-ответ» (RRS).</span><span class="sxs-lookup"><span data-stu-id="dc6de-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="dc6de-114">Разверните службу в рабочей среде и получите информацию о ключе API и конечной точке OData.</span><span class="sxs-lookup"><span data-stu-id="dc6de-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="dc6de-115">Используйте URL-адрес опубликованной веб-службы для публикации в [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="dc6de-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="dc6de-116">После отправки это предложение рассматривается и должно быть утверждено, прежде чем клиенты смогут начать приобретать его.</span><span class="sxs-lookup"><span data-stu-id="dc6de-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="dc6de-117">Процесс публикации может занять несколько рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="dc6de-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="dc6de-118">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="dc6de-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="dc6de-119">Шаг 1. Создание и публикация службы машинного обучения типа «запрос-ответ» (RRS)</span><span class="sxs-lookup"><span data-stu-id="dc6de-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="dc6de-120">Если вы еще не создали такую службу, ознакомьтесь с этим [пошаговым руководством](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="dc6de-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="dc6de-121">Шаг 2. Развертывание службы в рабочей среде, а также получение информации о ключе API и конечной точке OData.</span><span class="sxs-lookup"><span data-stu-id="dc6de-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="dc6de-122">На [классическом портале Azure](http://manage.windowsazure.com)выберите элемент **МАШИННОЕ ОБУЧЕНИЕ** на панели навигации слева, а затем рабочую область.</span><span class="sxs-lookup"><span data-stu-id="dc6de-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="dc6de-123">Щелкните вкладку **ВЕБ-СЛУЖБЫ** и выберите веб-службу, которую нужно опубликовать в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dc6de-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="dc6de-125">Выберите конечную точку, которую необходимо использовать в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dc6de-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="dc6de-126">Если вы не создали дополнительные конечные точки, можно выбрать конечную точку **По умолчанию** .</span><span class="sxs-lookup"><span data-stu-id="dc6de-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="dc6de-127">Щелкнув конечную точку, вы сможете увидеть **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="dc6de-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="dc6de-128">Скопируйте его. Эта информация потребуется далее на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="dc6de-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="dc6de-130">Щелкните метод **Запрос-ответ**. На этом этапе публикация служб пакетного выполнения в Marketplace не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="dc6de-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="dc6de-131">Вы перейдете на страницу справки API для метода «Запрос-ответ».</span><span class="sxs-lookup"><span data-stu-id="dc6de-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="dc6de-132">Скопируйте **адрес конечной точки OData**. Эти сведения потребуются далее на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="dc6de-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="dc6de-134">Разверните службу в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dc6de-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="dc6de-135">Шаг 3. Использование URL-адреса опубликованной веб-службы для публикации в Azure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="dc6de-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="dc6de-136">Перейдите к [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="dc6de-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="dc6de-137">Щелкните ссылку **Опубликовать** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dc6de-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="dc6de-138">Откроется страница [портала публикации Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="dc6de-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="dc6de-139">Щелкните раздел **Издатели** , чтобы зарегистрироваться как издатель.</span><span class="sxs-lookup"><span data-stu-id="dc6de-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="dc6de-140">При создании предложения выберите пункт **Службы данных**, а затем выберите команду **Create a New Data Service** (Создать службу данных).</span><span class="sxs-lookup"><span data-stu-id="dc6de-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="dc6de-142">На вкладке **Планы** укажите информацию о предложении, включая тарифный план.</span><span class="sxs-lookup"><span data-stu-id="dc6de-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="dc6de-143">Определите, будет ли предложение платной или бесплатной службой.</span><span class="sxs-lookup"><span data-stu-id="dc6de-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="dc6de-144">Для получения оплаты необходимо указать платежные реквизиты, такие как банковские и налоговые данные.</span><span class="sxs-lookup"><span data-stu-id="dc6de-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="dc6de-145">На вкладке **Маркетинг** укажите информацию о предложении, такую как заголовок и описание предложения.</span><span class="sxs-lookup"><span data-stu-id="dc6de-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="dc6de-146">На вкладке **Цены** можно установить цену для планов в конкретных странах или позволить системе автоматически назначить цену для вашего предложения.</span><span class="sxs-lookup"><span data-stu-id="dc6de-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="dc6de-147">На вкладке **Data Service** (Служба данных) выберите для параметра **Источник данных** значение **Веб-служба**.</span><span class="sxs-lookup"><span data-stu-id="dc6de-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="dc6de-149">Откройте информацию об URL-адресе и ключе API веб-службы, полученных на классическом портале Azure, как описано на шаге 2 выше.</span><span class="sxs-lookup"><span data-stu-id="dc6de-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="dc6de-150">В диалоговом окне настройки службы данных Marketplace в текстовом поле **URL-адрес службы** вставьте адрес конечной точки OData.</span><span class="sxs-lookup"><span data-stu-id="dc6de-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="dc6de-151">Для **проверки подлинности** выберите значение **Заголовок** для параметра **Authentication Scheme** (Схема проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="dc6de-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="dc6de-152">В поле **Имя заголовка**укажите Authorization.</span><span class="sxs-lookup"><span data-stu-id="dc6de-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="dc6de-153">В поле **Header Value** (Значение заголовка) введите Bearer (без кавычек), щелкните строку **Space** (Пространство), а затем вставьте ключ API.</span><span class="sxs-lookup"><span data-stu-id="dc6de-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="dc6de-154">Установите флажок **Это служба OData** .</span><span class="sxs-lookup"><span data-stu-id="dc6de-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="dc6de-155">Нажмите кнопку **Проверить подключение** , чтобы проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="dc6de-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="dc6de-156">На вкладке **Категории** выберите **Машинное обучение**.</span><span class="sxs-lookup"><span data-stu-id="dc6de-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="dc6de-157">После ввода всех метаданных о вашем предложении нажмите кнопку **Опубликовать**, а затем щелкните **Push to Staging** (Переместить в промежуточную среду).</span><span class="sxs-lookup"><span data-stu-id="dc6de-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="dc6de-158">На этом этапе вы получите уведомление об оставшихся нерешенных проблемах.</span><span class="sxs-lookup"><span data-stu-id="dc6de-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="dc6de-159">Если все проблемы решены, щелкните **Запросить утверждение для перемещения в рабочую среду**.</span><span class="sxs-lookup"><span data-stu-id="dc6de-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="dc6de-160">Процесс публикации может занять несколько рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="dc6de-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

