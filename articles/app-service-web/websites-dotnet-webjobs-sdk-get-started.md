---
title: "aaaCreate веб-задания .NET в службе приложений Azure | Документы Microsoft"
description: "Создание многоуровневого приложения с помощью ASP.NET MVC и Azure. Hello запускает в веб-приложения в службе приложений Azure и hello запускает в качестве веб-задания. приложение Hello используется Entity Framework, база данных SQL и очереди хранилища Azure и больших двоичных объектов."
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
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="97dd4-105">Создание веб-задания .NET в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="97dd4-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="97dd4-106">В этом учебнике показано, как toowrite кода для простой многоуровневого приложения ASP.NET MVC 5, использующий hello [SDK веб-задания](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="97dd4-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="97dd4-107">Здравствуйте, назначение hello [SDK веб-заданий](websites-webjobs-resources.md) является toosimplify hello код, предназначенный для выполнения стандартных задач, которые могут выполнять веб-задания, например обработки изображений, обработки очередей, объединение RSS, обслуживание файлов и отправки сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="97dd4-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="97dd4-108">Hello SDK веб-задания имеет встроенные функции для работы с хранилищем Azure и Service Bus, планирование задач и обработка ошибок и других стандартных сценариев.</span><span class="sxs-lookup"><span data-stu-id="97dd4-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="97dd4-109">Кроме того, он имеет разработан toobe расширяемой и [репозитория открытым исходным кодом для расширений](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="97dd4-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="97dd4-110">Пример приложения Hello является доски рекламных объявлений.</span><span class="sxs-lookup"><span data-stu-id="97dd4-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="97dd4-111">Пользователи могут загружать изображения для рекламных материалов и фоновой обработки преобразует hello toothumbnails изображения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="97dd4-112">Страница списка ad Hello показывает эскизы hello, а страница сведений о ad hello hello полноразмерное изображение.</span><span class="sxs-lookup"><span data-stu-id="97dd4-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="97dd4-113">Ниже приведен снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="97dd4-113">Here's a screenshot:</span></span>

![Список рекламы](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="97dd4-115">В этом примере приложение работает с [очередями Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) и [большими двоичными объектами Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="97dd4-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="97dd4-116">Hello учебнике показано, как toodeploy hello приложения слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) и [базы данных SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="97dd4-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="97dd4-117"><a id="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="97dd4-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="97dd4-118">Hello учебнике предполагается, что вы знаете, как toowork с [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) проектов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97dd4-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="97dd4-119">Учебник Hello первоначально был написан для Visual Studio 2013, но может использоваться с более поздними версиями Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97dd4-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="97dd4-120">При использовании Visual Studio 2015 или 2017 г обратить внимание, что перед запуском приложения hello локально, необходимо изменить hello `Data Source` частью строка подключения SQL Server LocalDB hello в файлах Web.config и App.config hello из `Data Source=(localdb)\v11.0` слишком`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="97dd4-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="97dd4-121"><a name="note"></a>Необходимо иметь учетную запись Azure toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="97dd4-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="97dd4-122">Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): вы получаете кредиты можно использовать tootry out платных служб Azure, и даже после того, они используются, можно защитить учетную запись hello и использовать свободного служб Azure, таких как веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="97dd4-123">Вашей кредитной карты не взимается, пока вы явным образом изменения параметров и попросите toobe взимается плата.</span><span class="sxs-lookup"><span data-stu-id="97dd4-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="97dd4-124">Вы можете [активировать ежемесячные деньги на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="97dd4-125">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="97dd4-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="97dd4-126">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="97dd4-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="97dd4-127"><a id="learn"></a>Содержание обучения</span><span class="sxs-lookup"><span data-stu-id="97dd4-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="97dd4-128">Hello учебнике показано, как hello toodo следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="97dd4-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="97dd4-129">Включите компьютер для разработки Azure, установив hello Azure SDK (только для Visual Studio 2013 и 2015 пользователей).</span><span class="sxs-lookup"><span data-stu-id="97dd4-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="97dd4-130">Создайте проект консольного приложения, которая автоматически развертывает как веб-задание Azure при развертывании hello связанного веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="97dd4-131">Проверка серверной части пакета SDK веб-задания на компьютере разработки hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="97dd4-132">Публикация приложения с веб-заданий tooa серверной части веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="97dd4-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="97dd4-133">Отправка файлов и сохранения их в hello службы больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="97dd4-134">Используйте toowork hello веб-заданий Azure SDK с очереди хранилища Azure и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="97dd4-135"><a id="contosoads"></a>Архитектура приложения</span><span class="sxs-lookup"><span data-stu-id="97dd4-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="97dd4-136">Пример приложения Hello использует hello [шаблон ориентированное очереди рабочих](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff нагрузки hello процессор действий по созданию эскизы tooa фоновой обработки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="97dd4-137">приложение Hello сохраняет рекламы в базе данных SQL, с помощью Entity Framework Code First таблиц hello toocreate и доступа к данным hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="97dd4-138">Для каждого рекламного объявления hello база данных хранит два URL-адреса: один для hello полноразмерное изображение и один для эскиза hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Таблица рекламы](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="97dd4-140">При отправке изображение, веб-приложения hello хранит изображения hello в [BLOB-объектов Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), и хранит сведения ad hello в базе данных hello с URL-адресом toohello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="97dd4-141">AT hello же времени, он записывает сообщение tooan очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="97dd4-142">Фоновый процесс, выполняющийся как веб-задания Azure hello SDK веб-заданий выполняет опрос очереди hello для новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="97dd4-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="97dd4-143">При появлении нового сообщения hello веб-задание создает эскиз для этого образа и обновления hello эскиза поле URL-адрес базы данных для данного рекламного объявления.</span><span class="sxs-lookup"><span data-stu-id="97dd4-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="97dd4-144">Вот это диаграмма, показывающая, как взаимодействуют компоненты hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Архитектура Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="97dd4-146">Hello учебника инструкции применяются tooAzure пакета SDK для .NET 2.7.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="97dd4-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="97dd4-147"><a id="storage"></a>Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="97dd4-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="97dd4-148">Учетная запись хранилища Azure предоставляет ресурсы для хранения данных больших двоичных объектов и очереди в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="97dd4-149">Он также используется hello данных журналов toostore SDK веб-заданий для мониторинга "hello".</span><span class="sxs-lookup"><span data-stu-id="97dd4-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="97dd4-150">В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="97dd4-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="97dd4-151">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="97dd4-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="97dd4-152">Откройте hello **обозревателя серверов** окна в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97dd4-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="97dd4-153">Щелкните правой кнопкой мыши hello **Azure** узла, а затем щелкните **подключения tooMicrosoft подписки Azure...** .</span><span class="sxs-lookup"><span data-stu-id="97dd4-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Подключение tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="97dd4-155">Выполните вход с использованием учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="97dd4-156">Щелкните правой кнопкой мыши **хранения** в разделе hello узла Azure, а затем нажмите кнопку **создать учетную запись хранилища**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="97dd4-158">В hello **создать учетную запись хранилища** диалоговое окно, введите имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="97dd4-159">Имя Hello должен быть уникальным (нет других учетной записи хранилища Azure может иметь hello таким же именем).</span><span class="sxs-lookup"><span data-stu-id="97dd4-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="97dd4-160">Если ввести имя hello уже используется, вы получите toochange вероятность его.</span><span class="sxs-lookup"><span data-stu-id="97dd4-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="97dd4-161">Здравствуйте, tooaccess URL-адрес учетной записи хранения будут *{имя}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="97dd4-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="97dd4-162">Набор hello **регион или территориальная группа** tooyou ближайший регион toohello раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="97dd4-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="97dd4-163">Этот параметр указывает, в каком центре обработки данных Azure будет размещаться учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="97dd4-164">Теоретически этот выбор не имеет большого значения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="97dd4-165">Однако для рабочего веб-приложения требуется веб-сервер и вашей toobe учетной записи хранилища в hello задержки toominimize же регионе и данные исходящих расходов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="97dd4-166">веб-приложения Hello (который вы создадите в более поздней версии) должно быть центра обработки данных, как закрыть как можно toohello браузеры, доступ к веб-приложения hello в порядке toominimize задержки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="97dd4-167">Набор hello **репликации** раскрывающемся списке слишком**локально избыточной**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="97dd4-168">При включении георепликации для учетной записи хранения hello хранимых содержимое является реплицированной tooa вторичный центр обработки данных tooenable перехода на другой ресурс в случае серьезной аварии в основное расположение hello toothat расположение.</span><span class="sxs-lookup"><span data-stu-id="97dd4-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="97dd4-169">Георепликация может потребовать дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="97dd4-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="97dd4-170">Для тестирования и разработки учетных записей обычно не следует toopay для георепликации.</span><span class="sxs-lookup"><span data-stu-id="97dd4-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="97dd4-171">Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="97dd4-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="97dd4-172">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-172">Click **Create**.</span></span>

    ![Новая учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="97dd4-174"><a id="download"></a>Загрузить приложение hello</span><span class="sxs-lookup"><span data-stu-id="97dd4-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="97dd4-175">Загрузите и распакуйте hello [завершения решения](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="97dd4-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="97dd4-176">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97dd4-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="97dd4-177">Из hello **файл** меню щелкните **откройте > проект или решение**, перейдите toowhere загруженный hello решение и затем откройте файл решения hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="97dd4-178">Нажмите клавиши CTRL + SHIFT + B toobuild hello решения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="97dd4-179">По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet hello, которое не входит в hello *.zip* файла.</span><span class="sxs-lookup"><span data-stu-id="97dd4-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="97dd4-180">Если не восстановить hello пакетов, установите их вручную, будут toohello **управление пакетами NuGet для решения** диалогового окна, нажав кнопку hello **восстановить** кнопки в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="97dd4-181">В **обозревателе решений**, убедитесь, что **ContosoAdsWeb** выбран в качестве запускаемого проекта hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="97dd4-182"><a id="configurestorage"></a>Настройка учетной записи хранения toouse приложения hello</span><span class="sxs-lookup"><span data-stu-id="97dd4-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="97dd4-183">Откройте приложение hello *Web.config* файл в проекте ContosoAdsWeb hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="97dd4-184">Hello файл содержит строку подключения SQL и строку соединения хранения Azure для работы с BLOB-объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="97dd4-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="97dd4-185">Строка подключения SQL Hello указывает tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) базы данных.</span><span class="sxs-lookup"><span data-stu-id="97dd4-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="97dd4-186">Строка подключения хранилища Hello приведен пример с заполнителями для hello хранилища учетной записи имя и ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="97dd4-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="97dd4-187">Это будет заменено строку подключения с именем hello и ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="97dd4-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="97dd4-188">Строка подключения хранилища Hello называется AzureWebJobsStorage так, как это имя hello приветствия использует пакет SDK веб-заданий по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="97dd4-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="97dd4-189">Здравствуйте, таким же именем используется здесь, чтобы обеспечить tooset только одно подключение строковое значение в среде Azure hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="97dd4-190">В **обозревателя серверов**, щелкните правой кнопкой мыши учетную запись хранилища в группе hello **хранения** , а затем щелкните **свойства**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Щелкните свойства учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="97dd4-192">В hello **свойства** окно, нажмите кнопку **ключи учетной записи хранения**и нажмите кнопку с многоточием hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Ключи учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="97dd4-194">Копировать hello **строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-194">Copy hello **Connection String**.</span></span>

    ![Диалоговое окно "Ключи учетной записи хранения"](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="97dd4-196">Замените строку соединения хранения hello в hello *Web.config* файл со строкой подключения hello был скопирован в буфер.</span><span class="sxs-lookup"><span data-stu-id="97dd4-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="97dd4-197">Убедитесь, что выбраны все внутри кавычек hello, но не включая кавычки hello перед вставкой.</span><span class="sxs-lookup"><span data-stu-id="97dd4-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="97dd4-198">Откройте hello *App.config* файл в проекте ContosoAdsWebJob hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="97dd4-199">Этот файл содержит две строки подключения хранилища: одну для данных приложения, а другую для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="97dd4-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="97dd4-200">Можно использовать отдельные учетные записи хранения для данных приложений и ведения журнала; также можно использовать [несколько учетных записей хранения для данных](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="97dd4-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="97dd4-201">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="97dd4-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="97dd4-202">строки подключения Hello имеют прототипы для hello ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-202">hello connection strings have placeholders for hello storage account keys.</span></span>

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

    <span data-ttu-id="97dd4-203">По умолчанию hello SDK веб-заданий ищет строки подключения с именем AzureWebJobsStorage и AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="97dd4-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="97dd4-204">Кроме того, вы можете [хранения строки подключения hello, однако требуется и передать его в явном виде toohello `JobHost` объекта](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="97dd4-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="97dd4-205">Замените строку подключения hello скопированный ранее обе строки подключения хранилища.</span><span class="sxs-lookup"><span data-stu-id="97dd4-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="97dd4-206">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-206">Save your changes.</span></span>

## <span data-ttu-id="97dd4-207"><a id="run"></a>Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="97dd4-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="97dd4-208">веб-клиентом toostart hello приложения hello, нажмите клавиши CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="97dd4-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="97dd4-209">toohello Домашняя страница откроется в браузере по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="97dd4-210">(hello веб-проекта запускается, поскольку вы внесли hello запускаемого проекта.)</span><span class="sxs-lookup"><span data-stu-id="97dd4-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Домашняя страница Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="97dd4-212">серверной части веб-задания hello toostart приложения hello, щелкните правой кнопкой мыши проект ContosoAdsWebJob hello в **обозревателе решений**, а затем нажмите кнопку **отладки** > **запустить новый экземпляр** .</span><span class="sxs-lookup"><span data-stu-id="97dd4-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="97dd4-213">Приложения окно консоли открывается и отображает сообщения для ведения журнала, указывающий, что запущен toorun hello объекта JobHost SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="97dd4-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Выполняется отображение этого hello серверной части окна приложения консоли](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="97dd4-215">В браузере нажмите кнопку **Create an Ad** (Создать рекламу).</span><span class="sxs-lookup"><span data-stu-id="97dd4-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="97dd4-216">Введите некоторые тестовые данные, выберите образ tooupload и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Страница создания](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="97dd4-218">приложение Hello переходит toohello страницы индекса, но он не отображается эскиз для нового ad hello, поскольку еще не произошло, обработку.</span><span class="sxs-lookup"><span data-stu-id="97dd4-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="97dd4-219">В то же время после короткого ожидания ведения журнала сообщений в окне приложения hello консоли показывает, что сообщения в очереди было получено и обработки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Окно приложения консоли, отображающее, что сообщение очереди обработано](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="97dd4-221">После появления hello, ведение журнала сообщений в окне приложения hello консоли обновите hello индекс страницы toosee hello эскиз.</span><span class="sxs-lookup"><span data-stu-id="97dd4-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Страница индексации](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="97dd4-223">Нажмите кнопку **сведения** для вашей toosee ad hello полноразмерное изображение.</span><span class="sxs-lookup"><span data-stu-id="97dd4-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Страница сведений](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="97dd4-225">Приложение hello работы локального компьютера и использует SQL Server, базы данных, расположенной на компьютере, но он работает с очередями и больших двоичных объектов в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="97dd4-226">В следующем разделе hello вы будете запускать приложение hello в облаке hello, используя это облачная база данных, а также большие двоичные объекты в облаке и очереди.</span><span class="sxs-lookup"><span data-stu-id="97dd4-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="97dd4-227"><a id="runincloud"></a>Запустите приложение hello в облаке hello</span><span class="sxs-lookup"><span data-stu-id="97dd4-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="97dd4-228">Вам предстоит выполнить hello следующие приложения hello toorun действия в облаке hello:</span><span class="sxs-lookup"><span data-stu-id="97dd4-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="97dd4-229">Развертывание приложений tooWeb.</span><span class="sxs-lookup"><span data-stu-id="97dd4-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="97dd4-230">Visual Studio автоматически создаст новое веб-приложение в службе приложений и экземпляр базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="97dd4-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="97dd4-231">Настройте hello web app toouse учетную запись базы данных и хранения данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="97dd4-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="97dd4-232">После создания некоторых рекламы при выполнении в облаке hello вы просмотрите hello SDK веб-задания мониторинга toosee hello широкие возможности, он имеет toooffer наблюдения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="97dd4-233">Развертывание приложений tooWeb</span><span class="sxs-lookup"><span data-stu-id="97dd4-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="97dd4-234">Закройте окно браузера hello и окно приложения hello консоли.</span><span class="sxs-lookup"><span data-stu-id="97dd4-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="97dd4-235">Следуйте указаниям hello hello [публикации tooAzure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) раздела.</span><span class="sxs-lookup"><span data-stu-id="97dd4-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="97dd4-236">После завершения hello шаги развертывания, продолжите hello оставшихся задач в этой статье.</span><span class="sxs-lookup"><span data-stu-id="97dd4-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="97dd4-237">Настроить hello web app toouse учетную запись базы данных и хранения данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="97dd4-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="97dd4-238">Рекомендации по безопасности является слишком[не размещайте конфиденциальные сведения, такие как строки соединения в файлах, которые хранятся в репозитории исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="97dd4-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="97dd4-239">Azure предоставляет toodo способ: можно задать строку подключения и другие значения параметров в среде Azure hello и интерфейсы API настройки ASP.NET автоматически получать эти значения при запуске приложения hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="97dd4-240">Эти значения можно задать в Azure с помощью **обозревателя серверов**, hello портал Azure, Windows PowerShell или hello межплатформенного интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="97dd4-241">Дополнительные сведения см. в статье [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложений и строки подключения).</span><span class="sxs-lookup"><span data-stu-id="97dd4-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="97dd4-242">В этом разделе используется **обозревателя серверов** tooset значений строки подключения в Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="97dd4-243">В **обозревателе сервера** щелкните правой кнопкой мыши свое веб-приложение в узле **Azure > Служба приложений > {ваша группа ресурсов}**, а затем щелкните **Просмотреть параметры**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="97dd4-244">Hello **веб-приложения Azure** в hello появится окно **конфигурации** вкладки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="97dd4-245">Изменение имени hello имя toohello строка подключения DefaultConnection hello выбран при настройке базы данных SQL hello в hello [публикации tooAzure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) статьи.</span><span class="sxs-lookup"><span data-stu-id="97dd4-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="97dd4-246">Azure автоматически создается в этой строке подключения при создании веб-приложения hello со связанной базой данных, поэтому уже имеет значение строки правой подключения hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="97dd4-247">Вы меняете только hello имя toowhat правильный код.</span><span class="sxs-lookup"><span data-stu-id="97dd4-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="97dd4-248">Добавьте две новые строки подключения с именами AzureWebJobsStorage и AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="97dd4-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="97dd4-249">Задайте тип базы данных hello слишком**настраиваемый**и набор hello подключения строковое значение toohello одинаковое значение, что вы использовали для hello *Web.config* и *App.config* файлов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="97dd4-250">(Убедитесь, включает строку hello все подключение, не только hello ключ доступа и не включать hello кавычки).</span><span class="sxs-lookup"><span data-stu-id="97dd4-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="97dd4-251">Эти строки подключения используются hello SDK веб-заданий, один для данных приложений и один для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="97dd4-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="97dd4-252">Как показано выше, hello, один для данных приложений также используется hello веб-интерфейса кода.</span><span class="sxs-lookup"><span data-stu-id="97dd4-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="97dd4-253">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-253">Click **Save**.</span></span>

    ![Строки подключения на портале Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="97dd4-255">В **обозревателя серверов**, щелкните правой кнопкой мыши веб-приложения hello и нажмите кнопку **остановить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="97dd4-256">После остановки веб-приложения hello, щелкните правой кнопкой мыши веб-приложение hello и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="97dd4-257">Hello веб-задание запускается автоматически при публикации, но он останавливается при изменении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97dd4-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="97dd4-258">toorestart, можно перезапустить веб-приложение hello или перезагрузите веб-задания hello в hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="97dd4-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="97dd4-259">Это обычно рекомендуется toorestart hello веб-приложения после изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97dd4-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="97dd4-260">Обновите окно браузера hello с URL-адрес приложения hello в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="97dd4-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="97dd4-261">Откроется домашняя страница приветствия.</span><span class="sxs-lookup"><span data-stu-id="97dd4-261">hello home page appears.</span></span>
8. <span data-ttu-id="97dd4-262">Создание рекламы, как в случае, когда вы [локально запустить приложение hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="97dd4-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="97dd4-263">страница индекса Hello показана без эскиза на первый.</span><span class="sxs-lookup"><span data-stu-id="97dd4-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="97dd4-264">Обновите страницу приветствия через несколько секунд и hello эскиза отображается.</span><span class="sxs-lookup"><span data-stu-id="97dd4-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="97dd4-265">Если эскиз hello не отображается, может потребоваться toowait приблизительно минуты для hello toorestart веб-задания.</span><span class="sxs-lookup"><span data-stu-id="97dd4-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="97dd4-266">Если после некоторое время, по-прежнему не отображается эскиз hello при обновлении страницы приветствия, hello веб-задания не может иметь автоматически начата.</span><span class="sxs-lookup"><span data-stu-id="97dd4-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="97dd4-267">В этом случае переход toohello **службы приложений** колонки в hello [портал Azure](https://portal.azure.com/), найдите веб-приложения и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="97dd4-268">Hello представления панели мониторинга пакета SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="97dd4-269">В hello [портал Azure](https://portal.azure.com/)выберите hello **колонку служб приложения**, найдите веб-приложения и выберите **веб-задания**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="97dd4-270">Выберите hello **журналы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-270">Select hello **Logs** tab.</span></span>

    ![Вкладка "Журналы"](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="97dd4-272">На новой вкладке браузера откроется toohello панели мониторинга пакета SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="97dd4-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="97dd4-273">панель мониторинга Hello показывает, hello веб-задание работает и отображается список функций в коде, пакет SDK веб-заданий запускается приветствия.</span><span class="sxs-lookup"><span data-stu-id="97dd4-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="97dd4-274">Выберите один из hello функции toosee сведения о его выполнения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-274">Click one of hello functions toosee details about its execution.</span></span>

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="97dd4-277">Hello **функция воспроизведения** кнопку на этой странице снова вызывает hello SDK веб-заданий для функции hello toocall framework, и она предоставляет функции вероятность toochange hello данные, передаваемые toohello сначала.</span><span class="sxs-lookup"><span data-stu-id="97dd4-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="97dd4-278">После окончания тестирования, рассмотрите возможность удаления веб-приложения hello, учетной записи хранилища и экземпляр базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="97dd4-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="97dd4-279">веб-приложения Hello предоставляется бесплатно, однако плата начисляется hello SQL учетной записи хранилища и экземпляр базы данных (хотя и минимальная из-за малого размера toohello).</span><span class="sxs-lookup"><span data-stu-id="97dd4-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="97dd4-280">Кроме того Если оставить hello веб-приложения под управлением любой пользователь находит URL-адрес, можно создать и просмотра рекламы.</span><span class="sxs-lookup"><span data-stu-id="97dd4-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="97dd4-281">Удаление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="97dd4-281">Delete your web app</span></span>
<span data-ttu-id="97dd4-282">На портале hello go toohello **службы приложений** колонки, найдите и выберите веб-приложения и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="97dd4-283">Если необходимо просто tootemporarily запретить другим пользователям доступ к веб-приложения hello, нажмите кнопку **остановить** вместо.</span><span class="sxs-lookup"><span data-stu-id="97dd4-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="97dd4-284">В этом случае накладные расходы по-прежнему tooaccrue для hello базы данных SQL и учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="97dd4-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="97dd4-285">Удаление учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="97dd4-285">Delete your storage account</span></span>
<span data-ttu-id="97dd4-286">toodelete вашей учетной записи хранения в разделе [удалить учетную запись хранения](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="97dd4-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="97dd4-287">Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="97dd4-287">Delete your database</span></span>
<span data-ttu-id="97dd4-288">toodelete SQL базы данных см. в разделе hello [API REST для базы данных SQL Azure](https://docs.microsoft.com/rest/api/sql/) документации.</span><span class="sxs-lookup"><span data-stu-id="97dd4-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="97dd4-289"><a id="create"></a>Создание приложения hello с нуля</span><span class="sxs-lookup"><span data-stu-id="97dd4-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="97dd4-290">В этом разделе вы выполните hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="97dd4-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="97dd4-291">Создание решения Visual Studio с веб-проектом.</span><span class="sxs-lookup"><span data-stu-id="97dd4-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="97dd4-292">Добавьте проект библиотеки классов для данных hello уровень доступа, общим для внешнего интерфейса hello и серверной части.</span><span class="sxs-lookup"><span data-stu-id="97dd4-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="97dd4-293">Добавьте проект консольного приложения для внутреннего hello с включено развертывание веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="97dd4-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="97dd4-294">Добавление пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="97dd4-294">Add NuGet packages.</span></span>
* <span data-ttu-id="97dd4-295">Указание ссылок на проекты.</span><span class="sxs-lookup"><span data-stu-id="97dd4-295">Set project references.</span></span>
* <span data-ttu-id="97dd4-296">Скопируйте файлы кода и конфигурации приложения из приложения загружаются hello, с которой выполнялись в предыдущем разделе hello hello учебника.</span><span class="sxs-lookup"><span data-stu-id="97dd4-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="97dd4-297">Просмотрите компоненты hello кода hello, поддерживающих Azure BLOB-объектов и очередей и hello SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="97dd4-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="97dd4-298">Создание решения Visual Studio с веб-проектом и проектом библиотеки класса</span><span class="sxs-lookup"><span data-stu-id="97dd4-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="97dd4-299">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="97dd4-300">В hello **новый проект** диалоговое окно, выберите **Visual C#** > **Web** > **веб-приложение ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="97dd4-301">Имя проекта hello ContosoAdsWeb, назовите решение hello ContosoAdsWebJobsSDK (изменить имя решения hello, если вы будете помещать в hello же папке, что hello загрузки решения) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Новый проект](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="97dd4-303">В hello **новое веб-приложение ASP.NET** диалоговое окно, выберите шаблон MVC hello и выберите **изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Изменить проверку подлинности](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="97dd4-305">В hello **изменить аутентификацию** диалоговое окно, выберите **без проверки подлинности**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Без аутентификации](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="97dd4-307">В hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="97dd4-308">Visual Studio создает решение hello и hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="97dd4-309">В **обозревателе решений**, щелкните правой кнопкой мыши решение hello (не hello проект), а затем выберите **добавить** > **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="97dd4-310">В hello **Добавление нового проекта** диалоговое окно, выберите **Visual C#** > **Windows классического** > **библиотека классов (.NET Платформа)** шаблона.</span><span class="sxs-lookup"><span data-stu-id="97dd4-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="97dd4-311">Имя проекта hello *ContosoAdsCommon*, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="97dd4-312">Этот проект будет содержать контекста Entity Framework hello и hello модели данных, для которых hello переднего плана и будет использовать серверной части.</span><span class="sxs-lookup"><span data-stu-id="97dd4-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="97dd4-313">Кроме того можно определить классы, связанные с EF hello в веб-проекте hello и ссылку на этот проект из проекта веб-задания hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="97dd4-314">Однако проект веб-задания будут иметь tooweb ссылочных сборок, которые ему не требуется.</span><span class="sxs-lookup"><span data-stu-id="97dd4-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="97dd4-315">Добавление проекта приложения консоли, в котором включено развертывание веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="97dd4-316">Щелкните правой кнопкой мыши веб-проект hello (не hello решение или проект библиотеки классов hello) и нажмите кнопку **добавить** > **новый проект веб-задания Azure**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Пункт меню "Новый проект веб-задания Azure"](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="97dd4-318">В hello **добавить веб-задание Azure** диалоговое окно, введите в качестве обеих hello ContosoAdsWebJob **имя проекта** и hello **имя веб-задания**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="97dd4-319">Оставить **режим запуска веб-задания** значение слишком**запуска постоянно**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="97dd4-320">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-320">Click **OK**.</span></span>

   <span data-ttu-id="97dd4-321">Visual Studio создает консольное приложение, настроенное toodeploy как веб-задания при каждом развертывании hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="97dd4-322">toodo, что она выполнена hello следующие задачи после создания проекта hello:</span><span class="sxs-lookup"><span data-stu-id="97dd4-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="97dd4-323">Добавлен *публикации settings.json веб-задания* файл в папке свойств проекта веб-задания hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="97dd4-324">Добавлен *list.json веб-заданий* файл в hello веб-проекта свойства папки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="97dd4-325">Установить пакет Microsoft.Web.WebJobs.Publish NuGet hello в проект веб-задания hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="97dd4-326">Дополнительные сведения об этих изменениях см. в разделе [как toodeploy веб-заданий с помощью Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="97dd4-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="97dd4-327">Добавление пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="97dd4-327">Add NuGet packages</span></span>
<span data-ttu-id="97dd4-328">Hello шаблон нового проекта для проекта веб-задания автоматически устанавливает пакет NuGet SDK веб-заданий hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="97dd4-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="97dd4-329">Один является зависимости пакета SDK веб-заданий, которые автоматически устанавливается в проект веб-задания hello hello hello библиотека клиента хранилища Azure (SCL).</span><span class="sxs-lookup"><span data-stu-id="97dd4-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="97dd4-330">Однако необходимо tooadd его toowork проект web toohello с BLOB-объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="97dd4-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="97dd4-331">Откройте hello **управление пакетами NuGet** диалоговое окно для решения hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="97dd4-332">Выберите в левой области hello **установленных пакетов**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="97dd4-333">Найти hello *хранилища Azure* пакета, а затем нажмите кнопку **управление**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="97dd4-334">В hello **выберите проекты** поле, выберите hello **ContosoAdsWeb** флажок и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="97dd4-335">Все три проекта используйте toowork hello Entity Framework с данными в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="97dd4-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="97dd4-336">Выберите в левой области hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="97dd4-337">Найти hello *EntityFramework* NuGet пакета и установить на всех трех проектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="97dd4-338">Установите ссылки проекта</span><span class="sxs-lookup"><span data-stu-id="97dd4-338">Set project references</span></span>
<span data-ttu-id="97dd4-339">Проекты веб-задания и веб работать с hello базы данных SQL, поэтому оба проекта ContosoAdsCommon toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="97dd4-340">В проекте ContosoAdsWeb hello установите проект ContosoAdsCommon toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="97dd4-341">(Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **добавить** > **ссылка**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="97dd4-342">В hello **диспетчер ссылок** выберите **проекты** > **решения** > **ContosoAdsCommon**, а затем нажмите кнопку **ОК**.)</span><span class="sxs-lookup"><span data-stu-id="97dd4-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="97dd4-343">проект веб-задания Hello необходимо ссылки для работы с изображениями и доступ к строки подключения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="97dd4-344">В проекте ContosoAdsWebJob hello, задать ссылку слишком`System.Drawing` и `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="97dd4-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="97dd4-345">Добавление кода и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="97dd4-345">Add code and configuration files</span></span>
<span data-ttu-id="97dd4-346">Этот учебник не содержит как слишком[создавать MVC контроллеры и представления, с помощью формирования шаблонов](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), также как[написать код платформы Entity Framework, который работает с базами данных SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), или [hello основы Асинхронное программирование в ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="97dd4-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="97dd4-347">Таким образом, все, что остается toodo — копирование файлов кода и конфигурации из решения hello загружены в решение новый hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="97dd4-348">После этого hello следующих разделах покажите и объясните основные части кода hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="97dd4-349">файлы tooadd tooa проект или папку, щелкните правой кнопкой мыши проект hello или папку и нажмите кнопку **добавить** > **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="97dd4-350">Выберите hello файлов требуется и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="97dd4-351">Если запрос на подтверждение tooreplace существующие файлы, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="97dd4-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="97dd4-352">В проекте ContosoAdsCommon hello, удалите hello *Class1.cs* и добавьте в его hello месте следующие файлы из проекта hello загрузки файла.</span><span class="sxs-lookup"><span data-stu-id="97dd4-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="97dd4-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-353">*Ad.cs*</span></span>
   * <span data-ttu-id="97dd4-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="97dd4-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="97dd4-356">В проекте ContosoAdsWeb hello добавьте следующие файлы из проекта загружаются hello hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="97dd4-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="97dd4-357">*Web.config*</span></span>
   * <span data-ttu-id="97dd4-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="97dd4-359">В hello *контроллеров* папки: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="97dd4-360">В hello *представления\общие* папки: *_Layout.cshtml* файла</span><span class="sxs-lookup"><span data-stu-id="97dd4-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="97dd4-361">В hello *Views\Home* папки: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="97dd4-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="97dd4-362">В hello *Views\Ad* папку (сначала создать папки hello): пять *.cshtml* файлов</span><span class="sxs-lookup"><span data-stu-id="97dd4-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="97dd4-363">В проекте ContosoAdsWebJob hello добавьте следующие файлы из проекта загружаются hello hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="97dd4-364">*App.config* (изменение hello фильтром типов файлов слишком**все файлы**)</span><span class="sxs-lookup"><span data-stu-id="97dd4-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="97dd4-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-365">*Program.cs*</span></span>
   * <span data-ttu-id="97dd4-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="97dd4-366">*Functions.cs*</span></span>

<span data-ttu-id="97dd4-367">Теперь можно построить, запуска и развертывания приложения hello, как описано ранее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="97dd4-368">Перед этим Однако остановите веб-задания, по-прежнему работает в hello первого веб-приложения, развернутые на hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="97dd4-369">В противном случае этого веб-задания будет обрабатывать сообщения очереди, созданные локально или по приложения hello в новое веб-приложение, так как все используете hello же учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="97dd4-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="97dd4-370"><a id="code"></a>Просмотрите код приложения hello</span><span class="sxs-lookup"><span data-stu-id="97dd4-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="97dd4-371">Hello ниже разделы содержат определение кода hello связанных tooworking с hello SDK веб-задания и больших двоичных объектах хранилища Azure и очереди.</span><span class="sxs-lookup"><span data-stu-id="97dd4-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="97dd4-372">Hello при кода определенного toohello SDK веб-заданий, см. toohello [Program.cs и Functions.cs](#programcs) разделы.</span><span class="sxs-lookup"><span data-stu-id="97dd4-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="97dd4-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="97dd4-374">файл Ad.cs Hello определяет перечисление для категорий ad и класс сущности POCO ad сведения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="97dd4-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="97dd4-376">Hello класс ContosoAdsContext указывает, используется класс Ad hello в коллекцию DbSet, что платформа Entity Framework хранит в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="97dd4-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="97dd4-377">Класс Hello имеет два конструктора.</span><span class="sxs-lookup"><span data-stu-id="97dd4-377">hello class has two constructors.</span></span> <span data-ttu-id="97dd4-378">Здравствуйте сначала используется hello веб-проекта и указывает имя строки подключения, которая хранится в файле Web.config hello или среды выполнения Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="97dd4-379">Второй конструктор Hello позволяет toopass в строку hello фактическое подключения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="97dd4-380">Необходим проект веб-задания hello поскольку он не содержит файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="97dd4-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="97dd4-381">Вы уже видели раньше была сохранена эта строка подключения, куда вы увидите позже как код hello извлекает hello строку подключения, когда он создает экземпляр класса DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="97dd4-382">ContosoAdsCommon — BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="97dd4-383">Hello `BlobInformation` класс — это toostore используется информация о BLOB-объект образа в очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="97dd4-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="97dd4-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="97dd4-385">Код, который вызывается из hello `Application_Start` метод создает *изображения* контейнер больших двоичных объектов и *изображения* очередь, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="97dd4-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="97dd4-386">Это гарантирует, что при каждом запуске с помощью новой учетной записи хранения hello требуемые контейнер больших двоичных объектов и очереди создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="97dd4-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="97dd4-387">Здравствуйте, учетной записи хранилища toohello кода получает доступ с помощью строки подключения к хранилищу hello из hello *Web.config* файл или среды выполнения Azure.</span><span class="sxs-lookup"><span data-stu-id="97dd4-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="97dd4-388">Затем он возвращает toohello ссылки *изображения* большого двоичного объекта контейнера, создает контейнер hello в том случае, если он еще не существует, и наборы разрешений доступа на новый контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="97dd4-389">По умолчанию новые контейнеры разрешено только клиенты с большими двоичными объектами tooaccess учетные данные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="97dd4-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="97dd4-390">веб-приложения Hello должен hello public toobe больших двоичных объектов, чтобы он может отображать изображения с помощью URL-адреса, большие двоичные объекты toohello точки изображения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

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

<span data-ttu-id="97dd4-391">Аналогичный код получает toohello ссылки *thumbnailrequest* ставить в очередь и создает новую очередь.</span><span class="sxs-lookup"><span data-stu-id="97dd4-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="97dd4-392">В этом случае изменений разрешений не требуется.</span><span class="sxs-lookup"><span data-stu-id="97dd4-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="97dd4-393">ContosoAdsWeb — _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="97dd4-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="97dd4-394">Hello *_Layout.cshtml* файл задает имя приложения hello в hello верхний и нижний колонтитулы и создает запись меню «Объявления».</span><span class="sxs-lookup"><span data-stu-id="97dd4-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="97dd4-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="97dd4-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="97dd4-396">Hello *Views\Home\Index.cshtml* файла отображаются категории ссылки на домашнюю страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="97dd4-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="97dd4-397">ссылки Hello передать целое значение hello hello `Category` перечисления в страницу индекса рекламы toohello переменной строки запроса.</span><span class="sxs-lookup"><span data-stu-id="97dd4-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="97dd4-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="97dd4-399">В hello *AdController.cs* файл, hello вызывает конструктор hello `InitializeStorage` метод toocreate клиентская библиотека хранилища Azure объекты, которые предоставляют API для работы с BLOB-объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="97dd4-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="97dd4-400">Затем код hello получает toohello ссылки *изображения* большого двоичного объекта контейнера, как было показано ранее в *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="97dd4-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="97dd4-401">При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="97dd4-402">политика повтора экспоненциально растущим по умолчанию Hello зависание веб-приложения hello дольше, чем через минуту на нескольких повторных попыток для временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="97dd4-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="97dd4-403">политика повтора Hello, указанные здесь ожидает три секунды после каждого повторите для копирования toothree попыток.</span><span class="sxs-lookup"><span data-stu-id="97dd4-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="97dd4-404">Аналогичный код получает toohello ссылки *изображения* очереди.</span><span class="sxs-lookup"><span data-stu-id="97dd4-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="97dd4-405">Большая часть кода hello контроллера является типичным для работы с моделью данных Entity Framework, с помощью класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="97dd4-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="97dd4-406">Исключение — hello HttpPost `Create` метод, который отправляет файл и сохраняет его в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="97dd4-407">предоставляет связыватель модели Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello метод объекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="97dd4-408">Если hello пользователь выбрал tooupload файла, кода hello передает файл hello, сохраняет его в большой двоичный объект и обновляет запись в базе данных Ad hello URL-адресом toohello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="97dd4-409">Hello код, hello передачи находится в hello `UploadAndSaveBlobAsync` метод.</span><span class="sxs-lookup"><span data-stu-id="97dd4-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="97dd4-410">Он создает имя GUID для hello больших двоичных объектов, передачи и сохраняет файл hello и возвращает toohello сохранен эталонный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="97dd4-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="97dd4-411">После hello HttpPost `Create` метод передает большой двоичный объект и обновления Здравствуйте, базы данных, он создает очередь сообщений tooinform hello серверной части процесс, образ будет готов для преобразования tooa эскиз.</span><span class="sxs-lookup"><span data-stu-id="97dd4-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="97dd4-412">Здравствуйте, код для hello HttpPost `Edit` метод аналогичен, за исключением того, что если hello пользователь выбирает новый файл образа, необходимо удалить все большие двоичные объекты, которые уже существуют для этой ad.</span><span class="sxs-lookup"><span data-stu-id="97dd4-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="97dd4-413">Ниже приведен код hello, удаляет большие двоичные объекты при удалении ad.</span><span class="sxs-lookup"><span data-stu-id="97dd4-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="97dd4-414">ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="97dd4-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="97dd4-415">Hello *Index.cshtml* файла отображаются эскизы с hello другие данные ad:</span><span class="sxs-lookup"><span data-stu-id="97dd4-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="97dd4-416">Hello *Details.cshtml* файл отображает hello полноразмерное изображение:</span><span class="sxs-lookup"><span data-stu-id="97dd4-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="97dd4-417">ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="97dd4-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="97dd4-418">Hello *Create.cshtml* и *Edit.cshtml* -файлы указывают кодирования, что включает hello контроллера tooget hello форм `HttpPostedFileBase` объекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="97dd4-419">`<input>` Элемент предписывает tooprovide браузера hello диалоговое окно выбора файла.</span><span class="sxs-lookup"><span data-stu-id="97dd4-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="97dd4-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="97dd4-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="97dd4-421">Когда hello запускает веб-задания hello `Main` вызовы методов hello SDK веб-заданий `JobHost.RunAndBlock` выполнения метода toobegin триггеру функций hello текущем потоке.</span><span class="sxs-lookup"><span data-stu-id="97dd4-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="97dd4-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="97dd4-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="97dd4-423">Этот метод вызывается Hello SDK веб-заданий при получении сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="97dd4-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="97dd4-424">Создает Hello метод эскиз и помещает hello эскиз URL-адрес в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

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
            // be instantiated and disposed within hello function.
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

* <span data-ttu-id="97dd4-425">Hello `QueueTrigger` атрибут направляет hello SDK веб-заданий toocall этот метод при получении нового сообщения в очереди thumbnailrequest hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="97dd4-426">Hello `BlobInformation` из очереди сообщения hello автоматически десериализовать в hello `blobInfo` параметра.</span><span class="sxs-lookup"><span data-stu-id="97dd4-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="97dd4-427">По завершении метода hello hello очереди сообщение удаляется.</span><span class="sxs-lookup"><span data-stu-id="97dd4-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="97dd4-428">При сбое метода hello перед завершением hello очереди сообщение не удаляется; После истечения срока аренды 10 минут, сообщение hello является выпущено toobe взял еще раз и обработки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="97dd4-429">Если сообщение вызывает исключение, эта последовательность не будет повторяться бесконечно.</span><span class="sxs-lookup"><span data-stu-id="97dd4-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="97dd4-430">После 5 неудачных попыток tooprocess сообщение, сообщение hello является перемещенный tooa очередь с именем {имя}-подозрительное.</span><span class="sxs-lookup"><span data-stu-id="97dd4-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="97dd4-431">Максимальное число попыток Hello настраивается.</span><span class="sxs-lookup"><span data-stu-id="97dd4-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="97dd4-432">Здравствуйте, два `Blob` атрибуты предоставляют объекты, привязанные tooblobs: один toohello существующего BLOB-объекта изображения и один tooa новый эскиза большой двоичный объект, создаваемый методом hello.</span><span class="sxs-lookup"><span data-stu-id="97dd4-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="97dd4-433">Имена больших двоичных объектов будут взяты из свойств объекта hello `BlobInformation` получено в очереди сообщение hello объекта (`BlobName` и `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="97dd4-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="97dd4-434">tooget hello всеми функциональными возможностями hello клиентской библиотеки хранилища, можно использовать hello `CloudBlockBlob` toowork класса с большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="97dd4-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="97dd4-435">Если требуется tooreuse кода, написанного toowork с `Stream` объектов, которые можно использовать hello `Stream` класса.</span><span class="sxs-lookup"><span data-stu-id="97dd4-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="97dd4-436">Дополнительные сведения о том, как toowrite функции, используйте пакет SDK веб-задания атрибутов см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="97dd4-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="97dd4-437">Как toouse Azure очередь хранилища с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="97dd4-438">Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="97dd4-439">Как toouse Azure таблицу хранилища с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="97dd4-440">Как toouse шины обслуживания Azure с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="97dd4-441">Если веб-приложение выполняется на нескольких виртуальных машин, несколько веб-задания будут выполняться одновременно, а в некоторых случаях это может привести к hello же данные, обработка несколько раз.</span><span class="sxs-lookup"><span data-stu-id="97dd4-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="97dd4-442">Это не проблема, при использовании встроенных очереди hello, BLOB-объекта и триггеры Service Bus.</span><span class="sxs-lookup"><span data-stu-id="97dd4-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="97dd4-443">Hello SDK гарантирует, что функций будет обрабатываться только один раз для каждого сообщения или большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="97dd4-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="97dd4-444">Сведения о том, как нормальное завершение работы tooimplement. в разделе [нормальное завершение работы](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="97dd4-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="97dd4-445">Здравствуйте, код в hello `ConvertImageToThumbnailJPG` метод (не показано) использует классы в hello `System.Drawing` пространство имен для простоты.</span><span class="sxs-lookup"><span data-stu-id="97dd4-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="97dd4-446">Однако hello классы этого пространства имен были разработаны для работы с Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="97dd4-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="97dd4-447">Они не поддерживаются в службе Windows или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97dd4-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="97dd4-448">Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования изображения с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).</span><span class="sxs-lookup"><span data-stu-id="97dd4-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="97dd4-449">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97dd4-449">Next steps</span></span>
<span data-ttu-id="97dd4-450">В этом учебнике было показано простое многоуровневого приложения, использующего hello SDK веб-заданий для серверной обработки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="97dd4-451">В этом разделе приведены рекомендации по дальнейшему изучению многоуровневых приложений ASP.NET и веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="97dd4-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="97dd4-452">Отсутствующие функции</span><span class="sxs-lookup"><span data-stu-id="97dd4-452">Missing features</span></span>
<span data-ttu-id="97dd4-453">приложение Hello довольно просты учебник Приступая к работе.</span><span class="sxs-lookup"><span data-stu-id="97dd4-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="97dd4-454">В реальном приложении следует реализовать [внедрения зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) и hello [репозитория и единицу работы шаблоны](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), используйте [интерфейса для ведения журнала](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), используйте [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage данные изменений в модели и использовать [устойчивость подключений EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage временный сетевой ошибки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="97dd4-455">Масштабирование веб-заданий</span><span class="sxs-lookup"><span data-stu-id="97dd4-455">Scaling WebJobs</span></span>
<span data-ttu-id="97dd4-456">Веб-задания выполняются в контексте веб-приложения hello и не масштабируемая отдельно.</span><span class="sxs-lookup"><span data-stu-id="97dd4-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="97dd4-457">Например если имеется один экземпляр приложения стандартные веб-сайтов, имеется только один экземпляр запущен процесс фоновой и она использует некоторые hello server ресурсов (ЦП, памяти и т. д.), в противном случае будут доступны tooserve веб-содержимого.</span><span class="sxs-lookup"><span data-stu-id="97dd4-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="97dd4-458">Если трафика зависит от времени день или день недели, и hello серверной обработки вы должны toodo может ожидать, может планировать toorun вашего веб-задания по низкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="97dd4-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="97dd4-459">Если hello нагрузки по-прежнему слишком большое для этого решения, можно запустить серверной hello как веб-задания в выделенном отдельные веб-приложения для этой цели.</span><span class="sxs-lookup"><span data-stu-id="97dd4-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="97dd4-460">Затем можно масштабировать веб-приложение внутреннего сервера отдельно от веб-приложения внешнего сервера.</span><span class="sxs-lookup"><span data-stu-id="97dd4-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="97dd4-461">Дополнительные сведения см. в разделе [Масштабирование веб-заданий](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="97dd4-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="97dd4-462">Предотвращение завершения работы веб-приложений из-за превышения времени ожидания</span><span class="sxs-lookup"><span data-stu-id="97dd4-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="97dd4-463">toomake убедиться, что веб-заданий всегда работает, и работает на всех экземплярах веб-приложения, у вас есть tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) компонентов.</span><span class="sxs-lookup"><span data-stu-id="97dd4-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="97dd4-464">С помощью пакета SDK веб-задания вне веб-заданий hello</span><span class="sxs-lookup"><span data-stu-id="97dd4-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="97dd4-465">Программа, использующая hello SDK веб-заданий не toorun в Azure в веб-задания.</span><span class="sxs-lookup"><span data-stu-id="97dd4-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="97dd4-466">Ее можно запустить локально, а также в другой среде, например в рабочей роли облачной службы или службы Windows.</span><span class="sxs-lookup"><span data-stu-id="97dd4-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="97dd4-467">Тем не менее можно только обращаться hello мониторинга SDK веб-заданий Azure веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="97dd4-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="97dd4-468">у вас есть tooconnect hello web app toohello учетной записи хранения вы используете, задав строку подключения AzureWebJobsDashboard hello на hello мониторинга hello toouse **Настройка** hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="97dd4-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="97dd4-469">Затем toohello панели мониторинга можно получить с помощью hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="97dd4-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="97dd4-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="97dd4-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="97dd4-471">Дополнительные сведения см. в разделе [получение панели мониторинга для локальной разработки с помощью hello SDK веб-заданий](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), но Обратите внимание, что в нем отображаются старые имя строки подключения.</span><span class="sxs-lookup"><span data-stu-id="97dd4-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="97dd4-472">Дополнительная документация по веб-заданиям</span><span class="sxs-lookup"><span data-stu-id="97dd4-472">More WebJobs documentation</span></span>
<span data-ttu-id="97dd4-473">Дополнительные сведения см. в статье [Документация по веб-заданиям Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="97dd4-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
