---
title: "Анализ мнений Twitter aaaReal времени с Azure Stream Analytics | Документы Microsoft"
description: "Узнайте, как toouse Stream Analytics в реальном времени анализа мнений Twitter. Пошаговые инструкции из toodata создания события на динамическую панель мониторинга."
keywords: "анализ тенденций twitter в режиме реального времени, анализ тональности, анализ социальных сетей, пример анализа тенденций"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Анализ тональности в Twitter в режиме реального времени в Azure Stream Analytics

Узнайте, как toobuild анализ мнений решения для социальных сетей аналитика в реальном времени путем Twitter событий в концентраторы событий Azure. После этого можно написать tooanalyze hello Azure Stream Analytics запроса данных и либо хранилище hello результаты для дальнейшего использования или использовать панели мониторинга и [Power BI](https://powerbi.com/) tooprovide аналитики в реальном времени.

Средства аналитики для социальных сетей помогают организациям определить популярные темы, то есть темы и отношения с большим количеством записей в социальных сетях. Анализ мнений, которая также называется *мнение интеллектуального анализа данных*, использует социальные analytics средства toodetermine отношении продуктов, представление и т. д. 

Анализ трендов в режиме реального времени Twitter является отличным примером аналитический инструмент, поскольку hello хэштегом подписки модели позволяет ключевые слова toospecific toolisten (хэш) и разрабатывать анализ мнений hello веб-канала.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Сценарий: анализ тональности в социальной сети в режиме реального времени

Организации, которая содержит веб-сайт новостей носителя заинтересована в получения преимущества по сравнению с его конкурентами с содержимым узел, непосредственно относящиеся tooits читателей. Hello компания использует анализа социальных сетей на разделы, соответствующие tooreaders, выполнив анализ мнений в реальном времени данных Twitter.

tooidentify тенденций разделы в режиме реального времени в Twitter, hello аналитика в реальном времени потребности компании об объеме твит hello и мнения по ключевые темы. Другими словами hello связано подсистема аналитики анализ мнений, на основании этого социальные веб-канала.

## <a name="prerequisites"></a>Предварительные требования
В этом учебнике используется клиентское приложение, которое подключается tooTwitter и ищет твиты, имеющих определенные хэш (который можно задать). В порядке toorun hello приложения и анализ твиты, с помощью потоковой передачи аналитики Azure, необходимо иметь следующие hello hello:

* Подписка Azure
* учетная запись Twitter; 
* Приложения Twitter и hello [маркера доступа OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) для этого приложения. Мы предоставляем высокого уровня инструкции toocreate приложения Twitter в более поздней версии.
* Hello TwitterWPFClient приложение, которое считывает hello Twitter веб-канала. tooget это приложение, hello загрузки [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) файла из GitHub и затем распакуйте hello пакета в папку на компьютере. Если вы хотите toosee hello исходного кода и запустить приложение hello в отладчик, можно получить hello исходного кода из [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Создание концентратора событий для входных данных Streaming Analytics

Пример приложения Hello создает события и помещает их tooan концентратор событий Azure. Концентраторы событий Azure — hello предпочтительный метод приема событий для Stream Analytics. Дополнительные сведения см. в разделе hello [документации концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий
В этой процедуре сначала создать пространство имен концентратора событий и затем добавьте пространство имен toothat концентратора событий. Пространства имен концентратора событий используются группы toologically связанные экземпляры шины событий. 

1. Войдите в портал Azure toohello и нажмите кнопку **New** > **Интернета вещей** > **концентратора событий**. 

2. В hello **создать пространство имен** колонки, введите имя пространства имен, например `<yourname>-socialtwitter-eh-ns`. Можно использовать любое имя для пространства имен hello, но hello имя должно быть допустимым URL-адреса и должно быть уникальным среди Azure. 
    
3. Выберите подписку, создайте или выберите группу ресурсов, а затем щелкните **Создать**. 

    ![Создание пространства имен концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. После завершения развертывания приветствия имен найти пространство имен концентратора событий hello в списке ресурсов Azure. 

5. Нажмите кнопку hello новое пространство имен затем в колонке приветствия имен  **+ &nbsp;концентратора событий**. 

    ![Кнопка добавления концентратора событий Hello для создания нового концентратора событий ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Новый концентратор событий имя hello `socialtwitter-eh`. Вы можете использовать другое имя. В противном случае запишите его, поскольку его нужно имя hello. Не нужно tooset другие параметры для концентратора событий hello.

    ![Колонка создания нового концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Щелкните **Создать**.


### <a name="grant-access-toohello-event-hub"></a>Концентратор событий toohello предоставление доступа

Процесс для отправки данных концентратора событий tooan, hello концентратора событий должен иметь политику, разрешающую соответствующие права доступа. политика доступа Hello создает строку подключения, которая включает сведения об авторизации.

1.  В колонке пространства имен событий hello щелкните **концентраторов событий** и щелкните имя hello нового концентратора событий.

2.  В колонке концентратора событий hello щелкните **политики общего доступа** и нажмите кнопку  **+ &nbsp;добавить**.

    >[!NOTE]
    >Убедитесь, что вы работаете с концентратора событий hello, не hello пространство имен концентратора событий.

3.  Добавьте политику с именем `socialtwitter-access`, а для параметра **Утверждение** выберите **Управление**.

    ![Колонка создания политики доступа для нового концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Щелкните **Создать**.

5.  После развертывания политики hello, щелкните его в списке hello политик общего доступа.

6.  Поле поиска hello **строки ПЕРВИЧНОГО ключа подключения** и выберите hello копирования кнопку Далее toohello строку подключения. 
    
    ![Копирование hello первичным соединением строковый ключ из политики доступа hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Вставьте строку подключения hello в текстовый редактор. Эта строка подключения для hello в следующем разделе, необходимо после внесения tooit некоторые небольшие изменения.

    Строка подключения Hello выглядит следующим образом:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Обратите внимание, что строка подключения hello содержит несколько пар ключ значение, разделенных точкой с запятой: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, и `EntityPath`.  

    > [!NOTE]
    > В целях безопасности были удалены части строки соединения hello в примере hello.

8.  В текстовом редакторе hello, удалите hello `EntityPath` пару из строки подключения hello (не забудьте tooremove hello точкой с запятой, за которым следуют его). Когда закончите, строка подключения hello выглядит следующим образом:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Настройте и запустите клиентское приложение hello Twitter
клиентское приложение Hello получает события твитов непосредственно из Twitter. Чтобы toodo так, поэтому он должен hello toocall разрешение API-интерфейсов потоковой передачи Twitter. tooconfigure разрешение, создать приложение в Twitter, который создает уникальные учетные данные (например токена OAuth). Затем можно настроить hello клиентского приложения toouse эти учетные данные, когда он выполняет вызовы API. 

### <a name="create-a-twitter-application"></a>Создание приложения Twitter
Если вы еще не создали приложение Twitter для этого руководства, сделайте это. У вас уже должна быть учетная запись Twitter.

> [!NOTE]
> процессы Hello в Twitter для создания приложения и начало hello keys, секреты и токен, может измениться. Если эти инструкции не совпадают, отображаемые на сайте Twitter hello, см. документацию для разработчиков toohello Twitter.

1. Go toohello [страницы управления приложения Twitter](https://apps.twitter.com/). 

2. Создайте новое приложение. 

    * URL-адрес веб-сайта hello укажите допустимый URL-адрес. Он не имеет toobe действующем сайте. (Нельзя просто указать `localhost`).
    * Оставьте пустым поле обратного вызова hello. клиентское приложение Hello, используемого в этом учебнике не требует обратных вызовов.

    ![Создание приложения в Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. При необходимости измените разрешения приложения hello только для tooread.

4. При создании приложения hello go toohello **ключей и маркеры доступа** страницы.

5. Нажмите кнопку hello toogenerate маркер доступа и секрет маркера доступа.

Следует иметь под рукой, так как он понадобится в следующей процедуре hello.

>[!NOTE]
>Hello ключи и секретные данные для приложения hello Twitter укажите учетную запись Twitter tooyour доступа. Относить эту информацию как конфиденциальные, hello таким же, как пароль Twitter. Например не внедрять эту информацию в приложении, присвоенное tooothers. 


### <a name="configure-hello-client-application"></a>Настройте клиентское приложение hello
Мы создали клиентское приложение, которое соединяется с использованием данных tooTwitter [API-интерфейсов потоковой передачи в Twitter](https://dev.twitter.com/streaming/overview) toocollect события твитов о определенный набор разделов. приложение Hello использует hello [Sentiment140](http://help.sentiment140.com/) средства открытым исходным кодом, которое назначает hello следующие твит tooeach мнений значение:

* 0 = негативная тональность
* 2 = нейтральная тональность
* 4 = позитивная тональность

После события твитов hello назначения значение мнений, они помещаются в стек toohello концентратора событий, которое было создано ранее.

Перед запуском приложения hello, требуются определенные сведения от вас, таких как ключи Twitter hello и строка подключения концентратора событий hello. Можно указать сведения о конфигурации hello следующими способами:

* Запустите приложение hello и затем с помощью приложения hello пользовательского интерфейса tooenter hello ключи, секреты и строки подключения. После этого данные конфигурации hello используется во время текущего сеанса, но он не сохраняется.
* Измените файл .config приложения hello и задавать значения hello, существует. Этот подход сохраняет сведения о конфигурации hello, но это также означает, что это потенциально конфиденциальная информация хранится в виде обычного текста на компьютере.

Hello следующей процедуре описываются оба подхода. 

1. Убедитесь, что вы загрузили и распаковал hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) приложения, как указано в предварительных требованиях для hello.

2. tooset hello значений во время выполнения (и только для текущего сеанса hello) выполните hello `TwitterWPFClient.exe` приложения. Когда приложение hello будет предложено, введите hello следующие значения:

    * Здравствуйте, ключ пользователя Twitter (ключ API).
    * Hello секрет пользователя Twitter (секрет API).
    * Здравствуйте, Twitter токена доступа.
    * Hello Twitter секрет маркера доступа.
    * Hello строку подключения, сохраненный ранее. Убедитесь, что используемая строка подключения hello удаленные hello `EntityPath` пару ключ значение из.
    * Здравствуйте Twitter ключевые слова, которые вы хотите toodetermine мнения по.

   ![Запущенное приложение TwitterWpfClient со скрытыми параметрами](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. значения hello tooset постоянно, используйте текстовый редактор tooopen hello TwitterWpfClient.exe.config файл. Затем в hello `<appSettings>` элемент, это сделать:

    * Задать `oauth_consumer_key` toohello Twitter потребителя ключом (API). 
    * Задать `oauth_consumer_secret` toohello секрет пользователя Twitter (секрет API).
    * Задать `oauth_token` toohello Twitter токена доступа.
    * Задать `oauth_token_secret` toohello Twitter секрет маркера доступа.

    Далее в hello `<appSettings>` элемент, внесите следующие изменения:

    * Задать `EventHubName` имя концентратора событий toohello (то есть toohello значение пути hello сущности).
    * Задать `EventHubNameConnectionString` toohello строку подключения. Убедитесь, что используемая строка подключения hello удаленные hello `EntityPath` пару ключ значение из.

    Hello `<appSettings>` раздел выглядит как следующий пример hello. (Для ясности и безопасности мы перенесли часть строк и удалили некоторые символы.)

    ![Файл конфигурации приложения TwitterWpfClient в текстовом редакторе, показывающая hello Twitter ключи и секретные данные и данные строки подключения концентратора событий hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Если вы уже не запускали приложение hello, программу TwitterWpfClient.exe. 

5. Щелкните hello зеленую кнопку toocollect социальных мнений. Можно увидеть события Твитов с hello **CreatedAt**, **разделе**, и **SentimentScore** значения, отправляемых tooyour концентратора событий.

    ![Запущенное приложение TwitterWpfClient со списком твитов](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Если возникают ошибки, и вы не видите поток твиты, отображаются в нижней части окна hello hello, повторно проверьте hello ключи и секретные коды. Также проверьте строку подключения hello (Убедитесь, что он не включает hello `EntityPath` ключей и значений.)


## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics

Теперь, когда события твитов потоковая передача в режиме реального времени из Twitter, настройкой tooanalyze задания Stream Analytics эти события в режиме реального времени.

1. В hello портал Azure, щелкните **New** > **Интернета вещей** > **задания Stream Analytics**.

2. Имя задания hello `socialtwitter-sa-job` и укажите подписки, группы ресурсов и расположение.

    Это помешает tooplace hello задания и hello концентратора событий в hello же регионе для оптимальной производительности и, что не придется tootransfer данных между регионами.

    ![Создание нового задания Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Щелкните **Создать**.

    создается задание Hello и hello портал отобразит сведения о задании.


## <a name="specify-hello-job-input"></a>Укажите входной задания hello

1. В задание Stream Analytics в разделе **топологии задания** в середине hello hello задания колонка, щелкните **входов**. 

2. В hello **входов** колонка, щелкните  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:

    * **Входной псевдоним**: hello используйте имя `TwitterStream`. Если используется другое имя, запишите его, так как оно понадобится позже.
    * **Тип источника**: выберите **Поток данных**.
    * **Источник**: выберите **Концентратор событий**.
    * **Вариант импорта**: выберите **Использовать концентратор событий из текущей подписки**. 
    * **Пространство имен служебной шины**: выберите пространство имен концентратора hello событий, созданной ранее (`<yourname>-socialtwitter-eh-ns`).
    * **Концентратор событий**: hello выберите концентратор событий, созданной ранее (`socialtwitter-eh`).
    * **Имя политики концентратора событий**: выберите политику доступа hello, созданной ранее (`socialtwitter-access`).

    ![Создание новых входных данных для задания Streaming Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Щелкните **Создать**.


## <a name="specify-hello-job-query"></a>Укажите запрос hello задания

Stream Analytics поддерживает простую декларативную модель запроса для описания преобразований. toolearn Дополнительные сведения о языке hello. в разделе hello [Справка языка запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Это руководство поможет создать и проверить несколько запросов по данным Twitter.

Количество hello toocompare упоминания между разделами, можно использовать [«переворачивающееся» окно](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello число упоминания по разделам каждые пять секунд.

1. Закрыть hello **входов** колонки, если это еще не сделано.

2. В колонке задания hello щелкните hello **запроса** поле. Azure перечислены hello входов и выходов, которые настроены для задания hello и позволяет создать запрос, который позволяет преобразования hello входного потока при передаче toohello выходные данные.

3. Убедитесь, что выполнение этого TwitterWpfClient приложения hello. 

3. В hello **запроса** колонке нажмите кнопку Далее toohello точек hello `TwitterStream` входных данных, а затем выберите **выборку данных из входных данных**.

    ![Меню параметров toouse образцы данных для hello запись в задание Streaming Analytics с «Образец данных из входных данных» выбран](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Это открывает колонку, которая позволяет указать, сколько tooget данных образца, определенные в терминах продолжительность tooread hello входного потока.

4. Задать **минут** too3 и нажмите кнопку **ОК**. 
    
    ![Параметры выборки hello входного потока с выбран «3 минут».](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure образцы данные из входного потока hello за 3 минуты и предлагает при готовности данных образец hello. (Это займет некоторое время.) 

    данные образца Hello временно хранятся и доступны после открытия окна запроса hello. Если закрыть окно запроса hello данные образца hello удаляются и имеют toocreate новый набор образца данных. 

5. Изменить запрос hello в редакторе toohello hello кода ниже:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Если не использовать `TwitterStream` как hello псевдоним для ввода hello, замените на псевдоним для `TwitterStream` в запросе hello.  

    Этот запрос использует hello **TIMESTAMP BY** ключевое слово toospecify поле метки времени в toobe hello полезных данных, используемых в hello временных вычислений. Если это поле не указана, операция над окнами hello выполняется с помощью hello времени поступления каждого события в концентратор событий hello. Дополнительные сведения в разделе "hello «время прибытия и время приложения»" [Справка запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Этот запрос также получают доступ к отметку времени для hello конца каждого окна с помощью hello **System.Timestamp** свойство.

5. Нажмите **Проверить**. запрос Hello запускает hello данные, которые вы выборки.
    
6. Щелкните **Сохранить**. Это экономит hello запроса как часть задание Streaming Analytics hello. (Он не сохраняет данные образца hello).


## <a name="experiment-using-different-fields-from-hello-stream"></a>Поэкспериментируйте с помощью разных полей из потока hello 

Hello следующей таблице перечислены поля hello, которые являются частью hello потоковой передачи данных JSON. При желании вы свободного tooexperiment в редакторе запросов hello.

|Свойство JSON | Определение|
|--- | ---|
|CreatedAt | Hello время была создана, твит hello|
|Раздел | Hello раздел, соответствующий hello указано ключевое слово|
|SentimentScore | показатель мнений Hello из Sentiment140|
|Автор | Дескриптор Twitter Hello отправки твитов hello|
|текст | Полный текст Hello твит hello|


## <a name="create-an-output-sink"></a>Создание приемника выходных данных

Поток событий, событий ввода tooingest концентратора событий и запроса tooperform преобразования потока hello успешно определена. Последний шаг Hello — toodefine приемника выходных данных для задания hello.  

В этом учебнике записи hello статистическая обработка события твитов из tooAzure запроса задания hello хранилища больших двоичных объектов.  Также можно отправить на результаты tooAzure базы данных SQL, хранилище таблиц Azure концентраторов событий или для Power BI, в зависимости от приложения.

## <a name="specify-hello-job-output"></a>Укажите результат выполнения задания hello

1. В hello **топологии задания** щелкните hello **вывода** поле. 

2. В hello **выходов** колонка, щелкните  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:

    * **Псевдоним вывода**: hello используйте имя `TwitterStream-Output`. 
    * **Приемник.** Выберите **хранилище BLOB-объектов**.
    * **Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**.
    * **Учетная запись хранения**. Выберите **Создать новую учетную запись хранения**.
    * **Учетная запись хранения** (второе диалоговое окно). Введите `YOURNAMEsa`, где `YOURNAME` — ваше имя или другая уникальная строка. Имя Hello можно использовать только строчные буквы и цифры и должно быть уникальным среди Azure. 
    * **Контейнер**: Укажите `socialtwitter`.
    Имя учетной записи хранения Hello и имя контейнера, используемые вместе tooprovide URI для хранилища больших двоичных объектов hello, следующим образом: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Колонка "Новые выходные данные" для задания Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Щелкните **Создать**. 

    Azure создает учетную запись хранения hello и автоматически создает ключ. 

5. Закрыть hello **выходов** колонку. 


## <a name="start-hello-job"></a>Запустить задание hello

Входные данные для задания, запрос и выходные данные указаны. Все задания Stream Analytics готов toostart hello.

1. Убедитесь, что выполнение этого TwitterWpfClient приложения hello. 

2. В колонке hello задания, нажмите кнопку **запустить**.

    ![Запустить задание Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. В hello **запуска задания** колонке для **время начала выходные данные задания**выберите **теперь** и нажмите кнопку **запустить**. 

    ![Колонка «Запустить задание» для задания Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure уведомляет о запуска задания hello и в колонке задания hello hello состояние отображается как **под управлением**.

    ![Выполнение задания](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Просмотр выходных данных для анализа тональности

После задания будет запущен и обрабатывается в режиме реального времени поток Twitter hello, можно просмотреть выходные данные hello для анализа мнений.

Можно использовать средства, подобного [обозреватель хранилищ Azure](https://http://storageexplorer.com/) или [обозреватель Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview вывода вашу работу в режиме реального времени. Здесь можно использовать [Power BI](https://powerbi.com/) tooextend вашего приложения tooinclude настроенной панели мониторинга, например hello показанной hello следующий снимок экрана:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Создать разделы тенденций tooidentify другого запроса

Зависит от другого запроса, можно использовать мнений Twitter toounderstand [скользящее окно](https://msdn.microsoft.com/library/azure/dn835051.aspx). tooidentify тенденций разделов, поиск разделов, которые пересекают пороговое значение для упоминания о в определенное время.

Для целей этого учебника hello Проверьте наличие разделы, в которых упоминаются более чем в 20 раз в hello последние 5 секунд.

1. В колонке hello задания, нажмите кнопку **остановить** toostop hello задания. 

2. В hello **топологии задания** щелкните hello **запроса** поле. 

3. Измените следующие toohello hello запроса:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Щелкните **Сохранить**.

5. Убедитесь, что выполнение этого TwitterWpfClient приложения hello. 

6. Нажмите кнопку **запустить** toorestart hello задания с помощью нового запроса hello.


## <a name="get-support"></a>Получение поддержки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
