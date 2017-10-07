---
title: "Службы данных предлагают для hello Marketplace aaaTesting | Документы Microsoft"
description: "Понимать, каким образом tootest службы данных предлагают для hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="34671-103">Тестирование предложения службы данных в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="34671-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34671-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="34671-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="34671-105">Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="34671-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="34671-106">Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="34671-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="34671-107">После выполнения первых двух действий hello объекта [создания учетной записи Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) и [Создание предложение службы данных на портал публикации](marketplace-publishing-data-service-creation.md) вы будете готовы для обеспечения доступности в hello ваше предложение Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="34671-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="34671-108">В этом разделе будет сначала пошаговыми руководствами hello, промежуточные, шаг с именем «промежуточный»</span><span class="sxs-lookup"><span data-stu-id="34671-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="34671-109">Промежуточная означает ваше предложение в «песочницу», где можно проверить и проверьте его функциональность перед принудительной отправки tooproduction закрытого развертывания.</span><span class="sxs-lookup"><span data-stu-id="34671-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="34671-110">предложение Hello, будет отображено в промежуточном так же, как будто он имеет tooa клиента, к которому она развернута.</span><span class="sxs-lookup"><span data-stu-id="34671-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="34671-111">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="34671-111">Step 1.</span></span> <span data-ttu-id="34671-112">Помещает toostaging вашего предложения</span><span class="sxs-lookup"><span data-stu-id="34671-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="34671-113">Помещает toostaging вашего предложения можно tootest hello предложение прежде чем она станет доступной toofuture подписчиков.</span><span class="sxs-lookup"><span data-stu-id="34671-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="34671-114">Вы увидите, как ваше предложение будет выглядеть и работать для подписанных данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="34671-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="34671-116">Имя входа в hello [портал публикации](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="34671-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="34671-117">Выберите **служб данных** в левой области навигации окна hello</span><span class="sxs-lookup"><span data-stu-id="34671-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="34671-118">Выберите предложение требуется toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="34671-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="34671-119">Вы увидите hello выше экрана.</span><span class="sxs-lookup"><span data-stu-id="34671-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="34671-120">Нажмите кнопку **Push tooStaging** кнопки.</span><span class="sxs-lookup"><span data-stu-id="34671-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="34671-121">При возникновении проблем с hello предложение, которое требуется toobe завершения предыдущего toopushing toostaging, вы увидите список отображается.</span><span class="sxs-lookup"><span data-stu-id="34671-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="34671-122">Исправьте эти элементы, щелкнув на каждый элемент в списке hello.</span><span class="sxs-lookup"><span data-stu-id="34671-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="34671-123">Когда все изменения, вносимые, нажмите кнопку **Push tooStaging** еще раз.</span><span class="sxs-lookup"><span data-stu-id="34671-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="34671-124">Если нет никаких проблем с вашего предложения вы увидите всплывающее окно hello ниже.</span><span class="sxs-lookup"><span data-stu-id="34671-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="34671-125">Если вы не являетесь планирования или не утвержденные toosurface вашего предложения на портале Azure (в настоящее время ограниченный объем), а затем просто закрыть hello всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="34671-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="34671-126">tootest данных службы на портале Azure (в дополнение toohello DataMarket портал), необходимо будет tootest идентификатор подписки Azure с.</span><span class="sxs-lookup"><span data-stu-id="34671-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="34671-127">Этот идентификатор подписки будет идентифицировать hello учетной записи, которая будет разрешено tootest ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="34671-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="34671-128">Вырезать и вставьте идентификатор подписки и щелкните галочку toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="34671-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="34671-130">Эти идентификаторы подписки Azure доступны только для тестирования и промежуточный в hello [портала управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="34671-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="34671-131">Они не являются обязательным tootest в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="34671-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="34671-132">Hello следующий экран отображается показывает, что публикация выполняется путем отображения hello в состоянии «выполняется» значок выделяются желтым ниже.</span><span class="sxs-lookup"><span data-stu-id="34671-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="34671-133">Помещает toostaging занимает от 10 минут too15.</span><span class="sxs-lookup"><span data-stu-id="34671-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="34671-134">Если прошло больше времени, сначала обновите страницу в браузере (в IE нажмите клавишу F5).</span><span class="sxs-lookup"><span data-stu-id="34671-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="34671-135">В редких случаях hello, где вы по-прежнему передаете toostaging через час после щелкните hello обратитесь к нам связать toolet нам знать, что имеется проблема.</span><span class="sxs-lookup"><span data-stu-id="34671-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="34671-137">По завершении hello tooStaging принудительной hello в состоянии «выполняется» значок приводит к остановке перемещение и hello состояние будет обновлено слишком «промежуточная».</span><span class="sxs-lookup"><span data-stu-id="34671-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="34671-138">Вы являются теперь готовы tootest ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="34671-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="34671-139">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="34671-139">Step 2.</span></span> <span data-ttu-id="34671-140">Тестирование предложения в промежуточной среде в DataMarket</span><span class="sxs-lookup"><span data-stu-id="34671-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="34671-141">Щелкните ссылку hello после текста hello **» содержится предложение на служб...»**</span><span class="sxs-lookup"><span data-stu-id="34671-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="34671-142">экран приветствия toodisplay, hello подписчика будут видеть переходом tooproduction ваше предложение и будет отображаться в DataMarket.</span><span class="sxs-lookup"><span data-stu-id="34671-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="34671-144">Тестирование или проверьте каждый из элементов 12 hello помечен выше tooensure все логотипы, цены и транзакции, текст, изображения, документация и ссылки были верны и работают правильно.</span><span class="sxs-lookup"><span data-stu-id="34671-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="34671-145">Это подходящий момент tooensure, все тестовые значения, введенные при создании вашего предложения заменяются фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="34671-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="34671-146">Эмблема предложения</span><span class="sxs-lookup"><span data-stu-id="34671-146">Offer logo</span></span>
2. <span data-ttu-id="34671-147">Название предложения</span><span class="sxs-lookup"><span data-stu-id="34671-147">Offer name</span></span>
3. <span data-ttu-id="34671-148">Веб-сайт компании tooyour издателя или ссылку с именем</span><span class="sxs-lookup"><span data-stu-id="34671-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="34671-149">Поисковые категории для предложения</span><span class="sxs-lookup"><span data-stu-id="34671-149">Search categories for your offer</span></span>
5. <span data-ttu-id="34671-150">Ваше предложение поддержки связи tooassist подписчиков</span><span class="sxs-lookup"><span data-stu-id="34671-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="34671-151">Контекстное описание предложения</span><span class="sxs-lookup"><span data-stu-id="34671-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="34671-152">План предложения, в котором отражены сведения о выставлении счетов</span><span class="sxs-lookup"><span data-stu-id="34671-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="34671-153">Код tooimplementation связи</span><span class="sxs-lookup"><span data-stu-id="34671-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="34671-154">Примеры изображений, иллюстрирующих использование предложения данных</span><span class="sxs-lookup"><span data-stu-id="34671-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="34671-155">Метаданные ввода-вывода для каждой службы в рамках предложения hello</span><span class="sxs-lookup"><span data-stu-id="34671-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="34671-156">Условия использования предложения</span><span class="sxs-lookup"><span data-stu-id="34671-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="34671-157">Предварительный просмотр данных hello предложение</span><span class="sxs-lookup"><span data-stu-id="34671-157">Preview of hello offer's data</span></span>

<span data-ttu-id="34671-158">Наконец убедитесь, что hello служба будет работать через hello Datamarket, щелкнув ссылку hello «ИЗУЧИТЬ этот набор данных».</span><span class="sxs-lookup"><span data-stu-id="34671-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="34671-159">Откроется новое окно в средстве hello мы называем «Обозреватель Service», можно просмотреть предварительные результаты hello запроса относительно службы.</span><span class="sxs-lookup"><span data-stu-id="34671-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="34671-160">В этом окне можно ввести hello параметры требуются и разделе hello результатов из запроса к службе.</span><span class="sxs-lookup"><span data-stu-id="34671-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="34671-161">Кроме того здесь указан hello URL-адрес для запроса.</span><span class="sxs-lookup"><span data-stu-id="34671-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="34671-162">Быть убедиться, что tooreview hello текстовое описание hello службы в верхней части hello.</span><span class="sxs-lookup"><span data-stu-id="34671-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="34671-163">Если ваше предложение состоит из двух или нескольких служб вызов вкладки hello в hello нижней tooswitch toohello Далее службы tooreview и тестирование.</span><span class="sxs-lookup"><span data-stu-id="34671-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="34671-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34671-164">Next step</span></span>
<span data-ttu-id="34671-165">Если у вас возникают проблемы и требуется помощь для их устранения, обратитесь в [службу поддержки издателей Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="34671-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="34671-166">Если вы удовлетворены, и готов toopublish ваше предложение прочитайте hello [tooProduction tooPush запросить утверждение](marketplace-publishing-push-to-production.md) документации.</span><span class="sxs-lookup"><span data-stu-id="34671-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="34671-167">См. также</span><span class="sxs-lookup"><span data-stu-id="34671-167">See Also</span></span>
* [<span data-ttu-id="34671-168">Приступая к работе: Как toopublish toohello предложение Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="34671-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

