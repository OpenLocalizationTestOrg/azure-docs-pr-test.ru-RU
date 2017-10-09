---
title: "aaaGet работы с поиском Azure в Node.js | Документы Microsoft"
description: "Пошаговое создание приложения поиска в облачной службе поиска Azure с использованием Node.js в качестве языка программирования."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="90dd0-103">Начало работы со службой поиска Azure на Node.js</span><span class="sxs-lookup"><span data-stu-id="90dd0-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90dd0-104">Портал</span><span class="sxs-lookup"><span data-stu-id="90dd0-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="90dd0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="90dd0-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="90dd0-106">Узнайте, как toobuild пользовательские Node.js поиск приложения, использующего поиска Azure для его результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="90dd0-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="90dd0-107">В этом учебнике используется hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello объекты и операции, используемые в этом упражнении.</span><span class="sxs-lookup"><span data-stu-id="90dd0-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="90dd0-108">Мы использовали [Node.js](https://Nodejs.org) и NPM, [Sublime текст 3](http://www.sublimetext.com/3)и Windows PowerShell на Windows 8.1 toodevelop и проверки кода.</span><span class="sxs-lookup"><span data-stu-id="90dd0-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="90dd0-109">toorun в этом примере необходимо иметь службы поиска Azure, который можно выполнить вход для hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90dd0-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90dd0-110">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) пошаговые инструкции.</span><span class="sxs-lookup"><span data-stu-id="90dd0-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="90dd0-111">О данных hello</span><span class="sxs-lookup"><span data-stu-id="90dd0-111">About hello data</span></span>
<span data-ttu-id="90dd0-112">В этом примере приложение использует данные из hello [США геологическое службы (универсальные группы безопасности)](http://geonames.usgs.gov/domestic/download_data.htm)фильтрацией на размер набора данных hello tooreduce состояние из Род-Айленд hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="90dd0-113">Мы будем использовать этот toobuild данных поиска приложения, которое возвращает ориентиров здания, например больницы школы, а также геологическое таких компонентов, как потоки, Озера и конференции.</span><span class="sxs-lookup"><span data-stu-id="90dd0-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="90dd0-114">В этом приложении hello **DataIndexer** программа создает и загружает hello индекса с помощью [индексатора](https://msdn.microsoft.com/library/azure/dn798918.aspx) конструкции, получение hello фильтрация набора данных универсальные группы безопасности из общей базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="90dd0-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="90dd0-115">Учетные данные и подключения источника данных в сети toohello информация представлена в коде программы hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="90dd0-116">Дальнейшая настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="90dd0-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="90dd0-117">Мы применен фильтр на этот набор данных toostay под hello 10 000 документов ограничение hello бесплатной ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="90dd0-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="90dd0-118">При использовании стандартного уровня hello, это ограничение не применяется.</span><span class="sxs-lookup"><span data-stu-id="90dd0-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="90dd0-119">Дополнительные сведения об ограничениях каждой ценовой категории см. в статье [Ограничения поиска Azure](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="90dd0-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="90dd0-120">Найти имя службы hello и ключ api службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="90dd0-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="90dd0-121">После создания службы hello, возвращают URL-адрес hello портала tooget toohello или `api-key`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="90dd0-122">Tooyour подключений службы поиска требует наличия обоих URL-адрес hello и `api-key` tooauthenticate hello вызовов.</span><span class="sxs-lookup"><span data-stu-id="90dd0-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="90dd0-123">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90dd0-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="90dd0-124">В панели переходов hello, щелкните **службы поиска** toolist подготовить все службы поиска Azure для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="90dd0-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="90dd0-125">Выберите службу hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="90dd0-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="90dd0-126">На панели мониторинга службы hello вы увидите плитки основные сведения, такие как hello значок ключа для доступа к ключи администратора hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="90dd0-127">Скопируйте URL-адрес службы hello ключа администратора и ключ запроса.</span><span class="sxs-lookup"><span data-stu-id="90dd0-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="90dd0-128">Все три необходимые данные при их добавлении файла config.js toohello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="90dd0-129">Загрузка файлов образца hello</span><span class="sxs-lookup"><span data-stu-id="90dd0-129">Download hello sample files</span></span>
<span data-ttu-id="90dd0-130">Используйте один из следующих подходов toodownload hello образец hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="90dd0-131">Go слишком[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="90dd0-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="90dd0-132">Нажмите кнопку **загрузить ZIP**, сохранить hello ZIP-файл, а затем извлечь все файлы hello в ней.</span><span class="sxs-lookup"><span data-stu-id="90dd0-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="90dd0-133">Все последующие изменения и операторы выполнения применяются к файлам в этой папке.</span><span class="sxs-lookup"><span data-stu-id="90dd0-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="90dd0-134">Обновите hello config.js.</span><span class="sxs-lookup"><span data-stu-id="90dd0-134">Update hello config.js.</span></span> <span data-ttu-id="90dd0-135">с помощью URL-адреса службы поиска и ключа API</span><span class="sxs-lookup"><span data-stu-id="90dd0-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="90dd0-136">С помощью hello URL-адрес и ключ api, который был скопирован ранее, укажите URL-адрес hello, ключ администратора и ключ запроса в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90dd0-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="90dd0-137">Ключи администратора предоставляют полный контроль над операциями службы, включая создание или удаление индекса и загрузку документов.</span><span class="sxs-lookup"><span data-stu-id="90dd0-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="90dd0-138">Напротив ключи запроса используются для операций чтения, обычно используется клиентскими приложениями, которые подключаются tooAzure поиска.</span><span class="sxs-lookup"><span data-stu-id="90dd0-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="90dd0-139">В этом примере мы включать hello запроса ключа toohelp дополнять hello рекомендация, с помощью ключа запроса hello в клиентских приложениях.</span><span class="sxs-lookup"><span data-stu-id="90dd0-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="90dd0-140">Привет, следуя снимке экрана показано **config.js** открыть в текстовом редакторе с hello соответствующие операции demarcated, чтобы можно было увидеть, где файл hello tooupdate с hello значения, которые являются допустимыми для службы поиска.</span><span class="sxs-lookup"><span data-stu-id="90dd0-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="90dd0-141">Узел среды выполнения для образца hello</span><span class="sxs-lookup"><span data-stu-id="90dd0-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="90dd0-142">Образец Hello требует HTTP-сервер, который можно установить глобально с помощью npm.</span><span class="sxs-lookup"><span data-stu-id="90dd0-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="90dd0-143">Окно PowerShell для hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="90dd0-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="90dd0-144">Перейдите в папку toohello, содержащую hello **package.json** файла.</span><span class="sxs-lookup"><span data-stu-id="90dd0-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="90dd0-145">Введите `npm install`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-145">Type `npm install`.</span></span>
3. <span data-ttu-id="90dd0-146">Введите `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="90dd0-147">Создание индекса hello и запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="90dd0-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="90dd0-148">Введите `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="90dd0-149">Введите `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="90dd0-150">Введите `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="90dd0-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="90dd0-151">В браузере откройте страницу `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="90dd0-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="90dd0-152">Поиск по данным USGS</span><span class="sxs-lookup"><span data-stu-id="90dd0-152">Search on USGS data</span></span>
<span data-ttu-id="90dd0-153">набор данных Hello универсальные группы безопасности включает записи, соответствующие toohello состояние из Род-Айленд.</span><span class="sxs-lookup"><span data-stu-id="90dd0-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="90dd0-154">Если щелкнуть **поиска** на поле поиска пустым, вы получаете hello 50 первых записей, которое является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="90dd0-155">Ввести поисковый термин дает hello поисковой системы что-нибудь toogo на.</span><span class="sxs-lookup"><span data-stu-id="90dd0-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="90dd0-156">Попробуйте ввести региональное имя или название.</span><span class="sxs-lookup"><span data-stu-id="90dd0-156">Try entering a regional name.</span></span> <span data-ttu-id="90dd0-157">«Roger Вильямса» был первый регулятор Род-Айленд hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="90dd0-158">В его честь названы многие парки, здания и школы.</span><span class="sxs-lookup"><span data-stu-id="90dd0-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="90dd0-159">Вы также можете попробовать одно из следующих условий поиска:</span><span class="sxs-lookup"><span data-stu-id="90dd0-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="90dd0-160">Потакет</span><span class="sxs-lookup"><span data-stu-id="90dd0-160">Pawtucket</span></span>
* <span data-ttu-id="90dd0-161">Пемброк</span><span class="sxs-lookup"><span data-stu-id="90dd0-161">Pembroke</span></span>
* <span data-ttu-id="90dd0-162">гусь +мыс</span><span class="sxs-lookup"><span data-stu-id="90dd0-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="90dd0-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90dd0-163">Next steps</span></span>
<span data-ttu-id="90dd0-164">Это hello учебник первого поиска Azure на основе Node.js и hello dataset универсальные группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="90dd0-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="90dd0-165">Со временем мы расширим этого учебника toodemonstrate дополнительные функции, может потребоваться toouse пользовательских решений.</span><span class="sxs-lookup"><span data-stu-id="90dd0-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="90dd0-166">Если у вас уже есть опыт работы с Поиском Azure, вы можете использовать этот пример как фундамент для средств подбора (запросы опережающего ввода или автозаполнения), фильтров и фасетной навигации.</span><span class="sxs-lookup"><span data-stu-id="90dd0-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="90dd0-167">Можно также повышают эффективность hello страницы результатов поиска, добавив счетчики и пакетную обработку документов, чтобы пользователи могут постраничного просмотра результатов hello.</span><span class="sxs-lookup"><span data-stu-id="90dd0-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="90dd0-168">Новый tooAzure поиска?</span><span class="sxs-lookup"><span data-stu-id="90dd0-168">New tooAzure Search?</span></span> <span data-ttu-id="90dd0-169">Рекомендуется попробовать другие учебники toodevelop понимание можно создать.</span><span class="sxs-lookup"><span data-stu-id="90dd0-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="90dd0-170">Посетите наш [страницы документации](https://azure.microsoft.com/documentation/services/search/) toofind больше ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90dd0-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="90dd0-171">Можно также просмотреть ссылки hello в нашем [список видео и учебник](search-video-demo-tutorial-list.md) tooaccess Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="90dd0-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
