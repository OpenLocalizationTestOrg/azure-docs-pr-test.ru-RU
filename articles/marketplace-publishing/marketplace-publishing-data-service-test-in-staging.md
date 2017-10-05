---
title: "Тестирование предложения службы данных для Marketplace | Документация Майкрософт"
description: "Узнайте, как протестировать предложение службы данных для Azure Marketplace."
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
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="0e659-103">Тестирование предложения службы данных в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="0e659-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0e659-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="0e659-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="0e659-105">Дополнительные сведения о публикации бизнес-приложения SaaS на AppSource см. [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="0e659-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="0e659-106">Дополнительные сведения о публикации приложений IaaS или службы разработчика в Azure Marketplace см. [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="0e659-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="0e659-107">После выполнения первых двух шагов из статьи [Создание учетной записи разработчика Майкрософт](marketplace-publishing-accounts-creation-registration.md) и [руководства по публикации службы данных для Azure Marketplace](marketplace-publishing-data-service-creation.md) вы готовы выставить свое предложение в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0e659-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="0e659-108">В этом разделе описывается первый промежуточный шаг под названием "Промежуточное развертывание".</span><span class="sxs-lookup"><span data-stu-id="0e659-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="0e659-109">Промежуточное развертывание подразумевает развертывание предложения в частной песочнице, в которой вы можете проверить все его функциональные возможности и убедиться в их работе перед публикацией в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0e659-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="0e659-110">Предложение будет выглядеть в промежуточной среде точно так же, как на компьютере клиента после развертывания.</span><span class="sxs-lookup"><span data-stu-id="0e659-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="0e659-111">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="0e659-111">Step 1.</span></span> <span data-ttu-id="0e659-112">Промежуточное развертывание предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-112">Pushing your offer to staging</span></span>
<span data-ttu-id="0e659-113">Промежуточное развертывание позволяет протестировать предложение, прежде чем оно станет доступным для будущих подписчиков.</span><span class="sxs-lookup"><span data-stu-id="0e659-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="0e659-114">Вы увидите, как ваше предложение будет выглядеть и работать для тех, кто подпишется на вашу службу.</span><span class="sxs-lookup"><span data-stu-id="0e659-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="0e659-116">Войдите на [портал публикации](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="0e659-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="0e659-117">Выберите **Службы данных** в левом окне навигации.</span><span class="sxs-lookup"><span data-stu-id="0e659-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="0e659-118">Выберите предложение, которое нужно переместить в промежуточную среду.</span><span class="sxs-lookup"><span data-stu-id="0e659-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="0e659-119">Появится экран, показанный выше.</span><span class="sxs-lookup"><span data-stu-id="0e659-119">You will see the above screen.</span></span>
4. <span data-ttu-id="0e659-120">Нажмите кнопку **Переместить в промежуточную среду** .</span><span class="sxs-lookup"><span data-stu-id="0e659-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="0e659-121">Если с предложением есть проблемы, которые нужно устранить до размещения в промежуточной среде, отобразится их список.</span><span class="sxs-lookup"><span data-stu-id="0e659-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="0e659-122">Исправьте эти проблемы, щелкнув каждую их них в списке.</span><span class="sxs-lookup"><span data-stu-id="0e659-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="0e659-123">Завершив исправления, нажмите кнопку **Переместить в промежуточную среду** еще раз.</span><span class="sxs-lookup"><span data-stu-id="0e659-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="0e659-124">Если проблем с предложением нет, то появится всплывающее окно, показанное ниже.</span><span class="sxs-lookup"><span data-stu-id="0e659-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="0e659-125">Если вы не планируете или не хотите открывать общий доступ к своему предложению на портале Azure (в настоящее время ресурсы ограничены), то просто закройте всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="0e659-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="0e659-126">Для тестирования службы данных на портале Azure (помимо портала DataMarket) требуется идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0e659-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="0e659-127">Этот идентификатор подписки указывает учетную запись, с помощью которой можно тестировать ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="0e659-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="0e659-128">Вырежьте и вставьте идентификатор подписки и установите флажок, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="0e659-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="0e659-130">Эти идентификаторы подписки Azure требуются только для тестирования и размещения в промежуточной среде на [портале управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0e659-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="0e659-131">Они не нужны для тестирования в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0e659-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="0e659-132">На следующем экране выделенный желтым значок "Выполняется" показывает, что идет публикация.</span><span class="sxs-lookup"><span data-stu-id="0e659-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="0e659-133">Перевод в промежуточную среду занимает от 10 до 15 минут.</span><span class="sxs-lookup"><span data-stu-id="0e659-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="0e659-134">Если прошло больше времени, сначала обновите страницу в браузере (в IE нажмите клавишу F5).</span><span class="sxs-lookup"><span data-stu-id="0e659-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="0e659-135">В редких случаях, когда предложение переводится в промежуточную среду больше часа, щелкните ссылку для связи с нами, чтобы сообщить о проблеме.</span><span class="sxs-lookup"><span data-stu-id="0e659-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="0e659-137">По завершении перевода в промежуточную среду значок "Выполняется" перестанет двигаться, а состояние предложения изменится на "Промежуточная среда".</span><span class="sxs-lookup"><span data-stu-id="0e659-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="0e659-138">Теперь все готово для тестирования предложения.</span><span class="sxs-lookup"><span data-stu-id="0e659-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="0e659-139">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="0e659-139">Step 2.</span></span> <span data-ttu-id="0e659-140">Тестирование предложения в промежуточной среде в DataMarket</span><span class="sxs-lookup"><span data-stu-id="0e659-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="0e659-141">Щелкните ссылку после текста **"Просмотреть предложение службы..."**</span><span class="sxs-lookup"><span data-stu-id="0e659-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="0e659-142">, чтобы открыть экран, который увидит подписчик, когда предложение будет опубликовано в рабочей среде и появится в DataMarket.</span><span class="sxs-lookup"><span data-stu-id="0e659-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="0e659-144">Проверьте каждый из 12 элементов, отмеченных выше, и убедитесь, что все эмблемы, цены и транзакции, текст, изображения, документы и ссылки верны и работают правильно.</span><span class="sxs-lookup"><span data-stu-id="0e659-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="0e659-145">На этом этапе стоит проверить, что все тестовые значения, введенные при создании предложения, были заменены фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="0e659-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="0e659-146">Эмблема предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-146">Offer logo</span></span>
2. <span data-ttu-id="0e659-147">Название предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-147">Offer name</span></span>
3. <span data-ttu-id="0e659-148">Имя издателя и ссылка на веб-сайт компании</span><span class="sxs-lookup"><span data-stu-id="0e659-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="0e659-149">Поисковые категории для предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-149">Search categories for your offer</span></span>
5. <span data-ttu-id="0e659-150">Ссылка, по которой подписчики смогут получить поддержку по предложению</span><span class="sxs-lookup"><span data-stu-id="0e659-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="0e659-151">Контекстное описание предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="0e659-152">План предложения, в котором отражены сведения о выставлении счетов</span><span class="sxs-lookup"><span data-stu-id="0e659-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="0e659-153">Ссылка на код реализации</span><span class="sxs-lookup"><span data-stu-id="0e659-153">Link to implementation code</span></span>
9. <span data-ttu-id="0e659-154">Примеры изображений, иллюстрирующих использование предложения данных</span><span class="sxs-lookup"><span data-stu-id="0e659-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="0e659-155">Метаданные ввода-вывода для каждой службы в составе предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="0e659-156">Условия использования предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="0e659-157">Предварительная версия данных предложения</span><span class="sxs-lookup"><span data-stu-id="0e659-157">Preview of the offer's data</span></span>

<span data-ttu-id="0e659-158">Наконец, убедитесь, что служба будет работать через Datamarket, щелкнув ссылку ПРОСМОТР НАБОРА ДАННЫХ.</span><span class="sxs-lookup"><span data-stu-id="0e659-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="0e659-159">В средстве, которое мы называем "обозревателем служб", откроется новое окно, где можно просмотреть результаты запроса к службе.</span><span class="sxs-lookup"><span data-stu-id="0e659-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="0e659-160">В этом окне можно ввести необходимые параметры и просмотреть результаты запроса к службе.</span><span class="sxs-lookup"><span data-stu-id="0e659-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="0e659-161">Также показан URL-адрес для запроса.</span><span class="sxs-lookup"><span data-stu-id="0e659-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="0e659-162">Проверьте текстовое описание службы, отображенное вверху.</span><span class="sxs-lookup"><span data-stu-id="0e659-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="0e659-163">И если предложение включает вызовы нескольких служб, с помощью вкладок внизу перейдите к следующей службе для проверки.</span><span class="sxs-lookup"><span data-stu-id="0e659-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="0e659-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e659-164">Next step</span></span>
<span data-ttu-id="0e659-165">Если у вас возникают проблемы и требуется помощь для их устранения, обратитесь в [службу поддержки издателей Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="0e659-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="0e659-166">Если все в порядке и вы готовы к публикации предложения, ознакомьтесь с документацией [Запросить утверждение для перемещения в рабочую среду](marketplace-publishing-push-to-production.md) .</span><span class="sxs-lookup"><span data-stu-id="0e659-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="0e659-167">См. также</span><span class="sxs-lookup"><span data-stu-id="0e659-167">See Also</span></span>
* [<span data-ttu-id="0e659-168">Приступая к работе: как опубликовать предложение в Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="0e659-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

