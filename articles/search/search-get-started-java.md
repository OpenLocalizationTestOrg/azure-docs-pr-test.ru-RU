---
title: "aaaGet работы с поиском Azure в Java | Документы Microsoft"
description: "Как toobuild размещенного облака поиск приложения в Azure, используя в качестве языка программирования Java."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="db2e0-103">Начало работы с Поиском Azure в Java</span><span class="sxs-lookup"><span data-stu-id="db2e0-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db2e0-104">Портал</span><span class="sxs-lookup"><span data-stu-id="db2e0-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="db2e0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="db2e0-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="db2e0-106">Узнайте, как toobuild пользовательские Java поиск приложения, использующего поиска Azure для его результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="db2e0-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="db2e0-107">В этом учебнике используется hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello объекты и операции, используемые в этом упражнении.</span><span class="sxs-lookup"><span data-stu-id="db2e0-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="db2e0-108">toorun в этом примере необходимо иметь службы поиска Azure, который можно выполнить вход для hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db2e0-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="db2e0-109">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) пошаговые инструкции.</span><span class="sxs-lookup"><span data-stu-id="db2e0-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="db2e0-110">Мы используются следующие toobuild программного обеспечения hello и тестирования в этом примере:</span><span class="sxs-lookup"><span data-stu-id="db2e0-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="db2e0-111">[Интегрированная среда разработки Eclipse для разработчиков Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="db2e0-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="db2e0-112">Быть убедиться, что версия EE hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="db2e0-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="db2e0-113">Один из шагов проверки hello требует функцию, которая находится только в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="db2e0-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="db2e0-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="db2e0-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="db2e0-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="db2e0-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="db2e0-116">О данных hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-116">About hello data</span></span>
<span data-ttu-id="db2e0-117">В этом примере приложение использует данные из hello [США геологическое службы (универсальные группы безопасности)](http://geonames.usgs.gov/domestic/download_data.htm)фильтрацией на размер набора данных hello tooreduce состояние из Род-Айленд hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="db2e0-118">Мы будем использовать этот toobuild данных поиска приложения, которое возвращает ориентиров здания, например больницы школы, а также геологическое таких компонентов, как потоки, Озера и конференции.</span><span class="sxs-lookup"><span data-stu-id="db2e0-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="db2e0-119">В этом приложении hello **SearchServlet.java** программа создает и загружает hello индекса с помощью [индексатора](https://msdn.microsoft.com/library/azure/dn798918.aspx) конструкции, получение hello фильтрация набора данных универсальные группы безопасности из общей базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="db2e0-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="db2e0-120">Предопределенных учетных данных и источник данных в сети toohello подключения сведения предоставляются в программном коде hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="db2e0-121">С точки зрения доступа к данным дальнейшая настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="db2e0-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="db2e0-122">Мы применен фильтр на этот набор данных toostay под hello 10 000 документов ограничение hello бесплатной ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="db2e0-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="db2e0-123">При использовании стандартного уровня hello, это ограничение не применяется, и вы можете изменить этот код toouse большего набора данных.</span><span class="sxs-lookup"><span data-stu-id="db2e0-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="db2e0-124">Подробнее об ограничениях каждой ценовой категории см. в разделе [Ограничения](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="db2e0-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="db2e0-125">Сведения о файлах программы hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-125">About hello program files</span></span>
<span data-ttu-id="db2e0-126">Hello следующий список содержит описание hello файлов, соответствующих toothis выборку.</span><span class="sxs-lookup"><span data-stu-id="db2e0-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="db2e0-127">Search.JSP: Предоставляет пользовательский интерфейс hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="db2e0-128">SearchServlet.java: Методы (аналогичный контроллер tooa в MVC) предоставляет</span><span class="sxs-lookup"><span data-stu-id="db2e0-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="db2e0-129">SearchServiceClient.java: обрабатывает HTTP-запросы</span><span class="sxs-lookup"><span data-stu-id="db2e0-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="db2e0-130">SearchServiceHelper.java: вспомогательный класс, предоставляющий статические методы</span><span class="sxs-lookup"><span data-stu-id="db2e0-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="db2e0-131">Document.Java: Модель данных hello предоставляет</span><span class="sxs-lookup"><span data-stu-id="db2e0-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="db2e0-132">config.Properties: задает URL-адрес службы поиска hello и ключ api</span><span class="sxs-lookup"><span data-stu-id="db2e0-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="db2e0-133">Pom.xml: зависимость Maven</span><span class="sxs-lookup"><span data-stu-id="db2e0-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="db2e0-134">Найти имя службы hello и ключ api службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="db2e0-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="db2e0-135">Все вызовы REST API службы поиска Azure требуется ввести URL-адрес службы hello и ключ api.</span><span class="sxs-lookup"><span data-stu-id="db2e0-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="db2e0-136">Войдите в toohello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db2e0-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="db2e0-137">В панели переходов hello, щелкните **службы поиска** toolist всех служб поиска Azure hello подготовлены для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="db2e0-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="db2e0-138">Выберите службу hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="db2e0-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="db2e0-139">На панели мониторинга службы hello вы увидите плитки основные сведения, а также значок ключа hello для доступа к ключи администратора hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="db2e0-140">Скопируйте URL-адрес службы hello и ключа администратора.</span><span class="sxs-lookup"><span data-stu-id="db2e0-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="db2e0-141">Они потребуются позже, при добавлении их toohello **config.properties** файла.</span><span class="sxs-lookup"><span data-stu-id="db2e0-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="db2e0-142">Загрузка файлов образца hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-142">Download hello sample files</span></span>
1. <span data-ttu-id="db2e0-143">Go слишком[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="db2e0-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="db2e0-144">Нажмите кнопку **загрузить ZIP**сохранить toodisk файла .zip hello и затем извлечь все файлы в ней hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="db2e0-145">Рассмотрите возможность извлечения hello файлов в рабочей области на Java toomake проще проекта toofind hello позже.</span><span class="sxs-lookup"><span data-stu-id="db2e0-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="db2e0-146">файлы образца Hello доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="db2e0-146">hello sample files are read-only.</span></span> <span data-ttu-id="db2e0-147">Щелкните правой кнопкой мыши папку свойств и hello снимите атрибут только для чтения.</span><span class="sxs-lookup"><span data-stu-id="db2e0-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="db2e0-148">Все последующие изменения и операторы выполнения будут применяться к файлам в этой папке.</span><span class="sxs-lookup"><span data-stu-id="db2e0-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="db2e0-149">Импорт проекта</span><span class="sxs-lookup"><span data-stu-id="db2e0-149">Import project</span></span>
1. <span data-ttu-id="db2e0-150">В Eclipse выберите **Файл** > **Импорт** > **Общие** > **Existing Projects into Workspace** (Существующие проекты в рабочую область).</span><span class="sxs-lookup"><span data-stu-id="db2e0-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="db2e0-151">В **выберите корневой каталог**, Обзор toohello папка, содержащая файлы примеров.</span><span class="sxs-lookup"><span data-stu-id="db2e0-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="db2e0-152">Выберите папку hello, содержащая hello папку проекта.</span><span class="sxs-lookup"><span data-stu-id="db2e0-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="db2e0-153">Hello проекта должны появиться в hello **проекты** список с выбранным элементом.</span><span class="sxs-lookup"><span data-stu-id="db2e0-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="db2e0-154">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="db2e0-154">Click **Finish**.</span></span>
4. <span data-ttu-id="db2e0-155">Используйте **обозревателя проектов** tooview и редактирования файлов hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="db2e0-156">Если он не открыт, нажмите кнопку **окна** > **Показать представление** > **обозревателя проектов** или используйте контекстное tooopen hello его.</span><span class="sxs-lookup"><span data-stu-id="db2e0-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="db2e0-157">Настройка URL-адрес службы hello и ключ api</span><span class="sxs-lookup"><span data-stu-id="db2e0-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="db2e0-158">В **обозревателя проектов**, дважды щелкните **config.properties** параметры конфигурации tooedit hello, содержащего имя сервера hello и ключ api.</span><span class="sxs-lookup"><span data-stu-id="db2e0-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="db2e0-159">См. шаги toohello ранее в этой статье, где найти URL-адрес службы hello и ключ api в hello [портала Azure](https://portal.azure.com), tooget значения hello, теперь войдет в **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="db2e0-160">В **config.properties**, замените hello ключ api для службы «Api-ключ».</span><span class="sxs-lookup"><span data-stu-id="db2e0-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="db2e0-161">Затем имя службы (hello первый компонент http://servicename.search.windows.net hello URL-адрес) заменяет «имя службы» в hello того же файла.</span><span class="sxs-lookup"><span data-stu-id="db2e0-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="db2e0-162">Настройка сред hello проекта, построения и выполнения</span><span class="sxs-lookup"><span data-stu-id="db2e0-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="db2e0-163">В обозревателе проектов Eclipse щелкните правой кнопкой мыши проект hello > **свойства** > **аспекты проекта**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="db2e0-164">Выберите **Dynamic Web Module** (Динамический веб-модуль), **Java** и **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="db2e0-165">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-165">Click **Apply**.</span></span>
4. <span data-ttu-id="db2e0-166">Выберите **Окно** > **Параметры** > **Сервер** > **Runtime Environments** (Среды выполнения) > **Добавить...**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="db2e0-167">Разверните Apache и выберите ранее установленный сервер Apache Tomcat hello версии hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="db2e0-168">В нашей системе мы установили версию 8.</span><span class="sxs-lookup"><span data-stu-id="db2e0-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="db2e0-169">На следующей странице hello укажите каталог установки Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="db2e0-170">На компьютере под управлением Windows это, скорее всего, будет C:\Program Files\Apache Software Foundation\Tomcat *версия*.</span><span class="sxs-lookup"><span data-stu-id="db2e0-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="db2e0-171">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="db2e0-171">Click **Finish**.</span></span>
8. <span data-ttu-id="db2e0-172">Выберите **Окно** > **Параметры** > **Java** > **Installed JREs** (Установленные JRE) > **Добавить...**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="db2e0-173">В окне **Add JRE** (Добавить JRE) выберите **Standard VM** (Стандартная виртуальная машина).</span><span class="sxs-lookup"><span data-stu-id="db2e0-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="db2e0-174">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-174">Click **Next**.</span></span>
11. <span data-ttu-id="db2e0-175">В разделе "Определение JRE" в главном окне выберите **Каталог**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="db2e0-176">Перейдите в слишком**Program Files** > **Java** и выберите hello JDK, ранее была установлена.</span><span class="sxs-lookup"><span data-stu-id="db2e0-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="db2e0-177">Это важные tooselect hello JDK как hello JRE.</span><span class="sxs-lookup"><span data-stu-id="db2e0-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="db2e0-178">В JREs установлены, выберите hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="db2e0-179">Параметры должны выглядеть примерно toohello следующий снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="db2e0-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="db2e0-180">При необходимости установите **окна** > **веб-браузер** > **Internet Explorer** tooopen приложения hello в окне внешнем браузере.</span><span class="sxs-lookup"><span data-stu-id="db2e0-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="db2e0-181">Использование внешнего браузера обеспечивает лучшую работу веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="db2e0-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="db2e0-182">Задачи настройки hello завершена.</span><span class="sxs-lookup"><span data-stu-id="db2e0-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="db2e0-183">Далее предстоит Постройте и запустите проект hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="db2e0-184">Построение проекта hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-184">Build hello project</span></span>
1. <span data-ttu-id="db2e0-185">В обозревателе решений, щелкните правой кнопкой мыши имя проекта hello и выберите **запуска от имени** > **Maven сборки...**  tooconfigure hello проекта.</span><span class="sxs-lookup"><span data-stu-id="db2e0-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="db2e0-186">В разделе "Изменить конфигурацию" в поле "Цели" введите "чистая установка" и нажмите **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="db2e0-187">Сообщения о состоянии, окно консоли toohello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="db2e0-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="db2e0-188">Вы увидите УСПЕШНОСТИ ПОСТРОЕНИЯ проекта является признаком того, hello построен без ошибок.</span><span class="sxs-lookup"><span data-stu-id="db2e0-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="db2e0-189">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="db2e0-189">Run hello app</span></span>
<span data-ttu-id="db2e0-190">В этом последнем шаге будет выполняться приложение hello в среде выполнения локального сервера.</span><span class="sxs-lookup"><span data-stu-id="db2e0-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="db2e0-191">Если среде выполнения сервера еще не указаны в Eclipse, вам потребуется toodo сначала.</span><span class="sxs-lookup"><span data-stu-id="db2e0-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="db2e0-192">В обозревателе проектов разверните **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="db2e0-193">Щелкните правой кнопкой мыши **Search.jsp** > **Запуск от имени** > **Запустить на сервере**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="db2e0-194">Выберите сервер Apache Tomcat hello и нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="db2e0-195">Если вы использовали toostore рабочей области не по умолчанию проекта, вам потребуется toomodify **Настройка запуска** toopoint toohello проекта расположение tooavoid ошибку при запуске сервера.</span><span class="sxs-lookup"><span data-stu-id="db2e0-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="db2e0-196">В обозревателе проектов щелкните правой кнопкой мыши **Search.jsp** > **Запуск от имени** > **Run Configurations** (Конфигурации запуска).</span><span class="sxs-lookup"><span data-stu-id="db2e0-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="db2e0-197">Выберите сервер Apache Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="db2e0-198">Выберите **Аргументы**.</span><span class="sxs-lookup"><span data-stu-id="db2e0-198">Click **Arguments**.</span></span> <span data-ttu-id="db2e0-199">Нажмите кнопку **рабочей** или **файловой системы** tooset hello папку, содержащую проект hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="db2e0-200">При запуске приложения hello, вы увидите окно браузера, предоставляя поле поиска для ввода условия.</span><span class="sxs-lookup"><span data-stu-id="db2e0-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="db2e0-201">Подождите около одной минуты, прежде чем нажимать кнопку **поиска** toogive hello службы времени toocreate и загрузка hello индекса.</span><span class="sxs-lookup"><span data-stu-id="db2e0-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="db2e0-202">Если возникает ошибка HTTP 404, необходимо просто toowait немного больше времени, прежде чем повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="db2e0-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="db2e0-203">Поиск по данным USGS</span><span class="sxs-lookup"><span data-stu-id="db2e0-203">Search on USGS data</span></span>
<span data-ttu-id="db2e0-204">набор данных Hello универсальные группы безопасности включает записи, соответствующие toohello состояние из Род-Айленд.</span><span class="sxs-lookup"><span data-stu-id="db2e0-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="db2e0-205">Если щелкнуть **поиска** на поле поиска пустым, вы получите hello 50 первых записей, которое является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="db2e0-206">Ввести условие поиска, даст hello поисковой системы что-нибудь toogo на.</span><span class="sxs-lookup"><span data-stu-id="db2e0-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="db2e0-207">Попробуйте ввести региональное имя или название.</span><span class="sxs-lookup"><span data-stu-id="db2e0-207">Try entering a regional name.</span></span> <span data-ttu-id="db2e0-208">«Roger Вильямса» был первый регулятор Род-Айленд hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="db2e0-209">В его честь названы многие парки, здания и школы.</span><span class="sxs-lookup"><span data-stu-id="db2e0-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="db2e0-210">Вы также можете попробовать одно из следующих условий поиска:</span><span class="sxs-lookup"><span data-stu-id="db2e0-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="db2e0-211">Потакет</span><span class="sxs-lookup"><span data-stu-id="db2e0-211">Pawtucket</span></span>
* <span data-ttu-id="db2e0-212">Пемброк</span><span class="sxs-lookup"><span data-stu-id="db2e0-212">Pembroke</span></span>
* <span data-ttu-id="db2e0-213">гусь +мыс</span><span class="sxs-lookup"><span data-stu-id="db2e0-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="db2e0-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db2e0-214">Next steps</span></span>
<span data-ttu-id="db2e0-215">Это hello учебник первого поиска Azure на основе Java и hello dataset универсальные группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="db2e0-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="db2e0-216">Со временем мы расширим этого учебника toodemonstrate дополнительные функции, может потребоваться toouse пользовательских решений.</span><span class="sxs-lookup"><span data-stu-id="db2e0-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="db2e0-217">Если уже есть определенные знания в поиске Azure, можно использовать этот образец как springboard для дальнейших экспериментов возможно дополнения hello [страницу поиска](search-pagination-page-layout.md), или реализовав [фасетная Навигация](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="db2e0-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="db2e0-218">Можно также повышают эффективность hello страницы результатов поиска, добавив счетчики и пакетную обработку документов, чтобы пользователи могут постраничного просмотра результатов hello.</span><span class="sxs-lookup"><span data-stu-id="db2e0-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="db2e0-219">Новый tooAzure поиска?</span><span class="sxs-lookup"><span data-stu-id="db2e0-219">New tooAzure Search?</span></span> <span data-ttu-id="db2e0-220">Рекомендуется попробовать другие учебники toodevelop понимание можно создать.</span><span class="sxs-lookup"><span data-stu-id="db2e0-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="db2e0-221">Посетите наш [страницы документации](https://azure.microsoft.com/documentation/services/search/) toofind больше ресурсов.</span><span class="sxs-lookup"><span data-stu-id="db2e0-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="db2e0-222">Можно также просмотреть ссылки hello в нашем [список видео и учебник](search-video-demo-tutorial-list.md) tooaccess Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="db2e0-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
