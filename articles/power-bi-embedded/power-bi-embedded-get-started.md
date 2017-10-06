---
title: "aaaGet работы с Microsoft Power BI Embedded"
description: "Power BI Embedded, добавление интерактивных отчетов Power BI в приложение бизнес-аналитики"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="7dabb-103">Начало работы с Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7dabb-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="7dabb-104">**Power BI Embedded** — это служба Azure, tooadd разработчики приложений включает интерактивных отчетов Power BI в собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="7dabb-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="7dabb-105">**Power BI Embedded** входа работает с существующие приложения без необходимости переработки и изменение пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7dabb-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="7dabb-106">Ресурсы для **Microsoft Power BI Embedded** подготовленные в hello [API-интерфейсов Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dabb-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="7dabb-107">В этом случае является подготовка ресурсов hello **коллекции рабочей области Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="7dabb-108">Создание коллекции рабочей области</span><span class="sxs-lookup"><span data-stu-id="7dabb-108">Create a workspace collection</span></span>

<span data-ttu-id="7dabb-109">Объект **коллекции рабочей** hello верхнего уровня ресурсов Azure и контейнер для содержимого hello, который будет внедрен в приложении.</span><span class="sxs-lookup"><span data-stu-id="7dabb-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="7dabb-110">**Коллекцию рабочей области** можно создать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="7dabb-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="7dabb-111">Вручную с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="7dabb-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="7dabb-112">Программно с помощью API-интерфейсов Manager(ARM) ресурсов Azure hello</span><span class="sxs-lookup"><span data-stu-id="7dabb-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="7dabb-113">Давайте рассмотрим hello действия toobuild **коллекции рабочей** с помощью портала Azure "hello".</span><span class="sxs-lookup"><span data-stu-id="7dabb-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="7dabb-114">Войдите на **портал Azure**по адресу [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7dabb-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="7dabb-115">Нажмите кнопку **+ создать** на верхней панели hello.</span><span class="sxs-lookup"><span data-stu-id="7dabb-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="7dabb-116">В разделе **Данные+аналитика** щелкните **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="7dabb-117">На hello **колонке коллекции рабочей**, введите hello необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="7dabb-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="7dabb-118">Дополнительные сведения о **ценообразовании** см. на странице с информацией о [ценах на Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="7dabb-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="7dabb-119">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-119">Click **Create**.</span></span>

<span data-ttu-id="7dabb-120">Hello **коллекции рабочей** займет несколько секунд tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7dabb-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="7dabb-121">После завершения вы будете перенаправлены toohello **колонке коллекции рабочей**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="7dabb-122">Hello **создания колонке** содержит hello информацию, необходимую hello toocall API-интерфейсы, создание рабочих областей и развертывание содержимого toothem.</span><span class="sxs-lookup"><span data-stu-id="7dabb-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="7dabb-123">Просмотр ключей доступа для вызова API Power BI</span><span class="sxs-lookup"><span data-stu-id="7dabb-123">View Power BI API access keys</span></span>

<span data-ttu-id="7dabb-124">Одно из наиболее важные части информации, необходимой toocall hello интерфейсы API REST Power BI hello, hello **клавиши доступа**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="7dabb-125">Ниже перечислены используемые toogenerate hello **токенов приложения** таблицы, используемые tooauthenticate запросов API.</span><span class="sxs-lookup"><span data-stu-id="7dabb-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="7dabb-126">tooview вашей **клавиши доступа**, нажмите кнопку **клавиши доступа** на hello **колонку параметров**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="7dabb-127">Дополнительные сведения о **маркерах приложений** см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="7dabb-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="7dabb-128">Обратите внимание: у вас есть два ключа.</span><span class="sxs-lookup"><span data-stu-id="7dabb-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="7dabb-129">Скопируйте эти ключи и надежно сохраните их в приложении.</span><span class="sxs-lookup"><span data-stu-id="7dabb-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="7dabb-130">Очень важно, можно обработать эти ключи как пароль, так как они будут позволяют получать доступ к содержимому hello tooall в вашей **рабочей коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="7dabb-131">Хотя указаны два ключа, в один момент времени используется только один из них.</span><span class="sxs-lookup"><span data-stu-id="7dabb-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="7dabb-132">второй ключ Hello предоставляется, можно периодически повторного создания ключей без прерывания работы служб toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="7dabb-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="7dabb-133">Теперь, когда у вас есть экземпляр Power BI для приложения и **ключи доступа**, вы можете импортировать отчет в свое приложение.</span><span class="sxs-lookup"><span data-stu-id="7dabb-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="7dabb-134">Прежде чем вы узнаете, как tooimport отчет hello следующий раздел описывает создание tooembed наборы данных и отчеты Power BI в приложение.</span><span class="sxs-lookup"><span data-stu-id="7dabb-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="7dabb-135">Работа с рабочими областями</span><span class="sxs-lookup"><span data-stu-id="7dabb-135">Working with workspaces</span></span>

<span data-ttu-id="7dabb-136">После создания коллекции рабочей области потребуется toocreate рабочей области, где будет размещена отчеты и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="7dabb-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="7dabb-137">toocreate рабочей области потребуется toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dabb-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="7dabb-138">Создание tooembed наборы данных и отчеты Power BI в приложение с помощью Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7dabb-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="7dabb-139">Вы создали экземпляр Power BI для приложения и наличии **клавиши доступа**, вам понадобится toocreate hello Power BI, наборы данных и отчеты, которые должны tooembed.</span><span class="sxs-lookup"><span data-stu-id="7dabb-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="7dabb-140">Наборы данных и отчеты можно создавать с помощью **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="7dabb-141">[Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662) можно скачать бесплатно.</span><span class="sxs-lookup"><span data-stu-id="7dabb-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="7dabb-142">Или, tooquickly приступить к работе, вы можете загрузить hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="7dabb-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="7dabb-143">Дополнительные сведения о том, как toolearn toouse **Power BI Desktop**, в разделе [Приступая к работе с Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="7dabb-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="7dabb-144">С **Power BI Desktop**, подключите tooyour источника данных путем импорта копии данных hello в **Power BI Desktop** или непосредственное подключение toohello данных источника с помощью **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="7dabb-145">Ниже приведены hello различия между использованием **импорта** и **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="7dabb-146">Импорт</span><span class="sxs-lookup"><span data-stu-id="7dabb-146">Import</span></span> | <span data-ttu-id="7dabb-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="7dabb-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="7dabb-148">Таблицы, столбцы *и данные* импортируются или копируются в **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7dabb-149">При работе с визуализациями, **Power BI Desktop** запрашивает копию данных hello.</span><span class="sxs-lookup"><span data-stu-id="7dabb-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="7dabb-150">toosee всех изменений, произошедших toohello базовых данных, необходимо обновить или импортировать завершения, текущее набора данных еще раз.</span><span class="sxs-lookup"><span data-stu-id="7dabb-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="7dabb-151">В *Power BI Desktop* импортируются или копируются только **таблицы и столбцы**.</span><span class="sxs-lookup"><span data-stu-id="7dabb-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7dabb-152">При работе с визуализациями, **Power BI Desktop** запросы hello базового источника данных, поэтому вы всегда просматриваете актуальные данные.</span><span class="sxs-lookup"><span data-stu-id="7dabb-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="7dabb-153">Дополнительные сведения о подключении источника данных tooa см. в разделе [подключить источник данных tooa](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="7dabb-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="7dabb-154">Когда вы сохраните документ в **Power BI Desktop**, будет создан PBIX-файл.</span><span class="sxs-lookup"><span data-stu-id="7dabb-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="7dabb-155">Этот файл содержит ваш отчет.</span><span class="sxs-lookup"><span data-stu-id="7dabb-155">This file contains your report.</span></span> <span data-ttu-id="7dabb-156">Кроме того, при импорте данных hello pbix-ФАЙЛ содержит hello всего набора данных, или если вы используете **DirectQuery**, hello pbix-ФАЙЛ содержит только схему набора данных.</span><span class="sxs-lookup"><span data-stu-id="7dabb-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="7dabb-157">Программным способом развертывания hello pbix-ФАЙЛ в рабочую область с помощью hello [импорта API Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dabb-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7dabb-158">**Power BI Embedded** имеет дополнительные интерфейсы API toochange hello сервера и базы данных, что набор данных указывает tooand набор учетных данных учетной записи службы, hello набор данных будет использовать базу данных tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7dabb-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="7dabb-159">Дополнительные сведения см. в статьях [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (Публикация SetAllConnections) и [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Исправление источника данных шлюза).</span><span class="sxs-lookup"><span data-stu-id="7dabb-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="7dabb-160">Создание наборов данных и отчетов Power BI с помощью API</span><span class="sxs-lookup"><span data-stu-id="7dabb-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="7dabb-161">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="7dabb-161">Datsets</span></span>

<span data-ttu-id="7dabb-162">Можно создать наборы данных в Power BI Embedded с помощью API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="7dabb-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="7dabb-163">Затем данные можно передать в свой набор данных.</span><span class="sxs-lookup"><span data-stu-id="7dabb-163">You can then push data into your dataset.</span></span> <span data-ttu-id="7dabb-164">Это позволяет toowork с данными без необходимости hello Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7dabb-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="7dabb-165">Дополнительные сведения см. в статье о [публикации наборов данных](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dabb-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="7dabb-166">Отчеты</span><span class="sxs-lookup"><span data-stu-id="7dabb-166">Reports</span></span>

<span data-ttu-id="7dabb-167">Можно создать отчет из набора данных непосредственно в приложение с помощью hello JavaScript API.</span><span class="sxs-lookup"><span data-stu-id="7dabb-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="7dabb-168">Дополнительные сведения см. в статье [Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="7dabb-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7dabb-169">См. также</span><span class="sxs-lookup"><span data-stu-id="7dabb-169">See Also</span></span>

[<span data-ttu-id="7dabb-170">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7dabb-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7dabb-171">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7dabb-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7dabb-172">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7dabb-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="7dabb-173">[Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Сохранение отчетов в Power BI Embedded](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="7dabb-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="7dabb-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7dabb-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7dabb-175">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="7dabb-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7dabb-176">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="7dabb-176">More questions?</span></span> [<span data-ttu-id="7dabb-177">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="7dabb-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

