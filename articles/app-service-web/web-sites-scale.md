---
title: "aaaScale копии приложения в Azure | Документы Microsoft"
description: "Узнайте, как tooscale копирование приложения службы приложений Azure tooadd возможностей и функций."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="fbbeb-103">Увеличение масштаба приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="fbbeb-103">Scale up an app in Azure</span></span>
<span data-ttu-id="fbbeb-104">В этой статье показано, как tooscale приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="fbbeb-105">Есть два рабочих процесса для масштабирования, масштабирования вверх и масштабирование и в этой статье объясняется hello масштабирования рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="fbbeb-106">[Увеличение масштаба](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — получение дополнительных ресурсов, в частности ЦП, памяти и места на диске, и дополнительных возможностей, таких как выделенные виртуальные машины, пользовательские домены и сертификаты, промежуточные слоты, автоматическое масштабирование и т. д.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="fbbeb-107">Можно масштабировать, изменяя Ценовая категория плана служб приложений, к которой принадлежит приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="fbbeb-108">[Горизонтальное масштабирование](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): увеличьте число hello экземпляров виртуальной Машины, запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="fbbeb-109">Можно масштабировать tooas многие как 20 экземпляров в зависимости от ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="fbbeb-110">[Среды службы приложения](../app-service/app-service-app-service-environments-readme.md) в **Premium** будет повышать уровень too50 ваших масштабирование числа экземпляров.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="fbbeb-111">Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="fbbeb-112">Приведены out, как автоматическое масштабирование toouse, который автоматически tooscale число экземпляров на основе предварительно определенные правила и расписания.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="fbbeb-113">Здравствуйте шкалы параметры принимают только секунд tooapply и влияют на все приложения в вашей [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="fbbeb-114">Они не требуют кода вы toochange или повторного развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="fbbeb-115">Сведения о ценах hello и функциональных возможностях отдельных планы служб приложений см. в разделе [сведения о ценах на приложение службы](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="fbbeb-116">Перед переключением план служб приложений из hello **Free** уровня, необходимо сначала удалить hello [лимиты оплаты,](https://azure.microsoft.com/pricing/spending-limits/) на месте для вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="fbbeb-117">tooview или измените параметры для вашей подписки службу приложений Microsoft Azure в разделе [подписки Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="fbbeb-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="fbbeb-118">Увеличение масштаба ценовой категории</span><span class="sxs-lookup"><span data-stu-id="fbbeb-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="fbbeb-119">Откройте в браузере, hello [портал Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="fbbeb-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="fbbeb-120">В колонке приложения щелкните **Все параметры**, а затем — **Увеличить масштаб**.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Перейдите tooscale копии приложения Azure.][ChooseWHP]
3. <span data-ttu-id="fbbeb-122">Выберите нужную категорию, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="fbbeb-123">Hello **уведомления** вкладка будет мигать зеленым **успех** после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="fbbeb-124">Масштабирование связанных ресурсов</span><span class="sxs-lookup"><span data-stu-id="fbbeb-124">Scale related resources</span></span>
<span data-ttu-id="fbbeb-125">Если приложение зависит от других служб, таких как база данных SQL Azure или служба хранилища Azure, их масштаб также можно увеличить в зависимости от ваших потребностей.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="fbbeb-126">Эти ресурсы не масштабируются hello план служб приложений и должен быть масштабирована отдельно.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="fbbeb-127">В **Essentials**, нажмите кнопку hello **группы ресурсов** ссылку.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Увеличение масштаба связанных ресурсов приложения Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="fbbeb-129">В hello **Сводка** частью hello **группы ресурсов** колонка, щелкните ресурс, что tooscale.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="fbbeb-130">Следующий снимок экрана приветствия показаны ресурс базы данных SQL и ресурса хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Перейдите tooscale колонке группы tooresource копии приложения Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="fbbeb-132">Ресурс базы данных SQL, щелкните **параметры** > **Ценовая категория** tooscale hello ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Вертикальное масштабирование hello серверной базы данных SQL для приложения Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="fbbeb-134">Можно также включить [георепликацию](../sql-database/sql-database-geo-replication-overview.md) для экземпляра базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="fbbeb-135">Для ресурса хранилища Azure, нажмите кнопку **параметры** > **конфигурации** tooscale копирование возможности хранения данных.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Вертикальное масштабирование учетной записи хранилища Azure hello, используемые приложением Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="fbbeb-137">Возможности для разработчика</span><span class="sxs-lookup"><span data-stu-id="fbbeb-137">Learn about developer features</span></span>
<span data-ttu-id="fbbeb-138">В зависимости от ценового уровня hello hello ориентированные на разработчиков доступны следующие функции:</span><span class="sxs-lookup"><span data-stu-id="fbbeb-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="fbbeb-139">Разрядность</span><span class="sxs-lookup"><span data-stu-id="fbbeb-139">Bitness</span></span>
* <span data-ttu-id="fbbeb-140">Hello **основные**, **Стандартная**, и **Premium** уровни поддержки 64-разрядных и 32-разрядных приложений.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="fbbeb-141">Hello **Free** и **Shared** плана уровней поддерживает только 32-разрядных приложений.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="fbbeb-142">Поддержка отладчика</span><span class="sxs-lookup"><span data-stu-id="fbbeb-142">Debugger support</span></span>
* <span data-ttu-id="fbbeb-143">Поддержка отладчика для hello **Free**, **Shared**, и **основные** режимов в одно подключение для каждого плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="fbbeb-144">Поддержка отладчика для hello **Стандартная** и **Premium** режимов в пяти одновременных подключений на план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="fbbeb-145">Дополнительные возможности</span><span class="sxs-lookup"><span data-stu-id="fbbeb-145">Learn about other features</span></span>
* <span data-ttu-id="fbbeb-146">Подробные сведения обо всех hello оставшихся возможности службы приложения hello схем, включая цены и признаки пользователей tooall процентов (включая разработчиков), см. [сведения о ценах на приложение службы](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="fbbeb-147">Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/) где немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fbbeb-148">Не требуется никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="fbbeb-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbbeb-149">Next steps</span></span>
* <span data-ttu-id="fbbeb-150">tooget работу с Azure, в разделе [бесплатная пробная версия Microsoft](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fbbeb-151">Сведения о ценах, поддержка и соглашение об уровне ОБСЛУЖИВАНИЯ посетите следующие ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="fbbeb-152">Сведения о ценах — передача данных</span><span class="sxs-lookup"><span data-stu-id="fbbeb-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="fbbeb-153">Планы поддержки Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fbbeb-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="fbbeb-154">Соглашения об уровне обслуживания</span><span class="sxs-lookup"><span data-stu-id="fbbeb-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="fbbeb-155">Сведения о ценах — база данных SQL</span><span class="sxs-lookup"><span data-stu-id="fbbeb-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="fbbeb-156">[Размеры виртуальных машин и облачных служб для Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="fbbeb-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="fbbeb-157">Сведения о ценах на службу приложений</span><span class="sxs-lookup"><span data-stu-id="fbbeb-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="fbbeb-158">Сведения о ценах на службу приложений — SSL-соединения</span><span class="sxs-lookup"><span data-stu-id="fbbeb-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="fbbeb-159">Рекомендации по использованию службы приложений Azure, в том числе по созданию масштабируемой и устойчивой архитектуры, см. [здесь](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbbeb-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="fbbeb-160">Видео о масштабировании приложения служб приложений см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="fbbeb-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="fbbeb-161">Если tooScale веб-сайтов Azure - с (Stefan Schackow)</span><span class="sxs-lookup"><span data-stu-id="fbbeb-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="fbbeb-162">Стефан Шаков (Stefan Schackow). Автоматическое масштабирование веб-сайтов Azure, ЦП или по расписанию</span><span class="sxs-lookup"><span data-stu-id="fbbeb-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="fbbeb-163">Стефан Шаков (Stefan Schackow). Как масштабируются веб-сайты Azure</span><span class="sxs-lookup"><span data-stu-id="fbbeb-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
