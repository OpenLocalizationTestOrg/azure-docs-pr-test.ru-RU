---
title: "aaaJava учебников по разработке приложений с использованием Azure Cosmos DB | Документы Microsoft"
description: "Это Java веб приложения учебнике рассказывается, как toouse hello Azure Cosmos DB и hello toostore DocumentDB API и доступа к данным из приложения Java, размещенных на веб-сайтов Azure."
keywords: "Разработка приложений, учебник по базе данных, приложение java, учебник по веб-приложениям java, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="e32d6-104">Построение веб-приложения Java, используя Azure Cosmos DB и hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="e32d6-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e32d6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e32d6-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="e32d6-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e32d6-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="e32d6-107">Java</span><span class="sxs-lookup"><span data-stu-id="e32d6-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="e32d6-108">Python</span><span class="sxs-lookup"><span data-stu-id="e32d6-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="e32d6-109">В этом учебнике приложения web Java показано как toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) службы toostore и доступ к данным из приложения Java, размещенных на веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e32d6-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="e32d6-110">Из этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="e32d6-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="e32d6-111">Как toobuild простое приложение JavaServer страниц (JSP) в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e32d6-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="e32d6-112">Как toowork с hello Azure Cosmos DB службы с использованием hello [пакета SDK для Java Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="e32d6-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="e32d6-113">Этот учебник приложения Java показано выполнение задач по toocreate веб сервера управления задачами приложения, которое позволяет вам toocreate, получение и пометить завершена, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="e32d6-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="e32d6-114">Каждая из задач hello в список ToDo hello хранятся в виде документов JSON в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e32d6-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Приложение My ToDo List на Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="e32d6-116">В данном учебнике по разработке приложения предполагается, что у вас имеется некоторый опыт использования Java.</span><span class="sxs-lookup"><span data-stu-id="e32d6-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="e32d6-117">Новый tooJava или hello [готовности к установке средства](#Prerequisites), рекомендуется загрузить полный hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) проекта из GitHub и построения с помощью [hello инструкции в конце hello объекта статья](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="e32d6-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="e32d6-118">После построения, можно просмотреть hello статьи toogain и подробные сведения о кода hello в контексте hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="e32d6-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="e32d6-119"><a id="Prerequisites"></a>Необходимые условия для изучения этого учебника по разработке веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="e32d6-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="e32d6-120">Перед началом этого учебника разработки приложения, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e32d6-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e32d6-121">An active Azure account.</span></span> <span data-ttu-id="e32d6-122">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e32d6-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e32d6-123">Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e32d6-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="e32d6-124">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="e32d6-124">OR</span></span>

    <span data-ttu-id="e32d6-125">Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="e32d6-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="e32d6-126">[Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="e32d6-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="e32d6-127">Интегрированная среда разработки Eclipse для разработчиков Java EE.</span><span class="sxs-lookup"><span data-stu-id="e32d6-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="e32d6-128">Открытый веб-сайт Azure со средой выполнения Java (например, Tomcat или Jetty).</span><span class="sxs-lookup"><span data-stu-id="e32d6-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="e32d6-129">При установке этих средств для hello первый раз, coreservlets.com предоставляет пошаговое руководство процесса установки hello раздела hello быстрого запуска их [учебника: Установка TomCat7 и его использование с Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) статьи.</span><span class="sxs-lookup"><span data-stu-id="e32d6-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="e32d6-130"><a id="CreateDB"></a>Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e32d6-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="e32d6-131">Давайте сначала создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e32d6-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="e32d6-132">Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание приложения hello Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="e32d6-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="e32d6-133"><a id="CreateJSP"></a>Шаг 2: Создание приложения hello Java JSP</span><span class="sxs-lookup"><span data-stu-id="e32d6-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="e32d6-134">hello toocreate JSP приложения:</span><span class="sxs-lookup"><span data-stu-id="e32d6-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="e32d6-135">Во-первых, необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="e32d6-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="e32d6-136">В меню Eclipse выберите **File** (Файл), щелкните **New** (Создать), а затем выберите **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="e32d6-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="e32d6-137">Если вы не видите **динамический веб-проект** в списке доступных проектов, hello следующие: щелкните **файл**, нажмите кнопку **New**, нажмите кнопку **проекта**..., разверните **Web**, нажмите кнопку **динамический веб-проект**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Разработка приложений JSP Java](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="e32d6-139">Введите имя проекта в hello **имя проекта** поле, а в hello **целевой среды выполнения** раскрывающееся меню, при необходимости выберите значение (например, Apache Tomcat v7.0) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="e32d6-140">Выбор целевой среды выполнения включает toorun вы проекте локально через Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e32d6-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="e32d6-141">В Eclipse в представлении обозревателя проектов hello, разверните проект.</span><span class="sxs-lookup"><span data-stu-id="e32d6-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="e32d6-142">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="e32d6-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="e32d6-143">В hello **Создание JSP-файла** диалоговое окно, имя файла hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="e32d6-144">Сохранить hello родительскую папку как **WebContent**, как показано в hello следующие иллюстрации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Создание файла JSP — учебник по разработке веб-приложений Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="e32d6-146">В hello **Выбор шаблона JSP** диалоговом выберите время проведения hello **новый JSP-файл (html)**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="e32d6-147">При открытии файла index.jsp hello в Eclipse добавьте текст toodisplay **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="e32d6-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="e32d6-148">в существующих hello <body> элемента.</span><span class="sxs-lookup"><span data-stu-id="e32d6-148">within hello existing <body> element.</span></span> <span data-ttu-id="e32d6-149">Обновленный <body> содержимое должно выглядеть hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="e32d6-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="e32d6-150">Сохраните файл index.jsp hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="e32d6-151">Если значение целевой среды выполнения на шаге 2, можно щелкнуть **проекта** и затем **запуска** toorun приложения JSP локально:</span><span class="sxs-lookup"><span data-stu-id="e32d6-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Привет, мир! — учебник по разработке приложений Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="e32d6-153"><a id="InstallSDK"></a>Шаг 3: Установка пакета DocumentDB Java SDK hello</span><span class="sxs-lookup"><span data-stu-id="e32d6-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="e32d6-154">Hello простым способом toopull в DocumentDB Java SDK hello и его зависимостей выполняется с помощью [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="e32d6-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="e32d6-155">toodo это, необходимо будет tooconvert проекта maven tooa проекта, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e32d6-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="e32d6-156">Щелкните правой кнопкой мыши проект в обозревателе проектов hello, щелкните **Настройка**, нажмите кнопку **преобразовать проект tooMaven**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="e32d6-157">В hello **создать новый POM** , примите значения по умолчанию hello и выберите команду **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="e32d6-158">В **обозревателя проектов**, откройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="e32d6-159">На hello **зависимости** hello на вкладке **зависимости** области, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="e32d6-160">В hello **выберите зависимостей** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e32d6-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="e32d6-161">В hello **идентификатор группы** введите com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="e32d6-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="e32d6-162">В hello **идентификатор артефакта** введите azure documentdb.</span><span class="sxs-lookup"><span data-stu-id="e32d6-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="e32d6-163">В hello **версии** введите 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="e32d6-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Установка пакета DocumentDB Java Application SDK](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="e32d6-165">Или добавить зависимость hello XML для группы кода и идентификатор артефакта непосредственно toohello pom.xml через текстовый редактор:</span><span class="sxs-lookup"><span data-stu-id="e32d6-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="e32d6-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="e32d6-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="e32d6-167">Нажмите кнопку **ОК** и Maven установит hello DocumentDB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="e32d6-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="e32d6-168">Сохраните файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="e32d6-169"><a id="UseService"></a>Шаг 4: Использование служб Azure Cosmos DB hello в приложение Java</span><span class="sxs-lookup"><span data-stu-id="e32d6-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="e32d6-170">Во-первых определим hello объекта TodoItem в TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="e32d6-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="e32d6-171">В этом проекте мы используем [Lombok проекта](http://projectlombok.org/) toogenerate hello конструктор, методы получения, задания и конструктор.</span><span class="sxs-lookup"><span data-stu-id="e32d6-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="e32d6-172">Кроме того, можно вручную записать этот код или он сформирован hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="e32d6-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="e32d6-173">Служба Azure Cosmos DB tooinvoke hello, необходимо создать экземпляр нового **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="e32d6-174">Как правило, это лучший hello tooreuse **DocumentClient** — вместо создания нового клиента для каждого последующего запроса, чем.</span><span class="sxs-lookup"><span data-stu-id="e32d6-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="e32d6-175">Мы повторно использовать hello клиента путем заключения клиента hello в **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="e32d6-176">В DocumentClientFactory.java, необходимо получить toopaste hello URI и ПЕРВИЧНОГО ключа значение был сохранен в буфер обмена tooyour в [шаг 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="e32d6-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="e32d6-177">Замените [YOUR\_ENDPOINT\_HERE] на универсальный код ресурса, а [YOUR\_KEY\_HERE] — на первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="e32d6-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="e32d6-178">Теперь давайте создадим tooabstract объекта доступа к данным (DAO), сохранение нашей tooAzure элементы ToDo Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e32d6-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="e32d6-179">Чтобы элементов ToDo toosave tooa коллекции, hello клиенту tooknow какие базы данных и коллекция toopersist слишком (ссылается ссылки SELF-Link).</span><span class="sxs-lookup"><span data-stu-id="e32d6-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="e32d6-180">Как правило, это лучший hello toocache базы данных и коллекции, если это возможно дополнительных циклов приема-передачи tooavoid toohello-базы данных.</span><span class="sxs-lookup"><span data-stu-id="e32d6-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="e32d6-181">Hello следующий код показывает, как tooretrieve наши базы данных и коллекции, если он существует, или создать новый, если он не существует:</span><span class="sxs-lookup"><span data-stu-id="e32d6-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="e32d6-182">Hello следующим шагом является toowrite некоторые hello toopersist кода TodoItems toohello коллекции.</span><span class="sxs-lookup"><span data-stu-id="e32d6-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="e32d6-183">В этом примере мы будем использовать [Gson](https://code.google.com/p/google-gson/) tooserialize и десериализацию документы tooJSON TodoItem простых старых объектов Java (POJOs).</span><span class="sxs-lookup"><span data-stu-id="e32d6-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="e32d6-184">Подобно используемым базам данных Azure Cosmos DB и коллекциям, документы также связываются с помощью самостоятельных ссылок.</span><span class="sxs-lookup"><span data-stu-id="e32d6-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="e32d6-185">Здравствуйте, следующие вспомогательные функции позволяет нам получить документы по другой атрибут (например, «id»), а не ссылкой:</span><span class="sxs-lookup"><span data-stu-id="e32d6-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="e32d6-186">Мы можно использовать вспомогательный метод hello в шаге 5 tooretrieve документ TodoItem JSON по идентификатору и затем десериализовать tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="e32d6-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="e32d6-187">Также можно использовать hello DocumentClient tooget коллекции или список TodoItems DocumentDB SQL с помощью:</span><span class="sxs-lookup"><span data-stu-id="e32d6-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="e32d6-188">Существует много способов tooupdate документ с hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="e32d6-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="e32d6-189">В нашем приложения списка задач нам нужно будет tootoggle toobe ли TodoItem.</span><span class="sxs-lookup"><span data-stu-id="e32d6-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="e32d6-190">Это можно сделать путем обновления атрибута «выполнено» hello в документе hello:</span><span class="sxs-lookup"><span data-stu-id="e32d6-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="e32d6-191">Наконец мы хотим toodelete возможность hello TodoItem из нашего списка.</span><span class="sxs-lookup"><span data-stu-id="e32d6-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="e32d6-192">toodo это, можно использовать вспомогательный метод hello мы писали ранее tooretrieve hello ссылкой и затем сообщить toodelete hello клиента он:</span><span class="sxs-lookup"><span data-stu-id="e32d6-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="e32d6-193"><a id="Wire"></a>Шаг 5: Вместе подключения hello остальной части hello проекта разработки приложения Java</span><span class="sxs-lookup"><span data-stu-id="e32d6-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="e32d6-194">Теперь, когда мы закончено hello fun bits - осталось — это быстрый пользовательский интерфейс toobuild и подключить tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="e32d6-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="e32d6-195">Во-первых давайте начнем с созданием нашей DAO toocall контроллера:</span><span class="sxs-lookup"><span data-stu-id="e32d6-195">First, let's start with building a controller toocall our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="e32d6-196">В более сложных приложений hello контроллер может разместить сложной бизнес-логики поверх hello DAO.</span><span class="sxs-lookup"><span data-stu-id="e32d6-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="e32d6-197">Далее мы создадим сервлетов tooroute HTTP-запросы toohello контроллер:</span><span class="sxs-lookup"><span data-stu-id="e32d6-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="e32d6-198">Он понадобится toohello веб-интерфейса пользователя toodisplay пользователя.</span><span class="sxs-lookup"><span data-stu-id="e32d6-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="e32d6-199">Давайте перепишите hello index.jsp, что созданный ранее:</span><span class="sxs-lookup"><span data-stu-id="e32d6-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="e32d6-200">И наконец, написание некоторые клиентские hello tootie JavaScript веб-интерфейсом и hello сервлетов вместе.</span><span class="sxs-lookup"><span data-stu-id="e32d6-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="e32d6-201">Отлично!</span><span class="sxs-lookup"><span data-stu-id="e32d6-201">Awesome!</span></span> <span data-ttu-id="e32d6-202">Теперь осталось — приложение hello tootest.</span><span class="sxs-lookup"><span data-stu-id="e32d6-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="e32d6-203">Запустите приложение hello локально и добавьте несколько элементов Todo, заполнив имя элемента hello и категории команду **добавить задачу**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="e32d6-204">После отображения элемента hello, можно обновить ли это будет выполнено при снятии флажка hello и щелкнув **обновление задачи**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="e32d6-205"><a id="Deploy"></a>Шаг 6: Развертывание вашей tooAzure приложения Java веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="e32d6-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="e32d6-206">Веб-сайты Azure упрощают развертывание приложений Java с помощью простого экспорта приложения в виде WAR-файла либо с помощью загрузки через систему управления версиями (например, GIT) или через клиент FTP.</span><span class="sxs-lookup"><span data-stu-id="e32d6-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="e32d6-207">tooexport приложения как WAR-файл, щелкните правой кнопкой мыши проект в **обозревателя проектов**, нажмите кнопку **Экспорт**, а затем нажмите кнопку **WAR-файл**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="e32d6-208">В hello **Экспорт WAR** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e32d6-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="e32d6-209">В hello Web проекта введите documentdb-java пример azure.</span><span class="sxs-lookup"><span data-stu-id="e32d6-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="e32d6-210">В поле назначения hello выберите целевой toosave hello WAR-файл.</span><span class="sxs-lookup"><span data-stu-id="e32d6-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="e32d6-211">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e32d6-211">Click **Finish**.</span></span>
3. <span data-ttu-id="e32d6-212">Теперь, когда вы располагаете WAR-файл в, можно просто передать его tooyour веб-сайта Azure **веб-приложений** каталога.</span><span class="sxs-lookup"><span data-stu-id="e32d6-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="e32d6-213">Инструкции по передаче файла hello см. в разделе [добавить tooAzure приложения Java веб-приложений служб приложения](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="e32d6-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="e32d6-214">После hello WAR-файл каталога toohello загруженного веб-приложений, среда выполнения hello обнаружит добавили его и автоматически загружает его.</span><span class="sxs-lookup"><span data-stu-id="e32d6-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="e32d6-215">tooview ГП, перейдите toohttp://YOUR\_САЙТА\_NAME.azurewebsites.net/azure-java-sample/ и начать добавлять задач!</span><span class="sxs-lookup"><span data-stu-id="e32d6-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="e32d6-216"><a id="GetProject"></a>Получить проект hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="e32d6-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="e32d6-217">Все образцы hello в этом учебнике, включаются в hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) проекта на GitHub.</span><span class="sxs-lookup"><span data-stu-id="e32d6-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="e32d6-218">проект todo tooimport hello в Eclipse, убедитесь, имеются hello программного обеспечения и ресурсах, перечисленных в hello [необходимые компоненты](#Prerequisites) статьи, а затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e32d6-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="e32d6-219">Установите [проект Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="e32d6-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="e32d6-220">Lombok — используется toogenerate конструкторы, методы получения, задания в проект hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="e32d6-221">После загрузки файла lombok.jar hello, дважды щелкните его tooinstall его или установите его из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="e32d6-222">Если Eclipse открыт, закройте его и перезапустите его tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="e32d6-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="e32d6-223">В Eclipse на hello **файл** меню, нажмите кнопку **импорта**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="e32d6-224">В hello **импорта** окно, нажмите кнопку **Git**, нажмите кнопку **проекты из Git**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="e32d6-225">На hello **Выбор источника репозитория** щелкните **клон URI**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="e32d6-226">На hello **исходный репозиторий Git** экрана в hello **URI** введите https://github.com/Azure-Samples/java-todo-app.git и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="e32d6-227">На hello **ветвь выбора** экране, убедитесь, что **master** выбран и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="e32d6-228">На hello **локальной целевой** щелкните **Обзор** tooselect папке, можно скопировать hello репозитория, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="e32d6-229">На hello **toouse мастер импорта проектов выберите** экране, убедитесь, что **импортировать существующие проекты** выбран и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="e32d6-230">На hello **импорта проектов** экрана, отмените выбор hello **DocumentDB** проекта, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="e32d6-231">Hello DocumentDB проект содержит hello Azure Cosmos DB Java пакета SDK, который мы будем добавлять как зависимость.</span><span class="sxs-lookup"><span data-stu-id="e32d6-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="e32d6-232">В **обозревателя проектов**перейдите tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java и замените значения узла и MASTER_KEY hello hello URI и первичный ключ для вашей учетной записи Azure Cosmos DB, а затем сохранить файл hello.</span><span class="sxs-lookup"><span data-stu-id="e32d6-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="e32d6-233">Дополнительные сведения см. в инструкции [Шаг 1. Создание учетной записи базы данных Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="e32d6-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="e32d6-234">В **обозревателя проектов**, щелкните правой кнопкой мыши hello **-documentdb-java пример azure**, нажмите кнопку **путь построения**, а затем нажмите кнопку **настроить путь построения**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="e32d6-235">На hello **путь построения Java** экрана приветствия правой панели выберите hello **библиотеки** , а затем щелкните **добавить внешний JAR-файлов**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="e32d6-236">Перейдите toohello расположение файла lombok.jar hello и нажмите кнопку **откройте**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="e32d6-237">Используйте шаг 12 tooopen hello **свойства** окно и hello левой панели нажмите кнопку **целевых сред выполнения**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="e32d6-238">На hello **целевых сред выполнения** щелкните **New**выберите **v7.0 Apache Tomcat**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="e32d6-239">Используйте шаг 12 tooopen hello **свойства** окно и hello левой панели нажмите кнопку **аспекты проекта**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="e32d6-240">На hello **аспекты проекта** выберите **динамических веб-модуля** и **Java**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="e32d6-241">На hello **серверы** hello нижней части экрана приветствия щелкните правой кнопкой мыши **Tomcat v7.0 Server в localhost** и нажмите кнопку **добавлять и удалять**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="e32d6-242">На hello **добавлять и удалять** окна, переместите **-documentdb-java пример azure** toohello **настроенный** , а затем щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="e32d6-243">В hello **серверы** щелкните правой кнопкой мыши **Tomcat v7.0 Server в localhost**, а затем нажмите кнопку **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="e32d6-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="e32d6-244">В браузере перейдите toohttp://localhost:8080 / azure-documentdb-java образец и и приступите к добавлению tooyour списка задач.</span><span class="sxs-lookup"><span data-stu-id="e32d6-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="e32d6-245">Обратите внимание, что если вы изменили свои значения порта по умолчанию, измените выбранное значение toohello 8080.</span><span class="sxs-lookup"><span data-stu-id="e32d6-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="e32d6-246">toodeploy tooan вашего проекта веб-сайте Azure в разделе [шаг 6. Развертывание вашего приложения tooAzure веб-сайтов](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="e32d6-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
