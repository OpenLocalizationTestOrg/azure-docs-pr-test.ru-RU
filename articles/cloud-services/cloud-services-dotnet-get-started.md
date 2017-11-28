---
title: "aaaGet работы с облачных служб Azure и ASP.NET | Документы Microsoft"
description: "Узнайте, как toocreate многоуровневые приложения, с помощью ASP.NET MVC и Azure. приложение Hello выполняется в облачной службе, с веб-ролью и рабочей роли. В его работе используются: Entity Framework, база данных SQL, очереди и BLOB-объекты службы хранилища Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="f099c-105">Начало работы с облачными службами Azure и ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f099c-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="f099c-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="f099c-106">Overview</span></span>
<span data-ttu-id="f099c-107">В этом учебнике показано как toocreate многоуровневое приложение .NET с ASP.NET MVC переднего плана и разверните его tooan [облачной службы Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="f099c-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="f099c-108">Здравствуйте, приложение использует [базы данных SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [службы больших двоичных объектов](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)и hello [службы очередей Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="f099c-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="f099c-109">Вы можете [загрузите проект Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) из hello коллекции кода MSDN.</span><span class="sxs-lookup"><span data-stu-id="f099c-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="f099c-110">Hello учебнике показано, как toobuild и выполнения hello приложения локально, как toodeploy его tooAzure и hello выполнения в облако и как toobuild ее с нуля.</span><span class="sxs-lookup"><span data-stu-id="f099c-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="f099c-111">Можно начать с создания с нуля и затем hello теста и после развертывания действия при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f099c-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="f099c-112">Приложение Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="f099c-112">Contoso Ads application</span></span>
<span data-ttu-id="f099c-113">приложение Hello — доски рекламных объявлений.</span><span class="sxs-lookup"><span data-stu-id="f099c-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="f099c-114">Пользователи создают рекламу, вводя текст и загружая изображения.</span><span class="sxs-lookup"><span data-stu-id="f099c-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="f099c-115">Их можно просмотреть список рекламы с помощью эскизов, и они могут просматривать полноразмерное изображение hello, при выборе сведения hello toosee ad.</span><span class="sxs-lookup"><span data-stu-id="f099c-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Список рекламы](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="f099c-117">приложение Hello использует hello [шаблон ориентированное очереди рабочих](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff нагрузки hello процессор действий по созданию эскизы tooa серверной части процесса.</span><span class="sxs-lookup"><span data-stu-id="f099c-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="f099c-118">Альтернативная архитектура: веб-сайты и веб-задания</span><span class="sxs-lookup"><span data-stu-id="f099c-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="f099c-119">В этом учебнике показано, как toorun переднего плана и серверной части в Azure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="f099c-120">Альтернативным вариантом является toorun hello переднего плана в [веб-сайте Azure](/services/web-sites/) и использовать hello [веб-заданий](http://go.microsoft.com/fwlink/?LinkId=390226) компонентов (в настоящее время в предварительной версии) для внутренней hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="f099c-121">Учебник, использующий веб-заданий, в разделе [Приступая к работе с веб-заданий Azure SDK hello](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f099c-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="f099c-122">Сведения о как toochoose hello службы, которые лучше всего соответствуют вашего сценария, см. в разделе [веб-сайтов Azure, облачных служб и виртуальных машин сравнения](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f099c-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f099c-123">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="f099c-123">What you'll learn</span></span>
* <span data-ttu-id="f099c-124">Как tooenable компьютер для разработки Azure, установив hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f099c-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="f099c-125">Как toocreate Visual Studio облачные службы проект с веб-роль ASP.NET MVC и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="f099c-126">Как tootest hello проекта облачной службы локально, с помощью эмулятора хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="f099c-127">Как toopublish hello облака проекта tooan Azure облачной службы и тестов, с помощью учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="f099c-128">Как tooupload файлов и сохранения их в hello Azure BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="f099c-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="f099c-129">Как toouse hello службы очередей Azure для обмена данными между уровнями.</span><span class="sxs-lookup"><span data-stu-id="f099c-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f099c-130">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f099c-130">Prerequisites</span></span>
<span data-ttu-id="f099c-131">Hello учебнике предполагается, что вы понимаете [основные понятия о Azure облачные службы](cloud-services-choose-me.md) например *веб-роли* и *рабочей роли* терминология.</span><span class="sxs-lookup"><span data-stu-id="f099c-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="f099c-132">Также предполагается, что вы знаете, как toowork с [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) или [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) проектов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f099c-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="f099c-133">Пример приложения Hello использует MVC, но большинство hello учебник также применяется tooWeb форм.</span><span class="sxs-lookup"><span data-stu-id="f099c-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="f099c-134">Вы можете запустить приложение hello локально без подписки Azure, но вам потребуется одно облако toohello toodeploy hello приложения.</span><span class="sxs-lookup"><span data-stu-id="f099c-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="f099c-135">Если у вас нет учетной записи, можно [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="f099c-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="f099c-136">Hello учебника инструкции работают с любой из следующих продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="f099c-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f099c-137">Visual Studio 2013</span></span>
* <span data-ttu-id="f099c-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f099c-138">Visual Studio 2015</span></span>
* <span data-ttu-id="f099c-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f099c-139">Visual Studio 2017</span></span>

<span data-ttu-id="f099c-140">Если у вас нет одного из этих, Visual Studio могут быть установлены автоматически при установке hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f099c-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="f099c-141">Архитектура приложения</span><span class="sxs-lookup"><span data-stu-id="f099c-141">Application architecture</span></span>
<span data-ttu-id="f099c-142">приложение Hello сохраняет рекламы в базе данных SQL, с помощью Entity Framework Code First таблиц hello toocreate и доступа к данным hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="f099c-143">Для каждого рекламного объявления hello базы данных хранилища два URL-адреса, один для hello полноразмерное изображение и один для hello эскиз.</span><span class="sxs-lookup"><span data-stu-id="f099c-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Таблица рекламы](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="f099c-145">Когда пользователь загружает изображение, hello переднего плана под управлением в веб-роли хранит изображения hello в [BLOB-объектов Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), и хранится такая информация ad hello в базе данных hello с URL-адресом toohello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f099c-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="f099c-146">AT hello же времени, он записывает сообщение tooan очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="f099c-147">Тыловой процесс, выполняющийся в рабочей роли периодически опрашивает очередь hello для новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="f099c-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="f099c-148">При появлении нового сообщения hello рабочей роли создает эскиз для этого образа и обновлений hello эскиза поле URL-адрес базы данных для данного рекламного объявления.</span><span class="sxs-lookup"><span data-stu-id="f099c-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="f099c-149">Hello следующей схеме показано, как части приложения hello, hello взаимодействуют.</span><span class="sxs-lookup"><span data-stu-id="f099c-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="f099c-151">Загрузите и запустите решение hello завершена</span><span class="sxs-lookup"><span data-stu-id="f099c-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="f099c-152">Загрузите и распакуйте hello [завершения решения](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="f099c-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="f099c-153">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f099c-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="f099c-154">Из hello **файл** меню щелкните **открыть проект**, перейдите toowhere загруженный hello решение и затем откройте файл решения hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="f099c-155">Нажмите клавиши CTRL + SHIFT + B toobuild hello решения.</span><span class="sxs-lookup"><span data-stu-id="f099c-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="f099c-156">По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet hello, которое не входит в hello *.zip* файла.</span><span class="sxs-lookup"><span data-stu-id="f099c-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="f099c-157">Если не восстановить hello пакетов, установите их вручную, будут toohello **управление пакетами NuGet для решения** диалоговое окно и щелкнув hello **восстановить** кнопки в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="f099c-158">В **обозревателе решений**, убедитесь, что **ContosoAdsCloudService** выбран в качестве запускаемого проекта hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="f099c-159">Если вы используете Visual Studio 2015 или более поздней версии, измените строку подключения SQL Server hello в приложение hello *Web.config* файла проекта ContosoAdsWeb hello и в hello *ServiceConfiguration.Local.cscfg* файл проекта ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="f099c-160">В каждом случае изменить «(localdb) \v11.0» слишком «(localdb) \MSSQLLocalDB».</span><span class="sxs-lookup"><span data-stu-id="f099c-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="f099c-161">Нажмите клавиши CTRL + F5 toorun hello приложения.</span><span class="sxs-lookup"><span data-stu-id="f099c-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="f099c-162">При локальном выполнении проекта облачной службы Visual Studio автоматически вызывает hello Azure *эмулятор вычислений* и Azure *эмулятор хранилища*.</span><span class="sxs-lookup"><span data-stu-id="f099c-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="f099c-163">Hello вычислений эмулятор использует компьютера ресурсы toosimulate hello веб-роли и роли рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="f099c-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="f099c-164">Эмулятор хранилища Hello использует [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate Azure облачного хранилища базы данных.</span><span class="sxs-lookup"><span data-stu-id="f099c-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="f099c-165">Hello первый раз при запуске проекта облачной службы занимает приблизительно минуты для Привет эмуляторы toostart вверх.</span><span class="sxs-lookup"><span data-stu-id="f099c-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="f099c-166">По завершении запуска эмулятора браузер по умолчанию hello откроется домашняя страница приложения toohello.</span><span class="sxs-lookup"><span data-stu-id="f099c-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="f099c-168">Нажмите кнопку **Create an Ad** (Создать приложение AD).</span><span class="sxs-lookup"><span data-stu-id="f099c-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="f099c-169">Введите некоторые тестовые данные и выберите *.jpg* изображения tooupload, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="f099c-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Страница создания](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="f099c-171">приложение Hello переходит toohello страницы индекса, но он не отображается эскиз для нового ad hello, поскольку еще не произошло, обработку.</span><span class="sxs-lookup"><span data-stu-id="f099c-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="f099c-172">Подождите немного, а затем обновить hello индекс страницы toosee hello эскиз.</span><span class="sxs-lookup"><span data-stu-id="f099c-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Страница индексации](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="f099c-174">Нажмите кнопку **сведения** для вашей toosee ad hello полноразмерное изображение.</span><span class="sxs-lookup"><span data-stu-id="f099c-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Страница сведений](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="f099c-176">Полностью на локальном компьютере без подключения облака toohello работы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="f099c-177">Эмулятор хранилища Hello хранит очередь hello и данные большого двоичного объекта в базе данных SQL Server Express LocalDB и приложения hello хранит данные ad hello в другой базе данных LocalDB.</span><span class="sxs-lookup"><span data-stu-id="f099c-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="f099c-178">Базы данных Active Directory Entity Framework Code First автоматически созданные hello hello веб-приложения hello пытался tooaccess при первом его.</span><span class="sxs-lookup"><span data-stu-id="f099c-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="f099c-179">В следующем разделе hello следует настроить ресурсы облако Azure toouse hello решения для очереди, BLOB-объектов и базы данных приложения hello при выполнении в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="f099c-180">Если нужна toocontinue toorun локально, но использует облачные ресурсы хранилища и базы данных, может сделать это.</span><span class="sxs-lookup"><span data-stu-id="f099c-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="f099c-181">Это лишь Настройка строки подключения, которые вы увидите как toodo.</span><span class="sxs-lookup"><span data-stu-id="f099c-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="f099c-182">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="f099c-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="f099c-183">Вам предстоит выполнить hello следующие приложения hello toorun действия в облаке hello:</span><span class="sxs-lookup"><span data-stu-id="f099c-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="f099c-184">Создайте облачную службу Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="f099c-185">Создайте базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="f099c-186">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="f099c-187">Настройка решения toouse hello базы данных Azure SQL при запуске в Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="f099c-188">Настройка решения toouse hello вашей учетной записи хранилища Azure при запуске в Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="f099c-189">Развертывание hello проекта tooyour Azure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="f099c-190">Создание облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-190">Create an Azure cloud service</span></span>
<span data-ttu-id="f099c-191">Приложение hello hello среды будет запущено в — облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="f099c-192">Откройте в браузере, hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f099c-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f099c-193">Щелкните **Создать > Вычисления > Облачная служба**.</span><span class="sxs-lookup"><span data-stu-id="f099c-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="f099c-194">В hello DNS поле ввода имени введите префикс URL-адреса для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="f099c-195">Этот URL-адрес имеет уникальный toobe.</span><span class="sxs-lookup"><span data-stu-id="f099c-195">This URL has toobe unique.</span></span>  <span data-ttu-id="f099c-196">Вы получите сообщение об ошибке, если префикс hello выбрать уже используется.</span><span class="sxs-lookup"><span data-stu-id="f099c-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="f099c-197">Укажите группу ресурсов для службы hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="f099c-198">Нажмите кнопку **создать новый** и затем введите имя в hello ресурсов группы поле ввода, такие как CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="f099c-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="f099c-199">Выберите нужное приложение hello toodeploy область hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="f099c-200">В этом поле указывается в каком центре обработки данных будет размещаться облачная служба.</span><span class="sxs-lookup"><span data-stu-id="f099c-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="f099c-201">В рабочем приложении следует выбрать клиентов tooyour ближайший регион hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="f099c-202">В этом учебнике выберите tooyou ближайший регион hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="f099c-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f099c-203">Click **Create**.</span></span>

    <span data-ttu-id="f099c-204">В следующие изображения hello облачная служба создается с hello CSvccontosoads.cloudapp.net URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f099c-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Новая облачная служба](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="f099c-206">Создание базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-206">Create an Azure SQL database</span></span>
<span data-ttu-id="f099c-207">При запуске приложения hello в облаке hello, он будет использовать базы данных на основе облака.</span><span class="sxs-lookup"><span data-stu-id="f099c-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="f099c-208">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Создать > базы данных > база данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="f099c-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="f099c-209">В hello **имя базы данных** введите *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="f099c-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="f099c-210">В hello **группы ресурсов**, нажмите кнопку **использовать существующие** и выберите hello группы ресурсов, используемой для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="f099c-211">В hello следующие изображения, щелкните **Server — необходимые настройки** и **Создание нового сервера**.</span><span class="sxs-lookup"><span data-stu-id="f099c-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Туннель toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="f099c-213">Кроме того Если ваша подписка уже имеет сервер, можно выберите сервер из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="f099c-214">В hello **имя сервера** введите *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="f099c-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="f099c-215">Введите **имя для входа в систему** и **пароль администратора**.</span><span class="sxs-lookup"><span data-stu-id="f099c-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="f099c-216">Если вы выбрали **Создать сервер**, не используйте имеющиеся имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="f099c-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="f099c-217">Вводите новое имя и пароль, что вы определяете теперь toouse позже при доступе к базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="f099c-218">Если был выбран сервер, который вы создали ранее, можно быть выведен hello пароль toohello административной учетной записи уже создан.</span><span class="sxs-lookup"><span data-stu-id="f099c-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="f099c-219">Выберите hello же **расположение** , выбранное для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="f099c-220">Когда hello облачной службы и базы данных находятся в разных центрах обработки данных (различных регионах), приведет к увеличению задержки и будет выставлен счет за пропускную способность за пределами центра обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="f099c-221">Пропускная способность в рамках центра обработки данных предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="f099c-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="f099c-222">Проверьте **разрешить службам azure tooaccess сервера**.</span><span class="sxs-lookup"><span data-stu-id="f099c-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="f099c-223">Нажмите кнопку **выберите** для нового сервера hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-223">Click **Select** for hello new server.</span></span>

    ![Новый сервер базы данных SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="f099c-225">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f099c-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="f099c-226">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-226">Create an Azure storage account</span></span>
<span data-ttu-id="f099c-227">Учетная запись хранилища Azure предоставляет ресурсы для хранения данных больших двоичных объектов и очереди в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="f099c-228">В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="f099c-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="f099c-229">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="f099c-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="f099c-230">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Создать > хранения > учетной записи хранения - больших двоичных объектов, файл таблицы, очереди**.</span><span class="sxs-lookup"><span data-stu-id="f099c-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="f099c-231">В hello **имя** введите префикс URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="f099c-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="f099c-232">Этот текст префикса и hello, отображаемые в окне приветствия будет hello уникальный URL-адрес tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f099c-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="f099c-233">Если префикс Привет вводимых вами уже используется другим пользователем, у вас будет toochoose другой префикс.</span><span class="sxs-lookup"><span data-stu-id="f099c-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="f099c-234">Набор hello **модель развертывания** слишком*классический*.</span><span class="sxs-lookup"><span data-stu-id="f099c-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="f099c-235">Набор hello **репликации** раскрывающемся списке слишком**локально избыточное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="f099c-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="f099c-236">При включении георепликации для учетной записи хранения hello хранимых содержимое является реплицированной tooa дополнительный ЦОД tooenable перехода на другой ресурс, случае серьезной аварии в основное расположение hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="f099c-237">Георепликация может потребовать дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="f099c-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="f099c-238">Для тестирования и разработки учетных записей обычно не следует toopay для георепликации.</span><span class="sxs-lookup"><span data-stu-id="f099c-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="f099c-239">Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f099c-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="f099c-240">В hello **группы ресурсов**, нажмите кнопку **использовать существующие** и выберите hello группы ресурсов, используемой для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="f099c-241">Набор hello **расположение** раскрывающегося списка toohello же регионе, выбранное для hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="f099c-242">Когда hello облачной службы и учетной записи хранения находятся в разных центрах обработки данных (различных регионах), приведет к увеличению задержки и будет выставлен счет за пропускную способность за пределами центра обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="f099c-243">Пропускная способность в рамках центра обработки данных предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="f099c-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="f099c-244">Территориальные группы Azure предоставляют механизм toominimize hello расстояние между ресурсами в центре обработки данных, который можно уменьшить задержку.</span><span class="sxs-lookup"><span data-stu-id="f099c-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="f099c-245">В этом учебнике территориальные группы не используются.</span><span class="sxs-lookup"><span data-stu-id="f099c-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="f099c-246">Дополнительные сведения см. в разделе [как tooCreate территориальную группу в Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="f099c-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="f099c-247">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f099c-247">Click **Create**.</span></span>

    ![Новая учетная запись хранения](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="f099c-249">В образе hello учетную запись хранения создается с hello URL-адрес `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="f099c-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="f099c-250">Настройка toouse hello решения базы данных Azure SQL, работающей в Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="f099c-251">Здравствуйте веб-проекта и hello проект рабочей роли каждого имеет собственную строку подключения базы данных, и каждый требуется база данных Azure SQL toohello toopoint, когда работает приложение hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="f099c-252">Вы воспользуетесь [преобразование файла Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello веб-роли и параметр среды облачной службы для hello рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="f099c-253">В данном разделе и следующем разделе hello хранить учетные данные в файлах проекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="f099c-254">[Не сохраняйте важные данные в общедоступном репозитории исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="f099c-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="f099c-255">В проекте ContosoAdsWeb hello откройте hello *Web.Release.config* файл преобразования для приложения hello *Web.config* файл, удалите блок комментариев hello, содержащий `<connectionStrings>` элемент и вставить Здравствуйте, следующий код на его месте.</span><span class="sxs-lookup"><span data-stu-id="f099c-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="f099c-256">Не закрывайте hello файл для редактирования.</span><span class="sxs-lookup"><span data-stu-id="f099c-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="f099c-257">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **баз данных SQL** hello левой панели щелкните hello базы данных, созданный в этом учебнике и нажмите кнопку **Показать строки подключения**.</span><span class="sxs-lookup"><span data-stu-id="f099c-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Показать строки подключения](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="f099c-259">портал Hello отображает строки соединения, с помощью заполнителя для hello пароля.</span><span class="sxs-lookup"><span data-stu-id="f099c-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Строки подключения](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="f099c-261">В hello *Web.Release.config* файл преобразования, удалите `{connectionstring}` и вставьте его месте hello строки подключения ADO.NET из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="f099c-262">В строке подключения hello, вставленного в hello *Web.Release.config* файл преобразования, замените `{your_password_here}` с hello пароль, созданный для hello новой базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="f099c-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="f099c-263">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-263">Save hello file.</span></span>  
6. <span data-ttu-id="f099c-264">Выделите и скопируйте строку подключения hello (без кавычек вокруг hello) для использования в hello, выполните действия по настройке hello проект рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="f099c-265">В **обозревателе решений**в разделе **ролей** hello проекта облачной службы, щелкните правой кнопкой мыши **ContosoAdsWorker** и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f099c-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="f099c-267">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f099c-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="f099c-268">Изменение **конфигурации службы** слишком**облака**.</span><span class="sxs-lookup"><span data-stu-id="f099c-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="f099c-269">Выберите hello **значение** для hello `ContosoAdsDbConnectionString` задание, а затем вставьте строку подключения hello, скопированный в предыдущем разделе учебника hello hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Строка подключения базы данных для рабочей роли](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="f099c-271">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="f099c-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="f099c-272">Настроить учетную запись хранилища Azure toouse решения hello, работающей в Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="f099c-273">Строки подключения учетной записи хранилища Azure для проекта веб-роли hello и hello проект рабочей роли хранятся в параметры среды в проект облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="f099c-274">Для каждого проекта отсутствует отдельный набор toobe параметры, используемые при запуске приложения hello локально и при выполнении в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="f099c-275">Обновите параметры среды hello облака для рабочих и веб-проектов роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="f099c-276">В **обозревателе решений**, щелкните правой кнопкой мыши **ContosoAdsWeb** под **ролей** в hello **ContosoAdsCloudService** проекта, а затем нажмите кнопку **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="f099c-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="f099c-278">Нажмите кнопку hello **параметры** вкладки. В hello **конфигурации службы** раскрывающегося списка выберите **облака**.</span><span class="sxs-lookup"><span data-stu-id="f099c-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Конфигурация облака](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="f099c-280">Выберите hello **StorageConnectionString** входа и вы увидите кнопку с многоточием (**...** ), расположенную hello справа от строки hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="f099c-281">Нажмите кнопку hello tooopen кнопку с многоточием hello **Создание строки подключения учетной записи хранилища** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f099c-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Откройте окно создания строки подключения](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="f099c-283">В hello **Создание строки подключения хранилища** диалоговое окно, нажмите кнопку **подписки**, выберите учетную запись хранения hello, которое было создано ранее и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="f099c-284">Если вы еще не вошли, появится запрос на ввод учетных данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Создайте строку подключения хранилища](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="f099c-286">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="f099c-286">Save your changes.</span></span>
6. <span data-ttu-id="f099c-287">Выполните hello же процедуру, которая используется для hello `StorageConnectionString` hello tooset строка соединения `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` строку подключения.</span><span class="sxs-lookup"><span data-stu-id="f099c-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="f099c-288">Эта строка подключения используется для журнала.</span><span class="sxs-lookup"><span data-stu-id="f099c-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="f099c-289">Выполните hello же процедуру, которая используется для hello **ContosoAdsWeb** tooset роли обе строки подключения для hello **ContosoAdsWorker** роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="f099c-290">Не забывайте tooset **конфигурации службы** слишком**облака**.</span><span class="sxs-lookup"><span data-stu-id="f099c-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="f099c-291">параметры среды роли Hello, настроенного с помощью пользовательского интерфейса Visual Studio hello хранятся в следующие файлы в проекте ContosoAdsCloudService hello hello:</span><span class="sxs-lookup"><span data-stu-id="f099c-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="f099c-292">*ServiceDefinition.csdef* -определяет имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="f099c-293">*ServiceConfiguration.Cloud.cscfg* -предоставляет значения, по которым будет выполняться приложение hello в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="f099c-294">*ServiceConfiguration.Local.cscfg* -предоставляет значения, по которым приложение hello будет выполняться локально.</span><span class="sxs-lookup"><span data-stu-id="f099c-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="f099c-295">Например hello ServiceDefinition.csdef включает hello следующие определения:</span><span class="sxs-lookup"><span data-stu-id="f099c-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="f099c-296">И hello *ServiceConfiguration.Cloud.cscfg* файл включает hello значениям, введенным для этих параметров в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f099c-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="f099c-297">Hello `<Instances>` определяет hello число виртуальных машин, Azure выполняет hello рабочей роли код на.</span><span class="sxs-lookup"><span data-stu-id="f099c-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="f099c-298">Hello [дальнейшие действия](#next-steps) раздел содержит toomore ссылки на сведения о горизонтальное масштабирование облачной службы</span><span class="sxs-lookup"><span data-stu-id="f099c-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="f099c-299">Развертывание проекта tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="f099c-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="f099c-300">В **обозреватель решений**, щелкните правой кнопкой мыши hello **ContosoAdsCloudService** облако проекта, а затем выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="f099c-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Меню публикации](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="f099c-302">В hello **входа** шага hello **публикации приложения Azure** мастера, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f099c-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Этап входа](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="f099c-304">В hello **параметры** шаг приветствия мастера нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f099c-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Этап настроек](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="f099c-306">Здравствуйте, параметры по умолчанию в hello **Дополнительно** вкладку допустимы для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="f099c-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="f099c-307">Сведения о вкладке "Дополнительно" hello, в разделе [мастер публикации приложений Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="f099c-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="f099c-308">В hello **Сводка** шаг, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="f099c-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Сводка действий](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="f099c-310">Hello **журнал действий Azure** открывается окно в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f099c-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="f099c-311">Выберите сведения о развертывании hello tooexpand в значок со стрелкой вправо hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="f099c-312">Hello развертывания может занять too5 минут или более toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f099c-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Окно журнал действий Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="f099c-314">После завершения состояние развертывания hello, нажмите кнопку hello **веб-приложения URL-адрес** toostart приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="f099c-315">Теперь можно протестировать приложение hello путем создания, просмотра и изменения некоторых рекламные объявления, как при запуске приложения hello локально.</span><span class="sxs-lookup"><span data-stu-id="f099c-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="f099c-316">После завершения тестирования, удаления или остановки hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f099c-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="f099c-317">Даже если вы не используете hello облачной службы, он накапливаемый расходы, так как для него зарезервированные ресурсы виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f099c-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="f099c-318">Если оставить ее работающей, любой кто найдет этот URL-адрес, сможет создать и просмотреть рекламу.</span><span class="sxs-lookup"><span data-stu-id="f099c-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="f099c-319">В hello [портал Azure](https://portal.azure.com), go toohello **Обзор** для облачной службы, а затем щелкните hello **удалить** кнопку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="f099c-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="f099c-320">Если необходимо просто tootemporarily никто другой не доступа к узлу hello, щелкните **остановить** вместо него.</span><span class="sxs-lookup"><span data-stu-id="f099c-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="f099c-321">В этом случае накладные расходы по-прежнему tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="f099c-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="f099c-322">Вы можете использовать аналогичную процедуру toodelete hello учетные записи хранилища и базы данных SQL, когда они больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="f099c-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="f099c-323">Создание приложения hello с нуля</span><span class="sxs-lookup"><span data-stu-id="f099c-323">Create hello application from scratch</span></span>
<span data-ttu-id="f099c-324">Если вы еще не загрузили [приложения hello завершения](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="f099c-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="f099c-325">Будет скопируйте файлы из проекта загружаются hello в новый проект hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="f099c-326">Создание приложения hello рекламы Contoso включает hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="f099c-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="f099c-327">Создайте новое решение облачной службы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f099c-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="f099c-328">Обновите и добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="f099c-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="f099c-329">Указание ссылок на проекты.</span><span class="sxs-lookup"><span data-stu-id="f099c-329">Set project references.</span></span>
* <span data-ttu-id="f099c-330">Настройте строки подключения.</span><span class="sxs-lookup"><span data-stu-id="f099c-330">Configure connection strings.</span></span>
* <span data-ttu-id="f099c-331">Добавьте файлы кода.</span><span class="sxs-lookup"><span data-stu-id="f099c-331">Add code files.</span></span>

<span data-ttu-id="f099c-332">После создания решения hello вам предстоит рассмотреть hello код, который является уникальным toocloud службы проектов Azure BLOB-объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="f099c-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="f099c-333">Создайте новое решение облачной службы в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f099c-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="f099c-334">В Visual Studio выберите **новый проект** из hello **файл** меню.</span><span class="sxs-lookup"><span data-stu-id="f099c-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="f099c-335">В левой области hello hello **новый проект** диалогового окна разверните **Visual C#** и выберите **облака** шаблонов и выберите hello **облачной службы Azure** шаблона.</span><span class="sxs-lookup"><span data-stu-id="f099c-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="f099c-336">Имя проекта hello и решения ContosoAdsCloudService и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Новый проект](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="f099c-338">В hello **новая облачная служба Azure** диалогового окна добавьте веб-роли и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="f099c-339">Имя веб-роли hello ContosoAdsWeb и имя рабочей роли hello ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="f099c-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="f099c-340">(Используйте значок карандаша hello в hello правой панели toochange hello по умолчанию имена ролей hello).</span><span class="sxs-lookup"><span data-stu-id="f099c-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Проект новой облачной службы](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="f099c-342">При появлении hello **новый проект ASP.NET** диалоговое окно приветствия веб-роли, Выбор шаблона MVC hello и нажмите кнопку **изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="f099c-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Изменить проверку подлинности](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="f099c-344">В hello **изменить аутентификацию** диалогового окна выберите **без проверки подлинности**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Без аутентификации](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="f099c-346">В hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="f099c-347">В **обозревателе решений**, щелкните правой кнопкой мыши hello решение (не hello проектов) и выберите **Add - новый проект**.</span><span class="sxs-lookup"><span data-stu-id="f099c-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="f099c-348">В hello **Добавление нового проекта** диалогового окна выберите **Windows** под **Visual C#** в hello левой панели, затем щелкните hello **библиотеки классов** шаблон.</span><span class="sxs-lookup"><span data-stu-id="f099c-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="f099c-349">Имя проекта hello *ContosoAdsCommon*, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="f099c-350">Необходимо tooreference hello hello и контекста модели данных Entity Framework из рабочих и веб-проектов роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="f099c-351">Кроме того можно определить классы, связанные с EF hello в проект веб-роли hello и ссылку на этот проект в проект рабочей роли hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="f099c-352">Но в hello альтернативный подход, проект рабочей роли ссылочные сборки tooweb, которые ему не требуется.</span><span class="sxs-lookup"><span data-stu-id="f099c-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="f099c-353">Обновите и добавьте пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="f099c-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="f099c-354">Откройте hello **управление пакетами NuGet** диалоговое окно для решения hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="f099c-355">Hello верхней части окна hello, выберите **обновления**.</span><span class="sxs-lookup"><span data-stu-id="f099c-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="f099c-356">Найдите hello *WindowsAzure.Storage* пакета и, если он находится в списке hello, выберите его и выберите tooupdate hello рабочих и веб-проектов, его и нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="f099c-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="f099c-357">Клиентская библиотека хранилища Hello обновляется чаще, чем шаблоны проектов Visual Studio, в toobe потребностей только что созданный проект обновлен часто вы найдете этой версии hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="f099c-358">Hello верхней части окна hello, выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="f099c-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="f099c-359">Найти hello *EntityFramework* NuGet пакета и установить на всех трех проектов.</span><span class="sxs-lookup"><span data-stu-id="f099c-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="f099c-360">Найти hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet пакет и установите его в проект рабочей роли hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="f099c-361">Установите ссылки проекта</span><span class="sxs-lookup"><span data-stu-id="f099c-361">Set project references</span></span>
1. <span data-ttu-id="f099c-362">В проекте ContosoAdsWeb hello установите проект ContosoAdsCommon toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="f099c-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="f099c-363">Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **ссылки** - **Добавление ссылок**.</span><span class="sxs-lookup"><span data-stu-id="f099c-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="f099c-364">В hello **диспетчер ссылок** установите флажок **решения — проекты** hello левой панели выберите **ContosoAdsCommon**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f099c-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="f099c-365">В проекте ContosoAdsWorker hello установите проект ContosAdsCommon toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="f099c-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="f099c-366">ContosoAdsCommon будет содержать hello Entity Framework данных модели и контекста класса, который будет использоваться в обоих hello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f099c-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="f099c-367">В проекте ContosoAdsWorker hello, задать ссылку слишком`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="f099c-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="f099c-368">Эта сборка используется toothumbnails изображения hello tooconvert серверной части.</span><span class="sxs-lookup"><span data-stu-id="f099c-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="f099c-369">Настройте строки подключения</span><span class="sxs-lookup"><span data-stu-id="f099c-369">Configure connection strings</span></span>
<span data-ttu-id="f099c-370">В этом разделе настройте хранилище Azure и строки подключения SQL для локального тестирования.</span><span class="sxs-lookup"><span data-stu-id="f099c-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="f099c-371">инструкции по развертыванию Hello ранее в учебнике hello объясняется, как tooset подключение hello строки для при hello приложение выполняется в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="f099c-372">В проект ContosoAdsWeb hello, hello откройте файл Web.config приложения и вставки hello следующие `connectionStrings` элемента после hello `configSections` элемента.</span><span class="sxs-lookup"><span data-stu-id="f099c-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="f099c-373">Если вы используете Visual Studio 2015 или более поздней версии, замените v11.0 на MSSQLLocalDB.</span><span class="sxs-lookup"><span data-stu-id="f099c-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="f099c-374">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="f099c-374">Save your changes.</span></span>
3. <span data-ttu-id="f099c-375">В проекте ContosoAdsCloudService hello, щелкните правой кнопкой мыши ContosoAdsWeb под **ролей**и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f099c-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="f099c-377">В hello **ContosAdsWeb [роль]** окне свойств щелкните hello **параметры** , а затем щелкните **добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="f099c-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="f099c-378">Оставить **конфигурации службы** значение слишком**все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="f099c-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="f099c-379">Добавьте настройку с именем *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="f099c-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="f099c-380">Задать **тип** слишком*ConnectionString*и задайте **значение** слишком*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="f099c-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Новая строка подключения](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="f099c-382">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="f099c-382">Save your changes.</span></span>
7. <span data-ttu-id="f099c-383">Выполните hello же процедура tooadd строки подключения хранилища в свойствах роли ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="f099c-384">По-прежнему в hello **ContosoAdsWorker [роль]** окно свойств добавить другую строку подключения:</span><span class="sxs-lookup"><span data-stu-id="f099c-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="f099c-385">Имя: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="f099c-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="f099c-386">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="f099c-386">Type: String</span></span>
   * <span data-ttu-id="f099c-387">Значение: Вставить hello же строка подключения, используемая для проекта веб-роли hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="f099c-388">(следующий пример hello предназначен для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f099c-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="f099c-389">Не забывайте hello toochange источника данных при копировании в этом примере, и вы используете Visual Studio 2015 или более поздней версии.)</span><span class="sxs-lookup"><span data-stu-id="f099c-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="f099c-390">Добавьте файлы кода</span><span class="sxs-lookup"><span data-stu-id="f099c-390">Add code files</span></span>
<span data-ttu-id="f099c-391">В этом разделе скопируйте файлы кода из решения загружаются hello в новое решение hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="f099c-392">Hello следующих разделах будет отображать и объясняются основные части этого кода.</span><span class="sxs-lookup"><span data-stu-id="f099c-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="f099c-393">файлы tooadd tooa проект или папку, щелкните правой кнопкой мыши проект hello или папку и нажмите кнопку **добавить** - **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="f099c-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="f099c-394">Выберите файлы hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="f099c-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="f099c-395">Если запрос на подтверждение tooreplace существующие файлы, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="f099c-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="f099c-396">В проекте ContosoAdsCommon hello, удалите hello *Class1.cs* и добавьте в его месте hello *Ad.cs* и *ContosoAdscontext.cs* файлы из hello загружен проекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="f099c-397">В проекте ContosoAdsWeb hello добавьте следующие файлы из проекта загружаются hello hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="f099c-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="f099c-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="f099c-399">В hello *представления\общие* папки:  *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f099c-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="f099c-400">В hello *Views\Home* папки: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f099c-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="f099c-401">В hello *контроллеров* папки: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="f099c-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="f099c-402">В hello *Views\Ad* папку (сначала создать папки hello): пять *.cshtml* файлов.</span><span class="sxs-lookup"><span data-stu-id="f099c-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="f099c-403">Добавьте в проект ContosoAdsWorker hello, *WorkerRole.cs* из hello загружен проекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="f099c-404">Теперь можно построить и запустить приложение hello, как описано ранее в учебнике hello и будет использовать приложение hello локальной базы данных и ресурсов эмулятора хранилища.</span><span class="sxs-lookup"><span data-stu-id="f099c-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="f099c-405">Hello ниже разделы содержат определение кода hello tooworking, связанные с hello среды Azure, большие двоичные объекты и очереди.</span><span class="sxs-lookup"><span data-stu-id="f099c-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="f099c-406">Этот учебник не объясняют, как toocreate MVC контроллеры и представления с помощью формирования шаблонов, как toowrite кода Entity Framework, работает с базами данных SQL Server или основы hello асинхронного программирования в ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="f099c-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="f099c-407">Сведения об этих темах см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f099c-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="f099c-408">Начало работы с MVC 5</span><span class="sxs-lookup"><span data-stu-id="f099c-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="f099c-409">Начало работы с EF 6 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="f099c-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="f099c-410">[Введение tooasynchronous программирование в .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="f099c-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="f099c-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="f099c-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="f099c-412">файл Ad.cs Hello определяет перечисление для категорий ad и класс сущности POCO ad сведения.</span><span class="sxs-lookup"><span data-stu-id="f099c-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="f099c-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="f099c-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="f099c-414">Класс ContosoAdsContext Hello указывает, используется класс Ad hello в коллекцию DbSet, что платформа Entity Framework будут храниться в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="f099c-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
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
```

<span data-ttu-id="f099c-415">Класс Hello имеет два конструктора.</span><span class="sxs-lookup"><span data-stu-id="f099c-415">hello class has two constructors.</span></span> <span data-ttu-id="f099c-416">Здравствуйте, сначала из них используется hello веб-проекта и указывает имя строки подключения, которая хранится в файле Web.config hello hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="f099c-417">Второй конструктор Hello позволяет toopass в hello фактическое строка подключения hello проект рабочей роли, поскольку он не содержит файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="f099c-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="f099c-418">Вы уже видели раньше была сохранена эта строка подключения, куда вы увидите позже как код hello извлекает hello строку подключения, когда он создает экземпляр класса DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="f099c-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="f099c-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="f099c-420">Код, который вызывается из hello `Application_Start` метод создает *изображения* контейнер больших двоичных объектов и *изображения* очередь, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="f099c-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="f099c-421">Это гарантирует, что каждый раз, когда начать работу с новой учетной записи хранения или начать использовать эмулятор хранилища hello на новом компьютере, контейнер hello необходимые больших двоичных объектов и очереди будет создана автоматически.</span><span class="sxs-lookup"><span data-stu-id="f099c-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="f099c-422">Здравствуйте, учетной записи хранилища toohello кода получает доступ с помощью строки подключения к хранилищу hello из hello *.cscfg* файла.</span><span class="sxs-lookup"><span data-stu-id="f099c-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="f099c-423">Затем он возвращает toohello ссылки *изображения* большого двоичного объекта контейнера, создает контейнер hello в том случае, если он еще не существует, и наборы разрешений доступа на новый контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="f099c-424">По умолчанию новые контейнеры только позволяют клиентам с помощью учетной записи хранилища больших двоичных объектов tooaccess учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f099c-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="f099c-425">Hello веб-сайт должен hello public toobe больших двоичных объектов, чтобы он может отображать изображения с помощью URL-адреса, большие двоичные объекты toohello точки изображения.</span><span class="sxs-lookup"><span data-stu-id="f099c-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="f099c-426">Аналогичный код получает toohello ссылки *изображения* ставить в очередь и создает новую очередь.</span><span class="sxs-lookup"><span data-stu-id="f099c-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="f099c-427">В этом случае изменения разрешений не требуется.</span><span class="sxs-lookup"><span data-stu-id="f099c-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="f099c-428">ContosoAdsWeb — \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="f099c-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="f099c-429">Hello *_Layout.cshtml* файл задает имя приложения hello в hello верхний и нижний колонтитулы и создает запись меню «Объявления».</span><span class="sxs-lookup"><span data-stu-id="f099c-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="f099c-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="f099c-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="f099c-431">Hello *Views\Home\Index.cshtml* файла отображаются категории ссылки на домашнюю страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="f099c-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="f099c-432">ссылки Hello передать целое значение hello hello `Category` перечисления в страницу индекса рекламы toohello переменной строки запроса.</span><span class="sxs-lookup"><span data-stu-id="f099c-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="f099c-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="f099c-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="f099c-434">В hello *AdController.cs* файл, hello вызывает конструктор hello `InitializeStorage` метод toocreate клиентская библиотека хранилища Azure объекты, которые предоставляют API для работы с BLOB-объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="f099c-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="f099c-435">После создания кода hello получает toohello ссылки *изображения* большого двоичного объекта контейнера, как было показано ранее в *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="f099c-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="f099c-436">При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f099c-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="f099c-437">политика повтора экспоненциально растущим по умолчанию Hello зависание веб-приложения hello дольше, чем через минуту на нескольких повторных попыток для временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="f099c-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="f099c-438">политика повтора Hello, указанные здесь ожидает три секунды после каждого повторите для копирования toothree попыток.</span><span class="sxs-lookup"><span data-stu-id="f099c-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="f099c-439">Аналогичный код получает toohello ссылки *изображения* очереди.</span><span class="sxs-lookup"><span data-stu-id="f099c-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="f099c-440">Большая часть кода hello контроллера является типичным для работы с моделью данных Entity Framework, с помощью класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="f099c-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="f099c-441">Исключение — hello HttpPost `Create` метод, который отправляет файл и сохраняет его в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f099c-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="f099c-442">предоставляет связыватель модели Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello метод объекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="f099c-443">Если hello пользователь выбрал tooupload файла, кода hello передает файл hello, сохраняет его в большой двоичный объект и обновляет запись в базе данных Ad hello URL-адресом toohello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f099c-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="f099c-444">Hello код, hello передачи находится в hello `UploadAndSaveBlobAsync` метод.</span><span class="sxs-lookup"><span data-stu-id="f099c-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="f099c-445">Он создает имя GUID для hello больших двоичных объектов, передачи и сохраняет файл hello и возвращает toohello сохранен эталонный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="f099c-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
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
```

<span data-ttu-id="f099c-446">После hello HttpPost `Create` метод передает большой двоичный объект и обновления hello базы данных, он создает tooinform очереди сообщений, образ будет готов для преобразования tooa эскиз серверной части процесса.</span><span class="sxs-lookup"><span data-stu-id="f099c-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="f099c-447">Здравствуйте, код для hello HttpPost `Edit` метод аналогичен за исключением того, что если hello пользователь выбирает новый файл образа необходимо удалить все большие двоичные объекты, которые уже существуют.</span><span class="sxs-lookup"><span data-stu-id="f099c-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="f099c-448">Следующий пример Hello показан hello код, который удаляет большие двоичные объекты при удалении ad.</span><span class="sxs-lookup"><span data-stu-id="f099c-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="f099c-449">ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="f099c-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="f099c-450">Hello *Index.cshtml* файла отображаются эскизы с hello другие данные ad.</span><span class="sxs-lookup"><span data-stu-id="f099c-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="f099c-451">Hello *Details.cshtml* файл отображает hello полноразмерное изображение.</span><span class="sxs-lookup"><span data-stu-id="f099c-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="f099c-452">ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="f099c-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="f099c-453">Hello *Create.cshtml* и *Edit.cshtml* -файлы указывают кодирования, что включает hello контроллера tooget hello форм `HttpPostedFileBase` объекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="f099c-454">`<input>` Элемент предписывает tooprovide браузера hello диалоговое окно выбора файла.</span><span class="sxs-lookup"><span data-stu-id="f099c-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="f099c-455">ContosoAdsWorker - WorkerRole.cs - метод OnStart</span><span class="sxs-lookup"><span data-stu-id="f099c-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="f099c-456">Hello Azure рабочей роли среда вызывает hello `OnStart` метод в hello `WorkerRole` класс при hello рабочая роль начало работы и вызывает hello `Run` метод при hello `OnStart` метод завершения.</span><span class="sxs-lookup"><span data-stu-id="f099c-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="f099c-457">Hello `OnStart` метод возвращает строку подключения базы данных hello из hello *.cscfg* файл и передает его toohello класса Entity Framework DbContext.</span><span class="sxs-lookup"><span data-stu-id="f099c-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="f099c-458">поставщик SQLClient Hello используется по умолчанию, поэтому не требуется toobe указан поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="f099c-459">После этого метод hello получает учетную запись хранения toohello ссылки и создает hello контейнер больших двоичных объектов и очереди, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="f099c-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="f099c-460">Код Hello, — примерно toowhat, вы уже видели в веб-роли hello `Application_Start` метод.</span><span class="sxs-lookup"><span data-stu-id="f099c-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="f099c-461">ContosoAdsWorker - WorkerRole.cs - метод Run</span><span class="sxs-lookup"><span data-stu-id="f099c-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="f099c-462">Hello `Run` метод вызывается, когда hello `OnStart` метод завершает свою работу инициализации.</span><span class="sxs-lookup"><span data-stu-id="f099c-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="f099c-463">метод Hello выполняется бесконечный цикл, который отслеживает наличие новых сообщений очереди и обрабатывает их при поступлении.</span><span class="sxs-lookup"><span data-stu-id="f099c-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="f099c-464">После каждой итерации цикла hello сообщения в очереди, если было обнаружено программа hello бездействует в течение секунды.</span><span class="sxs-lookup"><span data-stu-id="f099c-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="f099c-465">Это предотвращает расходов чрезмерного ЦП времени и объема хранилища транзакции hello рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="f099c-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="f099c-466">Hello группа консультантов по Microsoft истории о разработчике, забывший tooinclude, развернуты tooproduction и указывает слева для отпуска.</span><span class="sxs-lookup"><span data-stu-id="f099c-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="f099c-467">Когда он вернулся его контроля стоимость которой превышает отпуска hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="f099c-468">Иногда hello содержимое сообщения в очереди приводит к ошибке во время обработки.</span><span class="sxs-lookup"><span data-stu-id="f099c-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="f099c-469">Это называется *подозрительное сообщение*, и если вы только произошла ошибка и перезапуска цикла hello, ведут бесконечные попробуйте tooprocess это сообщение.</span><span class="sxs-lookup"><span data-stu-id="f099c-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="f099c-470">Поэтому блок catch hello включает if Здравствуйте, сколько раз приложение hello предпринял tooprocess инструкцию, которая проверяет toosee текущего сообщения, и если прошло более 5 раз приветственное сообщение удаляется из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="f099c-471">`ProcessQueueMessage` вызывается, когда сообщение найдено в очереди.</span><span class="sxs-lookup"><span data-stu-id="f099c-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="f099c-472">Этот код считывает URL-адрес hello базы данных tooget hello изображения, преобразует эскиз tooa рисунка hello, сохраняет эскиз hello в большом двоичном объекте, обновляет базу данных hello URL-адрес эскиза blob hello и удаляет сообщение hello очереди.</span><span class="sxs-lookup"><span data-stu-id="f099c-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="f099c-473">Здравствуйте, код в hello `ConvertImageToThumbnailJPG` метод использует классы в пространстве имен System.Drawing hello для простоты.</span><span class="sxs-lookup"><span data-stu-id="f099c-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="f099c-474">Однако hello классы этого пространства имен были разработаны для работы с Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="f099c-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="f099c-475">Они не поддерживаются в службе Windows или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f099c-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="f099c-476">Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация, IHttpHandlers и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования образов с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).</span><span class="sxs-lookup"><span data-stu-id="f099c-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="f099c-477">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f099c-477">Troubleshooting</span></span>
<span data-ttu-id="f099c-478">В случае, если что-то не сработает, пока вы следуете инструкциям hello в этом учебнике, ниже приведены некоторые распространенные ошибки и каким образом tooresolve их.</span><span class="sxs-lookup"><span data-stu-id="f099c-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="f099c-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="f099c-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="f099c-480">Hello `RoleEnvironment` при запуске приложения в Azure или при запуске локально с помощью эмулятора вычислений Azure hello объекта передается Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="f099c-481">Если эта ошибка появляется при запуске локально, убедитесь, что вы указали проекта ContosoAdsCloudService hello hello запускаемым проектом.</span><span class="sxs-lookup"><span data-stu-id="f099c-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="f099c-482">Это настраивает hello toorun проекта, с помощью эмулятора вычислений Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="f099c-483">Одно из действий hello использует приложение hello hello Azure RoleEnvironment для — tooget подключения hello строковых значений, хранящихся в hello *.cscfg* файлы, поэтому отсутствует строка подключения имеет другой причиной этого исключения.</span><span class="sxs-lookup"><span data-stu-id="f099c-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="f099c-484">Убедитесь, что вы создали StorageConnectionString приветствия для облака, как и локальные конфигурации в проекте ContosoAdsWeb hello и создания обеих строках подключения для обеих конфигураций, в проекте ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="f099c-485">Если сделать **найти все** поиска для StorageConnectionString в hello всего решения, вы должны увидеть его 9 раз в 6-файлы.</span><span class="sxs-lookup"><span data-stu-id="f099c-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="f099c-486">Не может переопределять tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="f099c-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="f099c-487">Новый порт ниже минимально разрешенного значения 8080 для протокола http</span><span class="sxs-lookup"><span data-stu-id="f099c-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="f099c-488">Попробуйте изменить номер порта hello hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="f099c-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="f099c-489">Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f099c-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="f099c-490">Нажмите кнопку hello **Web** , а затем измените номер порта hello в hello **URL-адрес проекта** параметр.</span><span class="sxs-lookup"><span data-stu-id="f099c-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="f099c-491">Другим способом, hello проблему можно разрешить см. hello в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="f099c-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="f099c-492">Другие ошибки при работе локально</span><span class="sxs-lookup"><span data-stu-id="f099c-492">Other errors when running locally</span></span>
<span data-ttu-id="f099c-493">По умолчанию новой облачной службы проекты используют hello вычислений Azure emulator express toosimulate hello среды Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="f099c-494">Это облегченная версия полной вычислений hello и в некоторых условиях hello полный эмулятор будут работать при версию express hello не.</span><span class="sxs-lookup"><span data-stu-id="f099c-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="f099c-495">toochange hello проекта toouse hello полный эмулятор, щелкните правой кнопкой мыши проект ContosoAdsCloudService hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f099c-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="f099c-496">В hello **свойства** щелкните hello **Web** , а затем щелкните hello **использовать полный эмулятор** переключатель.</span><span class="sxs-lookup"><span data-stu-id="f099c-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="f099c-497">В приложение hello toorun заказов с hello полный эмулятор имеют tooopen Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f099c-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f099c-498">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f099c-498">Next steps</span></span>
<span data-ttu-id="f099c-499">Hello приложение Contoso рекламы намеренно была сохранена в простой учебник Приступая к работе.</span><span class="sxs-lookup"><span data-stu-id="f099c-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="f099c-500">Например, он не реализует [внедрения зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) или hello [репозитория и единицу работы шаблоны](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), это не [используют интерфейс для ведения журнала](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), он не использовал [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) изменений в модели данных toomanage или [устойчивость подключений EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage временной ошибки сети и т. д.</span><span class="sxs-lookup"><span data-stu-id="f099c-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="f099c-501">Ниже приведены некоторые примеры приложений облачной службы, демонстрируют дополнительные реальных написания безопасного кода, перечисленными далее от менее сложные toomore сложных.</span><span class="sxs-lookup"><span data-stu-id="f099c-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="f099c-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="f099c-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="f099c-503">Аналогично окну tooContoso рекламы но реализует дополнительные функции и дополнительные реальных написания безопасного кода.</span><span class="sxs-lookup"><span data-stu-id="f099c-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="f099c-504">[Многоуровневое облачное приложение Azure с таблицами, квотами, и большими двоичными объектами](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="f099c-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="f099c-505">Представляет таблицы, а также большие двоичные объекты и очереди службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f099c-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="f099c-506">Исходя из более старой версии hello Azure SDK для .NET, требует toowork некоторые изменения в текущей версии hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="f099c-507">[Основы облачных служб в Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="f099c-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="f099c-508">Полный образец, демонстрирующий широкий спектр советы и рекомендации, созданных группой шаблонов и методов Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="f099c-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="f099c-509">Общие сведения о разработке для облака hello см. в разделе [Создание реальных облачных приложений с Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="f099c-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="f099c-510">Для tooAzure Видеообзор хранилища лучшие шаблоны и практические рекомендации см. в разделе [хранилища Microsoft Azure — новые, рекомендации и шаблоны](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="f099c-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="f099c-511">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f099c-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="f099c-512">Облачные службы Azure, часть 1: Введение</span><span class="sxs-lookup"><span data-stu-id="f099c-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="f099c-513">Как toomanage облачных служб</span><span class="sxs-lookup"><span data-stu-id="f099c-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="f099c-514">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="f099c-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="f099c-515">Как поставщиком услуг toochoose облака</span><span class="sxs-lookup"><span data-stu-id="f099c-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
