---
title: "Начало работы с облачными службами Azure и ASP.NET | Документация Майкрософт"
description: "Узнайте, как можно создать многоуровневое приложение с помощью ASP.NET MVC и Azure. Такое приложение выполняется в облачной службе и обладает веб-ролью и рабочей ролью. В его работе используются: Entity Framework, база данных SQL, очереди и BLOB-объекты службы хранилища Azure."
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
ms.openlocfilehash: d2c197db73477d06d86d1c4faa8c4a2f58c7b391
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="7ea15-105">Начало работы с облачными службами Azure и ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7ea15-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="7ea15-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="7ea15-106">Overview</span></span>
<span data-ttu-id="7ea15-107">Это руководство описывает, как создавать многоуровневое приложение .NET с внешним ASP.NET MVC и как развернуть его в [облачной службе Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="7ea15-108">Приложение использует [базу данных Azure SQL](http://msdn.microsoft.com/library/azure/ee336279), [службу BLOB-объектов Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) и [службу очередей Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="7ea15-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="7ea15-109">Можно [загрузить проект Visual Studio](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) из галереи кода MSDN.</span><span class="sxs-lookup"><span data-stu-id="7ea15-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="7ea15-110">В руководстве показано, как строить и запускать приложение локально, как разворачивать его в Azure и запускать в облаке и как создавать его с нуля.</span><span class="sxs-lookup"><span data-stu-id="7ea15-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="7ea15-111">Можно начать с построения с нуля и затем выполнить шаги по тестированию и развертыванию по желанию.</span><span class="sxs-lookup"><span data-stu-id="7ea15-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="7ea15-112">Приложение Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="7ea15-112">Contoso Ads application</span></span>
<span data-ttu-id="7ea15-113">Приложение представляет собой рекламную доску объявлений.</span><span class="sxs-lookup"><span data-stu-id="7ea15-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="7ea15-114">Пользователи создают рекламу, вводя текст и загружая изображения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="7ea15-115">Они могут видеть список рекламы по эскизам изображений, и они могут видеть изображения в полном размере, когда выбирают рекламу для просмотра деталей.</span><span class="sxs-lookup"><span data-stu-id="7ea15-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![Список рекламы](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="7ea15-117">Приложение использует [рабочий шаблон на основе очередей](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) для разгрузки процессора от задач создания эскизов в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="7ea15-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="7ea15-118">Альтернативная архитектура: веб-сайты и веб-задания</span><span class="sxs-lookup"><span data-stu-id="7ea15-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="7ea15-119">Это руководство описывает, как запускать фоновые и интерфейсные компоненты в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="7ea15-120">Альтернативой является запуск интерфейсного компонента на [веб-сайте Azure](/services/web-sites/) и использование [веб-заданий](http://go.microsoft.com/fwlink/?LinkId=390226) (пока предварительной версии) для фонового компонента.</span><span class="sxs-lookup"><span data-stu-id="7ea15-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="7ea15-121">Руководство по веб-заданиям см. в статье [Создание веб-задания .NET в службе приложений Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="7ea15-122">Сведения о том, как выбрать службы, см. в статье о [сравнении веб-сайтов, облачных служб и виртуальных машин Azure](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7ea15-123">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="7ea15-123">What you'll learn</span></span>
* <span data-ttu-id="7ea15-124">Как подготовить компьютер к разработке для Azure путем установки пакета Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="7ea15-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="7ea15-125">Как создать облачный проект Visual Studio с веб-ролью ASP.NET MVC и рабочей ролью ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="7ea15-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="7ea15-126">Как тестировать локально проект облачной службы, используя эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="7ea15-127">Как опубликовать облачный проект в облачной службе Azure и тестировать его с использованием учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="7ea15-128">Как отправлять файлы и хранить их в службе BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="7ea15-129">Как использовать службу очередей Azure для связи между уровнями.</span><span class="sxs-lookup"><span data-stu-id="7ea15-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ea15-130">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7ea15-130">Prerequisites</span></span>
<span data-ttu-id="7ea15-131">В руководстве предполагается, что вы понимаете [базовые концепции облачной службы Azure](cloud-services-choose-me.md), такие как термины *веб-роль* и *рабочая роль*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="7ea15-132">Кроме того, предполагается, что вы знаете, как работать с проектами [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) или [веб-форм](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ea15-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="7ea15-133">Пример приложения использует MVC, но многое в руководство также применимо к веб-формам.</span><span class="sxs-lookup"><span data-stu-id="7ea15-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="7ea15-134">Вы можете запускать приложение локально без подписки Azure, но она понадобится для развертывания приложения в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="7ea15-135">Если у вас нет учетной записи, можно [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="7ea15-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="7ea15-136">Инструкции руководства применимы со следующими продуктами:</span><span class="sxs-lookup"><span data-stu-id="7ea15-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="7ea15-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7ea15-137">Visual Studio 2013</span></span>
* <span data-ttu-id="7ea15-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7ea15-138">Visual Studio 2015</span></span>
* <span data-ttu-id="7ea15-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7ea15-139">Visual Studio 2017</span></span>

<span data-ttu-id="7ea15-140">Если у вас нет ни одного из этих продуктов, Visual Studio может быть установлен автоматически при установке пакета SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="7ea15-141">Архитектура приложения</span><span class="sxs-lookup"><span data-stu-id="7ea15-141">Application architecture</span></span>
<span data-ttu-id="7ea15-142">Приложение хранит рекламу в базе данных SQL, используя Entity Framework Code First для создания таблиц и доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="7ea15-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="7ea15-143">Для каждого рекламного объявления база данных хранит два URL-адреса: один для полноразмерного изображения, другой для эскиза.</span><span class="sxs-lookup"><span data-stu-id="7ea15-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Таблица рекламы](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="7ea15-145">Когда пользователь отправляет изображение, внешнее приложение, работающее в веб-роли, сохраняет его в [большой двоичный объект Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), а информацию о рекламе с URL-адресом, который указывает на большой двоичный объект, — в базе данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="7ea15-146">В это же время оно записывает сообщение в очередь Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="7ea15-147">Фоновый процесс, работающий в рабочей роли, периодически опрашивает очередь о новых сообщениях.</span><span class="sxs-lookup"><span data-stu-id="7ea15-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="7ea15-148">Когда появляется новое сообщение, рабочая роль создает эскиз для изображения и обновляет поле базы данных с URL-адресом эскиза для этой рекламы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="7ea15-149">На схеме ниже показано, как взаимодействуют части приложения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-149">The following diagram shows how the parts of the application interact.</span></span>

![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="7ea15-151">Загрузка и запуск готового решения</span><span class="sxs-lookup"><span data-stu-id="7ea15-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="7ea15-152">Загрузите и распакуйте [готовое решение](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="7ea15-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="7ea15-153">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ea15-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="7ea15-154">В меню **Файл** выберите **Открыть проект**, перейдите к папке, куда вы скачали решение, а затем откройте файл решения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="7ea15-155">Чтобы построить решение, нажмите CTRL+SHIFT+B.</span><span class="sxs-lookup"><span data-stu-id="7ea15-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="7ea15-156">По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet, которое не включено в *ZIP*-файл.</span><span class="sxs-lookup"><span data-stu-id="7ea15-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="7ea15-157">Если пакеты не восстановлены, установите их вручную, перейдя к диалоговому окну **Управление пакетами NuGet** для решения и нажав кнопку **Восстановить** вверху справа.</span><span class="sxs-lookup"><span data-stu-id="7ea15-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="7ea15-158">В **обозревателе решений** в качестве запускаемого проекта должен быть выбран **ContosoAdsCloudService**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="7ea15-159">Если вы используете Visual Studio 2015 или более поздней версии, измените строку подключения SQL Server в файле приложения *Web.config* в проекте ContosoAdsWeb и в файле *ServiceConfiguration.Local.cscfg* проекта ContosoAdsCloudService.</span><span class="sxs-lookup"><span data-stu-id="7ea15-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="7ea15-160">В каждом файле измените (localdb)\v11.0 на (localdb)\MSSQLLocalDB.</span><span class="sxs-lookup"><span data-stu-id="7ea15-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="7ea15-161">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="7ea15-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="7ea15-162">Когда запускаете локально проект облачной службы, Visual Studio автоматически вызывает *эмулятор вычислений* Azure и *эмулятор хранилища* Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="7ea15-163">Эмулятор хранилища использует ресурсы компьютера для эмуляции сред рабочей и веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="7ea15-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="7ea15-164">Эмулятор хранилища использует базу данных [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) для эмуляции работы хранилища Azure в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="7ea15-165">При первом запуске проекта облачной службы, запуск эмулятора займет порядка одной минуты.</span><span class="sxs-lookup"><span data-stu-id="7ea15-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="7ea15-166">После завершения работы эмулятора стандартный браузер открывается с домашней страницей приложения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="7ea15-168">Нажмите кнопку **Create an Ad** (Создать приложение AD).</span><span class="sxs-lookup"><span data-stu-id="7ea15-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="7ea15-169">Введите тестовые данные, выберите файл изображения с расширением *.jpg* , предназначенный для загрузки, и нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Страница создания](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="7ea15-171">Приложение переходит к странице индексации, но не показывает эскиз для новой рекламы, поскольку индексирование еще не проводилось.</span><span class="sxs-lookup"><span data-stu-id="7ea15-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="7ea15-172">Подождите немного и затем обновите страницу индексации, чтобы увидеть эскиз.</span><span class="sxs-lookup"><span data-stu-id="7ea15-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Страница индексации](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="7ea15-174">Щелкните **Details** , чтобы увидеть рекламу в полный размер.</span><span class="sxs-lookup"><span data-stu-id="7ea15-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Страница сведений](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="7ea15-176">Приложение запущено полностью локально, без соединения с облаком.</span><span class="sxs-lookup"><span data-stu-id="7ea15-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="7ea15-177">Эмулятор хранилища сохраняет очередь и данные большого двоичного объекта в базе данных SQL Server Express LocalDB, и приложение хранит данные рекламы в другой базе данных LocalDB.</span><span class="sxs-lookup"><span data-stu-id="7ea15-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="7ea15-178">Entity Framework Code First автоматически создает базу данных рекламы в первый раз при обращении приложения к ней.</span><span class="sxs-lookup"><span data-stu-id="7ea15-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="7ea15-179">В следующем разделе будет настроено решение для использования ресурсов облака Azure для очередей, больших двоичных объектов и базы данных приложения, когда оно работает в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="7ea15-180">При желании можно запускать приложение локально и далее, но можно делать это, используя облачные ресурсы хранилища и базы данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="7ea15-181">Все зависит только от задания строк подключения, что показано далее.</span><span class="sxs-lookup"><span data-stu-id="7ea15-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="7ea15-182">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-182">Deploy the application to Azure</span></span>
<span data-ttu-id="7ea15-183">Чтобы запустить приложение в облаке, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7ea15-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="7ea15-184">Создайте облачную службу Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="7ea15-185">Создайте базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="7ea15-186">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="7ea15-187">Настройте приложение для использования базы данных SQL Azure, когда оно работает в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="7ea15-188">Настройте приложение на использование вашей учетной записи хранения при запуске в Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="7ea15-189">Разверните проект в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="7ea15-190">Создание облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-190">Create an Azure cloud service</span></span>
<span data-ttu-id="7ea15-191">Облачная служба Azure — это среда, в которой запускают приложение.</span><span class="sxs-lookup"><span data-stu-id="7ea15-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="7ea15-192">В браузере откройте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ea15-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7ea15-193">Щелкните **Создать > Вычисления > Облачная служба**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="7ea15-194">В поле ввода DNS-имени введите префикс URL-адреса для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="7ea15-195">Этот URL-адрес должен быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="7ea15-195">This URL has to be unique.</span></span>  <span data-ttu-id="7ea15-196">Если выбранный префикс уже используется, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="7ea15-197">Укажите новую группу ресурсов для службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="7ea15-198">Щелкните **Создать**, а затем введите имя группы ресурсов в поле ввода, например CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="7ea15-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="7ea15-199">Задайте регион, в котором требуется развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="7ea15-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="7ea15-200">В этом поле указывается в каком центре обработки данных будет размещаться облачная служба.</span><span class="sxs-lookup"><span data-stu-id="7ea15-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="7ea15-201">В рабочем приложении следует выбрать регион, ближайший к заказчикам.</span><span class="sxs-lookup"><span data-stu-id="7ea15-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="7ea15-202">Выберите здесь ближайший к вам регион.</span><span class="sxs-lookup"><span data-stu-id="7ea15-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="7ea15-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-203">Click **Create**.</span></span>

    <span data-ttu-id="7ea15-204">На следующем рисунке показано, как создается облачная служба с использованием URL-адреса CSvccontosoads.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7ea15-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![Новая облачная служба](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="7ea15-206">Создание базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-206">Create an Azure SQL database</span></span>
<span data-ttu-id="7ea15-207">Когда приложение запускается в облаке, оно использует расположенную в облаке базу данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="7ea15-208">На [портале Azure](https://portal.azure.com) щелкните **Создать > Базы данных > База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-208">In the [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="7ea15-209">В поле **Имя базы данных** введите *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="7ea15-210">В разделе **Группа ресурсов** щелкните **Использовать существующий** и выберите группу ресурсов, используемую для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="7ea15-211">Щелкните **Сервер —Настроить обязательные параметры** и **Создать сервер**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Туннель к серверу базы данных](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="7ea15-213">Если в подписке уже есть сервер, можно выбрать его в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="7ea15-214">В поле **Имя сервера** введите *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="7ea15-215">Введите **имя для входа в систему** и **пароль администратора**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="7ea15-216">Если вы выбрали **Создать сервер**, не используйте имеющиеся имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7ea15-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="7ea15-217">Введите новые имя и пароль, которые в дальнейшем будут использоваться при обращении к базе данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="7ea15-218">Если выбран созданный ранее сервер, появится запрос на ввод пароля для ранее созданной административной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7ea15-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="7ea15-219">Выберите то же **расположение**, что и для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="7ea15-220">Когда облачная служба и база данных находятся в разных центрах обработки данных (различных регионах), увеличивается задержка и вам потребуется оплачивать пропускную способность за пределами центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="7ea15-221">Пропускная способность в рамках центра обработки данных предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="7ea15-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="7ea15-222">Проверьте **Разрешить службам Azure доступ к серверу**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="7ea15-223">Нажмите кнопку **Выбрать** для нового сервера.</span><span class="sxs-lookup"><span data-stu-id="7ea15-223">Click **Select** for the new server.</span></span>

    ![Новый сервер базы данных SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="7ea15-225">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="7ea15-226">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-226">Create an Azure storage account</span></span>
<span data-ttu-id="7ea15-227">Учетная запись хранилища Azure обеспечивает ресурсы для хранения данных очередей и больших двоичных объектов в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="7ea15-228">В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="7ea15-229">В этом руководстве будет использоваться одна учетная запись.</span><span class="sxs-lookup"><span data-stu-id="7ea15-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="7ea15-230">На [портале Azure](https://portal.azure.com) щелкните **Создать > Хранилище > Учетная запись хранения — большой двоичный объект, файл, таблица, очередь**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-230">In the [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="7ea15-231">В поле ввода **Имя** введите префикс URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7ea15-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="7ea15-232">Этот префикс в сочетании с текстом, который отображается под полем, будет уникальным URL-адресом для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="7ea15-233">Если введенный префикс уже использован где-либо, придется выбрать другой.</span><span class="sxs-lookup"><span data-stu-id="7ea15-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="7ea15-234">Задайте *классическую* **модель развертывания**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="7ea15-235">В раскрывающемся списке **Репликация** установите значение **Locally redundant storage** (Локально избыточное хранилище).</span><span class="sxs-lookup"><span data-stu-id="7ea15-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="7ea15-236">При включении георепликации для учетной записи хранения хранящиеся данные реплицируются в дополнительный центр обработки данных для обеспечения возможности отработки отказа в случае крупной аварии в основном расположении.</span><span class="sxs-lookup"><span data-stu-id="7ea15-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="7ea15-237">Георепликация может потребовать дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="7ea15-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="7ea15-238">Для учетных записей тестирования и разработки оплачивать георепликацию обычно не требуется.</span><span class="sxs-lookup"><span data-stu-id="7ea15-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="7ea15-239">Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="7ea15-240">В разделе **Группа ресурсов** щелкните **Использовать существующий** и выберите группу ресурсов, используемую для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="7ea15-241">В раскрывающемся списке **Расположение** выберите тот же регион, который выбрали для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="7ea15-242">Когда облачная служба и учетная запись хранения находятся в разных центрах обработки данных (различных областях), увеличивается задержка и вам потребуется оплачивать пропускную способность за пределами центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="7ea15-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="7ea15-243">Пропускная способность в рамках центра обработки данных предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="7ea15-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="7ea15-244">Территориальные группы Azure обеспечивают механизм для минимизации расстояния между ресурсами в центре обработки данных, что позволяет уменьшить задержку.</span><span class="sxs-lookup"><span data-stu-id="7ea15-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="7ea15-245">В этом учебнике территориальные группы не используются.</span><span class="sxs-lookup"><span data-stu-id="7ea15-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="7ea15-246">Дополнительные сведения см. в разделе о [создании территориальной группы в Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea15-246">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="7ea15-247">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-247">Click **Create**.</span></span>

    ![Новая учетная запись хранения](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="7ea15-249">На следующем рисунке показано создание учетной записи хранилища с URL-адресом `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="7ea15-250">Настройка приложения для использования базы данных SQL Azure, когда оно работает в облаке Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="7ea15-251">Веб-проект и проект рабочей роли имеют свои строки подключения к базе данных, и обе они должны указывать на базу данных SQL Azure, когда приложение работает в Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="7ea15-252">Мы используем [преобразование Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) для веб-роли и настройку среды облачной службы для рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea15-253">В этом и следующем разделах учетные данные будут сохранены в файлах проектов.</span><span class="sxs-lookup"><span data-stu-id="7ea15-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="7ea15-254">[Не сохраняйте важные данные в общедоступном репозитории исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="7ea15-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="7ea15-255">В проекте ContosoAdsWeb откройте файл преобразования *Web.Release.config* для файла приложения *Web.config*, удалите блок комментариев, содержащий элемент `<connectionStrings>`, и вставьте вместо него следующий код.</span><span class="sxs-lookup"><span data-stu-id="7ea15-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="7ea15-256">Оставьте файл открытым для редактирования.</span><span class="sxs-lookup"><span data-stu-id="7ea15-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="7ea15-257">На [портале Azure](https://portal.azure.com) в области слева щелкните **Базы данных SQL**, выберите базу данных, созданную для этого руководства, а затем щелкните **Показать строки подключения**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Показать строки подключения](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="7ea15-259">Портал выведет строки подключения со звездочками вместо пароля.</span><span class="sxs-lookup"><span data-stu-id="7ea15-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Строки подключения](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="7ea15-261">В файле преобразования *Web.Release.config* удалите `{connectionstring}` и вставьте на это место строку подключения ADO.NET с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="7ea15-262">В строке подключения, вставленной в файл преобразования *Web.Release.config*, замените `{your_password_here}` паролем, созданным для новой базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7ea15-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="7ea15-263">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="7ea15-263">Save the file.</span></span>  
6. <span data-ttu-id="7ea15-264">Выберите и скопируйте строку подключения (без знаков кавычек) для использования на следующих шагах настройки проекта с рабочей ролью.</span><span class="sxs-lookup"><span data-stu-id="7ea15-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="7ea15-265">В **обозревателе решений** в разделе **Роли** в проекте облачной службы щелкните правой кнопкой мыши пункт **ContosoAdsWorker** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="7ea15-267">Перейдите на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="7ea15-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="7ea15-268">В раскрывающемся списке **Конфигурация службы** выберите значение **Облако**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="7ea15-269">Выберите поле **Значение** для параметра `ContosoAdsDbConnectionString` и вставьте строку подключения, которую скопировали в предыдущем разделе руководства.</span><span class="sxs-lookup"><span data-stu-id="7ea15-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Строка подключения базы данных для рабочей роли](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="7ea15-271">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="7ea15-272">Настройка приложения для использования вашей учетной записи хранения при запуске в Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="7ea15-273">Строки подключения учетной записи хранения Azure для проектов рабочей роли и веб-роли сохраняются в настройках среды в проекте облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="7ea15-274">Для каждого проекта используется отдельный набор настроек, если приложение запущено локально или в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="7ea15-275">Следует обновить настройки облачной среды для проектов рабочей роли и веб-роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="7ea15-276">В **обозревателе решений** щелкните правой кнопкой мыши пункт **ContosoAdsWeb** в области **Роли** проекта **ContosoAdsCloudService**, а затем выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="7ea15-278">Перейдите на вкладку **Параметры** . В раскрывающемся списке **Конфигурация службы** выберите значение **Облако**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Конфигурация облака](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="7ea15-280">Выберите запись **StorageConnectionString**, и вы увидите кнопку с многоточием (**...**) в правом конце строки.</span><span class="sxs-lookup"><span data-stu-id="7ea15-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="7ea15-281">Нажмите эту кнопку с многоточием, чтобы открыть диалоговое окно **Создание строки подключения учетной записи хранения** .</span><span class="sxs-lookup"><span data-stu-id="7ea15-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Откройте окно создания строки подключения](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="7ea15-283">В диалоговом окне **Создание строки подключения к хранилищу** установите переключатель **Ваша подписка**, выберите учетную запись хранения, созданную ранее, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="7ea15-284">Если вы еще не вошли, появится запрос на ввод учетных данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Создайте строку подключения хранилища](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="7ea15-286">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-286">Save your changes.</span></span>
6. <span data-ttu-id="7ea15-287">Следуйте той же процедуре, которую использовали для строки подключения `StorageConnectionString`, чтобы задать строку подключения `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="7ea15-288">Эта строка подключения используется для журнала.</span><span class="sxs-lookup"><span data-stu-id="7ea15-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="7ea15-289">Выполните ту же процедуру, которую использовали для роли **ContosoAdsWeb**, чтобы задать строки подключения для роли **ContosoAdsWorker**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="7ea15-290">В раскрывающемся списке **Конфигурация службы** выберите значение **Облако**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="7ea15-291">Настройки среды роли, которые были заданы с использованием интерфейса Visual Studio, сохраняются в следующих файлах в проекте ContosoAdsCloudService:</span><span class="sxs-lookup"><span data-stu-id="7ea15-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="7ea15-292">*ServiceDefinition.csdef* - определяет имена настроек.</span><span class="sxs-lookup"><span data-stu-id="7ea15-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="7ea15-293">*ServiceConfiguration.Cloud.cscfg* - предоставляет значения для приложения при запуске в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="7ea15-294">*ServiceConfiguration.Cloud.cscfg* - предоставляет значения для приложения при локальном запуске.</span><span class="sxs-lookup"><span data-stu-id="7ea15-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="7ea15-295">Например, ServiceDefinition.csdef включает следующие определения:</span><span class="sxs-lookup"><span data-stu-id="7ea15-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="7ea15-296">Файл *ServiceConfiguration.Cloud.cscfg* включает значения, которые были введены для этих настроек в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7ea15-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="7ea15-297">Параметр `<Instances>` указывает число виртуальных машин, на которых Azure будет запускать код рабочий роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="7ea15-298">В раздел [Дальнейшие действия](#next-steps) включены ссылки на дополнительную информацию о горизонтальном масштабировании облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="7ea15-299">Развертывание проекта в Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="7ea15-300">В **обозревателе решений** щелкните правой кнопкой мыши проект **ContosoAdsCloudService** и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Меню публикации](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="7ea15-302">На шаге **Вход** мастера **публикации приложений Azure** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Этап входа](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="7ea15-304">На этапе **Настройки** мастера нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Этап настроек](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="7ea15-306">Заданные на вкладке **Дополнительно** значения по умолчанию подходят для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="7ea15-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="7ea15-307">Дополнительные сведения о вкладке "Дополнительно" см. в разделе о [мастере публикации приложения Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea15-307">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="7ea15-308">На этапе **Сводка** щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-308">In the **Summary** step, click **Publish**.</span></span>

    ![Сводка действий](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="7ea15-310">В Visual Studio открывается окно **Журнал действий Azure** .</span><span class="sxs-lookup"><span data-stu-id="7ea15-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="7ea15-311">Нажмите значок со стрелкой вправо, чтобы развернуть сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="7ea15-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="7ea15-312">Развертывание может занять около 5 минут и более.</span><span class="sxs-lookup"><span data-stu-id="7ea15-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Окно журнал действий Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="7ea15-314">После завершения развертывания щелкните **URL-адрес веб-приложения** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="7ea15-315">Теперь можно протестировать приложение, создавая, просматривая и редактируя некоторые элементы рекламы так же, как это происходило при локальном запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea15-316">После завершения тестирования удалите или остановите облачную службу.</span><span class="sxs-lookup"><span data-stu-id="7ea15-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="7ea15-317">Даже если облачная служба не используется, плата за нее начисляется, поскольку ресурсы виртуальной машины для нее зарезервированы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="7ea15-318">Если оставить ее работающей, любой кто найдет этот URL-адрес, сможет создать и просмотреть рекламу.</span><span class="sxs-lookup"><span data-stu-id="7ea15-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="7ea15-319">На [портале Azure](https://portal.azure.com) перейдите на вкладку **Обзор** для облачной службы, а затем в верхней части страницы щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="7ea15-320">Если необходимо временно предотвратить доступ посторонних к сайту, вместо этого щелкните **Остановить** .</span><span class="sxs-lookup"><span data-stu-id="7ea15-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="7ea15-321">В этом случае плата будет взиматься.</span><span class="sxs-lookup"><span data-stu-id="7ea15-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="7ea15-322">Можно повторить эту же процедуру для удаления базы данных SQL и учетной записи хранилища, если они больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="7ea15-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="7ea15-323">Создание приложения с нуля</span><span class="sxs-lookup"><span data-stu-id="7ea15-323">Create the application from scratch</span></span>
<span data-ttu-id="7ea15-324">Если [завершенное приложение](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)еще не загружено, сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="7ea15-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="7ea15-325">Скопируйте файлы из загруженного проекта в новый проект.</span><span class="sxs-lookup"><span data-stu-id="7ea15-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="7ea15-326">Создание приложения Contoso Ads состоит из следующих шагов:</span><span class="sxs-lookup"><span data-stu-id="7ea15-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="7ea15-327">Создайте новое решение облачной службы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ea15-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="7ea15-328">Обновите и добавьте пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ea15-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="7ea15-329">Указание ссылок на проекты.</span><span class="sxs-lookup"><span data-stu-id="7ea15-329">Set project references.</span></span>
* <span data-ttu-id="7ea15-330">Настройте строки подключения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-330">Configure connection strings.</span></span>
* <span data-ttu-id="7ea15-331">Добавьте файлы кода.</span><span class="sxs-lookup"><span data-stu-id="7ea15-331">Add code files.</span></span>

<span data-ttu-id="7ea15-332">После создания решения просмотрите код, уникальный для проектов облачных служб, больших двоичных объектов и очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="7ea15-333">Создайте новое решение облачной службы в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ea15-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="7ea15-334">В Visual Studio выберите **Новый проект** from the **Файл** .</span><span class="sxs-lookup"><span data-stu-id="7ea15-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="7ea15-335">В диалоговом окне **Создание проекта** в области слева разверните раздел **Visual C#**, выберите шаблоны **Облако** и шаблон **Облачная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="7ea15-336">Присвойте проекту имя ContosoAdsCloudService и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Новый проект](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="7ea15-338">В диалоговом окне **Новая облачная служба Azure** добавьте веб-роль и рабочую роль.</span><span class="sxs-lookup"><span data-stu-id="7ea15-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="7ea15-339">Присвойте веб-роли имя ContosoAdsWeb, а рабочей роли — ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7ea15-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="7ea15-340">(Используйте значок карандаша на правой панели для изменения имен ролей по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="7ea15-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![Проект новой облачной службы](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="7ea15-342">Когда появится диалоговое окно **Новый проект ASP.NET** для веб-роли, выберите шаблон MVC и щелкните **Изменить проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Изменить проверку подлинности](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="7ea15-344">В диалоговом окне **Изменение проверки подлинности** щелкните **Без проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Без аутентификации](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="7ea15-346">В диалоговом окне **Новый проект ASP.NET** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="7ea15-347">В **обозревателе решений** щелкните правой кнопкой мыши решение (не проект) и выберите **Добавить новый проект**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="7ea15-348">В диалоговом окне **Добавить новый проект** выберите **Windows** в разделе **Visual C#** на панели слева, а затем щелкните шаблон **Библиотека классов**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="7ea15-349">Присвойте проекту имя *ContosoAdsCommon*и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="7ea15-350">Необходимо сослаться на контекст и модель данных Entity Framework в обоих проектах — веб-роли и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="7ea15-351">Как вариант, можно определить связанные с EF классы в проекте веб-роли и сослаться на этот проект из проекта рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="7ea15-352">Но в случае альтернативного метода в проекте рабочей роли будет ссылка на веб-сборки, которые ему не нужны.</span><span class="sxs-lookup"><span data-stu-id="7ea15-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="7ea15-353">Обновите и добавьте пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="7ea15-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="7ea15-354">Откройте диалоговое окно **Управление пакетами NuGet** для решения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="7ea15-355">В верхней части окна выберите пункт **Обновления**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="7ea15-356">Найдите пакет *WindowsAzure.Storage* и, если он есть в списке, выберите его и выберите веб-проект и проект рабочей роли для обновления пакета в этих проектах, а затем нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="7ea15-357">Клиентская библиотека хранилища обновляется чаще, чем шаблоны проектов Visual Studio, поэтому часто происходит так, что версию во вновь создаваемых проектах необходимо обновить.</span><span class="sxs-lookup"><span data-stu-id="7ea15-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="7ea15-358">В верхней части окна выберите пункт **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="7ea15-359">Найдите пакет NuGet *EntityFramework* и установите его во все проекты.</span><span class="sxs-lookup"><span data-stu-id="7ea15-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="7ea15-360">Найдите пакет NuGet *Microsoft.WindowsAzure.ConfigurationManager* и установите его в проект рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="7ea15-361">Установите ссылки проекта</span><span class="sxs-lookup"><span data-stu-id="7ea15-361">Set project references</span></span>
1. <span data-ttu-id="7ea15-362">Задайте в проекте ContosoAdsWeb ссылку на проект ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="7ea15-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="7ea15-363">Щелкните правой кнопкой мыши проект ContosoAdsWeb и выберите пункты **Ссылки** - **Добавление ссылок**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="7ea15-364">В диалоговом окне **Диспетчер ссылок** выберите пункты **Решение — Проекты** на панели слева, щелкните **ContosoAdsCommon**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="7ea15-365">Задайте в проекте ContosoAdsWorker ссылку на проект ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="7ea15-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="7ea15-366">ContosoAdsCommon будет содержать модель данных и контекстный класс Entity Framework, который будет использован как фоновой, так и интерфейсной службой.</span><span class="sxs-lookup"><span data-stu-id="7ea15-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="7ea15-367">Задайте в проекте ContosoAdsWorker ссылку на `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="7ea15-368">Сборка используется внутренней службой для преобразования изображений в эскизы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="7ea15-369">Настройте строки подключения</span><span class="sxs-lookup"><span data-stu-id="7ea15-369">Configure connection strings</span></span>
<span data-ttu-id="7ea15-370">В этом разделе настройте хранилище Azure и строки подключения SQL для локального тестирования.</span><span class="sxs-lookup"><span data-stu-id="7ea15-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="7ea15-371">Инструкции по развертыванию ранее в этом руководстве объясняют, как установить строки подключения в случае, когда приложение работает в облаке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="7ea15-372">В проекте ContosoAdsWeb откройте файл приложения Web.config и вставьте следующий элемент `connectionStrings` после элемента `configSections`:</span><span class="sxs-lookup"><span data-stu-id="7ea15-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="7ea15-373">Если вы используете Visual Studio 2015 или более поздней версии, замените v11.0 на MSSQLLocalDB.</span><span class="sxs-lookup"><span data-stu-id="7ea15-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="7ea15-374">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-374">Save your changes.</span></span>
3. <span data-ttu-id="7ea15-375">В проекте ContosoAdsCloudService щелкните правой кнопкой мыши ContosoAdsWeb в разделе **Роли**, а затем выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="7ea15-377">В окне свойств **ContosAdsWeb [роль]** щелкните вкладку **Настройки** и затем щелкните **Добавить настройку**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="7ea15-378">В раскрывающемся списке **Конфигурация службы** выберите значение **Все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="7ea15-379">Добавьте настройку с именем *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="7ea15-380">Задайте для параметра **Тип** значение *ConnectionString*, а для параметра **Значение** — *UseDevelopmentStorage=true*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![Новая строка подключения](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="7ea15-382">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-382">Save your changes.</span></span>
7. <span data-ttu-id="7ea15-383">Следуйте этой же процедуре для добавления строки подключения хранилища в свойства роли ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7ea15-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="7ea15-384">Там же в окне свойств **ContosoAdsWorker [роль]** добавьте другую строку подключения:</span><span class="sxs-lookup"><span data-stu-id="7ea15-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="7ea15-385">Имя: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="7ea15-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="7ea15-386">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="7ea15-386">Type: String</span></span>
   * <span data-ttu-id="7ea15-387">Значение. Вставьте ту же строку подключения, которая была использована для проекта веб-роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="7ea15-388">(Этот пример предназначен для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7ea15-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="7ea15-389">Не забудьте изменить источник данных при копировании этого примера для Visual Studio 2015 или более поздней версии.)</span><span class="sxs-lookup"><span data-stu-id="7ea15-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="7ea15-390">Добавьте файлы кода</span><span class="sxs-lookup"><span data-stu-id="7ea15-390">Add code files</span></span>
<span data-ttu-id="7ea15-391">В этом разделе скопируйте файлы кода из скачанного решения в новое решение.</span><span class="sxs-lookup"><span data-stu-id="7ea15-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="7ea15-392">Следующие разделы покажут и объяснят важные части этого кода.</span><span class="sxs-lookup"><span data-stu-id="7ea15-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="7ea15-393">Чтобы добавить файлы в проект или папку, щелкните правой кнопкой мыши проект или папку и щелкните **Добавить** - **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="7ea15-394">Выберите необходимые файлы и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="7ea15-395">При запросе о том, заменять ли существующие файлы, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="7ea15-396">В проекте ContosoAdsCommon удалите файл *Class1.cs* и добавьте на его место файлы *Ad.cs* и *ContosoAdscontext.cs* из скачанного проекта.</span><span class="sxs-lookup"><span data-stu-id="7ea15-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="7ea15-397">В проекте ContosoAdsCommon добавьте следующие файлы из загруженного проекта.</span><span class="sxs-lookup"><span data-stu-id="7ea15-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="7ea15-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="7ea15-399">В папку *Views\Shared*: файл *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="7ea15-400">В папку *Views\Home*: файл *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="7ea15-401">В папку *Controllers*: файл *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="7ea15-402">В папку *Views\Ad* (сначала создайте эту папку): пять файлов *CSHTML*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="7ea15-403">В проекте ContosoAdsCommon добавьте *WorkerRole.cs* из загруженного проекта.</span><span class="sxs-lookup"><span data-stu-id="7ea15-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="7ea15-404">Теперь можно создать и запустить приложение, как описывали инструкции ранее в этом руководстве, и приложение будет использовать локальные ресурсы эмуляторов базы данных и хранилища.</span><span class="sxs-lookup"><span data-stu-id="7ea15-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="7ea15-405">В следующих разделах объясняется код, связанный с работой среды Azure, больших двоичных объектов и очередей.</span><span class="sxs-lookup"><span data-stu-id="7ea15-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="7ea15-406">В этом учебнике не представлены следующие пошаговые инструкции: "Создание контроллеров и представлений MVC с помощью формирования шаблонов", "Запись кода Entity Framework, который работает с базами данных SQL Server" или "Основы асинхронного программирования в ASP.NET 4.5".</span><span class="sxs-lookup"><span data-stu-id="7ea15-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="7ea15-407">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7ea15-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="7ea15-408">Начало работы с MVC 5</span><span class="sxs-lookup"><span data-stu-id="7ea15-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="7ea15-409">Начало работы с EF 6 и MVC 5</span><span class="sxs-lookup"><span data-stu-id="7ea15-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="7ea15-410">[Введение в асинхронное программирование в .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)</span><span class="sxs-lookup"><span data-stu-id="7ea15-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="7ea15-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="7ea15-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="7ea15-412">Файл Ad.cs определяет перечисляемый тип для класса Ad и класс сущностей POCO для информации в рекламе.</span><span class="sxs-lookup"><span data-stu-id="7ea15-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="7ea15-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="7ea15-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="7ea15-414">Класс ContosoAdsContext указывает, что класс Ad используется коллекцией DbSet, которую Entity Framework хранит в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7ea15-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="7ea15-415">Класс имеет два конструктора.</span><span class="sxs-lookup"><span data-stu-id="7ea15-415">The class has two constructors.</span></span> <span data-ttu-id="7ea15-416">Первый из них используется веб-проектом и указывает имя строки подключения, которая сохранена в файле Web.config</span><span class="sxs-lookup"><span data-stu-id="7ea15-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="7ea15-417">Второй конструктор дает возможность передачи действующей строки подключения, которая используется проектом рабочей роли, так как она не имеет файла Web.config.</span><span class="sxs-lookup"><span data-stu-id="7ea15-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="7ea15-418">Ранее было показано, где хранится строка подключения, а потом будет показано, как код извлекает строку подключения, когда он создает экземпляр класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="7ea15-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="7ea15-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="7ea15-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="7ea15-420">Код, который вызывается из метода `Application_Start`, создает контейнер больших двоичных объектов *images* и очередь *images*, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="7ea15-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="7ea15-421">Это гарантирует, что при начале использования новой учетной записи хранения или эмулятора хранилища на новом компьютере требуемый контейнер больших двоичных объектов и очередь создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="7ea15-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="7ea15-422">Код получает доступ к учетной записи хранилища, используя строку подключения из файла *.cscfg* .</span><span class="sxs-lookup"><span data-stu-id="7ea15-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="7ea15-423">Затем он получает ссылку на контейнер больших двоичных объектов *images* , создает контейнер, если он еще не существует, и устанавливает разрешения доступа к новому контейнеру.</span><span class="sxs-lookup"><span data-stu-id="7ea15-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="7ea15-424">По умолчанию новые контейнеры разрешают доступ к большим двоичным объектам только клиентам с данными учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="7ea15-425">Веб-сайту требуются общедоступные большие двоичные объекты, чтобы он мог выводить изображения с использованием URL-адресов, которые указывают на объекты изображений.</span><span class="sxs-lookup"><span data-stu-id="7ea15-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="7ea15-426">Аналогичный код получает ссылку на очередь *images* и создает новую очередь.</span><span class="sxs-lookup"><span data-stu-id="7ea15-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="7ea15-427">В этом случае изменения разрешений не требуется.</span><span class="sxs-lookup"><span data-stu-id="7ea15-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="7ea15-428">ContosoAdsWeb — \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="7ea15-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="7ea15-429">Файл *_Layout.cshtml* задает имя приложения в заголовке и нижнем колонтитуле и создает запись меню "Ads".</span><span class="sxs-lookup"><span data-stu-id="7ea15-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="7ea15-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="7ea15-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="7ea15-431">Файл *Views\Home\Index.cshtml* выводит ссылки категорий на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="7ea15-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="7ea15-432">Ссылки передают целочисленное значение перечисляемого типа `Category` в переменную querystring на странице индекса Ads.</span><span class="sxs-lookup"><span data-stu-id="7ea15-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="7ea15-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="7ea15-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="7ea15-434">В файле *AdController.cs* конструктор вызывает метод `InitializeStorage` для создания объектов клиентской библиотеки службы хранилища Azure, которые предоставляют API-интерфейс для работы с большими двоичными объектами и очередями.</span><span class="sxs-lookup"><span data-stu-id="7ea15-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="7ea15-435">Затем код получает ссылку на контейнер больших двоичных объектов *images*, как показано ранее в *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ea15-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="7ea15-436">При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="7ea15-437">Политика повторения с экспоненциальной задержкой по умолчанию может застопорить веб-приложение более чем на минуту при повторяющихся повторах во время кратковременного сбоя.</span><span class="sxs-lookup"><span data-stu-id="7ea15-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="7ea15-438">Политика повторения здесь указывает ожидание в три секунды после каждой попытки, всего до трех повторений.</span><span class="sxs-lookup"><span data-stu-id="7ea15-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="7ea15-439">Аналогичный код получает ссылку на очередь *images* .</span><span class="sxs-lookup"><span data-stu-id="7ea15-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="7ea15-440">Большая часть кода контроллера обычна для работы с моделью данных Entity Framework с использованием класса DbContext.</span><span class="sxs-lookup"><span data-stu-id="7ea15-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="7ea15-441">Исключением является метод `Create` HttpPost, который отправляет файл и сохраняет его в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="7ea15-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="7ea15-442">Связыватель модели предоставляет объект [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) для метода.</span><span class="sxs-lookup"><span data-stu-id="7ea15-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="7ea15-443">При выбора файла для отправки код отправляет его, сохраняет его в большом двоичном объекте и обновляет запись базы данных URL-адресом, который указывает на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="7ea15-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="7ea15-444">Код отправки содержится в методе `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="7ea15-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="7ea15-445">Он создает имя GUID для большого двоичного объекта, отправляет и сохраняет файл, а также возвращает ссылку на сохраненный большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="7ea15-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="7ea15-446">После того как метод HttpPost `Create` загружает большой двоичный объект и обновляет базу данных, он создает сообщение очереди для информирования фонового процесса о том, что изображение готово для преобразования в эскиз.</span><span class="sxs-lookup"><span data-stu-id="7ea15-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="7ea15-447">Код для метода HttpPost `Edit` аналогичен, за одним исключением — если пользователь выбирает новый файл изображения, все существующие большие двоичные объекты должны быть удалены.</span><span class="sxs-lookup"><span data-stu-id="7ea15-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="7ea15-448">Ниже представлен пример кода, который удаляет большие двоичные объекты при удалении элемента рекламы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="7ea15-449">ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="7ea15-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="7ea15-450">Файл *Index.cshtml* выводит эскиз с другими данными рекламы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="7ea15-451">Файл *Details.cshtml* выводит изображение в полном размере.</span><span class="sxs-lookup"><span data-stu-id="7ea15-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="7ea15-452">ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="7ea15-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="7ea15-453">Файлы *Create.cshtml* и *Edit.cshtml* указывают кодирование формы, которое дает возможность контроллеру получить объект `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="7ea15-454">Элемент `<input>` сообщает браузеру, что нужно открыть диалоговое окно выбора файла.</span><span class="sxs-lookup"><span data-stu-id="7ea15-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="7ea15-455">ContosoAdsWorker - WorkerRole.cs - метод OnStart</span><span class="sxs-lookup"><span data-stu-id="7ea15-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="7ea15-456">Среда рабочей роли Azure вызывает метод `OnStart` в классе `WorkerRole`, когда рабочая роль начинает работу, и вызывает метод `Run`, когда метод `OnStart` завершает работу.</span><span class="sxs-lookup"><span data-stu-id="7ea15-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="7ea15-457">Метод `OnStart` получает строку подключения к базе данных из *CSCFG-файла* и передает ее в класс Entity Framework DbContext.</span><span class="sxs-lookup"><span data-stu-id="7ea15-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="7ea15-458">Поставщик SQLClient используется по умолчанию, поэтому поставщик не нужно указывать.</span><span class="sxs-lookup"><span data-stu-id="7ea15-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="7ea15-459">Затем метод получит ссылку на учетную запись хранилища и создаст контейнер больших двоичных объектов и очередь, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="7ea15-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="7ea15-460">Этот код аналогичен тому, что показан в методе `Application_Start` веб-роли.</span><span class="sxs-lookup"><span data-stu-id="7ea15-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="7ea15-461">ContosoAdsWorker - WorkerRole.cs - метод Run</span><span class="sxs-lookup"><span data-stu-id="7ea15-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="7ea15-462">Метод `Run` вызывается, когда метод `OnStart` завершает свою начальную работу.</span><span class="sxs-lookup"><span data-stu-id="7ea15-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="7ea15-463">Метод выполняет бесконечный цикл, в котором ждет новые сообщения в очереди и обрабатывает их, когда они прибывают.</span><span class="sxs-lookup"><span data-stu-id="7ea15-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="7ea15-464">После каждой итерации цикла, если сообщение найдено в очереди, программа останавливается на секунду.</span><span class="sxs-lookup"><span data-stu-id="7ea15-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="7ea15-465">Это защищает рабочую роль от создания ненужных затрат при использовании времени процессора и транзакций в хранилище.</span><span class="sxs-lookup"><span data-stu-id="7ea15-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="7ea15-466">Команда Microsoft Customer Advisory рассказывала о разработчике, который забыл включить этот функционал, развернул код в рабочей среде и ушел в отпуск.</span><span class="sxs-lookup"><span data-stu-id="7ea15-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="7ea15-467">Когда он вернулся, то выяснил, что забывчивость встала ему в копеечку.</span><span class="sxs-lookup"><span data-stu-id="7ea15-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="7ea15-468">Иногда содержимое сообщения очереди вызывает ошибку при обработке.</span><span class="sxs-lookup"><span data-stu-id="7ea15-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="7ea15-469">Это *ядовитое сообщение* — если ошибка только протоколируется и цикл будет перезапущен, то сообщение можно обрабатывать бесконечно.</span><span class="sxs-lookup"><span data-stu-id="7ea15-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="7ea15-470">Поэтому блок catch включает правило if, которое проверяет, сколько раз приложение пыталось обработать текущее сообщение. Если уже насчитано 5 раз, сообщение удаляется из очереди.</span><span class="sxs-lookup"><span data-stu-id="7ea15-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="7ea15-471">`ProcessQueueMessage` вызывается, когда сообщение найдено в очереди.</span><span class="sxs-lookup"><span data-stu-id="7ea15-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="7ea15-472">Код читает базу данных для получения URL-адреса изображения, конвертирует изображение в эскиз, сохраняет эскиз в большой двоичный объект, добавляет в базу данных URL-адрес большого двоичного объекта эскиза и удаляет сообщение из очереди.</span><span class="sxs-lookup"><span data-stu-id="7ea15-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea15-473">Для простоты код в методе `ConvertImageToThumbnailJPG` использует классы в пространстве имен System.Drawing.</span><span class="sxs-lookup"><span data-stu-id="7ea15-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="7ea15-474">Однако классы в этом пространстве имен были спроектированы для использования с формами Windows.</span><span class="sxs-lookup"><span data-stu-id="7ea15-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="7ea15-475">Они не поддерживаются в службе Windows или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7ea15-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="7ea15-476">Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация, IHttpHandlers и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования образов с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).</span><span class="sxs-lookup"><span data-stu-id="7ea15-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="7ea15-477">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7ea15-477">Troubleshooting</span></span>
<span data-ttu-id="7ea15-478">У вас что-то не работает, когда вы выполняете инструкции из этого руководства? Вот несколько общих ошибок и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="7ea15-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="7ea15-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="7ea15-480">Объект `RoleEnvironment` предоставляется Azure, когда приложение запущено в Azure или локально с использованием эмулятора вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="7ea15-481">Если сообщение об этой ошибке появляется при локальном выполнении, убедитесь, что проект ContosoAdsCloudService установлен как начальный.</span><span class="sxs-lookup"><span data-stu-id="7ea15-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="7ea15-482">Это настраивает проект для запуска с использованием эмулятора вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="7ea15-483">Одной из причин, по которым приложение использует RoleEnvironment в Azure, — это получение значений строки подключения, которые что они хранятся в файлах *.cscfg* , поэтому другой причиной этого исключения является отсутствие строки подключения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="7ea15-484">Убедитесь, что настройка StorageConnectionString создана для вариантов "Облако" и "Локально" в проекте ContosoAdsWeb, и что созданы обе строки подключения для обоих вариантов в проекте ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7ea15-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="7ea15-485">Выполните поиск **Найти все** по StorageConnectionString во всем решении; запись должна появиться 9 раз в 6 файлах.</span><span class="sxs-lookup"><span data-stu-id="7ea15-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="7ea15-486">Невозможно переопределить на порт ххх.</span><span class="sxs-lookup"><span data-stu-id="7ea15-486">Cannot override to port xxx.</span></span> <span data-ttu-id="7ea15-487">Новый порт ниже минимально разрешенного значения 8080 для протокола http</span><span class="sxs-lookup"><span data-stu-id="7ea15-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="7ea15-488">Попробуйте изменить номер порта, используемый веб-проектом.</span><span class="sxs-lookup"><span data-stu-id="7ea15-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="7ea15-489">Щелкните правой кнопкой мыши проект ContosoAdsWeb и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="7ea15-490">Щелкните вкладку **Веб** и измените номер порта в параметре **URL-адрес проекта**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="7ea15-491">Другим вариантом может быть решение в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="7ea15-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="7ea15-492">Другие ошибки при работе локально</span><span class="sxs-lookup"><span data-stu-id="7ea15-492">Other errors when running locally</span></span>
<span data-ttu-id="7ea15-493">По умолчанию новые проекты облачной службы используют облегченный эмулятор вычислений Azure для имитации среды Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="7ea15-494">Это облегченная версия полнофункционального эмулятора вычислений; при некоторых условиях полнофункциональный эмулятор будет работать, а облегченный — нет.</span><span class="sxs-lookup"><span data-stu-id="7ea15-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="7ea15-495">Для переключения проекта на использование полнофункционального эмулятора щелкните правой кнопкой мыши проект ContosoAdsCloudService и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="7ea15-496">В окне **Свойства** щелкните вкладку **Веб**, а затем установите переключатель **Использовать полный эмулятор**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="7ea15-497">Для запуска приложения с полным эмулятором следует открыть Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7ea15-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea15-498">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ea15-498">Next steps</span></span>
<span data-ttu-id="7ea15-499">Приложение Contoso Ads намеренно сделано простым для руководства по началу работы.</span><span class="sxs-lookup"><span data-stu-id="7ea15-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="7ea15-500">Например, оно не реализует [вставку зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) или [репозиторий и блок рабочих шаблонов](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), не использует [интерфейс для журналов](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), не использует [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) для управления изменениями модели данных или [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) для управления кратковременными ошибками сети и т. д.</span><span class="sxs-lookup"><span data-stu-id="7ea15-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="7ea15-501">Есть несколько примеров приложений облачной службы, которые демонстрируют более жизненные примеры кодирования — от менее сложных к более сложным:</span><span class="sxs-lookup"><span data-stu-id="7ea15-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="7ea15-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="7ea15-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="7ea15-503">Похоже на Contoso Ads, но реализует больше функций и больше примеров реального кода.</span><span class="sxs-lookup"><span data-stu-id="7ea15-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="7ea15-504">[Многоуровневое облачное приложение Azure с таблицами, квотами, и большими двоичными объектами](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="7ea15-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="7ea15-505">Представляет таблицы, а также большие двоичные объекты и очереди службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="7ea15-506">Этот пример основан на более старой версии пакета SDK для Azure для .NET, поэтому для работы с текущей версией потребуются некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="7ea15-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="7ea15-507">[Основы облачных служб в Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="7ea15-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="7ea15-508">Полный пример для демонстрации широкого набора приемов, применяемых группой Microsoft Patterns and Practices.</span><span class="sxs-lookup"><span data-stu-id="7ea15-508">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="7ea15-509">Общую информацию об облачной разработке см. в статье о [создании реальных облачных приложений в Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="7ea15-509">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="7ea15-510">Видеоинструкции по рекомендациям для службы хранилища Azure см. в разделе [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628) (Хранилище Microsoft — новости, рекомендации и шаблоны).</span><span class="sxs-lookup"><span data-stu-id="7ea15-510">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="7ea15-511">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7ea15-511">For more information, see the following resources:</span></span>

* [<span data-ttu-id="7ea15-512">Облачные службы Azure, часть 1: Введение</span><span class="sxs-lookup"><span data-stu-id="7ea15-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="7ea15-513">Управление облачными службами</span><span class="sxs-lookup"><span data-stu-id="7ea15-513">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="7ea15-514">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="7ea15-515">Как выбрать поставщика облачных служб</span><span class="sxs-lookup"><span data-stu-id="7ea15-515">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
