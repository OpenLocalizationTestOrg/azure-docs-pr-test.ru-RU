---
title: "AAA(deprecated) публикации машинного самообучения, web service tooAzure Marketplace | Документы Microsoft"
description: "(устарело) Как toopublish toohello вашего веб-служба Azure Machine Learning Azure Marketplace"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="e1b83-103">(устарело) Публикация веб-служба Azure Machine Learning toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e1b83-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="e1b83-104">Работа DataMarket и служб данных прекращается. Начиная с 31 марта 2017 г. имеющиеся подписки выводятся из эксплуатации и будут отменены.</span><span class="sxs-lookup"><span data-stu-id="e1b83-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="e1b83-105">Поэтому мы не рекомендуем использовать эту статью.</span><span class="sxs-lookup"><span data-stu-id="e1b83-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="e1b83-106">В качестве альтернативы можно опубликовать эксперименты в машинное обучение toohello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/) преимущество hello сообщества обработки и анализа данных hello.</span><span class="sxs-lookup"><span data-stu-id="e1b83-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="e1b83-107">Дополнительные сведения см. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="e1b83-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="e1b83-108">Hello Azure Marketplace позволяет hello веб-службы машинного обучения Azure toopublish как платная или освобождения службы для потребления внешними клиентами.</span><span class="sxs-lookup"><span data-stu-id="e1b83-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="e1b83-109">В этой статье Общие сведения об этом процессе с tooget tooguidelines ссылки, который был запущен.</span><span class="sxs-lookup"><span data-stu-id="e1b83-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="e1b83-110">Используя этот процесс, можно сделать доступными для других tooconsume разработчики веб-служб в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="e1b83-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="e1b83-111">Обзор процесса публикации hello</span><span class="sxs-lookup"><span data-stu-id="e1b83-111">Overview of hello publishing process</span></span>
<span data-ttu-id="e1b83-112">Hello ниже приведены шаги hello для публикации tooAzure службы web машинного обучения Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e1b83-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="e1b83-113">Создайте и опубликуйте службу машинного обучения типа «запрос-ответ» (RRS).</span><span class="sxs-lookup"><span data-stu-id="e1b83-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="e1b83-114">Развертывание службы tooproduction hello и получите hello ключ API и OData сведения о конечной точке.</span><span class="sxs-lookup"><span data-stu-id="e1b83-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="e1b83-115">URL-адрес hello для hello используйте опубликованных web service toopublish слишком[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="e1b83-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="e1b83-116">После отправки, анализируется ваше предложение и должен toobe утверждения перед клиентов можно запустить его приобретения.</span><span class="sxs-lookup"><span data-stu-id="e1b83-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="e1b83-117">Hello публикации может занять несколько рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="e1b83-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="e1b83-118">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="e1b83-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="e1b83-119">Шаг 1. Создание и публикация службы машинного обучения типа «запрос-ответ» (RRS)</span><span class="sxs-lookup"><span data-stu-id="e1b83-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="e1b83-120">Если вы еще не создали такую службу, ознакомьтесь с этим [пошаговым руководством](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e1b83-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="e1b83-121">Шаг 2: Развертывание службы tooproduction hello и получить hello сведения о конечной точке OData и ключ API</span><span class="sxs-lookup"><span data-stu-id="e1b83-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="e1b83-122">Из hello [классический портал Azure](http://manage.windowsazure.com)выберите hello **МАШИННОГО ОБУЧЕНИЯ** hello левой навигационной панели и выберите рабочую область.</span><span class="sxs-lookup"><span data-stu-id="e1b83-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="e1b83-123">Щелкните hello **веб-службы** вкладку и выберите hello веб-службы требуется toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="e1b83-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="e1b83-125">Выберите конечную точку hello бы как toohave hello marketplace использовать.</span><span class="sxs-lookup"><span data-stu-id="e1b83-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="e1b83-126">Если вы не создали все дополнительные конечные точки, можно выбрать hello **по умолчанию** конечной точки.</span><span class="sxs-lookup"><span data-stu-id="e1b83-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="e1b83-127">При щелчке на конечной точке hello будет hello может toosee **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="e1b83-128">Скопируйте его. Эта информация потребуется далее на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="e1b83-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="e1b83-130">Щелкните hello **запрос-ОТВЕТ** метод на этом этапе мы не поддерживаем Публикация выполнения пакета служб toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="e1b83-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="e1b83-131">Будет выполнен toohello API страницы справки для hello метода запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="e1b83-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="e1b83-132">Копировать hello **адрес конечной точки OData**, вам потребуется эта информация позже на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="e1b83-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="e1b83-134">развертывание службы hello в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e1b83-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="e1b83-135">Шаг 3: Используйте URL hello hello опубликованных tooAzure toopublish web service Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="e1b83-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="e1b83-136">Перейдите в слишком[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="e1b83-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="e1b83-137">Щелкните hello **публикации** ссылку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e1b83-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="e1b83-138">Это может занять toohello [портал публикации Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="e1b83-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="e1b83-139">Щелкните hello **издателей** tooregister раздел как издатель.</span><span class="sxs-lookup"><span data-stu-id="e1b83-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="e1b83-140">При создании предложения выберите пункт **Службы данных**, а затем выберите команду **Create a New Data Service** (Создать службу данных).</span><span class="sxs-lookup"><span data-stu-id="e1b83-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="e1b83-142">На вкладке **Планы** укажите информацию о предложении, включая тарифный план.</span><span class="sxs-lookup"><span data-stu-id="e1b83-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="e1b83-143">Определите, будет ли предложение платной или бесплатной службой.</span><span class="sxs-lookup"><span data-stu-id="e1b83-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="e1b83-144">tooget оплачен, предоставляют сведения о платеже, такие как данные налогов и банка.</span><span class="sxs-lookup"><span data-stu-id="e1b83-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="e1b83-145">В разделе **маркетинга** предоставляют сведения о вашем предложении, например hello заголовок и описание для вашего предложения.</span><span class="sxs-lookup"><span data-stu-id="e1b83-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="e1b83-146">В разделе **цены** задать hello цены для планов для определенных стран или позволить системе hello «autoprice» ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="e1b83-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="e1b83-147">На hello **службы данных** щелкните **веб-службы** как hello **источника данных**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="e1b83-149">Получите hello web service URL-адрес и ключ API из hello классический портал Azure, как описано в шаге 2 выше.</span><span class="sxs-lookup"><span data-stu-id="e1b83-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="e1b83-150">В hello службы данных Marketplace диалогового окна настройки вставьте адрес конечной точки OData hello в hello **URL-адрес службы** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="e1b83-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="e1b83-151">Для **проверки подлинности**, выберите **заголовок** как hello **схему проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="e1b83-152">Введите «Авторизации» hello **имя заголовка**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="e1b83-153">Для hello **значение заголовка**введите «Bearer» (без кавычек hello), щелкните hello **пространства** панели, а затем вставьте ключ hello API.</span><span class="sxs-lookup"><span data-stu-id="e1b83-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="e1b83-154">Выберите hello **данная служба является OData** флажок.</span><span class="sxs-lookup"><span data-stu-id="e1b83-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="e1b83-155">Нажмите кнопку **проверить подключение** tootest hello соединения.</span><span class="sxs-lookup"><span data-stu-id="e1b83-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="e1b83-156">На вкладке **Категории** выберите **Машинное обучение**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="e1b83-157">По завершении ввода всех hello метаданные о вашем предложении, нажмите кнопку **публикации**, а затем **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="e1b83-158">На этом этапе вы получите уведомление о неполадках остальные необходимые toofix.</span><span class="sxs-lookup"><span data-stu-id="e1b83-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="e1b83-159">Убедившись завершения всех проблем hello щелкните **запросить утверждение toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="e1b83-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="e1b83-160">Hello публикации может занять несколько рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="e1b83-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

