# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени

Этот учебник конца в конец показано, как toouse Azure Stream Analytics. Вы узнаете, как выполнять следующие задачи: 

* Перенести события потоковой передачи в экземпляр концентраторов событий Azure. В рамках этого руководства вы будете использовать соответствующее приложение, имитирующее поток записей метаданных мобильного устройства.

* Запись запросов tootransform SQL-подобного Stream Analytics данных, сведения об агрегировании или поиске шаблонов. Вы увидите, как toouse tooexamine запроса hello входящего потока и поиск вызовов, которые могут быть мошеннические.

* Отправьте hello результаты tooan приемником потока (хранилище), можно анализировать Дополнительные сведения. В этом случае будет отправлено hello подозрительные вызов данных tooAzure BLOB-объекта хранилища.

В этом учебнике мы используем пример hello в режиме реального времени мошенничества, на основе данных телефонный звонок. Но способ hello демонстрируется также подходит для других типов мошенничества, таких как кража мошенничества или кредитной карты. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Сценарий. Выявление мошенничества в отношении телекоммуникаций и SIM-карт в режиме реального времени

У поставщика телекоммуникационных услуг есть большой объем данных для входящих вызовов. фирма toodetect мошеннические вызовов в режиме реального времени, чтобы они могут уведомить клиентов или завершение работы службы на определенное количество Hello. Один тип мошенничества SIM включает в себя несколько вызовов из hello удостоверением вокруг hello же время, однако в географически различных мест. toodetect этот тип мошенничества, hello компании потребностей tooexamine входящих записей, phone и поиск конкретных шаблонов — в этом случае для вызовов, сделанных вокруг hello одновременно в разных странах. Любой телефон, в эту категорию попадают записи toostorage для последующего анализа.

## <a name="prerequisites"></a>Предварительные требования

В рамках этого руководства вы смоделируете данные вызовов с помощью клиентского приложения, которое создает пример метаданных вызова. Некоторые записи hello, hello приложение создает выглядят мошеннические вызовов. 

Прежде чем начать, убедитесь, что у вас есть следующие hello:

* Учетная запись Azure.
* приложение генератор события вызова Hello. Это можно получить, загрузив hello [TelcoGenerator.zip файл](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) из центра загрузки Майкрософт hello. Распакуйте этот пакет в папку на компьютере. Если требуется toosee hello исходный код и приложение hello выполнения в отладчике, можно получить исходный код приложения hello из [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows может блокировать hello загружен ZIP-файл. Если вы не удается распаковать его, щелкните правой кнопкой мыши файл hello и выберите **свойства**. Если вы видите hello сообщение «этот файл получен с другого компьютера и может быть заблокированных toohelp защитить этот компьютер», выберите hello **Unblock** и нажмите кнопку **применить**.

Если требуется, чтобы результаты hello tooexamine задание Streaming Analytics hello, необходимо также средство просмотра содержимого hello контейнера хранилища больших двоичных объектов. Если вы используете Visual Studio, можно использовать [инструменты Azure для Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) или [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Кроме того, можно установить автономные средства, например [обозреватель хранилищ Azure](http://storageexplorer.com/) или [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Создать событие Azure tooingest концентраторов событий

поток данных tooanalyze вы *приема* его в Azure. Типичный способ tooingest данных является toouse [концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md), которая позволяет приема миллионов событий в секунду и последующей обработки и хранения информации о событиях hello. В этом учебнике вы создаете концентратор событий и иметь hello события вызова генератор приложения отправки вызова данных toothat концентратора событий. Дополнительные сведения о концентраторах событий см. в разделе hello [документации Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Более подробные версию этой процедуры см. в разделе [создать пространство имен концентраторов событий и концентратора событий с помощью портала Azure "hello"](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Создание пространства имен и концентратора событий
В этой процедуре сначала создать пространство имен концентратора событий и затем добавить namepsace toothat концентратора событий. Пространства имен концентратора событий используются группы toologically связанные экземпляры шины событий. 

1. Войдите на портал Azure hello и щелкните **New** > **Интернета вещей** > **концентратора событий**. 

2. В hello **создать пространство имен** колонки, введите имя пространства имен, например `<yourname>-eh-ns-demo`. Можно использовать любое имя для пространства имен hello, но hello имя должно быть допустимым URL-адреса и должно быть уникальным среди Azure. 
    
3. Выберите подписку, создайте или выберите группу ресурсов, а затем щелкните **Создать**. 

    ![Создание пространства имен концентратора событий](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. После завершения развертывания приветствия имен найти пространство имен концентратора событий hello в списке ресурсов Azure. 

5. Нажмите кнопку hello новое пространство имен затем в колонке приветствия имен  **+ &nbsp;концентратора событий**. 

    ![Кнопка добавления концентратора событий Hello для создания нового концентратора событий ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Новый концентратор событий имя hello `sa-eh-frauddetection-demo`. Вы можете использовать другое имя. В противном случае запишите его, поскольку его нужно имя hello. Не нужно tooset другие параметры для концентратора событий hello прямо сейчас.

    ![Колонка создания нового концентратора событий](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Щелкните **Создать**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Предоставление доступа к концентратору событий toohello и получить строку подключения

Процесс для отправки данных концентратора событий tooan, hello концентратора событий должен иметь политику, разрешающую соответствующие права доступа. политика доступа Hello создает строку подключения, которая включает сведения об авторизации.

1.  В колонке пространства имен событий hello щелкните **концентраторов событий** и щелкните имя hello нового концентратора событий.

2.  В колонке концентратора событий hello щелкните **политики общего доступа** и нажмите кнопку  **+ &nbsp;добавить**.

    >[!NOTE]
    >Убедитесь, что вы работаете с концентратора событий hello, не hello пространство имен концентратора событий.

3.  Добавьте политику с именем `sa-policy-manage-demo`, а для параметра **Утверждение** выберите **Управление**.

    ![Колонка создания политики доступа для нового концентратора событий](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Щелкните **Создать**.

5.  После развертывания политики hello, щелкните его в списке hello политик общего доступа.

6.  Поле поиска hello **строки ПЕРВИЧНОГО ключа подключения** и выберите hello копирования кнопку Далее toohello строку подключения. 
    
    ![Копирование hello первичным соединением строковый ключ из политики доступа hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Вставьте строку подключения hello в текстовый редактор. Эта строка подключения для hello в следующем разделе, необходимо после внесения tooit некоторые небольшие изменения.

    Строка подключения Hello выглядит следующим образом:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Обратите внимание, что строка подключения hello содержит несколько пар ключ значение, разделенных точкой с запятой: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, и `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Настройка и запуск приложения генератора событий hello

Перед началом TelcoGenerator приложение hello задана, чтобы он отправлял концентратора событий toohello записей вызов только что созданный.

### <a name="configure-hello-telcogeneratorapp"></a>Настройка hello TelcoGeneratorapp

1.  В редакторе hello скопированной строки подключения hello, запишите hello `EntityPath` значение, а затем удалите hello `EntityPath` пары (не забудьте tooremove hello точкой с запятой, за которым следуют его). 

2.  В папке hello, куда было распаковано hello TelcoGenerator.zip файл откройте файл telcodatagen.exe.config hello в редакторе. (Имеется более одного config-файл, поэтому при открытии hello вправо на один.)

3.  В hello `<appSettings>` элемент, это сделать:

    * Задайте значение hello hello `EventHubName` имя концентратора событий ключа toohello (то есть toohello значение пути hello сущности).
    * Задайте значение hello hello `Microsoft.ServiceBus.ConnectionString` ключа toohello строку подключения. 

    Hello `<appSettings>` раздел будет выглядеть, как следующий пример hello. (Для ясности мы hello строк с переносом и удалены некоторые символы из маркера авторизации hello.)

    ![Файл конфигурации приложения TelcoGenerator, показывающая hello события концентратора имя и строку подключения](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Сохраните файл hello. 

### <a name="start-hello-app"></a>Запуск приложения hello
1.  Откройте окно командной строки и измените toohello папку, где приложение hello TelcoGenerator распакованную.
2.  Введите следующую команду hello:

        telcodatagen.exe 1000 .2 2

    используются следующие параметры Hello. 

    * Число записей подробных сведений о звонках за час. 
    * Вероятность мошенничества карты SIM: Как часто, в процентах для всех вызовов, приложение hello должны моделировать мошеннические вызова. значение Hello.2 означает, что примерно на 20% записей вызов hello выглядят мошеннические.
    * Продолжительность в часах. Выполняйте Hello количество часов, приложение hello. Также можно остановить приложение hello любое время, нажав клавиши Ctrl + C hello командной строки.

    Через несколько секунд приложение hello начинается отображение записей телефонный звонок на экране приветствия, поскольку отправляет их toohello концентратора событий.

Hello ниже приведены некоторые hello ключевых полей, которые вы будете использовать в этом приложении обнаружения мошенничества в режиме реального времени.

|**Запись**|**Определение**|
|----------|--------------|
|`CallrecTime`|время начала Hello отметки времени для вызова hello. |
|`SwitchNum`|Hello коммутатора используется вызов tooconnect hello. Например коммутаторы hello являются строк, которые представляют Привет Страна происхождения (США, Китае, Великобритании, Германии или Австралия). |
|`CallingNum`|номер телефона Hello hello вызывающего объекта. |
|`CallingIMSI`|Hello международной Mobile подписчика идентификатора IMSI. Это уникальный идентификатор hello hello вызывающего объекта. |
|`CalledNum`|номер телефона получателя вызова hello Hello. |
|`CalledIMSI`|Идентификатор IMSI. Это уникальный идентификатор получателя вызова hello hello. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Создание toomanage задания Stream Analytics, потоковая передача данных

Теперь, когда у вас есть поток событий вызовов, вы можете настроить задание Stream Analytics. Задание Hello будет считывать данные из концентратора событий hello, которую вы настроили. 

### <a name="create-hello-job"></a>Создание задания hello 

1. В hello портал Azure, щелкните **New** > **Интернета вещей** > **задания Stream Analytics**.

2. Имя задания hello `sa_frauddetection_job_demo`, укажите подписки, группы ресурсов и расположение.

    Это помешает tooplace hello задания и hello концентратора событий в hello же регионе для оптимальной производительности и, что не придется tootransfer данных между регионами.

    ![Создание нового задания Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Щелкните **Создать**.

    создается задание Hello и hello портал отобразит сведения о задании. Ничего не выполняется, хотя — имеется tooconfigure hello задания, прежде чем можно будет запустить.

### <a name="configure-job-input"></a>Настройка входных данных для задания

1. В панели мониторинга hello или hello **все ресурсы** колонки, найдите и выберите hello `sa_frauddetection_job_demo` задания Stream Analytics. 
2. В hello **топологии задания** раздел hello колонке задания Stream Analytics, щелкните hello **ввода** поле.

    ![Поле ввода в топологии в колонке задание Streaming Analytics hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Нажмите кнопку  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:

    * **Входной псевдоним**: hello используйте имя `CallStream`. Если используется другое имя, запишите его, так как оно понадобится позже.
    * **Тип источника**: выберите **Поток данных**. (**Ссылочные данные** ссылается toostatic уточняющего запроса данных, который не будет использовать в данном руководстве.)
    * **Источник**: выберите **Концентратор событий**.
    * **Вариант импорта**: выберите **Использовать концентратор событий из текущей подписки**. 
    * **Пространство имен служебной шины**: выберите пространство имен концентратора hello событий, созданной ранее (`<yourname>-eh-ns-demo`).
    * **Концентратор событий**: hello выберите концентратор событий, созданной ранее (`sa-eh-frauddetection-demo`).
    * **Имя политики концентратора событий**: выберите политику доступа hello, созданной ранее (`sa-policy-manage-demo`).

    ![Создание новых входных данных для задания Streaming Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Щелкните **Создать**.

## <a name="create-queries-tootransform-real-time-data"></a>Создание запросов в реальном времени данных tootransform

На этом этапе необходимо настроить tooread поток входящих данных задания Stream Analytics. Hello следующим шагом является toocreate преобразование, которое анализирует данные hello в режиме реального времени. Сделаем это с помощью создания запроса. Stream Analytics поддерживает простую декларативную модель запроса для описания преобразований для обработки в режиме реального времени. Hello запросы используют SQL-подобного языка, который имеет некоторые расширения определенного toostream analytics. 

Очень простой запрос может считать всех входящих данных hello. Тем не менее часто создают запросы, которые выглядят для конкретных данных, или для связи в данных hello. В этом разделе учебника hello будет создать и проверить несколько запросов toolearn несколькими способами, в которых можно преобразовать входной поток для анализа. 

запросы Hello, созданный здесь будет только с экрана hello преобразованные данные toohello. В следующем разделе вы настроите приемник выходных данных и запрос, который записывает приемник toothat hello преобразованные данные.

toolearn Дополнительные сведения о языке hello. в разделе hello [Справка языка запросов Azure Stream Analytics](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Получение образца данных для запросов для тестирования

приложение Hello TelcoGenerator отправляет концентратора событий toohello вызовов записи и задание Stream Analytics является настроенным tooread из концентратора событий hello. Можно использовать запрос tootest hello задания toomake убедиться, что он правильно чтения. слишком проверить запрос в hello консоли Azure, необходимо образцов данных. В этом пошаговом руководстве будет извлечь образец данных из потока hello, поступают в концентратор событий hello.

1. Убедитесь, что запущен и формирует вызовах, записываемых TelcoGenerator приложение hello.
2. На портале hello возвращают колонке задание Streaming Analytics toohello. (При закрытии колонке hello поиск `sa_frauddetection_job_demo` в hello **все ресурсы** колонке.)
3. Нажмите кнопку hello **запроса** поле. Azure перечислены hello входов и выходов, которые настроены для задания hello и позволяет создать запрос, который позволяет преобразования hello входного потока при передаче toohello выходные данные.
4. В hello **запроса** колонке нажмите кнопку Далее toohello точек hello `CallStream` входных данных, а затем выберите **выборку данных из входных данных**.

    ![Меню параметров toouse образцы данных для hello запись в задание Streaming Analytics с «Образец данных из входных данных» выбран](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Это открывает колонку, которая позволяет указать, сколько tooget данных образца, определенные в терминах продолжительность tooread hello входного потока.

5. Задать **минут** too3 и нажмите кнопку **ОК**. 
    
    ![Параметры выборки hello входного потока с выбран «3 минут».](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure образцы данные из входного потока hello за 3 минуты и предлагает при готовности данных образец hello. (Это займет некоторое время.) 

данные образца Hello временно хранятся и доступны после открытия окна запроса hello. Если закрыть окно запроса hello данные образца hello удаляются, и будет toocreate новый набор образца данных. 

В качестве альтернативы можно получить JSON-файл, содержащую образец данных [из GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)и затем передать файл, .json toouse как образцы данных для hello `CallStream` ввода. 

### <a name="test-using-a-pass-through-query"></a>Проверка с помощью запроса к серверу

Следует tooarchive каждого события можно использовать tooread передаваемый запрос всех полей hello в hello полезных данных события hello.

1. В окне запроса hello введите этот запрос:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Как и при использовании SQL, регистр ключевых слов не учитывается, пробел не имеет значения.

    В этом запросе `CallStream` hello псевдонимов, которые указаны при создании hello входных данных. Если вы использовали другой псевдоним, используйте его, соответственно.

2. Нажмите **Проверить**.

    Задание Stream Analytics Hello выполняет запрос hello данных образец hello и выходных данных hello hello нижней части окна hello. Это означает, что hello концентратора событий и задание Streaming Analytics hello настроены правильно. (Как уже отмечалось, позже вы создадите приемника выходных данных этого hello запроса может записывать данные в.)

    ![Выходные данные задания Stream Analytics, отображающие 73 созданные записи](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    точное число записей, отображаемых в Hello зависит количество записей были записаны в вашем примере 3 минуты.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Сократите число hello полей с помощью проекции столбца

Во многих случаях анализа не все столбцы hello из входного потока hello. Можно использовать запрос tooproject, меньшего количества возвращаемых полей, чем в запросе к серверу hello.

1. Изменить запрос hello в редакторе toohello hello кода ниже:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Снова щелкните **Проверка**. 

    ![Выходные данные задания Stream Analytics для заполнения столбцов, отображающие 25 созданных записей](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Количество входящих вызовов по региону: "переворачивающееся" окно с агрегированием

Предположим, что следует toocount hello число входящих вызовов в одном регионе. В потоковой передачи данных, при необходимости tooperform агрегатных функций, например инвентаризации, необходим toosegment hello поток в temporal единицы (поскольку фактически бесконечные hello непосредственно источник данных). Это можно сделать с помощью [функции окна](stream-analytics-window-functions.md) Streaming Analytics. С hello данных в этом окне можно будет работать как единое целое.

Для такого преобразования нужна последовательность временных окон, которые не перекрываются. У каждого окна будет дискретный набор данных, которые можно группировать и статистически обрабатывать. Этот тип окна находится ссылка tooas *«переворачивающееся» окно* . В «переворачивающееся» окно приветствия, можно получить количество входящих вызовов hello, сгруппированные по `SwitchNum`, представляющий hello стране, где поступил вызов hello. 

1. Изменить запрос hello в редакторе toohello hello кода ниже:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Этот запрос использует hello `Timestamp By` ключевое слово в hello `FROM` toospecify предложение, какое поле timestamp в hello входной поток toouse toodefine hello «переворачивающееся» окно. В этом случае окно hello делит hello данные на сегменты hello `CallRecTime` поля в каждой записи. (Если не указано, операция над окнами hello использует время hello, поступающих каждого события в концентратор событий hello. Дополнительные сведения см. в разделе о времени поступления и времени приложения в [справочнике по языку запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    проекция Hello включает `System.Timestamp`, который возвращает отметку времени для hello конца каждого окна. 

    toospecify, что требуется toouse «переворачивающегося» окна, используйте hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) функции hello `GROUP BY `предложения. В функции hello укажите единицу времени (в любом из tooa в микросекунды день) и размер (количество единиц). В этом примере «переворачивающееся» окно hello состоит из каждые 5 секунд, вы получите число по странам для вызовов, накопленные за каждые 5 секунд.

2. Снова щелкните **Проверка**. В результатах hello, обратите внимание, отметки времени hello в **WindowEnd** , с шагом 5 секунд.

    ![Выходные данные задания Stream Analytics для статистической обработки, отображающие 13 созданных записей](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Выявление мошенничества в отношении SIM-карт с помощью самосоединения

В этом примере мы считаем мошеннические использования toobe вызовов, которые получаются из hello же пользователя, но в разных местах в течение 5 секунд друг от друга. Например, hello того же пользователя не может вызвать основаниях из hello США и Австралии на hello то же время. 

toocheck в этих случаях можно использовать самосоединение hello потоковой передачи данных toojoin hello поток tooitself основании hello `CallRecTime` значение. Затем можно найти для вызова записывает там, где hello `CallingIMSI` Здравствуйте значение (hello, рассчитанные на число), таким же, но hello `SwitchNum` значение (Страна происхождения) не является таким же hello.

При использовании соединения с потоковой передачи данных hello соединения необходимо предоставить некоторые ограничения на насколько hello сопоставление строк можно разделить вовремя. (Как уже отмечалось, hello, потоковая передача данных — фактически бесконечный). заданных ограничений по времени Hello соотношение hello hello `ON` предложения join hello с помощью hello `DATEDIFF` функции. В этом случае hello соединение основано на 5-секундного интервала данных вызова.

1. Изменить запрос hello в редакторе toohello hello кода ниже: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Этот запрос подобен любого другого соединения SQL, за исключением hello `DATEDIFF` функции в соединении hello. Это — это версия `DATEDIFF` это конкретных tooStreaming аналитика, и он должен указываться в hello `ON...BETWEEN` предложения. Параметры Hello — единица измерения времени (в этом примере секунды) и псевдонимы hello hello двух источников для hello соединения. (Это отличается от стандартного SQL hello `DATEDIFF` функции.) 

    Hello `WHERE` предложение включает hello условие, которое помечает мошеннические вызов hello: hello исходного ключи не являются hello таким же. 

2. Снова щелкните **Проверка**. 

    ![Выходные данные задания Stream Analytics для самосоединения, отображающие 6 созданных записей](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Щелкните **Сохранить**. Это экономит hello самосоединение запроса как часть задание Streaming Analytics hello. (Он не сохраняет данные образца hello).

    ![Сохранение задания Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Создать выходные данные преобразования toostore приемника

Поток событий, событий ввода tooingest концентратора событий и запроса tooperform преобразования определили hello потока. Hello последний шаг — toodefine приемника выходных данных для задания hello, т. е hello toowrite месте преобразования потока. 

Вы можете использовать многие ресурсы в качестве приемников выходных данных — базу данных SQL Server, хранилище таблиц, хранилище озера данных, Power BI и даже другой концентратор событий. В этом учебнике вы будете писать tooAzure hello потока хранилища больших двоичных объектов, что является обычной вариантом для сбора данных сведения о событии для последующего анализа, так как она предусматривает неструктурированных данных.

Если у вас есть учетная запись хранения BLOB-объектов, вы можете ее использовать. В этом учебнике мы покажем, как toocreate новое хранилище учетную запись только для этого учебника.

### <a name="create-an-azure-blob-storage-account"></a>Создание учетной записи хранения BLOB-объектов Azure

1. В hello портал Azure возвращают колонке задание Streaming Analytics toohello. (При закрытии колонке hello поиск `sa_frauddetection_job_demo` в hello **все ресурсы** колонке.)
2. В hello **топологии задания** щелкните hello **вывода** поле. 
3. В hello **выходов** колонка, щелкните  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:

    * **Псевдоним вывода**: hello используйте имя `CallStream-FraudulentCalls`. 
    * **Приемник.** Выберите **хранилище BLOB-объектов**.
    * **Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**.
    * **Учетная запись хранения**. Выберите **Создать новую учетную запись хранения.**
    * **Учетная запись хранения** (второе диалоговое окно). Введите `YOURNAMEsademo`, где `YOURNAME` — ваше имя или другая уникальная строка. Имя Hello можно использовать только строчные буквы и цифры и должно быть уникальным среди Azure. 
    * **Контейнер**: Укажите `sa-fraudulentcalls-demo`.
    Имя учетной записи хранения Hello и имя контейнера, используемые вместе tooprovide URI для хранилища больших двоичных объектов hello, следующим образом: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Колонка "Новые выходные данные" для задания Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Щелкните **Создать**. 

    Azure создает учетную запись хранения hello и автоматически создает ключ. 

5. Закрыть hello **выходов** колонку. 

## <a name="start-hello-streaming-analytics-job"></a>Запустить задание Streaming Analytics hello

Теперь настроен Hello задания. Вы указали входных данных (hello концентратора событий), преобразование (toolook запроса hello мошеннические вызовов) и выход (хранилище больших двоичных объектов). Теперь вы можете запустить задание hello. 

1. Убедитесь, что приложение hello TelcoGenerator выполняется.

2. В колонке hello задания, нажмите кнопку **запустить**.

    ![Запустить задание Stream Analytics hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. В hello **запуска задания** колонке для вывода время запуска задания, выберите **теперь**. 

4. Нажмите **Запуск**. 

    ![Колонка «Запустить задание» для задания Stream Analytics hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure уведомляет о запуска задания hello и в колонке задания hello hello состояние отображается как **под управлением**.

    ![Состояние задания Stream Analytics, отображающее состояние "Выполнение"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Проверьте данные преобразуются hello

Теперь у вас есть готовое задание Streaming Analytics. Hello задания проверки потока метаданных телефонный звонок, поиск мошеннические телефонные звонки в режиме реального времени и записи информации об этих toostorage мошеннические вызовы. 

toocomplete этого учебника вы можете toolook hello данных, записанных задание Streaming Analytics hello. данные Hello записывается tooAzure хранилища больших двоичных фрагментами (файлы). Вы можете использовать любое средство, считывающее хранилище BLOB-объектов Azure. Как упоминалось в разделе предварительных требований hello, можно использовать расширения Azure в Visual Studio, или можно воспользоваться инструментом [обозреватель хранилищ Azure](http://storageexplorer.com/) или [обозреватель Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

При проверке hello содержимое файла в хранилище больших двоичных объектов, появится примерно hello следующим образом:

![Хранилище BLOB-объектов Azure с выходными данными Streaming Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Очистка ресурсов

У нас есть дополнительные статьи, продолжите hello мошенничества сценарии, которые используют ресурсы hello, созданные в этом учебнике. Следует toocontinue просмотра предложений hello под **дальнейшие действия** позже.

Тем не менее если не требуется hello ресурсы, которые вы создали завершения, их можно удалить, чтобы вы не взимается ненужные Azure. В этом случае мы предлагаем, что hello следующие:

1. Остановите задание Streaming Analytics hello. В hello **заданий** колонка, щелкните **остановить** вверху hello.
2. Остановите приложение hello Telco генератора. В окне команд hello первоначальное приложение hello нажмите Ctrl + C.
3. Если вы создали новую учетную запись хранения BLOB-объектов только для работы с этим руководством, удалите ее. 
4. Удалите задание Streaming Analytics hello.
5. Удаление концентратора событий hello.
6. Удалите пространство имен концентратора событий hello.

## <a name="get-support"></a>Получение поддержки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

Этот учебник можно будет продолжить hello в следующих статьях:

* [Stream Analytics и Power BI. Панель мониторинга для анализа потоковой передачи данных](stream-analytics-power-bi-dashboard.md). В этой статье показано, как toosend hello выходные данные TelCo hello Stream Analytics задания tooPower бизнес-Аналитики для визуализации в режиме реального времени и анализа.
* [Как toostore данные из Azure Stream Analytics в кэше Redis для Azure с помощью функций Azure](stream-analytics-functions-redis.md). В этой статье показано, как мошеннические toowrite функции Azure toouse вызывает tooan кэша redis для Azure — с помощью очереди Service Bus.

Узнать больше о Stream Analytics в целом вы можете с помощью следующих ресурсов:

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
