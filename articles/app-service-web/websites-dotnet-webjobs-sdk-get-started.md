---
title: "Создание веб-задания .NET в службе приложений Azure | Документация Майкрософт"
description: "Создание многоуровневого приложения с помощью ASP.NET MVC и Azure. Внешний сервер запускается как веб-приложение в службе приложений Azure, а внутренний сервер — как веб-задание. Приложение использует Entity Framework, базу данных SQL, очереди службы хранилища Azure и большие двоичные объекты."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="645d6-105">Создание веб-задания .NET в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="645d6-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="645d6-106">В этом руководстве показано, как написать код для простого многоуровневого приложения ASP.NET MVC 5, которое использует пакет [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="645d6-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="645d6-107">Назначение [веб-заданий SDK](websites-webjobs-resources.md) — упрощение кода, с помощью которого веб-задание выполняет такие общие задачи, как обработка изображений, обработка очереди, объединение RSS, обслуживание файлов и отправка сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="645d6-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="645d6-108">Пакет SDK для веб-заданий имеет встроенные функции для работы с хранилищем Azure и служебной шиной для планирования задач и обработки ошибок, а также других распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="645d6-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="645d6-109">Этот пакет расширяемый; также существует [репозиторий открытого кода для расширений](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="645d6-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="645d6-110">Пример приложения представляет собой рекламную доску объявлений.</span><span class="sxs-lookup"><span data-stu-id="645d6-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="645d6-111">Пользователи могут загружать изображения для рекламы, а серверный процесс преобразует эти изображения в эскизы.</span><span class="sxs-lookup"><span data-stu-id="645d6-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="645d6-112">На странице списка рекламных объявлений отображаются эскизы, а на странице подробных рекламных сведений — полноразмерное изображение.</span><span class="sxs-lookup"><span data-stu-id="645d6-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="645d6-113">Ниже приведен снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="645d6-113">Here's a screenshot:</span></span>

![Список рекламы](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="645d6-115">В этом примере приложение работает с [очередями Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) и [большими двоичными объектами Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="645d6-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="645d6-116">В руководстве показано, как развернуть приложение в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) и [Базе данных SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="645d6-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="645d6-117"><a id="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="645d6-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="645d6-118">Предполагается, что у вас есть опыт работы с проектами [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="645d6-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="645d6-119">Это руководство изначально было написано для Visual Studio 2013, но его можно использовать с более поздними версиями Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="645d6-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="645d6-120">Если вы используете Visual Studio 2015 или 2017, то имейте в виду, что перед запуском приложения в локальной среде необходимо изменить часть `Data Source` строки подключения SQL Server LocalDB в файлах Web.config и App.config с `Data Source=(localdb)\v11.0` на `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="645d6-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="645d6-121"><a name="note"></a> Для работы с этим руководством требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="645d6-122">Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) — вы получаете кредиты, которые можно использовать для опробования платных служб Azure, и даже после израсходования кредитов вы сохраняете учетную запись и возможность использовать бесплатные службы Azure, например веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="645d6-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="645d6-123">С вашей кредитной карты не будет взиматься плата, если вы явно не измените параметры и не попросите снимать плату.</span><span class="sxs-lookup"><span data-stu-id="645d6-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="645d6-124">Вы можете [активировать ежемесячные деньги на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="645d6-125">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="645d6-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="645d6-126">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="645d6-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="645d6-127"><a id="learn"></a>Содержание обучения</span><span class="sxs-lookup"><span data-stu-id="645d6-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="645d6-128">В учебнике показано, как выполнять следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="645d6-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="645d6-129">Подготовьте компьютер к разработке Azure, установив пакет Azure SDK (только для пользователей Visual Studio 2013 и 2015).</span><span class="sxs-lookup"><span data-stu-id="645d6-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="645d6-130">Создание проекта приложения консоли, который автоматически развертывается как веб-задание Azure при развертывании связанного веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="645d6-131">Локальное тестирование внутреннего сервера SDK веб-заданий на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="645d6-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="645d6-132">Публикация приложения с помощью внутреннего сервера веб-заданий в веб-приложение в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="645d6-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="645d6-133">Отправка файлов и сохранение их в службе больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="645d6-134">Использование пакета SDK веб-заданий Azure для работы с очередями и большими двоичными объектами хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="645d6-135"><a id="contosoads"></a>Архитектура приложения</span><span class="sxs-lookup"><span data-stu-id="645d6-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="645d6-136">Пример приложения использует [рабочий шаблон на основе очередей](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) для разгрузки процессора от задач создания эскизов для обработки внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="645d6-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="645d6-137">Приложение хранит рекламу в базе данных SQL, используя Entity Framework Code First для создания таблиц и доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="645d6-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="645d6-138">Для каждого рекламного объявления база данных хранит два URL-адреса: один для полноразмерного изображения, другой для эскиза.</span><span class="sxs-lookup"><span data-stu-id="645d6-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Таблица рекламы](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="645d6-140">Когда пользователь отправляет изображение, веб-приложение сохраняет его в [BLOB-объекте Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), а рекламную информацию — в базе данных с URL-адресом, который указывает на этот BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="645d6-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="645d6-141">В это же время оно записывает сообщение в очередь Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="645d6-142">В ходе серверного процесса, выполняемого как веб-задание Azure, пакет WebJobs SDK опрашивает очередь на предмет новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="645d6-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="645d6-143">Когда появляется новое сообщение, веб-задание создает эскиз для изображения и обновляет поле базы данных с URL-адресом эскиза для этой рекламы.</span><span class="sxs-lookup"><span data-stu-id="645d6-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="645d6-144">Вот диаграмма, которая показывает, как взаимодействуют части приложения:</span><span class="sxs-lookup"><span data-stu-id="645d6-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Архитектура Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="645d6-146">Инструкции учебника применимы к пакету Azure SDK для .NET 2.7.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="645d6-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="645d6-147"><a id="storage"></a>Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="645d6-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="645d6-148">Учетная запись хранилища Azure обеспечивает ресурсы для хранения данных очередей и больших двоичных объектов в облаке.</span><span class="sxs-lookup"><span data-stu-id="645d6-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="645d6-149">Она также используется пакетом SDK веб-заданий для хранения данных журналов для панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="645d6-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="645d6-150">В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="645d6-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="645d6-151">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="645d6-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="645d6-152">Откройте окно **Обозреватель серверов** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="645d6-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="645d6-153">Щелкните правой кнопкой мыши узел **Azure** и выберите **Подключиться к подписке Microsoft Azure...**.</span><span class="sxs-lookup"><span data-stu-id="645d6-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Подключение к Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="645d6-155">Выполните вход с использованием учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="645d6-156">Щелкните правой кнопкой мыши **Хранилище** в узле Azure и выберите пункт **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="645d6-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="645d6-158">В диалоговом окне **Создание учетной записи хранения** введите имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="645d6-159">Имя должно быть уникальным (не допускается существование учетных записей хранения Azure с одинаковыми именами).</span><span class="sxs-lookup"><span data-stu-id="645d6-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="645d6-160">Если введенное имя уже используется, вы получите возможность изменить его.</span><span class="sxs-lookup"><span data-stu-id="645d6-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="645d6-161">URL-адрес для доступа к вашей учетной записи хранения будет выглядеть следующим образом: *{имя}*.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="645d6-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="645d6-162">В раскрывающемся списке **Регион или территориальная группа** укажите ближайший к вам регион.</span><span class="sxs-lookup"><span data-stu-id="645d6-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="645d6-163">Этот параметр указывает, в каком центре обработки данных Azure будет размещаться учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="645d6-164">Теоретически этот выбор не имеет большого значения.</span><span class="sxs-lookup"><span data-stu-id="645d6-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="645d6-165">Но для рабочего веб-приложения веб-сервер и учетная запись хранения должны находиться в одном регионе, чтобы свести к минимуму задержку и стоимость исходящих данных.</span><span class="sxs-lookup"><span data-stu-id="645d6-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="645d6-166">Веб-приложение (которое будет создано позже) должно находиться как можно ближе к браузерам, получившим доступ к нему, чтобы свести к минимуму задержку.</span><span class="sxs-lookup"><span data-stu-id="645d6-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="645d6-167">В раскрывающемся списке **Репликация** установите значение **Локально избыточное**.</span><span class="sxs-lookup"><span data-stu-id="645d6-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="645d6-168">При включении георепликации для учетной записи хранения хранящиеся данные реплицируются в дополнительный центр обработки данных для обеспечения возможности отработки отказа в это расположение в случае крупной аварии в основном расположении.</span><span class="sxs-lookup"><span data-stu-id="645d6-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="645d6-169">Георепликация может потребовать дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="645d6-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="645d6-170">Для учетных записей тестирования и разработки оплачивать георепликацию обычно не требуется.</span><span class="sxs-lookup"><span data-stu-id="645d6-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="645d6-171">Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="645d6-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="645d6-172">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="645d6-172">Click **Create**.</span></span>

    ![Новая учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="645d6-174"><a id="download"></a>Загрузка приложения</span><span class="sxs-lookup"><span data-stu-id="645d6-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="645d6-175">Загрузите и распакуйте [готовое решение](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="645d6-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="645d6-176">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="645d6-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="645d6-177">В меню **Файл** выберите **Открыть > Решение или проект**, перейдите к скачанному решению и откройте файл решения.</span><span class="sxs-lookup"><span data-stu-id="645d6-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="645d6-178">Чтобы построить решение, нажмите CTRL+SHIFT+B.</span><span class="sxs-lookup"><span data-stu-id="645d6-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="645d6-179">По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet, которое не включено в *ZIP*-файл.</span><span class="sxs-lookup"><span data-stu-id="645d6-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="645d6-180">Если пакеты не восстановлены, установите их вручную, перейдя к диалоговому окну **Управление пакетами для NuGet решения** и нажав кнопку **Восстановить** вверху справа.</span><span class="sxs-lookup"><span data-stu-id="645d6-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="645d6-181">В **обозревателе решений** выберите **ContosoAdsWeb** в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="645d6-182"><a id="configurestorage"></a>Настройка приложения для использования учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="645d6-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="645d6-183">Откройте файл приложения *Web.config* в проекте ContosoAdsWeb.</span><span class="sxs-lookup"><span data-stu-id="645d6-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="645d6-184">Файл содержит строку подключения SQL и строку подключения хранилища Azure для работы с большими двоичными объектами и очередями.</span><span class="sxs-lookup"><span data-stu-id="645d6-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="645d6-185">Строка подключения SQL указывает на базу данных [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) .</span><span class="sxs-lookup"><span data-stu-id="645d6-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="645d6-186">В примере строки подключения к хранилищу использованы заполнители для имени учетной записи хранения и ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="645d6-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="645d6-187">Замените это строкой подключения, которая содержит имя и ключ для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="645d6-188">Строка подключения хранилища называется AzureWebJobsStorage, поскольку пакет SDK веб-заданий использует это имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="645d6-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="645d6-189">Здесь используется то же имя, поэтому вам нужно задать только одно значение строки подключения в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="645d6-190">В **обозревателе сервера** щелкните правой кнопкой мыши учетную запись хранения в узле **Хранилище** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="645d6-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Щелкните свойства учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="645d6-192">В окне **Свойства** щелкните **Ключи учетной записи хранилища** и нажмите кнопку с многоточием.</span><span class="sxs-lookup"><span data-stu-id="645d6-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Ключи учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="645d6-194">Скопируйте **строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="645d6-194">Copy the **Connection String**.</span></span>

    ![Диалоговое окно "Ключи учетной записи хранения"](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="645d6-196">Замените строку подключения к хранилищу в файле *Web.config* на скопированную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="645d6-197">Перед вставкой убедитесь, что выбраны все элементы внутри кавычек, но не сами кавычки.</span><span class="sxs-lookup"><span data-stu-id="645d6-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="645d6-198">Откройте файл *App.config* в проекте ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="645d6-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="645d6-199">Этот файл содержит две строки подключения хранилища: одну для данных приложения, а другую для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="645d6-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="645d6-200">Можно использовать отдельные учетные записи хранения для данных приложений и ведения журнала; также можно использовать [несколько учетных записей хранения для данных](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="645d6-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="645d6-201">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="645d6-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="645d6-202">Строки подключения имеют заполнители для ключей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-202">The connection strings have placeholders for the storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="645d6-203">По умолчанию пакет SDK веб-заданий ищет строки подключения с именами AzureWebJobsStorage и AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="645d6-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="645d6-204">В качестве альтернативы можно [сохранить строку подключения любым способом и передать ее явно в `JobHost`объект](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="645d6-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="645d6-205">Замените обе строки подключения к хранилищу скопированной ранее строкой подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="645d6-206">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="645d6-206">Save your changes.</span></span>

## <span data-ttu-id="645d6-207"><a id="run"></a>Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="645d6-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="645d6-208">Чтобы запустить внешний сервер приложения, нажмите клавиши CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="645d6-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="645d6-209">Откроется домашняя страница браузера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="645d6-209">The default browser opens to the home page.</span></span> <span data-ttu-id="645d6-210">(Запускается веб-проект, поскольку он стал запускаемым проектом.)</span><span class="sxs-lookup"><span data-stu-id="645d6-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Домашняя страница Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="645d6-212">Чтобы запустить внутренний сервер веб-задания приложения, щелкните правой кнопкой мыши проект ContosoAdsWebJob в **обозревателе решений** и нажмите **Отладка** > **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="645d6-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="645d6-213">Окно консоли приложения открывает и отображает сообщение для ведения журнала, указывающее начало выполнения объекта JobHost из веб-заданий SDK.</span><span class="sxs-lookup"><span data-stu-id="645d6-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Окно приложения консоли, отображающее, что внутренний сервер запущен](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="645d6-215">В браузере нажмите кнопку **Create an Ad** (Создать рекламу).</span><span class="sxs-lookup"><span data-stu-id="645d6-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="645d6-216">Введите тестовые данные, выберите изображение для отправки и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="645d6-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Страница создания](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="645d6-218">Приложение переходит к странице индексации, но не показывает эскиз для новой рекламы, поскольку индексирование еще не проводилось.</span><span class="sxs-lookup"><span data-stu-id="645d6-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="645d6-219">В то же время после короткого ожидания в окне приложения консоли отобразится сообщение журнала, что сообщение очереди было получено и обработано.</span><span class="sxs-lookup"><span data-stu-id="645d6-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Окно приложения консоли, отображающее, что сообщение очереди обработано](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="645d6-221">После того, как вы увидите сообщения журнала в окне приложения консоли, обновите страницу индексов, чтобы увидеть эскиз.</span><span class="sxs-lookup"><span data-stu-id="645d6-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Страница индексации](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="645d6-223">Щелкните **Details** , чтобы увидеть рекламу в полный размер.</span><span class="sxs-lookup"><span data-stu-id="645d6-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Страница сведений](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="645d6-225">Вы запустили приложение на локальном компьютере, и оно использует базу данных SQL Server, расположенную на компьютере, но она работает с очередями и большими двоичными объектами в облаке.</span><span class="sxs-lookup"><span data-stu-id="645d6-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="645d6-226">В следующем разделе вы запустите приложение в облаке с помощью облачной базы данных, а также облачных больших двоичных объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="645d6-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="645d6-227"><a id="runincloud"></a>Запуск приложения в облаке</span><span class="sxs-lookup"><span data-stu-id="645d6-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="645d6-228">Чтобы запустить приложение в облаке, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="645d6-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="645d6-229">Развертывание веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="645d6-229">Deploy to Web Apps.</span></span> <span data-ttu-id="645d6-230">Visual Studio автоматически создаст новое веб-приложение в службе приложений и экземпляр базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="645d6-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="645d6-231">Настройка веб-приложения для использования базы данных SQL Azure и учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="645d6-232">После создания рекламы во время работы в облаке вы просмотрите панель мониторинга SDK веб-заданий, чтобы увидеть предлагаемые обширные функции мониторинга.</span><span class="sxs-lookup"><span data-stu-id="645d6-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="645d6-233">Развертывание веб-приложений</span><span class="sxs-lookup"><span data-stu-id="645d6-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="645d6-234">Закройте браузер и окно приложения консоли.</span><span class="sxs-lookup"><span data-stu-id="645d6-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="645d6-235">Следуйте указаниям, описанным в разделе [Публикация в Azure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="645d6-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="645d6-236">После выполнения действий по развертыванию продолжите выполнять оставшиеся задачи из этой статьи.</span><span class="sxs-lookup"><span data-stu-id="645d6-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="645d6-237">Настройка веб-приложения для использования базы данных SQL Azure и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="645d6-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="645d6-238">В целях безопасности рекомендуется [не указывать конфиденциальную информацию, такую как строки подключения, в файлах, которые хранятся в репозиториях исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="645d6-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="645d6-239">Это можно сделать с помощью Azure: вы можете задать строку подключения и другие значения параметров в среде Azure, и API конфигурации ASP.NET автоматически выберут эти значения при запуске приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="645d6-240">Вы можете задать эти значения в Azure с помощью **обозревателя сервера**, портала Azure, Windows PowerShell или кроссплатформенного интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="645d6-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="645d6-241">Дополнительные сведения см. в статье [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложений и строки подключения).</span><span class="sxs-lookup"><span data-stu-id="645d6-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="645d6-242">В этом разделе вы сможете задать значения строк подключения в Azure с помощью **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="645d6-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="645d6-243">В **обозревателе сервера** щелкните правой кнопкой мыши свое веб-приложение в узле **Azure > Служба приложений > {ваша группа ресурсов}**, а затем щелкните **Просмотреть параметры**.</span><span class="sxs-lookup"><span data-stu-id="645d6-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="645d6-244">Окно **Веб-приложение Azure** откроется на вкладке **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="645d6-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="645d6-245">Измените имя строки подключения DefaultConnection на имя, выбранное при настройке базы данных SQL во время работы с разделом [Публикация в Azure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="645d6-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="645d6-246">Служба Azure автоматически создала эту строку подключения, когда вы создали веб-приложение со связанной базой данных, поэтому она автоматически содержит правильное значение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="645d6-247">Нужно только изменить имя на искомый код.</span><span class="sxs-lookup"><span data-stu-id="645d6-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="645d6-248">Добавьте две новые строки подключения с именами AzureWebJobsStorage и AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="645d6-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="645d6-249">Задайте **настраиваемый** тип базы данных, а затем задайте для строки подключения то же значение, которое использовалось ранее для файлов *Web.config* и *App.config*.</span><span class="sxs-lookup"><span data-stu-id="645d6-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="645d6-250">(Убедитесь, что включили всю строку подключения без кавычек, а не только ключ доступа.)</span><span class="sxs-lookup"><span data-stu-id="645d6-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="645d6-251">Эти строки подключения используются пакетом SDK веб-заданий: одна для данных приложения, а другая для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="645d6-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="645d6-252">Как было показано ранее, строка подключения для данных приложения также используется кодом внешнего сервера.</span><span class="sxs-lookup"><span data-stu-id="645d6-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="645d6-253">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-253">Click **Save**.</span></span>

    ![Строки подключения на портале Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="645d6-255">В **обозревателе сервера** щелкните правой кнопкой мыши веб-приложение, а затем нажмите кнопку **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="645d6-256">Остановив веб-приложение, снова щелкните его правой кнопкой мыши и выберите **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="645d6-257">Веб-задание запустится автоматически при публикации, но остановится при внесении изменений в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="645d6-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="645d6-258">Его можно запустить повторно, перезапустив веб-приложение или веб-задание на [портале Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="645d6-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="645d6-259">Обычно рекомендуется перезапускать веб-приложение после изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="645d6-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="645d6-260">Обновите окно браузера, которое содержит URL-адрес веб-приложения в адресной строке.</span><span class="sxs-lookup"><span data-stu-id="645d6-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="645d6-261">Появится домашняя страница.</span><span class="sxs-lookup"><span data-stu-id="645d6-261">The home page appears.</span></span>
8. <span data-ttu-id="645d6-262">Создайте рекламу, как вы делали это при [локальном запуске приложения](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="645d6-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="645d6-263">Сначала появится страница индексов без эскизов.</span><span class="sxs-lookup"><span data-stu-id="645d6-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="645d6-264">Через несколько секунд обновите страницу, чтобы появился эскиз.</span><span class="sxs-lookup"><span data-stu-id="645d6-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="645d6-265">Если эскиз не отображается, подождите какое-то время (около минуты), пока веб-задание запустится повторно.</span><span class="sxs-lookup"><span data-stu-id="645d6-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="645d6-266">Если через некоторое время эскиз по-прежнему не отображается при обновлении страницы, возможно, веб-задание не запускается автоматически.</span><span class="sxs-lookup"><span data-stu-id="645d6-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="645d6-267">В этом случае перейдите в колонку **Службы приложений** на [портале Azure](https://portal.azure.com/), найдите веб-приложение, а затем щелкните **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="645d6-268">Просмотр панели мониторинга SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="645d6-269">На [портале Azure](https://portal.azure.com/) выберите колонку **Службы приложений**, найдите веб-приложение и выберите **Веб-задания**.</span><span class="sxs-lookup"><span data-stu-id="645d6-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="645d6-270">Откройте вкладку **Журналы**.</span><span class="sxs-lookup"><span data-stu-id="645d6-270">Select the **Logs** tab.</span></span>

    ![Вкладка "Журналы"](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="645d6-272">На панели мониторинга SDK веб-заданий откроется новая вкладка браузера.</span><span class="sxs-lookup"><span data-stu-id="645d6-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="645d6-273">На панели мониторинга отобразится, что веб-задание запущено, и появится список функций в коде, активированных пакетом SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="645d6-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="645d6-274">Щелкните одну из функций, чтобы получить сведения о ее выполнении.</span><span class="sxs-lookup"><span data-stu-id="645d6-274">Click one of the functions to see details about its execution.</span></span>

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="645d6-277">Кнопка **Повторить функцию** на этой странице позволяет платформе SDK веб-заданий повторно вызывать функцию и дает возможность изменить данные, изначально переданные в функцию.</span><span class="sxs-lookup"><span data-stu-id="645d6-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="645d6-278">После окончания тестирования вы можете удалить веб-приложения, учетную запись хранения и экземпляр базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="645d6-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="645d6-279">Веб-приложение бесплатно, но за экземпляр базы данных и учетную запись хранения SQL взимается плата (хотя и минимальная из-за небольшого размера).</span><span class="sxs-lookup"><span data-stu-id="645d6-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="645d6-280">Также, если оставить веб-приложение работающим, любой, кто найдет этот URL-адрес, сможет создать и просмотреть рекламу.</span><span class="sxs-lookup"><span data-stu-id="645d6-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="645d6-281">Удаление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="645d6-281">Delete your web app</span></span>
<span data-ttu-id="645d6-282">На портале перейдите в колонку **Службы приложений**, найдите и выберите свое веб-приложение, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="645d6-283">Если необходимо временно предотвратить доступ посторонних к веб-приложению, щелкните **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="645d6-284">В этом случае плата за базы данных SQL и учетную запись хранения продолжит взиматься.</span><span class="sxs-lookup"><span data-stu-id="645d6-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="645d6-285">Удаление учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="645d6-285">Delete your storage account</span></span>
<span data-ttu-id="645d6-286">Дополнительные сведения об удалении учетной записи хранения см. в [этом разделе](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="645d6-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="645d6-287">Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="645d6-287">Delete your database</span></span>
<span data-ttu-id="645d6-288">Дополнительные сведения об удалении базы данных SQL см. в статье [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) (REST API базы данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="645d6-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="645d6-289"><a id="create"></a>Создание приложения с самого начала</span><span class="sxs-lookup"><span data-stu-id="645d6-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="645d6-290">В этом разделе предстоит выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="645d6-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="645d6-291">Создание решения Visual Studio с веб-проектом.</span><span class="sxs-lookup"><span data-stu-id="645d6-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="645d6-292">Добавление проекта библиотеки класса для уровня доступа данных, который совместно используется внешним и внутренним сервером.</span><span class="sxs-lookup"><span data-stu-id="645d6-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="645d6-293">Добавление проекта приложения консоли для внутреннего сервера с включенным развертыванием веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="645d6-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="645d6-294">Добавление пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="645d6-294">Add NuGet packages.</span></span>
* <span data-ttu-id="645d6-295">Указание ссылок на проекты.</span><span class="sxs-lookup"><span data-stu-id="645d6-295">Set project references.</span></span>
* <span data-ttu-id="645d6-296">Копирование кода приложения и файлов конфигурации из скачанного приложения, с которым вы работали в предыдущем разделе учебника.</span><span class="sxs-lookup"><span data-stu-id="645d6-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="645d6-297">Просмотр фрагментов кода, которые работают с большими двоичными объектами и очередями Azure и пакетом SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="645d6-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="645d6-298">Создание решения Visual Studio с веб-проектом и проектом библиотеки класса</span><span class="sxs-lookup"><span data-stu-id="645d6-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="645d6-299">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="645d6-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="645d6-300">В диалоговом окне **Создать проект** выберите **Visual C#** > **Веб** > **Веб-приложение ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="645d6-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="645d6-301">Назовите проект "ContosoAdsWeb", назовите решение "ContosoAdsWebJobsSDK" (измените имя решения, если планируете поместить его в ту же папку, что и скачанное решение), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Новый проект](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="645d6-303">В диалоговом окне **Создать веб-приложение ASP.NET** выберите шаблон MVC, а затем выберите **Изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="645d6-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Изменить проверку подлинности](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="645d6-305">В диалоговом окне **Изменить способ проверки подлинности** щелкните **Без проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Без аутентификации](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="645d6-307">В диалоговом окне **Создать веб-приложение ASP.NET** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="645d6-308">Visual Studio создаст решение и веб-проект.</span><span class="sxs-lookup"><span data-stu-id="645d6-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="645d6-309">В **обозревателе решений** щелкните правой кнопкой мыши решение (а не проект) и выберите **Добавить** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="645d6-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="645d6-310">В диалоговом окне **Добавление нового проекта** выберите шаблон **Visual C#** > **Классический рабочий стол Windows** > **Библиотека классов (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="645d6-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="645d6-311">Присвойте проекту имя *ContosoAdsCommon*и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="645d6-312">Этот проект будет содержать контекст и модель данных Entity Framework, которые будут использовать внешний и внутренний сервер.</span><span class="sxs-lookup"><span data-stu-id="645d6-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="645d6-313">Как вариант, можно определить связанные с EF классы в веб-проекте и сослаться на этот проект из проекта веб-задания.</span><span class="sxs-lookup"><span data-stu-id="645d6-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="645d6-314">Но тогда проект веб-задания будет содержать ссылку на веб-сборки, которые ему не нужны.</span><span class="sxs-lookup"><span data-stu-id="645d6-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="645d6-315">Добавление проекта приложения консоли, в котором включено развертывание веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="645d6-316">Щелкните правой кнопкой мыши проект (а не решение или проект библиотеки классов) и нажмите кнопку **Добавить** > **Новый проект веб-задания Azure**.</span><span class="sxs-lookup"><span data-stu-id="645d6-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Пункт меню "Новый проект веб-задания Azure"](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="645d6-318">В диалоговом окне **Добавить веб-задание Azure** введите ContosoAdsWebJob в поля **Имя проекта** и **Имя веб-задания**.</span><span class="sxs-lookup"><span data-stu-id="645d6-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="645d6-319">Оставьте в поле **Режим выполнения веб-задания** значение **Выполнять непрерывно**.</span><span class="sxs-lookup"><span data-stu-id="645d6-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="645d6-320">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-320">Click **OK**.</span></span>

   <span data-ttu-id="645d6-321">Visual Studio создает приложение консоли, которое настроено для развертывания в качестве веб-задания при каждом развертывании веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="645d6-322">Для этого после создания проекта выполняются следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="645d6-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="645d6-323">Добавляется файл *webjob-publish-settings.json* в папку "Свойства" проекта веб-задания.</span><span class="sxs-lookup"><span data-stu-id="645d6-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="645d6-324">Добавляется файл *webjobs-list.json* в папку "Свойства" веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="645d6-325">Устанавливается пакет NuGet Microsoft.Web.WebJobs.Publish в проект веб-задания.</span><span class="sxs-lookup"><span data-stu-id="645d6-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="645d6-326">Дополнительные сведения об этих изменениях см. в статье [Развертывание веб-заданий с помощью Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="645d6-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="645d6-327">Добавление пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="645d6-327">Add NuGet packages</span></span>
<span data-ttu-id="645d6-328">Шаблон нового проекта для проекта веб-задания автоматически устанавливает пакет веб-заданий SDK NuGet [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) и зависимости.</span><span class="sxs-lookup"><span data-stu-id="645d6-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="645d6-329">Одна из зависимостей пакета SDK веб-заданий, которая автоматически устанавливается в проекте веб-задания, это клиентская библиотека хранилища Azure (SCL).</span><span class="sxs-lookup"><span data-stu-id="645d6-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="645d6-330">Однако, чтобы она работала с BLOB-объектами и очередями, вам необходимо добавить ее в веб-проект.</span><span class="sxs-lookup"><span data-stu-id="645d6-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="645d6-331">Откройте диалоговое окно **Управление пакетами NuGet** для решения.</span><span class="sxs-lookup"><span data-stu-id="645d6-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="645d6-332">В левой области выберите **Установленные пакеты**.</span><span class="sxs-lookup"><span data-stu-id="645d6-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="645d6-333">Найдите пакет *Хранилище Azure* и щелкните кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="645d6-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="645d6-334">В поле **Выбор проектов** установите флажок **ContosoAdsWeb** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="645d6-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="645d6-335">Все три проекта используют Entity Framework для работы с данными в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="645d6-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="645d6-336">В левой области щелкните **В сети**.</span><span class="sxs-lookup"><span data-stu-id="645d6-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="645d6-337">Найдите пакет NuGet *EntityFramework* и установите его во все проекты.</span><span class="sxs-lookup"><span data-stu-id="645d6-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="645d6-338">Установите ссылки проекта</span><span class="sxs-lookup"><span data-stu-id="645d6-338">Set project references</span></span>
<span data-ttu-id="645d6-339">Веб-проекты и проекты веб-заданий работают с базой данных SQL, поэтому и для тех, и для других необходима ссылка на проект ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="645d6-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="645d6-340">Задайте в проекте ContosoAdsWeb ссылку на проект ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="645d6-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="645d6-341">(Щелкните правой кнопкой мыши проект ContosoAdsWeb и нажмите кнопку **Добавить** > **Ссылка**.</span><span class="sxs-lookup"><span data-stu-id="645d6-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="645d6-342">В диалоговом окне **Диспетчер ссылок** выберите **Проекты** > **Решение** > **ContosoAdsCommon**, а затем нажмите кнопку **OK**.)</span><span class="sxs-lookup"><span data-stu-id="645d6-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="645d6-343">Для проекта веб-задания нужны ссылки для работы с изображениями и для доступа к строкам подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="645d6-344">Задайте в проекте ContosoAdsWebJob ссылку на `System.Drawing` и `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="645d6-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="645d6-345">Добавление кода и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="645d6-345">Add code and configuration files</span></span>
<span data-ttu-id="645d6-346">В этом руководстве не описывается, как [создать контроллеры и представления MVC с помощью формирования шаблонов](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), [записывать код Entity Framework, который работает с базами данных SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), или [основы асинхронного программирования в ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="645d6-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="645d6-347">Поэтому все, что нужно сделать, — скопировать код и файлы конфигурации из скачанного решения в новое.</span><span class="sxs-lookup"><span data-stu-id="645d6-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="645d6-348">После этого в следующих разделах будут показаны и объяснены основные фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="645d6-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="645d6-349">Чтобы добавить файлы в проект или папку, щелкните правой кнопкой мыши проект или папку и нажмите **Добавить** > **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="645d6-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="645d6-350">Выберите необходимые файлы и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="645d6-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="645d6-351">При запросе о том, заменять ли существующие файлы, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="645d6-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="645d6-352">В проекте ContosoAdsCommon удалите файл *Class1.cs* и добавьте на его место следующие файлы из скачанного проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="645d6-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-353">*Ad.cs*</span></span>
   * <span data-ttu-id="645d6-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="645d6-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="645d6-356">В проекте ContosoAdsCommon добавьте следующие файлы из загруженного проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="645d6-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="645d6-357">*Web.config*</span></span>
   * <span data-ttu-id="645d6-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="645d6-359">в папку *Controllers*: *AdController.cs*;</span><span class="sxs-lookup"><span data-stu-id="645d6-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="645d6-360">в папку *Views\Shared*: файл *_Layout.cshtml*;</span><span class="sxs-lookup"><span data-stu-id="645d6-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="645d6-361">в папку *Views\Home*: файл *Index.cshtml*;</span><span class="sxs-lookup"><span data-stu-id="645d6-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="645d6-362">в папку *Views\Ad* (сначала создайте эту папку): пять файлов *CSHTML*.</span><span class="sxs-lookup"><span data-stu-id="645d6-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="645d6-363">В проекте ContosoAdsWebJob добавьте следующие файлы из скачанного проекта.</span><span class="sxs-lookup"><span data-stu-id="645d6-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="645d6-364">*App.config* (измените фильтр типов файлов на **Все файлы**)</span><span class="sxs-lookup"><span data-stu-id="645d6-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="645d6-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-365">*Program.cs*</span></span>
   * <span data-ttu-id="645d6-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="645d6-366">*Functions.cs*</span></span>

<span data-ttu-id="645d6-367">Теперь вы можете создать, запустить и развернуть приложение, как показано ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="645d6-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="645d6-368">Однако перед этим остановите веб-задание, которое все еще выполняется в первом веб-приложении, на котором произведено развертывание.</span><span class="sxs-lookup"><span data-stu-id="645d6-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="645d6-369">В противном случае такое веб-задание обработает сообщения очереди, созданные локально или запущенные приложением в новом веб-приложении, так как все они используют одну учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="645d6-370"><a id="code"></a>Просмотр кода приложения</span><span class="sxs-lookup"><span data-stu-id="645d6-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="645d6-371">В следующих разделах объясняется код, связанный с работой с пакетом SDK веб-заданий и большими двоичными объектами и очередями Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="645d6-372">Код, связанный с пакетом SDK для веб-заданий, см. в разделах о [Program.cs и Functions.cs](#programcs).</span><span class="sxs-lookup"><span data-stu-id="645d6-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="645d6-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="645d6-374">Файл Ad.cs определяет перечисляемый тип для класса Ad и класс сущностей POCO для информации в рекламе.</span><span class="sxs-lookup"><span data-stu-id="645d6-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="645d6-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="645d6-376">Класс ContosoAdsContext указывает, что класс Ad используется коллекцией DbSet, которую Entity Framework хранит в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="645d6-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

<span data-ttu-id="645d6-377">Класс имеет два конструктора.</span><span class="sxs-lookup"><span data-stu-id="645d6-377">The class has two constructors.</span></span> <span data-ttu-id="645d6-378">Первый из них используется веб-проектом и указывает имя строки подключения, которая хранится в файле Web.config или в среде выполнения Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="645d6-379">Второй конструктор дает возможность передачи действующей строки подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="645d6-380">Это необходимо проекту веб-задания, поскольку он не имеет файла Web.config.</span><span class="sxs-lookup"><span data-stu-id="645d6-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="645d6-381">Ранее было показано, где хранится строка подключения, а потом будет показано, как код извлекает строку подключения, когда он создает экземпляр класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="645d6-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="645d6-382">ContosoAdsCommon — BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="645d6-383">Класс `BlobInformation` используется для хранения информации о BLOB-объекте изображения в сообщении очереди.</span><span class="sxs-lookup"><span data-stu-id="645d6-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="645d6-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="645d6-385">Код, который вызывается из метода `Application_Start`, создает контейнер больших двоичных объектов *images* и очередь *images*, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="645d6-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="645d6-386">Это гарантирует, что при каждом использовании новой учетной записи хранения необходимый контейнер больших двоичных объектов и очередь будут создаваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="645d6-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="645d6-387">Код получает доступ к учетной записи хранения, используя строку подключения из файла *Web.config* или среду выполнения Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="645d6-388">Затем он получает ссылку на контейнер больших двоичных объектов *изображений*, создает контейнер, если он еще не существует, и устанавливает разрешения доступа к новому контейнеру.</span><span class="sxs-lookup"><span data-stu-id="645d6-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="645d6-389">По умолчанию новые контейнеры разрешают доступ к большим двоичным объектам только клиентам с учетными данными записи хранения.</span><span class="sxs-lookup"><span data-stu-id="645d6-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="645d6-390">Веб-приложению требуются общедоступные большие двоичные объекты, чтобы оно могло выводить изображения с использованием URL-адресов, которые указывают на объекты изображений.</span><span class="sxs-lookup"><span data-stu-id="645d6-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="645d6-391">Похожий код получает ссылку на очередь *thumbnailrequest* и создает новую очередь.</span><span class="sxs-lookup"><span data-stu-id="645d6-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="645d6-392">В этом случае изменений разрешений не требуется.</span><span class="sxs-lookup"><span data-stu-id="645d6-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="645d6-393">ContosoAdsWeb — _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="645d6-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="645d6-394">Файл *_Layout.cshtml* задает имя приложения в заголовке и нижнем колонтитуле и создает запись меню "Ads".</span><span class="sxs-lookup"><span data-stu-id="645d6-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="645d6-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="645d6-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="645d6-396">Файл *Views\Home\Index.cshtml* выводит ссылки категорий на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="645d6-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="645d6-397">Ссылки передают целочисленное значение перечисляемого типа `Category` в переменную querystring на странице индекса Ads.</span><span class="sxs-lookup"><span data-stu-id="645d6-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="645d6-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="645d6-399">В файле *AdController.cs* конструктор вызывает метод `InitializeStorage` для создания объектов клиентской библиотеки службы хранилища Azure, которые предоставляют API-интерфейс для работы с большими двоичными объектами и очередями.</span><span class="sxs-lookup"><span data-stu-id="645d6-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="645d6-400">Затем код получает ссылку на контейнер больших двоичных объектов *изображений*, как показано ранее в *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="645d6-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="645d6-401">При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="645d6-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="645d6-402">Политика повторения с экспоненциальной задержкой по умолчанию может застопорить веб-приложение более чем на минуту при повторяющихся повторах во время кратковременного сбоя.</span><span class="sxs-lookup"><span data-stu-id="645d6-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="645d6-403">Политика повторения здесь указывает ожидание в три секунды после каждой попытки, всего до трех повторений.</span><span class="sxs-lookup"><span data-stu-id="645d6-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="645d6-404">Аналогичный код получает ссылку на очередь *images* .</span><span class="sxs-lookup"><span data-stu-id="645d6-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="645d6-405">Большая часть кода контроллера обычна для работы с моделью данных Entity Framework с использованием класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="645d6-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="645d6-406">Исключением является метод `Create` HttpPost, который отправляет файл и сохраняет его в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="645d6-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="645d6-407">Связыватель модели предоставляет объект [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) для метода.</span><span class="sxs-lookup"><span data-stu-id="645d6-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="645d6-408">При выбора файла для отправки код отправляет его, сохраняет его в большом двоичном объекте и обновляет запись базы данных URL-адресом, который указывает на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="645d6-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="645d6-409">Код отправки содержится в методе `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="645d6-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="645d6-410">Он создает имя GUID для большого двоичного объекта, отправляет и сохраняет файл, а также возвращает ссылку на сохраненный большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="645d6-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

<span data-ttu-id="645d6-411">После того как метод `Create` HttpPost отправит большой двоичный объект и обновит базу данных, он создаст сообщение в очереди для информирования фонового процесса о том, что изображение готово для конвертации в эскиз.</span><span class="sxs-lookup"><span data-stu-id="645d6-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="645d6-412">Код для метода `Edit` HttpPost аналогичен, за одним исключением — если пользователь выбирает новый файл изображения, все большие двоичные объекты, которые уже существуют для этой рекламы, должны быть удалены.</span><span class="sxs-lookup"><span data-stu-id="645d6-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="645d6-413">Вот код, который удаляет большие двоичные объекты при удалении элемента рекламы:</span><span class="sxs-lookup"><span data-stu-id="645d6-413">Here is the code that deletes blobs when you delete an ad:</span></span>

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="645d6-414">ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="645d6-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="645d6-415">Файл *Index.cshtml* выводит эскиз с другими данными рекламы:</span><span class="sxs-lookup"><span data-stu-id="645d6-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="645d6-416">Файл *Details.cshtml* выводит изображение в полном размере:</span><span class="sxs-lookup"><span data-stu-id="645d6-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="645d6-417">ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="645d6-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="645d6-418">Файлы *Create.cshtml* и *Edit.cshtml* указывают кодирование формы, которое дает возможность контроллеру получить объект `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="645d6-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="645d6-419">Элемент `<input>` сообщает браузеру, что нужно открыть диалоговое окно выбора файла.</span><span class="sxs-lookup"><span data-stu-id="645d6-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="645d6-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="645d6-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="645d6-421">При запуске веб-задания метод `Main` вызывает метод пакета `JobHost.RunAndBlock` SDK веб-заданий, чтобы начать выполнение инициированных функций в текущем потоке.</span><span class="sxs-lookup"><span data-stu-id="645d6-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="645d6-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="645d6-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="645d6-423">Пакет SDK веб-заданий вызывает этот метод при получении сообщения очереди.</span><span class="sxs-lookup"><span data-stu-id="645d6-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="645d6-424">Метод создает эскиз и помещает URL-адрес эскиза в базу данных.</span><span class="sxs-lookup"><span data-stu-id="645d6-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="645d6-425">Атрибут `QueueTrigger` направляет пакет SDK веб-заданий для вызова этого метода при получении нового сообщения в очереди запросов эскизов.</span><span class="sxs-lookup"><span data-stu-id="645d6-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="645d6-426">Для объекта `BlobInformation` в сообщении очереди автоматически выполняется десериализация в параметр `blobInfo`.</span><span class="sxs-lookup"><span data-stu-id="645d6-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="645d6-427">По завершении метода сообщение очереди удаляется.</span><span class="sxs-lookup"><span data-stu-id="645d6-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="645d6-428">Если происходит сбой метода до его завершения, сообщение очереди не удаляется. После истечения 10-минутного срока действия аренды сообщение передается для повторной обработки.</span><span class="sxs-lookup"><span data-stu-id="645d6-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="645d6-429">Если сообщение вызывает исключение, эта последовательность не будет повторяться бесконечно.</span><span class="sxs-lookup"><span data-stu-id="645d6-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="645d6-430">После 5 неудачных попыток обработать сообщение, оно будет перемещено в очередь с именем {queuename}-poison.</span><span class="sxs-lookup"><span data-stu-id="645d6-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="645d6-431">Можно настроить максимальное количество попыток.</span><span class="sxs-lookup"><span data-stu-id="645d6-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="645d6-432">Два атрибута `Blob` указывают на объекты, связанные с большими двоичными объектами: первый — на существующий большой двоичный объект изображения, второй — на большой двоичный объект эскиза, создаваемый методом.</span><span class="sxs-lookup"><span data-stu-id="645d6-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="645d6-433">Имена больших двоичных объектов задаются в соответствии со свойствами объекта `BlobInformation`, полученного в сообщении очереди (`BlobName` и `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="645d6-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="645d6-434">Чтобы получить все функции клиентской библиотеки хранилища, можно использовать класс `CloudBlockBlob` для работы с большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="645d6-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="645d6-435">Если вы хотите повторно использовать код, написанный для работы с объектами `Stream`, можно использовать класс `Stream`.</span><span class="sxs-lookup"><span data-stu-id="645d6-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="645d6-436">Дополнительные сведения о написании функций, использующих атрибуты пакета SDK для веб-заданий, см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="645d6-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="645d6-437">Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure</span><span class="sxs-lookup"><span data-stu-id="645d6-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="645d6-438">Использование хранилища больших двоичных объектов Azure с пакетом SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="645d6-439">Использование табличного хранилища Azure с пакетом SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="645d6-440">Использование служебной шины Azure с пакетом SDK для веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="645d6-441">Если веб-приложение выполняется на нескольких виртуальных машинах, одновременно будет выполнятся несколько веб-заданий, а это в некоторых случаях может привести к многократной обработке одних и тех же данных.</span><span class="sxs-lookup"><span data-stu-id="645d6-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="645d6-442">Такой проблемы не будет при использовании встроенной очереди, BLOB-объектов и триггеров служебной шины.</span><span class="sxs-lookup"><span data-stu-id="645d6-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="645d6-443">Пакет SDK гарантирует, что функции для каждого сообщения или BLOB-объекта будут обрабатываться только один раз.</span><span class="sxs-lookup"><span data-stu-id="645d6-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="645d6-444">Сведения о нормальном завершении работы см. в [этом разделе](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="645d6-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="645d6-445">Для простоты код в методе `ConvertImageToThumbnailJPG` (не показан) использует классы в пространстве имен `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="645d6-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="645d6-446">Однако классы в этом пространстве имен были спроектированы для использования с формами Windows.</span><span class="sxs-lookup"><span data-stu-id="645d6-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="645d6-447">Они не поддерживаются в службе Windows или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="645d6-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="645d6-448">Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования изображения с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).</span><span class="sxs-lookup"><span data-stu-id="645d6-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="645d6-449">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="645d6-449">Next steps</span></span>
<span data-ttu-id="645d6-450">В этом руководстве было показано простое многоуровневое приложение, которое использует пакет SDK веб-заданий для обработки внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="645d6-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="645d6-451">В этом разделе приведены рекомендации по дальнейшему изучению многоуровневых приложений ASP.NET и веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="645d6-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="645d6-452">Отсутствующие функции</span><span class="sxs-lookup"><span data-stu-id="645d6-452">Missing features</span></span>
<span data-ttu-id="645d6-453">Приложение намеренно сделано простым, поскольку это учебник для начинающих.</span><span class="sxs-lookup"><span data-stu-id="645d6-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="645d6-454">В реальном приложении вам понадобилось бы реализовать [внедрение зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection), а также [репозиторий и блок рабочих шаблонов](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), использовать [интерфейс для ведения журнала](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), использовать [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) для управления изменениями модели данных и [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) для управления кратковременными ошибками сети.</span><span class="sxs-lookup"><span data-stu-id="645d6-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="645d6-455">Масштабирование веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-455">Scaling WebJobs</span></span>
<span data-ttu-id="645d6-456">Веб-задания запускаются в контексте веб-приложения и не масштабируются отдельно.</span><span class="sxs-lookup"><span data-stu-id="645d6-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="645d6-457">Например, если у вас есть один экземпляр веб-приложения Standard, вы можете запустить только один экземпляр внутренней обработки и он будет использовать некоторые ресурсы сервера (ЦП, память и т. д.), которые в противном случае были бы доступны для обработки веб-содержимого.</span><span class="sxs-lookup"><span data-stu-id="645d6-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="645d6-458">Если трафик зависит от времени дня или дня недели и если необходимую обработку внутреннего сервера можно запустить позже, запланируйте запуск веб-заданий на период, когда трафик мало используется.</span><span class="sxs-lookup"><span data-stu-id="645d6-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="645d6-459">Если нагрузка по-прежнему слишком высока для данного решения, серверную часть можно запускать как веб-задание в отдельном веб-приложении, выделенном для этой цели.</span><span class="sxs-lookup"><span data-stu-id="645d6-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="645d6-460">Затем можно масштабировать веб-приложение внутреннего сервера отдельно от веб-приложения внешнего сервера.</span><span class="sxs-lookup"><span data-stu-id="645d6-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="645d6-461">Дополнительные сведения см. в разделе [Масштабирование веб-заданий](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="645d6-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="645d6-462">Предотвращение завершения работы веб-приложений из-за превышения времени ожидания</span><span class="sxs-lookup"><span data-stu-id="645d6-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="645d6-463">Чтобы веб-задания всегда выполнялись и работали во всех экземплярах веб-приложения, необходимо включить функцию [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx).</span><span class="sxs-lookup"><span data-stu-id="645d6-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="645d6-464">Использование пакета SDK веб-заданий вне сферы применения веб-заданий</span><span class="sxs-lookup"><span data-stu-id="645d6-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="645d6-465">Программа, которая использует пакет SDK веб-заданий, не должна запускаться в Azure в веб-задании.</span><span class="sxs-lookup"><span data-stu-id="645d6-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="645d6-466">Ее можно запустить локально, а также в другой среде, например в рабочей роли облачной службы или службы Windows.</span><span class="sxs-lookup"><span data-stu-id="645d6-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="645d6-467">Однако доступ к панели мониторинга пакета SDK веб-заданий можно получить только с помощью веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="645d6-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="645d6-468">Чтобы использовать панель мониторинга, необходимо подключить веб-приложение к используемой учетной записи хранения, указав строку подключения AzureWebJobsDashboard на вкладке **Настройка** классического портала.</span><span class="sxs-lookup"><span data-stu-id="645d6-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="645d6-469">Затем можно перейти на панель мониторинга по URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="645d6-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="645d6-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="645d6-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="645d6-471">Дополнительные сведения см. в записи блога [Получение панели мониторинга для локальной разработки с помощью пакета SDK веб-заданий](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), но обратите внимание, что она отображает имя старой строки подключения.</span><span class="sxs-lookup"><span data-stu-id="645d6-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="645d6-472">Дополнительная документация по веб-заданиям</span><span class="sxs-lookup"><span data-stu-id="645d6-472">More WebJobs documentation</span></span>
<span data-ttu-id="645d6-473">Дополнительные сведения см. в статье [Документация по веб-заданиям Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="645d6-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
