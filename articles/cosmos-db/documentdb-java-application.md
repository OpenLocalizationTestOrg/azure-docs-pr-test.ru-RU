---
title: "Руководство по разработке приложений Java с использованием Azure Cosmos DB | Документация Майкрософт"
description: "В этом руководстве по разработке веб-приложения Java показано, как использовать службу Azure Cosmos DB и API DocumentDB для хранения данных и обеспечения доступа к ним из приложения Java, размещенного на веб-сайтах Azure."
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
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="76997-104">Создание веб-приложения Java с использованием Azure Cosmos DB и API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="76997-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76997-105">.NET</span><span class="sxs-lookup"><span data-stu-id="76997-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="76997-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="76997-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="76997-107">Java</span><span class="sxs-lookup"><span data-stu-id="76997-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="76997-108">Python</span><span class="sxs-lookup"><span data-stu-id="76997-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="76997-109">В этом руководстве по разработке веб-приложения Java показано, как использовать службу [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) для хранения данных и обеспечения доступа к ним из приложения Java, размещенного в Azure при помощи функции "Веб-приложения службы приложений".</span><span class="sxs-lookup"><span data-stu-id="76997-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="76997-110">Из этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="76997-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="76997-111">Как создать основное приложение JavaServer Pages (JSP) в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="76997-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="76997-112">Как работать со службой Azure Cosmos DB с помощью [пакета SDK для Java для Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="76997-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="76997-113">В данном руководстве рассказывается о том, как создать веб-приложение для управления задачами, с помощью которого можно создавать и извлекать задачи, а также помечать их как завершенные, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="76997-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="76997-114">Каждая задача из списка ToDo будет храниться в виде документов JSON в службе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76997-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Приложение My ToDo List на Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="76997-116">В данном учебнике по разработке приложения предполагается, что у вас имеется некоторый опыт использования Java.</span><span class="sxs-lookup"><span data-stu-id="76997-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="76997-117">Если вы никогда не работали с Java или [необходимыми инструментами](#Prerequisites), мы рекомендуем скачать полный учебный проект [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) с портала GitHub и создать его, следуя [инструкциям, приведенным в конце этой статьи](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="76997-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="76997-118">После создания ознакомьтесь со статьей, чтобы разобраться в коде этого проекта.</span><span class="sxs-lookup"><span data-stu-id="76997-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="76997-119"><a id="Prerequisites"></a>Необходимые условия для изучения этого учебника по разработке веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="76997-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="76997-120">Для работы с этим учебником необходимы:</span><span class="sxs-lookup"><span data-stu-id="76997-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="76997-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="76997-121">An active Azure account.</span></span> <span data-ttu-id="76997-122">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="76997-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="76997-123">Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76997-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="76997-124">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="76997-124">OR</span></span>

    <span data-ttu-id="76997-125">Локальная установка [эмулятора Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="76997-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="76997-126">[Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="76997-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="76997-127">Интегрированная среда разработки Eclipse для разработчиков Java EE.</span><span class="sxs-lookup"><span data-stu-id="76997-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="76997-128">Открытый веб-сайт Azure со средой выполнения Java (например, Tomcat или Jetty).</span><span class="sxs-lookup"><span data-stu-id="76997-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="76997-129">При первой установке этих средств воспользуйтесь пошаговым руководством по установке, представленным на сайте coreservlets.com в разделе «Быстрый запуск» статьи [Учебник по установке TomCat7 и его использованию с Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) .</span><span class="sxs-lookup"><span data-stu-id="76997-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="76997-130"><a id="CreateDB"></a>Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76997-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="76997-131">Давайте сначала создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76997-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="76997-132">Если у вас уже есть учетная запись или вы используете эмулятор Azure Cosmos DB в этом руководстве, можно перейти к разделу [Шаг 2. Создание приложения Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="76997-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="76997-133"><a id="CreateJSP"></a>шагу 2 (создание приложения Java JSP)</span><span class="sxs-lookup"><span data-stu-id="76997-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="76997-134">Для создания приложения JSP:</span><span class="sxs-lookup"><span data-stu-id="76997-134">To create the JSP application:</span></span>

1. <span data-ttu-id="76997-135">Во-первых, необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="76997-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="76997-136">В меню Eclipse выберите **File** (Файл), щелкните **New** (Создать), а затем выберите **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="76997-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="76997-137">Если элемента **Dynamic Web Project** (Динамический веб-проект) нет в списке доступных проектов, откройте меню **File** (Файл), щелкните пункт **New** (Создать), а затем выберите **Project** (Проект), разверните список **Web** (Интернет), выберите **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Разработка приложений JSP Java](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="76997-139">Введите имя проекта в **соответствующем** поле и в раскрывающемся меню **Target Runtime** (Целевая среда выполнения). Если необходимо, выберите значение (например, Apache Tomcat v7.0), а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="76997-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="76997-140">Выбор целевой среды выполнения позволит вам запустить локальный проект через Eclipse.</span><span class="sxs-lookup"><span data-stu-id="76997-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="76997-141">В обозревателе проектов Eclipse разверните проект.</span><span class="sxs-lookup"><span data-stu-id="76997-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="76997-142">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="76997-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="76997-143">В диалоговом окне **New JSP File** (Новый JSP-файл) укажите для файла имя **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="76997-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="76997-144">Сохраните родительскую папку с именем **WebContent**, как показано на следующей иллюстрации, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Создание файла JSP — учебник по разработке веб-приложений Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="76997-146">В диалоговом окне **Select JSP Template** (Выбор шаблона JSP) в целях обучения выберите **New JSP File (html)** (Новый JSP-файл (html)) и нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="76997-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="76997-147">Открыв файл index.jsp в Eclipse, добавьте текст для отображения **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="76997-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="76997-148">в существующий элемент <body>.</span><span class="sxs-lookup"><span data-stu-id="76997-148">within the existing <body> element.</span></span> <span data-ttu-id="76997-149">Обновленное содержимое элемента <body> должно отображаться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="76997-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="76997-150">Сохраните файл index.jsp.</span><span class="sxs-lookup"><span data-stu-id="76997-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="76997-151">Если вы задали целевую среду выполнения в рамках шага 2, можете щелкнуть **Project** (Проект), а затем **Run** (Запуск) для локального запуска приложения JSP:</span><span class="sxs-lookup"><span data-stu-id="76997-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Привет, мир! — учебник по разработке приложений Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="76997-153"><a id="InstallSDK"></a>Шаг 3. Установка пакета DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="76997-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="76997-154">Самый простой способ извлечь данные из пакета DocumentDB Java SDK и его зависимости — использовать [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="76997-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="76997-155">Для этого необходимо преобразовать проект в проект Maven, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="76997-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="76997-156">Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Configure** (Настроить) и щелкните **Convert to Maven Project** (Преобразовать в проект Maven).</span><span class="sxs-lookup"><span data-stu-id="76997-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="76997-157">В окне **Create new POM** (Создать новый POM) примите параметры по умолчанию и нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="76997-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="76997-158">В **обозревателе проектов**откройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="76997-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="76997-159">На вкладке **Dependencies** (Зависимости) в **соответствующей** колонке щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="76997-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="76997-160">В окне **Select Dependency** (Выбор зависимости) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="76997-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="76997-161">В поле **Group Id** (Идентификатор группы) введите com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="76997-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="76997-162">В поле **Artifact Id** (Идентификатор артефакта) введите azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="76997-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="76997-163">В поле **Version** (Версия) введите 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="76997-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Установка пакета DocumentDB Java Application SDK](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="76997-165">Либо добавьте зависимость XML для идентификаторов группы и артефакта непосредственно в pom.xml в текстовом редакторе:</span><span class="sxs-lookup"><span data-stu-id="76997-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="76997-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="76997-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="76997-167">Нажмите кнопку **ОК**, и Maven установит пакет SDK для Java в DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="76997-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="76997-168">Сохраните файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="76997-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="76997-169"><a id="UseService"></a>Шаг 4. Использование службы Azure Cosmos DB в приложении Java</span><span class="sxs-lookup"><span data-stu-id="76997-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="76997-170">Сначала определим объект TodoItem в файле TodoItem.java.</span><span class="sxs-lookup"><span data-stu-id="76997-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="76997-171">В этом проекте мы используем [Проект Lombok](http://projectlombok.org/) для создания конструктора, получателя, задания и построителя.</span><span class="sxs-lookup"><span data-stu-id="76997-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="76997-172">Альтернационным способом можно написать следующий код вручную, либо сгенерировать его в IDE.</span><span class="sxs-lookup"><span data-stu-id="76997-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="76997-173">Чтобы вызвать службу Azure Cosmos DB, необходимо создать новый экземпляр **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="76997-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="76997-174">В общем, рекомендуется повторно использовать **DocumentClient** вместо создания нового клиента для каждого последующего запроса.</span><span class="sxs-lookup"><span data-stu-id="76997-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="76997-175">Мы можем повторно использовать клиент, поместив его в **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="76997-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="76997-176">В файле DocumentClientFactory.java необходимо вставить универсальный код ресурса (URI) и первичный ключ, сохраненные в буфер обмена на [шаге 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="76997-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="76997-177">Замените [YOUR\_ENDPOINT\_HERE] на универсальный код ресурса, а [YOUR\_KEY\_HERE] — на первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="76997-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="76997-178">Теперь давайте создадим объект доступа к данным (DAO) для абстрагирования сохранения элементов ToDo в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="76997-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="76997-179">Для сохранения элементов ToDo в коллекции клиент должен знать, какие базы данных и коллекции необходимо связать (с помощью самостоятельных ссылок).</span><span class="sxs-lookup"><span data-stu-id="76997-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="76997-180">Как правило, лучше всего кэшировать базы данных и коллекции, если это возможно для того, чтобы избежать дополнительных обращений к базе данных.</span><span class="sxs-lookup"><span data-stu-id="76997-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="76997-181">Следующий код иллюстрирует способ получения базы данных и коллекции, если он существует, или создать новый, если он не существует:</span><span class="sxs-lookup"><span data-stu-id="76997-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="76997-182">Следующим шагом является написание кода для сохранения элементов TodoItems в коллекции.</span><span class="sxs-lookup"><span data-stu-id="76997-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="76997-183">В этом примере мы будем использовать [Gson](https://code.google.com/p/google-gson/) для сериализации и десериализации элементов TodoItem POJO в документы JSON.</span><span class="sxs-lookup"><span data-stu-id="76997-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="76997-184">Подобно используемым базам данных Azure Cosmos DB и коллекциям, документы также связываются с помощью самостоятельных ссылок.</span><span class="sxs-lookup"><span data-stu-id="76997-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="76997-185">Следующая вспомогательная функция позволит получать документы с определенным атрибутом (например, id) без использования самостоятельных ссылок:</span><span class="sxs-lookup"><span data-stu-id="76997-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. <span data-ttu-id="76997-186">Указанный в шаге 5 вспомогательный метод можно использовать для извлечения документа TodoItem JSON по идентификатору и затем десериализовать его в POJO:</span><span class="sxs-lookup"><span data-stu-id="76997-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="76997-187">Можно также использовать DocumentClient для получения коллекции или перечня элементов TodoItems, используя DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="76997-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="76997-188">Существует множество способов обновления документа с помощью DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="76997-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="76997-189">В приложении списка дел необходимо иметь возможность переключения между режимами в случае завершения TodoItem.</span><span class="sxs-lookup"><span data-stu-id="76997-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="76997-190">Это достигается путем обновления атрибута "complete" (Завершено) в документе:</span><span class="sxs-lookup"><span data-stu-id="76997-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="76997-191">Наконец мы хотим иметь возможность удалить элементы TodoItem из нашего списка.</span><span class="sxs-lookup"><span data-stu-id="76997-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="76997-192">Чтобы сделать это, можно использовать вспомогательный метод, который был записан ранее, для получения ссылок и дать клиенту команду для удаления.</span><span class="sxs-lookup"><span data-stu-id="76997-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="76997-193"><a id="Wire"></a>Шаг 5. Подключение другой части проекта по разработке приложений Java</span><span class="sxs-lookup"><span data-stu-id="76997-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="76997-194">Теперь нам необходимо создать пользовательский интерфейс и привязать его к нашему объекту DAO.</span><span class="sxs-lookup"><span data-stu-id="76997-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="76997-195">Во-первых, необходимо начать с построения контроллера для вызова DAO:</span><span class="sxs-lookup"><span data-stu-id="76997-195">First, let's start with building a controller to call our DAO:</span></span>
   
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
   
    <span data-ttu-id="76997-196">В более сложных приложениях контроллер может включать сложные бизнес-логики в верхней части DAO.</span><span class="sxs-lookup"><span data-stu-id="76997-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="76997-197">Далее мы создадим сервлет, чтобы перенаправлять запросы HTTP к контроллеру:</span><span class="sxs-lookup"><span data-stu-id="76997-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
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
3. <span data-ttu-id="76997-198">Нам потребуется пользовательский веб-интерфейс, который будет отображаться для пользователя.</span><span class="sxs-lookup"><span data-stu-id="76997-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="76997-199">Повторно напишем файл index.jsp, созданный ранее:</span><span class="sxs-lookup"><span data-stu-id="76997-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="76997-200">И, наконец, запишем несколько сценариев Javascript на стороне клиента, чтобы связать пользовательский веб-интерфейс и сервлет.</span><span class="sxs-lookup"><span data-stu-id="76997-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. <span data-ttu-id="76997-201">Отлично!</span><span class="sxs-lookup"><span data-stu-id="76997-201">Awesome!</span></span> <span data-ttu-id="76997-202">Теперь осталось протестировать приложение.</span><span class="sxs-lookup"><span data-stu-id="76997-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="76997-203">Запустите приложение локально и добавьте несколько элементов Todo, заполнив имя элемента и категории и нажав кнопку **Add Task**(Добавить задачу).</span><span class="sxs-lookup"><span data-stu-id="76997-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="76997-204">Как только элемент появится, вы можете проверить его завершение, отметив флажком и щелкнув команду **Update Tasks**(Обновить задачи).</span><span class="sxs-lookup"><span data-stu-id="76997-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="76997-205"><a id="Deploy"></a>Шаг 6. Развертывание приложения Java на веб-сайтах Azure</span><span class="sxs-lookup"><span data-stu-id="76997-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="76997-206">Веб-сайты Azure упрощают развертывание приложений Java с помощью простого экспорта приложения в виде WAR-файла либо с помощью загрузки через систему управления версиями (например, GIT) или через клиент FTP.</span><span class="sxs-lookup"><span data-stu-id="76997-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="76997-207">Чтобы экспортировать приложение в виде WAR-файла, щелкните правой кнопкой мыши проект в **обозревателе проектов**, выберите **Export** (Экспорт) и щелкните **WAR File** (WAR-файл).</span><span class="sxs-lookup"><span data-stu-id="76997-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="76997-208">В окне **WAR Export** (Экспорт WAR-файла) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="76997-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="76997-209">В поле веб-проекта введите azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="76997-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="76997-210">В поле Destination (Назначение) выберите место назначения для сохранения WAR-файла.</span><span class="sxs-lookup"><span data-stu-id="76997-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="76997-211">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="76997-211">Click **Finish**.</span></span>
3. <span data-ttu-id="76997-212">Теперь, когда вы создали WAR-файл, можно просто передать его на веб-сайт Azure в каталог **webapps**.</span><span class="sxs-lookup"><span data-stu-id="76997-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="76997-213">Инструкции по передаче файла см. в статье [Добавление приложения Java в веб-приложения службы приложений Azure](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="76997-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="76997-214">После загрузки WAR-файла в каталог веб-приложения среда выполнения обнаруживает, что вы добавили его и автоматически загрузит ее.</span><span class="sxs-lookup"><span data-stu-id="76997-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="76997-215">Чтобы просмотреть готовый проект, перейдите по адресу http://ИМЯ\_САЙТА\_.azurewebsites.net/azure-java-sample/ и начните добавлять свои задачи.</span><span class="sxs-lookup"><span data-stu-id="76997-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="76997-216"><a id="GetProject"></a>Получение проекта из GitHub</span><span class="sxs-lookup"><span data-stu-id="76997-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="76997-217">Все примеры в этом учебнике включены в проект [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="76997-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="76997-218">Чтобы импортировать проект todo в Eclipse, убедитесь, что у вас есть программное обеспечение и ресурсы, перечисленные в разделе [Необходимые условия](#Prerequisites) , а затем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="76997-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="76997-219">Установите [проект Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="76997-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="76997-220">Lombok используется для формирования конструкторов, получателей и заданий в проекте.</span><span class="sxs-lookup"><span data-stu-id="76997-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="76997-221">Дважды щелкните загруженный файл lombok.jar для установки или установите его из командной строки.</span><span class="sxs-lookup"><span data-stu-id="76997-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="76997-222">Если открыта рабочая область Eclipse, закройте ее и запустите снова для загрузки проекта Lombok.</span><span class="sxs-lookup"><span data-stu-id="76997-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="76997-223">В Eclipse откройте меню **File** (Файл) и щелкните **Import** (Импорт).</span><span class="sxs-lookup"><span data-stu-id="76997-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="76997-224">В окне **Import** (Импорт) щелкните **Git**, а затем выберите **Projects from Git** (Проекты из Git) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="76997-225">На экране **Select Repository Source** (Выбрать источник репозитория) щелкните **Clone URI** (Клон URI).</span><span class="sxs-lookup"><span data-stu-id="76997-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="76997-226">На экране **Source Git Repository** (Исходный репозиторий Git) в поле **URI** введите https://github.com/Azure-Samples/java-todo-app.git, а затем нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="76997-227">На экране **Branch Selection** (Выбор ветви) выберите значение **master** и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="76997-228">На экране **Local Destination** (Локальная папка назначения) нажмите кнопку **Browse** (Обзор), выберите папку, в которую можно копировать репозитории, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="76997-229">Проверьте, установлен ли на экране **Select a wizard to use for importing projects** (Выбор мастера для импорта проектов) флажок **Import existing projects** (Импортировать существующие проекты), и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="76997-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="76997-230">На экране **Import Projects** (Импорт проектов) снимите флажок возле проекта **DocumentDB** и нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="76997-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="76997-231">В проекте DocumentDB содержится пакет Java SDK для Azure Cosmos DB, который будет добавлен в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="76997-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="76997-232">В **обозревателе проектов** перейдите в расположение azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java и замените значения в полях host и master_key значениями URI и первичного ключа своей учетной записи Azure Cosmos DB, а затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="76997-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="76997-233">Дополнительные сведения см. в инструкции [Шаг 1. Создание учетной записи базы данных Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="76997-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="76997-234">В **обозревателе проектов** щелкните правой кнопкой правой кнопкой элемент **azure-documentdb-java-sample**, а затем выберите **Build Path** (Путь сборки) и щелкните **Configure Build Path** (Настройка пути сборки).</span><span class="sxs-lookup"><span data-stu-id="76997-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="76997-235">На экране **Java Build Path** (Путь сборки Java) в правой области откройте вкладку **Libraries** (Библиотеки) и щелкните **Add External JAR** (Добавить внешние JAR-файлы).</span><span class="sxs-lookup"><span data-stu-id="76997-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="76997-236">Перейдите в расположение файла lombok.jar, щелкните **Open** (Открыть), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="76997-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="76997-237">Используйте инструкцию из шага 12, то есть снова откройте окно **Properties** (Свойства), а затем в левой области щелкните **Targeted Runtimes** (Целевые среды выполнения).</span><span class="sxs-lookup"><span data-stu-id="76997-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="76997-238">На экране **Targeted Runtimes** (Целевые среды выполнения) щелкните **New** (Создать), выберите **Apache Tomcat v7.0** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="76997-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="76997-239">Используйте инструкцию из шага 12, то есть снова откройте окно **Properties** (Свойства), а затем в левой области щелкните **Project Facets** (Аспекты проекта).</span><span class="sxs-lookup"><span data-stu-id="76997-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="76997-240">На экране **Project Facets** (Аспекты проекта) выберите **Dynamic Web Module** (Динамический веб-модуль) и **Java**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="76997-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="76997-241">На вкладке **Servers** (Серверы) в нижней части экрана щелкните правой кнопкой мыши **Tomcat v7.0 Server at localhost** (Tomcat v7.0 Server на localhost), а затем нажмите кнопку **Add and Remove** (Добавить или удалить).</span><span class="sxs-lookup"><span data-stu-id="76997-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="76997-242">В окне **Add and Remove** (Добавить или удалить) переместите элемент **azure-documentdb-java-sample** в поле **Configured** (Настроено), а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="76997-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="76997-243">На вкладке **Server** (Сервер) щелкните правой кнопкой мыши **Tomcat v7.0 Server at localhost** (Сервер Tomcat версии 7.0 на localhost), а затем нажмите кнопку **Restart** (Перезапуск).</span><span class="sxs-lookup"><span data-stu-id="76997-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="76997-244">В браузере перейдите по адресу http://localhost:8080/azure-documentdb-java-sample/ и начните добавлять задачи в список задач.</span><span class="sxs-lookup"><span data-stu-id="76997-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="76997-245">Обратите внимание, что в случае изменения заданных по умолчанию значений портов необходимо изменить значение 8080 выбранным вами значением.</span><span class="sxs-lookup"><span data-stu-id="76997-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="76997-246">Инструкции по развертыванию проекта на веб-сайтах Azure см. в пункте [Шаг 6. Развертывание приложений на веб-сайтах Azure](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="76997-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
