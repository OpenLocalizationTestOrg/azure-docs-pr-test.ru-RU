---
title: "Начало работы с Microsoft Power BI Embedded"
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
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="4e863-103">Начало работы с Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e863-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="4e863-104">**Power BI Embedded** — это служба Azure, которая позволяет разработчикам приложений добавлять интерактивные отчеты Power BI в свои приложения.</span><span class="sxs-lookup"><span data-stu-id="4e863-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="4e863-105">**Power BI Embedded** работала с существующими приложениями, вам не нужно изменять способ, с помощью которого пользователи выполняют вход.</span><span class="sxs-lookup"><span data-stu-id="4e863-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="4e863-106">Ресурсы для **Microsoft Power BI Embedded** подготавливаются через [API-интерфейсы ARM Azure](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e863-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="4e863-107">В нашем примере подготавливаемый ресурс — это **коллекция рабочих областей Power BI**.</span><span class="sxs-lookup"><span data-stu-id="4e863-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="4e863-108">Создание коллекции рабочей области</span><span class="sxs-lookup"><span data-stu-id="4e863-108">Create a workspace collection</span></span>

<span data-ttu-id="4e863-109">**Коллекция рабочей области** — это ресурс и контейнер Azure верхнего уровня для содержимого, которое будет внедрено в приложение.</span><span class="sxs-lookup"><span data-stu-id="4e863-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="4e863-110">**Коллекцию рабочей области** можно создать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="4e863-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="4e863-111">вручную с помощью портала Azure;</span><span class="sxs-lookup"><span data-stu-id="4e863-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="4e863-112">программно с помощью интерфейсов API Resource Manager (ARM).</span><span class="sxs-lookup"><span data-stu-id="4e863-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="4e863-113">Давайте узнаем, как создать **коллекцию рабочей области** с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4e863-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="4e863-114">Войдите на **портал Azure**по адресу [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e863-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="4e863-115">На панели вверху щелкните **+Создать** .</span><span class="sxs-lookup"><span data-stu-id="4e863-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="4e863-116">В разделе **Данные+аналитика** щелкните **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="4e863-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="4e863-117">В колонке **Коллекция рабочей области** введите необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="4e863-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="4e863-118">Дополнительные сведения о **ценообразовании** см. на странице с информацией о [ценах на Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="4e863-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="4e863-119">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4e863-119">Click **Create**.</span></span>

<span data-ttu-id="4e863-120">Подготовка **коллекции рабочей области** займет несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="4e863-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="4e863-121">После этого откроется колонка **Коллекция рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="4e863-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="4e863-122">Эта **колонка создания** содержит сведения, необходимые для вызова API-интерфейсов, которые создают рабочие области и развертывают содержимое.</span><span class="sxs-lookup"><span data-stu-id="4e863-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="4e863-123">Просмотр ключей доступа для вызова API Power BI</span><span class="sxs-lookup"><span data-stu-id="4e863-123">View Power BI API access keys</span></span>

<span data-ttu-id="4e863-124">Сведения, необходимые для вызова REST API Power BI, включают в себя такой важный элемент, как **ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="4e863-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="4e863-125">Эти ключи используются для создания **маркеров приложения** для проверки подлинности запросов к API.</span><span class="sxs-lookup"><span data-stu-id="4e863-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="4e863-126">Чтобы просмотреть **ключи доступа**, в **колонке параметров** щелкните **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="4e863-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="4e863-127">Дополнительные сведения о **маркерах приложений** см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="4e863-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="4e863-128">Обратите внимание: у вас есть два ключа.</span><span class="sxs-lookup"><span data-stu-id="4e863-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="4e863-129">Скопируйте эти ключи и надежно сохраните их в приложении.</span><span class="sxs-lookup"><span data-stu-id="4e863-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="4e863-130">Очень важно обращаться с этими ключами как с паролем, так как они предоставляют доступ ко всему содержимому в **коллекции рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="4e863-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="4e863-131">Хотя указаны два ключа, в один момент времени используется только один из них.</span><span class="sxs-lookup"><span data-stu-id="4e863-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="4e863-132">Второй ключ нужен, чтобы не прерывать доступ к службе во время периодического повторного создания ключей.</span><span class="sxs-lookup"><span data-stu-id="4e863-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="4e863-133">Теперь, когда у вас есть экземпляр Power BI для приложения и **ключи доступа**, вы можете импортировать отчет в свое приложение.</span><span class="sxs-lookup"><span data-stu-id="4e863-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="4e863-134">Прежде чем вы узнаете, как импортировать отчет, в следующем разделе мы расскажем о создании наборов данных и отчетов Power BI, которые будут внедрены в приложение.</span><span class="sxs-lookup"><span data-stu-id="4e863-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="4e863-135">Работа с рабочими областями</span><span class="sxs-lookup"><span data-stu-id="4e863-135">Working with workspaces</span></span>

<span data-ttu-id="4e863-136">После создания коллекции рабочих областей необходимо создать рабочую область для размещения отчетов и наборов данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="4e863-137">Чтобы создать рабочую область, необходимо использовать [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e863-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="4e863-138">Создание наборов данных и отчетов Power BI для внедрения в приложение с помощью Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="4e863-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="4e863-139">Теперь, когда вы создали экземпляр Power BI для приложения и получили **ключи доступа**, можно приступать к созданию наборов данных и отчетов Power BI для внедрения.</span><span class="sxs-lookup"><span data-stu-id="4e863-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="4e863-140">Наборы данных и отчеты можно создавать с помощью **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="4e863-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="4e863-141">[Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662) можно скачать бесплатно.</span><span class="sxs-lookup"><span data-stu-id="4e863-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="4e863-142">Или же, чтобы быстро приступить к работе, можно скачать [PBIX-файл с примером анализа данных о продажах](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="4e863-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="4e863-143">Дополнительные сведения об использовании **Power BI Desktop** см. в статье [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="4e863-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="4e863-144">С помощью **Power BI Desktop** вы можете подключиться к источнику данных. Для этого импортируйте копию данных в **Power BI Desktop** или подключитесь непосредственно к источнику данных с помощью **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="4e863-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="4e863-145">Ниже описаны различия между **импортом** и **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="4e863-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="4e863-146">Импорт</span><span class="sxs-lookup"><span data-stu-id="4e863-146">Import</span></span> | <span data-ttu-id="4e863-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="4e863-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="4e863-148">Таблицы, столбцы *и данные* импортируются или копируются в **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="4e863-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="4e863-149">При работе с представлениями **Power BI Desktop** запрашивает копию данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="4e863-150">Чтобы определить изменения в базовых данных, вам нужно повторно обновить или импортировать готовый текущий набор данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="4e863-151">В *Power BI Desktop* импортируются или копируются только **таблицы и столбцы**.</span><span class="sxs-lookup"><span data-stu-id="4e863-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="4e863-152">При работе с представлениями **Power BI Desktop** запрашивает базовый источник данных (это значит, что вы всегда просматриваете актуальные данные).</span><span class="sxs-lookup"><span data-stu-id="4e863-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="4e863-153">Дополнительные сведения о подключении к источнику данных см. в [этой статье](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="4e863-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="4e863-154">Когда вы сохраните документ в **Power BI Desktop**, будет создан PBIX-файл.</span><span class="sxs-lookup"><span data-stu-id="4e863-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="4e863-155">Этот файл содержит ваш отчет.</span><span class="sxs-lookup"><span data-stu-id="4e863-155">This file contains your report.</span></span> <span data-ttu-id="4e863-156">Кроме того, при импорте данных PBIX-файл будет содержать полный набор данных, а при использовании **DirectQuery**— только схему набора данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="4e863-157">В рабочей области PBIX-файл развертывается программным способом с помощью [API импорта Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e863-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4e863-158">**Power BI Embedded** предусматривает дополнительные API. С их помощью можно изменять сервер и базу данных, на которые указывает ваш набор данных, а также указывать данные учетной записи службы для подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="4e863-159">Дополнительные сведения см. в статьях [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (Публикация SetAllConnections) и [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Исправление источника данных шлюза).</span><span class="sxs-lookup"><span data-stu-id="4e863-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="4e863-160">Создание наборов данных и отчетов Power BI с помощью API</span><span class="sxs-lookup"><span data-stu-id="4e863-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="4e863-161">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="4e863-161">Datsets</span></span>

<span data-ttu-id="4e863-162">Вы можете создавать наборы данных в Power BI Embedded с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="4e863-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="4e863-163">Затем данные можно передать в свой набор данных.</span><span class="sxs-lookup"><span data-stu-id="4e863-163">You can then push data into your dataset.</span></span> <span data-ttu-id="4e863-164">Это позволит работать с данными без использования Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="4e863-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="4e863-165">Дополнительные сведения см. в статье о [публикации наборов данных](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e863-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="4e863-166">Отчеты</span><span class="sxs-lookup"><span data-stu-id="4e863-166">Reports</span></span>

<span data-ttu-id="4e863-167">С помощью API JavaScript можно создать отчет на основе набора данных прямо в приложении.</span><span class="sxs-lookup"><span data-stu-id="4e863-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="4e863-168">Дополнительные сведения см. в статье [Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="4e863-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4e863-169">См. также</span><span class="sxs-lookup"><span data-stu-id="4e863-169">See Also</span></span>

[<span data-ttu-id="4e863-170">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e863-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="4e863-171">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e863-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="4e863-172">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e863-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="4e863-173">[Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Сохранение отчетов в Power BI Embedded](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="4e863-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="4e863-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="4e863-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="4e863-175">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e863-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="4e863-176">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="4e863-176">More questions?</span></span> [<span data-ttu-id="4e863-177">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="4e863-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)

