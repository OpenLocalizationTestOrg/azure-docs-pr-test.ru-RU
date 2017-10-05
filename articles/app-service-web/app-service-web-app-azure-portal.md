---
title: "Краткий справочник по навигации на портале Azure"
description: "Узнайте о различиях в пользовательском интерфейсе для веб-службы приложений между порталом управления и порталом Azure."
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="d1a3c-103">Краткий справочник по навигации на портале Azure</span><span class="sxs-lookup"><span data-stu-id="d1a3c-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="d1a3c-104">Веб-сайты Azure теперь называются [Веб-приложения службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d1a3c-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d1a3c-105">Мы обновляем всю документацию, чтобы отобразить изменения в имени и предоставить инструкции для портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="d1a3c-106">До завершения этого процесса вы можете использовать настоящий документ в качестве руководства по работе с веб-приложениями на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="d1a3c-107">Будущее классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d1a3c-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="d1a3c-108">Хотя вы заметите изменение фирменной символики на классическом портале Azure, он находится в процессе замены на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="d1a3c-109">По мере вывода классического портала из эксплуатации все последующие операции по разработке перемещаются на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="d1a3c-110">Все новые возможности для веб-приложений будут появляться на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="d1a3c-111">Начните работу с порталом Azure, чтобы воспользоваться преимуществами самых новых и лучших возможностей веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="d1a3c-112">Отличия в структуре классического портала Azure и портала Azure</span><span class="sxs-lookup"><span data-stu-id="d1a3c-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="d1a3c-113">На классическом портале все службы Azure перечислены слева.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="d1a3c-114">Навигация по классическому порталу основана на древовидной структуре, где вы начинаете со службы и переходите к каждому следующему элементу.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="d1a3c-115">Эту структуру удобно использовать при управлении независимыми компонентами.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="d1a3c-116">Однако приложения, построенные на платформе Azure, представляют собой коллекцию взаимосвязанных служб, а древовидная структура не слишком хорошо подходит для работы с коллекциями служб.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="d1a3c-117">Портал Azure облегчает процесс комплексного создания приложений с использованием компонентов из нескольких служб.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="d1a3c-118">Портал организован по принципу *путей взаимодействия*(journey).</span><span class="sxs-lookup"><span data-stu-id="d1a3c-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="d1a3c-119">*Journey*— это последовательность *колонок*, которые являются контейнерами для различных компонентов.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="d1a3c-120">Например, настройка автомасштабирования для веб-приложения является *путем взаимодействия*, предоставляющим вам несколько колонок, как показано в следующем примере: колонка **веб-сайта** (заголовок этой колонки еще не обновлен в соответствии с новой терминологией), колонка **Параметры** и колонка **Горизонтальное масштабирование**.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="d1a3c-121">В этом примере автомасштабирование задано зависимым от уровня загрузки ЦП, поэтому используется также выноска **Процент ЦП** .</span><span class="sxs-lookup"><span data-stu-id="d1a3c-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="d1a3c-122">Компоненты в *колонках* называются *частями*, которые похожи на элементы.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="d1a3c-123">Пример навигации: создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d1a3c-123">Navigation example: create a web app</span></span>
<span data-ttu-id="d1a3c-124">Создание нового веб-приложения осуществляется просто, как 1 — 2 — 3.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="d1a3c-125">На следующем рисунке показаны классический портал Azure и портал Azure, чтобы продемонстрировать, что число шагов, необходимых для создания и запуска веб-приложения, осталось примерно на прежнем уровне.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="d1a3c-126">На портале можно выбрать один из наиболее распространенных типов веб-приложений, включая популярные приложения из коллекции, такие как WordPress.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="d1a3c-127">Полный список доступных приложений доступен на сайте [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="d1a3c-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="d1a3c-128">При создании веб-приложения необходимо указать URL-адрес, план службы приложений и расположение на портале — все точно так же, как и на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="d1a3c-129">Кроме того, портал позволяет определять другие общие параметры.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="d1a3c-130">Например, [группы ресурсов](../azure-resource-manager/resource-group-overview.md) упрощают просмотр связанных ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="d1a3c-131">Пример навигации: параметры и возможности</span><span class="sxs-lookup"><span data-stu-id="d1a3c-131">Navigation example: settings and features</span></span>
<span data-ttu-id="d1a3c-132">Все параметры и возможности теперь логически сгруппированы в одной выноске, с которой вы можете осуществлять навигацию.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="d1a3c-133">Например, можно создать пользовательские домены, щелкнув **Пользовательские домены и SSL** в колонке **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="d1a3c-134">Чтобы настроить оповещение мониторинга, щелкните **Запросы и ошибки**, а затем выберите **Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="d1a3c-135">Чтобы включить диагностику, щелкните **Журналы диагностики** в колонке **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="d1a3c-136">Чтобы настроить параметры приложения, щелкните **Параметры приложения** в колонке **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="d1a3c-137">За исключением имени торговой марки, на портале имеется довольно мало компонентов, которые были переименованы или иначе сгруппированы, что позволяет упростить их поиск.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="d1a3c-138">Например, ниже приведен снимок экрана с соответствующей страницей параметров приложения (**Настройка**) на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="d1a3c-139">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d1a3c-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="d1a3c-140">[Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="d1a3c-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="d1a3c-141">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d1a3c-142">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="d1a3c-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="d1a3c-143">Изменения</span><span class="sxs-lookup"><span data-stu-id="d1a3c-143">What's changed</span></span>
* <span data-ttu-id="d1a3c-144">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d1a3c-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

