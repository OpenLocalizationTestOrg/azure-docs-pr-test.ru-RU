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
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Создание диаграммы базы данных с использованием Java и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

Это краткое руководство создает граф базы данных с помощью hello портала средства Azure для Azure Cosmos DB. Это краткое руководство также показано, как tooquickly создать консольное приложение Java с помощью graph базу данных, используя hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) драйвера. Hello инструкции в этом кратком руководстве можно выполнять в любой операционной системе, поддерживающий работу Java. Это краткое руководство знакомит вас с создания и изменения ресурсов graph в hello пользовательского интерфейса или программно, какое значение имеет параметры. 

## <a name="prerequisites"></a>Предварительные требования

* [Комплект разработчика Java (JDK 1.7+)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * В Ubuntu — команду, запустите `apt-get install default-jdk` tooinstall hello JDK.
    * Быть убедиться, что tooset hello JAVA_HOME среды переменной toopoint toohello папка, содержащая hello JDK.
* [Скачайте](http://maven.apache.org/download.cgi) и [установите](http://maven.apache.org/install.html) двоичный архив [Maven](http://maven.apache.org/).
    * Ubuntu, запускаются `apt-get install maven` tooinstall Maven.
* [Git.](https://www.git-scm.com/)
    * Ubuntu, запускаются `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

Перед созданием диаграммы базы данных необходимо toocreate учетную запись базы данных Gremlin (график) с Azure Cosmos DB.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Добавление графа

Теперь можно использовать анализатор данных hello в hello Azure портала toocreate диаграммы базы данных. 

1. В hello портал Azure, в меню навигации слева hello, щелкните **обозреватель данных (Предварительная версия)**. 
2. В hello **обозреватель данных (Предварительная версия)** колонка, щелкните **новый граф**, затем заполните страницу приветствия, используя hello следующую информацию:

    ![Обозреватель данных в hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    Настройка|Рекомендуемое значение|Описание
    ---|---|---
    Идентификатор базы данных|sample-database|Идентификатор Hello новой базы данных. Имя базы данных может иметь длину от 1 до 255 символов и не может содержать `/ \ # ?` или пробел.
    Идентификатор графа|sample-graph|Идентификатор Hello новых диаграмм. График имена имеют hello требования же символов как идентификаторы базы данных.
    Емкость хранилища| 10 ГБ|Оставьте значение по умолчанию hello. Это объем памяти hello hello базы данных.
    Пропускная способность|400 ЕЗ|Оставьте значение по умолчанию hello. Можно увеличивать масштаб пропускной способности hello позже Если tooreduce задержки.
    Ключ секции|Не указывайте|В целях hello краткого руководства не указывайте ключ раздела hello.

3. После заполнения формы hello, нажмите кнопку **ОК**.

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клонировать приложении графа из github, задайте строку подключения hello и запустите его. Вы видите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello `Program.java` файл из папки \src\GetStarted hello и найдите следующие строки кода. 

* Hello Gremlin `Client` инициализируется из конфигурации hello в `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Последовательность шагов Gremlin выполняются с помощью hello `client.submit` метод.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>Обновление строки подключения

1. Привет открыть файл src/remote.yaml. 

3. Заполните вашей *узлов*, *username*, и *пароль* значения в файле src/remote.yaml hello. остальные параметры в hello Hello toobe изменения не требуется.

    Настройка|Рекомендуемое значение|Описание
    ---|---|---
    Узлы|[***.graphs.azure.com]|См. снимок экрана приветствия после этой таблицы. Это значение является значением Gremlin URI hello на странице приветствия Обзор hello в квадратных скобках с конечными hello портале Azure: 443 / удален.<br><br>Это значение также можно получить из вкладки ключи hello, используя значение URI hello, удаляя https://, документы toographs изменение и удаление в конце hello: 443 /.
    Имя пользователя|/dbs/sample-database/colls/sample-graph|Здравствуйте ресурсов hello формы `/dbs/<db>/colls/<coll>` где `<db>` — это имя существующей базы данных и `<coll>` — это имя существующей коллекции.
    Пароль|*Первичный главный ключ*|См. второй снимок экрана приветствия после этой таблицы. Это значение является первичного ключа, которое можно получить со страницы приветствия ключи hello портал Azure, в поле hello первичный ключ. Скопируйте значение hello, с помощью "Копировать" hello "hello правой стороны прямоугольника hello.

    Для значения узлов hello, скопируйте hello **Gremlin URI** значение из hello **Обзор** страницы. Если она отсутствует, см. инструкции hello в строку hello узлов в предшествующей таблице о создании hello Gremlin URI из колонки ключи hello hello.
![Просмотр и копирование значение Gremlin URI hello на странице обзора hello в hello портал Azure](./media/create-graph-java/gremlin-uri.png)

    Для hello значение пароля, скопируйте hello **первичного ключа** из hello **ключей** колонки: ![Просмотр и копирование первичного ключа в hello портал Azure, ключи страницы](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Запустите консольное приложение hello

1. В окне терминала git hello `cd` toohello azure-cosmos-db-graph-java-getting-started папки.

2. В окне терминала git hello, введите `mvn package` tooinstall hello необходимые пакеты Java.

3. Выполните в окне терминала git hello, `mvn exec:java -D exec.mainClass=GetStarted.Program` в hello окно терминала toostart работу приложений Java.

окно терминала Hello отображает hello вершин, добавляемом toohello графа. После завершения программы hello переключиться назад toohello портал Azure в веб-браузере. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Просмотр и добавление демонстрационных данных

Теперь, можно вернуться tooData обозревателя и разделе вершины hello добавлен toohello graph и добавить дополнительные точки данных.

1. В обозревателе данных разверните hello **базы данных образец**/**Образец диаграммы**, нажмите кнопку **Graph**и нажмите кнопку **применить фильтр**. 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. В hello **результатов** Обратите внимание, добавлять новых пользователей hello toohello графа. Выберите **Бен** и обратите внимание, что он подключен toorobin. Можно перемещать hello вершин в обозреватель graph hello, увеличивать и уменьшать и увеличить размер hello hello graph explorer поверхности. 

   ![Новый вершины графике hello в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Давайте добавим несколько новых пользователей toohello с помощью граф hello обозреватель данных. Нажмите кнопку hello **новыми шейдером вершин** кнопку tooadd данных tooyour графа.

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Введите метку для *лицо* введите hello следующих разделов и значений toocreate hello первой вершины графике hello. Обратите внимание, что вы можете создать уникальные свойства для каждого пользователя в графе. Требуется только hello идентификатора ключа.

    key|value|Примечания
    ----|----|----
    id|ashley|Уникальный идентификатор Hello для hello вершины. Если не указать идентификатор, он создастся автоматически.
    gender|Женский| 
    Технология | java | 

    > [!NOTE]
    > В этом кратком руководстве мы создадим несекционированную коллекцию. Тем не менее если создать секционированную коллекцию, указав ключ секции во время создания коллекции hello, необходимо ключ раздела tooinclude hello в каждой новой вершины в качестве ключа. 

5. Нажмите кнопку **ОК**. Может потребоваться tooexpand вашего экрана toosee **ОК** hello нижней части экрана приветствия.

6. Еще раз нажмите кнопку **New Vertex** (Создать вершину), чтобы добавить нового пользователя. Введите метку для *лицо* введите hello следующие ключи и значения:

    key|value|Примечания
    ----|----|----
    id|rakesh|Уникальный идентификатор Hello для hello вершины. Если не указать идентификатор, он создастся автоматически.
    gender|Мужской| 
    Учебное заведение|MIT| 

7. Нажмите кнопку **ОК**. 

8. Нажмите кнопку **применить фильтр** по умолчанию hello `g.V()` фильтра. Все пользователи hello теперь Показать hello **результатов** списка. По мере добавления дополнительных данных, можно использовать фильтры toolimit результаты. По умолчанию используется обозреватель данных `g.V()` tooretrieve всех вершин в диаграмму, но можно изменить, другой tooa [запрос graph](tutorial-query-graph.md), такие как `g.V().count()`, tooreturn количество всех вершин hello hello диаграммы в формате JSON.

9. Теперь можно будет соединить пользователей rakesh и ashley. Убедитесь, **ashley** в выбранной в hello **результатов** , а затем нажмите кнопку "Изменить" hello Далее слишком**цели** нижней правой части. Может потребоваться toowiden вашей hello toosee окна **свойства** области.

   ![Изменение целевой версии hello вершины в виде графа](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. В hello **целевой** введите *rakesh*и в hello **границы метки** введите *знает*и щелкните флажок "hello".

   ![Создание связи между пользователями ashley и rakesh в обозревателе данных](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. Теперь выберите **rakesh** из списка результатов hello и см. в разделе, ashley и rakesh были подключены. 

   ![Две вершины, связанные в обозревателе данных](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности. Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.



## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги: 

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как создать граф, с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения. Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin. 

> [!div class="nextstepaction"]
> [Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)](tutorial-query-graph.md)

