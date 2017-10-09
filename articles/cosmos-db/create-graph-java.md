---
title: "aaaCreate базе graph Azure Cosmos DB с Java | Документы Microsoft"
description: "Содержит пример, можно использовать tooconnect tooand запроса графические данные в базу данных Cosmos Azure, используя Gremlin кода Java."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="cc51e-103">Azure Cosmos DB: Создание диаграммы базы данных с использованием Java и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cc51e-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="cc51e-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cc51e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cc51e-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="cc51e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cc51e-106">Это краткое руководство создает граф базы данных с помощью hello портала средства Azure для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cc51e-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="cc51e-107">Это краткое руководство также показано, как tooquickly создать консольное приложение Java с помощью graph базу данных, используя hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) драйвера.</span><span class="sxs-lookup"><span data-stu-id="cc51e-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="cc51e-108">Hello инструкции в этом кратком руководстве можно выполнять в любой операционной системе, поддерживающий работу Java.</span><span class="sxs-lookup"><span data-stu-id="cc51e-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="cc51e-109">Это краткое руководство знакомит вас с создания и изменения ресурсов graph в hello пользовательского интерфейса или программно, какое значение имеет параметры.</span><span class="sxs-lookup"><span data-stu-id="cc51e-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cc51e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc51e-110">Prerequisites</span></span>

* [<span data-ttu-id="cc51e-111">Комплект разработчика Java (JDK 1.7+)</span><span class="sxs-lookup"><span data-stu-id="cc51e-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="cc51e-112">В Ubuntu — команду, запустите `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="cc51e-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="cc51e-113">Быть убедиться, что tooset hello JAVA_HOME среды переменной toopoint toohello папка, содержащая hello JDK.</span><span class="sxs-lookup"><span data-stu-id="cc51e-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="cc51e-114">[Скачайте](http://maven.apache.org/download.cgi) и [установите](http://maven.apache.org/install.html) двоичный архив [Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="cc51e-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="cc51e-115">Ubuntu, запускаются `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="cc51e-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="cc51e-116">Git.</span><span class="sxs-lookup"><span data-stu-id="cc51e-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="cc51e-117">Ubuntu, запускаются `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="cc51e-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="cc51e-118">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="cc51e-118">Create a database account</span></span>

<span data-ttu-id="cc51e-119">Перед созданием диаграммы базы данных необходимо toocreate учетную запись базы данных Gremlin (график) с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cc51e-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="cc51e-120">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="cc51e-120">Add a graph</span></span>

<span data-ttu-id="cc51e-121">Теперь можно использовать анализатор данных hello в hello Azure портала toocreate диаграммы базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="cc51e-122">В hello портал Azure, в меню навигации слева hello, щелкните **обозреватель данных (Предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="cc51e-123">В hello **обозреватель данных (Предварительная версия)** колонка, щелкните **новый граф**, затем заполните страницу приветствия, используя hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="cc51e-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Обозреватель данных в hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="cc51e-125">Настройка</span><span class="sxs-lookup"><span data-stu-id="cc51e-125">Setting</span></span>|<span data-ttu-id="cc51e-126">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="cc51e-126">Suggested value</span></span>|<span data-ttu-id="cc51e-127">Описание</span><span class="sxs-lookup"><span data-stu-id="cc51e-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="cc51e-128">Идентификатор базы данных</span><span class="sxs-lookup"><span data-stu-id="cc51e-128">Database ID</span></span>|<span data-ttu-id="cc51e-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="cc51e-129">sample-database</span></span>|<span data-ttu-id="cc51e-130">Идентификатор Hello новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-130">hello ID for your new database.</span></span> <span data-ttu-id="cc51e-131">Имя базы данных может иметь длину от 1 до 255 символов и не может содержать `/ \ # ?` или пробел.</span><span class="sxs-lookup"><span data-stu-id="cc51e-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="cc51e-132">Идентификатор графа</span><span class="sxs-lookup"><span data-stu-id="cc51e-132">Graph ID</span></span>|<span data-ttu-id="cc51e-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="cc51e-133">sample-graph</span></span>|<span data-ttu-id="cc51e-134">Идентификатор Hello новых диаграмм.</span><span class="sxs-lookup"><span data-stu-id="cc51e-134">hello ID for your new graph.</span></span> <span data-ttu-id="cc51e-135">График имена имеют hello требования же символов как идентификаторы базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="cc51e-136">Емкость хранилища</span><span class="sxs-lookup"><span data-stu-id="cc51e-136">Storage Capacity</span></span>| <span data-ttu-id="cc51e-137">10 ГБ</span><span class="sxs-lookup"><span data-stu-id="cc51e-137">10 GB</span></span>|<span data-ttu-id="cc51e-138">Оставьте значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-138">Leave hello default value.</span></span> <span data-ttu-id="cc51e-139">Это объем памяти hello hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="cc51e-140">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="cc51e-140">Throughput</span></span>|<span data-ttu-id="cc51e-141">400 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="cc51e-141">400 RUs</span></span>|<span data-ttu-id="cc51e-142">Оставьте значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-142">Leave hello default value.</span></span> <span data-ttu-id="cc51e-143">Можно увеличивать масштаб пропускной способности hello позже Если tooreduce задержки.</span><span class="sxs-lookup"><span data-stu-id="cc51e-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="cc51e-144">Ключ секции</span><span class="sxs-lookup"><span data-stu-id="cc51e-144">Partition key</span></span>|<span data-ttu-id="cc51e-145">Не указывайте</span><span class="sxs-lookup"><span data-stu-id="cc51e-145">Leave blank</span></span>|<span data-ttu-id="cc51e-146">В целях hello краткого руководства не указывайте ключ раздела hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="cc51e-147">После заполнения формы hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="cc51e-148">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="cc51e-148">Clone hello sample application</span></span>

<span data-ttu-id="cc51e-149">Теперь давайте клонировать приложении графа из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="cc51e-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="cc51e-150">Вы видите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="cc51e-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="cc51e-151">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="cc51e-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="cc51e-152">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="cc51e-153">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="cc51e-153">Review hello code</span></span>

<span data-ttu-id="cc51e-154">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="cc51e-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="cc51e-155">Откройте hello `Program.java` файл из папки \src\GetStarted hello и найдите следующие строки кода.</span><span class="sxs-lookup"><span data-stu-id="cc51e-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="cc51e-156">Hello Gremlin `Client` инициализируется из конфигурации hello в `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="cc51e-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="cc51e-157">Последовательность шагов Gremlin выполняются с помощью hello `client.submit` метод.</span><span class="sxs-lookup"><span data-stu-id="cc51e-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="cc51e-158">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="cc51e-158">Update your connection string</span></span>

1. <span data-ttu-id="cc51e-159">Привет открыть файл src/remote.yaml.</span><span class="sxs-lookup"><span data-stu-id="cc51e-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="cc51e-160">Заполните вашей *узлов*, *username*, и *пароль* значения в файле src/remote.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="cc51e-161">остальные параметры в hello Hello toobe изменения не требуется.</span><span class="sxs-lookup"><span data-stu-id="cc51e-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="cc51e-162">Настройка</span><span class="sxs-lookup"><span data-stu-id="cc51e-162">Setting</span></span>|<span data-ttu-id="cc51e-163">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="cc51e-163">Suggested value</span></span>|<span data-ttu-id="cc51e-164">Описание</span><span class="sxs-lookup"><span data-stu-id="cc51e-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="cc51e-165">Узлы</span><span class="sxs-lookup"><span data-stu-id="cc51e-165">Hosts</span></span>|<span data-ttu-id="cc51e-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="cc51e-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="cc51e-167">См. снимок экрана приветствия после этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="cc51e-167">See hello screenshot following this table.</span></span> <span data-ttu-id="cc51e-168">Это значение является значением Gremlin URI hello на странице приветствия Обзор hello в квадратных скобках с конечными hello портале Azure: 443 / удален.</span><span class="sxs-lookup"><span data-stu-id="cc51e-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="cc51e-169">Это значение также можно получить из вкладки ключи hello, используя значение URI hello, удаляя https://, документы toographs изменение и удаление в конце hello: 443 /.</span><span class="sxs-lookup"><span data-stu-id="cc51e-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="cc51e-170">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="cc51e-170">Username</span></span>|<span data-ttu-id="cc51e-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="cc51e-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="cc51e-172">Здравствуйте ресурсов hello формы `/dbs/<db>/colls/<coll>` где `<db>` — это имя существующей базы данных и `<coll>` — это имя существующей коллекции.</span><span class="sxs-lookup"><span data-stu-id="cc51e-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="cc51e-173">Пароль</span><span class="sxs-lookup"><span data-stu-id="cc51e-173">Password</span></span>|<span data-ttu-id="cc51e-174">*Первичный главный ключ*</span><span class="sxs-lookup"><span data-stu-id="cc51e-174">*Your primary master key*</span></span>|<span data-ttu-id="cc51e-175">См. второй снимок экрана приветствия после этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="cc51e-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="cc51e-176">Это значение является первичного ключа, которое можно получить со страницы приветствия ключи hello портал Azure, в поле hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="cc51e-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="cc51e-177">Скопируйте значение hello, с помощью "Копировать" hello "hello правой стороны прямоугольника hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="cc51e-178">Для значения узлов hello, скопируйте hello **Gremlin URI** значение из hello **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="cc51e-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="cc51e-179">Если она отсутствует, см. инструкции hello в строку hello узлов в предшествующей таблице о создании hello Gremlin URI из колонки ключи hello hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="cc51e-180">![Просмотр и копирование значение Gremlin URI hello на странице обзора hello в hello портал Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="cc51e-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="cc51e-181">Для hello значение пароля, скопируйте hello **первичного ключа** из hello **ключей** колонки: ![Просмотр и копирование первичного ключа в hello портал Azure, ключи страницы](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="cc51e-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="cc51e-182">Запустите консольное приложение hello</span><span class="sxs-lookup"><span data-stu-id="cc51e-182">Run hello console app</span></span>

1. <span data-ttu-id="cc51e-183">В окне терминала git hello `cd` toohello azure-cosmos-db-graph-java-getting-started папки.</span><span class="sxs-lookup"><span data-stu-id="cc51e-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="cc51e-184">В окне терминала git hello, введите `mvn package` tooinstall hello необходимые пакеты Java.</span><span class="sxs-lookup"><span data-stu-id="cc51e-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="cc51e-185">Выполните в окне терминала git hello, `mvn exec:java -D exec.mainClass=GetStarted.Program` в hello окно терминала toostart работу приложений Java.</span><span class="sxs-lookup"><span data-stu-id="cc51e-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="cc51e-186">окно терминала Hello отображает hello вершин, добавляемом toohello графа.</span><span class="sxs-lookup"><span data-stu-id="cc51e-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="cc51e-187">После завершения программы hello переключиться назад toohello портал Azure в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="cc51e-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="cc51e-188">Просмотр и добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="cc51e-188">Review and add sample data</span></span>

<span data-ttu-id="cc51e-189">Теперь, можно вернуться tooData обозревателя и разделе вершины hello добавлен toohello graph и добавить дополнительные точки данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="cc51e-190">В обозревателе данных разверните hello **базы данных образец**/**Образец диаграммы**, нажмите кнопку **Graph**и нажмите кнопку **применить фильтр**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="cc51e-192">В hello **результатов** Обратите внимание, добавлять новых пользователей hello toohello графа.</span><span class="sxs-lookup"><span data-stu-id="cc51e-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="cc51e-193">Выберите **Бен** и обратите внимание, что он подключен toorobin.</span><span class="sxs-lookup"><span data-stu-id="cc51e-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="cc51e-194">Можно перемещать hello вершин в обозреватель graph hello, увеличивать и уменьшать и увеличить размер hello hello graph explorer поверхности.</span><span class="sxs-lookup"><span data-stu-id="cc51e-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Новый вершины графике hello в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="cc51e-196">Давайте добавим несколько новых пользователей toohello с помощью граф hello обозреватель данных.</span><span class="sxs-lookup"><span data-stu-id="cc51e-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="cc51e-197">Нажмите кнопку hello **новыми шейдером вершин** кнопку tooadd данных tooyour графа.</span><span class="sxs-lookup"><span data-stu-id="cc51e-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="cc51e-199">Введите метку для *лицо* введите hello следующих разделов и значений toocreate hello первой вершины графике hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="cc51e-200">Обратите внимание, что вы можете создать уникальные свойства для каждого пользователя в графе.</span><span class="sxs-lookup"><span data-stu-id="cc51e-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="cc51e-201">Требуется только hello идентификатора ключа.</span><span class="sxs-lookup"><span data-stu-id="cc51e-201">Only hello id key is required.</span></span>

    <span data-ttu-id="cc51e-202">key</span><span class="sxs-lookup"><span data-stu-id="cc51e-202">key</span></span>|<span data-ttu-id="cc51e-203">value</span><span class="sxs-lookup"><span data-stu-id="cc51e-203">value</span></span>|<span data-ttu-id="cc51e-204">Примечания</span><span class="sxs-lookup"><span data-stu-id="cc51e-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="cc51e-205">id</span><span class="sxs-lookup"><span data-stu-id="cc51e-205">id</span></span>|<span data-ttu-id="cc51e-206">ashley</span><span class="sxs-lookup"><span data-stu-id="cc51e-206">ashley</span></span>|<span data-ttu-id="cc51e-207">Уникальный идентификатор Hello для hello вершины.</span><span class="sxs-lookup"><span data-stu-id="cc51e-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="cc51e-208">Если не указать идентификатор, он создастся автоматически.</span><span class="sxs-lookup"><span data-stu-id="cc51e-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="cc51e-209">gender</span><span class="sxs-lookup"><span data-stu-id="cc51e-209">gender</span></span>|<span data-ttu-id="cc51e-210">Женский</span><span class="sxs-lookup"><span data-stu-id="cc51e-210">female</span></span>| 
    <span data-ttu-id="cc51e-211">Технология</span><span class="sxs-lookup"><span data-stu-id="cc51e-211">tech</span></span> | <span data-ttu-id="cc51e-212">java</span><span class="sxs-lookup"><span data-stu-id="cc51e-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="cc51e-213">В этом кратком руководстве мы создадим несекционированную коллекцию.</span><span class="sxs-lookup"><span data-stu-id="cc51e-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="cc51e-214">Тем не менее если создать секционированную коллекцию, указав ключ секции во время создания коллекции hello, необходимо ключ раздела tooinclude hello в каждой новой вершины в качестве ключа.</span><span class="sxs-lookup"><span data-stu-id="cc51e-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="cc51e-215">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-215">Click **OK**.</span></span> <span data-ttu-id="cc51e-216">Может потребоваться tooexpand вашего экрана toosee **ОК** hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="cc51e-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="cc51e-217">Еще раз нажмите кнопку **New Vertex** (Создать вершину), чтобы добавить нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc51e-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="cc51e-218">Введите метку для *лицо* введите hello следующие ключи и значения:</span><span class="sxs-lookup"><span data-stu-id="cc51e-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="cc51e-219">key</span><span class="sxs-lookup"><span data-stu-id="cc51e-219">key</span></span>|<span data-ttu-id="cc51e-220">value</span><span class="sxs-lookup"><span data-stu-id="cc51e-220">value</span></span>|<span data-ttu-id="cc51e-221">Примечания</span><span class="sxs-lookup"><span data-stu-id="cc51e-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="cc51e-222">id</span><span class="sxs-lookup"><span data-stu-id="cc51e-222">id</span></span>|<span data-ttu-id="cc51e-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="cc51e-223">rakesh</span></span>|<span data-ttu-id="cc51e-224">Уникальный идентификатор Hello для hello вершины.</span><span class="sxs-lookup"><span data-stu-id="cc51e-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="cc51e-225">Если не указать идентификатор, он создастся автоматически.</span><span class="sxs-lookup"><span data-stu-id="cc51e-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="cc51e-226">gender</span><span class="sxs-lookup"><span data-stu-id="cc51e-226">gender</span></span>|<span data-ttu-id="cc51e-227">Мужской</span><span class="sxs-lookup"><span data-stu-id="cc51e-227">male</span></span>| 
    <span data-ttu-id="cc51e-228">Учебное заведение</span><span class="sxs-lookup"><span data-stu-id="cc51e-228">school</span></span>|<span data-ttu-id="cc51e-229">MIT</span><span class="sxs-lookup"><span data-stu-id="cc51e-229">MIT</span></span>| 

7. <span data-ttu-id="cc51e-230">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-230">Click **OK**.</span></span> 

8. <span data-ttu-id="cc51e-231">Нажмите кнопку **применить фильтр** по умолчанию hello `g.V()` фильтра.</span><span class="sxs-lookup"><span data-stu-id="cc51e-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="cc51e-232">Все пользователи hello теперь Показать hello **результатов** списка.</span><span class="sxs-lookup"><span data-stu-id="cc51e-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="cc51e-233">По мере добавления дополнительных данных, можно использовать фильтры toolimit результаты.</span><span class="sxs-lookup"><span data-stu-id="cc51e-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="cc51e-234">По умолчанию используется обозреватель данных `g.V()` tooretrieve всех вершин в диаграмму, но можно изменить, другой tooa [запрос graph](tutorial-query-graph.md), такие как `g.V().count()`, tooreturn количество всех вершин hello hello диаграммы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cc51e-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="cc51e-235">Теперь можно будет соединить пользователей rakesh и ashley.</span><span class="sxs-lookup"><span data-stu-id="cc51e-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="cc51e-236">Убедитесь, **ashley** в выбранной в hello **результатов** , а затем нажмите кнопку "Изменить" hello Далее слишком**цели** нижней правой части.</span><span class="sxs-lookup"><span data-stu-id="cc51e-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="cc51e-237">Может потребоваться toowiden вашей hello toosee окна **свойства** области.</span><span class="sxs-lookup"><span data-stu-id="cc51e-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Изменение целевой версии hello вершины в виде графа](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="cc51e-239">В hello **целевой** введите *rakesh*и в hello **границы метки** введите *знает*и щелкните флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="cc51e-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Создание связи между пользователями ashley и rakesh в обозревателе данных](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="cc51e-241">Теперь выберите **rakesh** из списка результатов hello и см. в разделе, ashley и rakesh были подключены.</span><span class="sxs-lookup"><span data-stu-id="cc51e-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Две вершины, связанные в обозревателе данных](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="cc51e-243">Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="cc51e-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="cc51e-244">Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc51e-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="cc51e-245">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cc51e-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cc51e-246">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc51e-246">Clean up resources</span></span>

<span data-ttu-id="cc51e-247">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cc51e-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="cc51e-248">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="cc51e-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="cc51e-249">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="cc51e-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc51e-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc51e-250">Next steps</span></span>

<span data-ttu-id="cc51e-251">В этом кратком руководстве вы узнали, как создать граф, с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="cc51e-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="cc51e-252">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cc51e-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc51e-253">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cc51e-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

