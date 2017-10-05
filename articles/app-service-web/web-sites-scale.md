---
title: "Увеличение масштаба приложения в Azure | Документация Майкрософт"
description: "Узнайте, как увеличить масштаб приложения в службе приложений Azure для добавления емкости и расширения функций."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="d0765-103">Увеличение масштаба приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="d0765-103">Scale up an app in Azure</span></span>
<span data-ttu-id="d0765-104">В этой статье показано, как масштабировать приложение в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="d0765-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="d0765-105">Существует два рабочих процесса масштабирования (увеличение масштаба и развертывание), и в этой статье рассматривается первый из них.</span><span class="sxs-lookup"><span data-stu-id="d0765-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="d0765-106">[Увеличение масштаба](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — получение дополнительных ресурсов, в частности ЦП, памяти и места на диске, и дополнительных возможностей, таких как выделенные виртуальные машины, пользовательские домены и сертификаты, промежуточные слоты, автоматическое масштабирование и т. д.</span><span class="sxs-lookup"><span data-stu-id="d0765-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="d0765-107">Чтобы увеличить масштаб приложения, следует изменить ценовую категорию плана службы приложений, к которому относится ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d0765-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="d0765-108">[Развертывание](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — увеличение количества экземпляров виртуальных машин, на которых работает приложение.</span><span class="sxs-lookup"><span data-stu-id="d0765-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="d0765-109">В зависимости от ценовой категории вы можете развернуть приложение на виртуальных машинах в количестве до 20 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="d0765-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="d0765-110">Использование [сред службы приложений](../app-service/app-service-app-service-environments-readme.md) на уровне **Премиум** позволит увеличить количество экземпляров до 50.</span><span class="sxs-lookup"><span data-stu-id="d0765-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="d0765-111">Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d0765-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="d0765-112">В ней вы узнаете, как использовать автомасштабирование, которое позволяет масштабировать число экземпляров автоматически на основе предварительно определенных правил и расписаний.</span><span class="sxs-lookup"><span data-stu-id="d0765-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="d0765-113">Применение этих параметров масштаба занимает всего несколько секунд, но они влияют на все приложения в вашем [плане службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0765-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="d0765-114">Для этого не требуется вносить изменения в код или повторно развертывать приложение.</span><span class="sxs-lookup"><span data-stu-id="d0765-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="d0765-115">Сведения о ценах и функциях отдельных планов службы приложений см. [здесь](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d0765-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="d0765-116">Прежде чем сменить уровень **Бесплатный** для плана службы приложений, следует снять имеющиеся [ограничения на расходы](https://azure.microsoft.com/pricing/spending-limits/), установленные для вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d0765-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="d0765-117">Просмотреть или изменить параметры подписки на службу приложений Microsoft Azure можно на странице [подписок Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="d0765-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="d0765-118">Увеличение масштаба ценовой категории</span><span class="sxs-lookup"><span data-stu-id="d0765-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="d0765-119">В браузере откройте [портал Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d0765-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="d0765-120">В колонке приложения щелкните **Все параметры**, а затем — **Увеличить масштаб**.</span><span class="sxs-lookup"><span data-stu-id="d0765-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Переход для увеличения масштаба приложения Azure][ChooseWHP]
3. <span data-ttu-id="d0765-122">Выберите нужную категорию, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d0765-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="d0765-123">После завершения операции на вкладке **Уведомления** появится зеленая надпись **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="d0765-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="d0765-124">Масштабирование связанных ресурсов</span><span class="sxs-lookup"><span data-stu-id="d0765-124">Scale related resources</span></span>
<span data-ttu-id="d0765-125">Если приложение зависит от других служб, таких как база данных SQL Azure или служба хранилища Azure, их масштаб также можно увеличить в зависимости от ваших потребностей.</span><span class="sxs-lookup"><span data-stu-id="d0765-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="d0765-126">Эти ресурсы не масштабируется с планом службы приложений и должны масштабироваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="d0765-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="d0765-127">В разделе **Основное** щелкните ссылку **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="d0765-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Увеличение масштаба связанных ресурсов приложения Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="d0765-129">В области **Сводка** колонки**Группа ресурсов** щелкните ресурс, который нужно масштабировать.</span><span class="sxs-lookup"><span data-stu-id="d0765-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="d0765-130">На приведенном ниже снимке экрана показаны ресурс базы данных SQL и ресурс службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d0765-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Переход в колонку группы ресурсов для увеличения масштаба приложения Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="d0765-132">Для ресурса базы данных SQL щелкните **Параметры** > **Ценовая категория**, чтобы изменить ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="d0765-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Увеличение масштаба внутреннего сервера базы данных SQL для приложения Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="d0765-134">Можно также включить [георепликацию](../sql-database/sql-database-geo-replication-overview.md) для экземпляра базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d0765-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="d0765-135">Для ресурса службы хранилища Azure щелкните **Параметры** > **Конфигурация**, чтобы изменить возможности хранилища.</span><span class="sxs-lookup"><span data-stu-id="d0765-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Увеличение масштаба учетной записи хранения Azure, используемой приложением Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="d0765-137">Возможности для разработчика</span><span class="sxs-lookup"><span data-stu-id="d0765-137">Learn about developer features</span></span>
<span data-ttu-id="d0765-138">В зависимости от ценовой категории будут доступны следующие возможности для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="d0765-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="d0765-139">Разрядность</span><span class="sxs-lookup"><span data-stu-id="d0765-139">Bitness</span></span>
* <span data-ttu-id="d0765-140">Уровни **Базовый**, **Стандартный** и **Премиум** поддерживают 64-разрядные и 32-разрядные приложения.</span><span class="sxs-lookup"><span data-stu-id="d0765-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="d0765-141">Уровни **Бесплатный** и **Общий** поддерживают только 32-разрядные приложения.</span><span class="sxs-lookup"><span data-stu-id="d0765-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="d0765-142">Поддержка отладчика</span><span class="sxs-lookup"><span data-stu-id="d0765-142">Debugger support</span></span>
* <span data-ttu-id="d0765-143">Отладчик поддерживается на уровнях **Бесплатный**, **Общий** и **Базовый** для одного подключения на план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d0765-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="d0765-144">Отладчик поддерживается на уровнях **Стандартный** и **Премиум** для пяти одновременных подключений на план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d0765-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="d0765-145">Дополнительные возможности</span><span class="sxs-lookup"><span data-stu-id="d0765-145">Learn about other features</span></span>
* <span data-ttu-id="d0765-146">Подробные сведения обо всех оставшихся функциях в планах службы приложений, включая цены и функции, интересующие всех пользователей (в том числе разработчиков), см. [здесь](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d0765-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="d0765-147">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Try App Service](https://azure.microsoft.com/try/app-service/) (Пробное использование службы приложений), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="d0765-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d0765-148">Не требуется никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="d0765-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="d0765-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0765-149">Next steps</span></span>
* <span data-ttu-id="d0765-150">Чтобы начать работу с Azure, [создайте бесплатную пробную учетную запись Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0765-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d0765-151">Сведения о ценах, поддержке и соглашениях об уровне обслуживания см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="d0765-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="d0765-152">Сведения о ценах — передача данных</span><span class="sxs-lookup"><span data-stu-id="d0765-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="d0765-153">Планы поддержки Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0765-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="d0765-154">Соглашения об уровне обслуживания</span><span class="sxs-lookup"><span data-stu-id="d0765-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="d0765-155">Сведения о ценах — база данных SQL</span><span class="sxs-lookup"><span data-stu-id="d0765-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="d0765-156">[Размеры виртуальных машин и облачных служб для Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="d0765-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="d0765-157">Сведения о ценах на службу приложений</span><span class="sxs-lookup"><span data-stu-id="d0765-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="d0765-158">Сведения о ценах на службу приложений — SSL-соединения</span><span class="sxs-lookup"><span data-stu-id="d0765-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="d0765-159">Рекомендации по использованию службы приложений Azure, в том числе по созданию масштабируемой и устойчивой архитектуры, см. [здесь](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0765-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="d0765-160">Видео о масштабировании приложений службы приложений см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="d0765-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="d0765-161">Стефан Шаков (Stefan Schackow). Когда следует масштабировать веб-сайты Azure</span><span class="sxs-lookup"><span data-stu-id="d0765-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="d0765-162">Стефан Шаков (Stefan Schackow). Автоматическое масштабирование веб-сайтов Azure, ЦП или по расписанию</span><span class="sxs-lookup"><span data-stu-id="d0765-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="d0765-163">Стефан Шаков (Stefan Schackow). Как масштабируются веб-сайты Azure</span><span class="sxs-lookup"><span data-stu-id="d0765-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
