---
title: "Интеграция Stream Analytics и машинное обучение aaaAzure | Документы Microsoft"
description: "Как toouse определяемой пользователем функции и машинного обучения в задании Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Выполнение анализа тональности с помощью Azure Stream Analytics и Машинного обучения Azure
В этой статье описывается настройка для простого задания Azure Stream Analytics, который интегрирует машинного обучения Azure tooquickly. Используйте модель машинного обучения мнений analytics из hello коллекции аналитики Cortana tooanalyze потоковой передачи текстовых данных и определения мнений hello в режиме реального времени. С помощью hello Cortana аналитики Suite позволяет выполнения этой задачи, не беспокоясь о особенностей hello построение модели анализа мнений.

Полученные знания можно применить из этой статьи tooscenarios такие:

* при анализе тональности в режиме реального времени в потоковых данных Twitter;
* при анализе записей разговоров клиента со специалистами службы поддержки;
* при оценке комментариев на форумах, в блогах и видео; 
* а также во многих других сценариях прогнозной оценки в реальном времени.

В реальном сценарии получаемому hello данных непосредственно из потока данных Twitter. toosimplify hello учебнике мы написали его, чтобы hello задание Streaming Analytics возвращает твиты из CSV-файла в хранилище больших двоичных объектов Azure. Можно создать CSV-файл, или можно использовать пример CSV-файла, как показано в hello после изображения:

![пример твитов в CSV-файле](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

Задание Streaming Analytics Hello, создаваемом применяется модель анализа мнений hello определяемой пользователем функции (UDF) на hello образца текстовых данных из хранилища больших двоичных объектов hello. Hello (hello результат анализа мнений hello) записываться toohello одного хранилища BLOB-объекта в другой файл CSV. 

Hello на рисунке ниже демонстрируется этой конфигурации. Как указано, для повышения реалистичности сценария элемент ввода для хранилища BLOB-объектов можно заменить потоковыми данными Twitter из элемента ввода концентраторов событий Azure. Кроме того, можно построить [Microsoft Power BI](https://powerbi.microsoft.com/) в режиме реального времени визуализацию статистических мнений hello.    

![Обзор интеграции машинного обучения в Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать, убедитесь, что у вас есть следующие hello:

* Активная подписка Azure.
* CSV-файл с данными. Вы можете скачать файл hello, показанного выше из [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), или можно создать свой собственный файл. В этой статье мы предполагаем, что вы используете файл hello из GitHub.

На высоком уровне toocomplete hello задачи, описанные в этой статье вы hello следующие:

1. Создайте учетную запись хранилища Azure и контейнер хранилища больших двоичных объектов и отправьте контейнер toohello входной файл в формате CSV.
3. Добавьте модель анализа мнений hello коллекции аналитики Cortana tooyour машинного обучения Azure рабочей и развернуть эту модель в качестве веб-службы в рабочей области машинного обучения hello.
5. Создайте задание Stream Analytics, которое вызывает веб-службу в качестве функции спада toodetermine заказа для ввода текста hello.
6. Запустить задание Stream Analytics hello и проверьте выходные данные hello.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Создать контейнер хранилища и передачи входного файла CSV hello
Для выполнения этого шага можно использовать любой CSV-файла, например hello один, доступный из GitHub.

1. В hello портал Azure, щелкните **New** &gt; **хранения** &gt; **учетной записи хранилища**.

   ![создание новой учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Введите имя (`samldemo` в примере hello). Имя Hello можно использовать только строчные буквы и цифры и должно быть уникальным среди Azure. 

3. Укажите существующую группу ресурсов и расположение. Для расположения, мы рекомендуем, все ресурсы hello, созданные в данном руководстве используйте hello же расположение.

    ![указание сведений об учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. В hello портал Azure выберите учетную запись хранения hello. В колонке hello учетной записи хранилища щелкните **контейнеры** и нажмите кнопку  **+ &nbsp;контейнера** toocreate хранилища больших двоичных объектов.

    ![создание контейнера больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Введите имя для контейнера hello (`azuresamldemoblob` в примере hello) и убедитесь, что **тип доступа** задано слишком**большого двоичного объекта**. Закончив, нажмите кнопку **OK**.

    ![указание сведений о контейнере больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. В hello **контейнеры** колонки, выберите hello новый контейнер, который открывает колонку hello для этого контейнера.

7. Щелкните **Отправить**.

    ![Кнопка передачи для контейнера](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. В hello **передачи BLOB-объекта** колонке укажите hello CSV-файла, что требуется toouse для этого учебника. Для **больших двоичных объектов типа**выберите **блочного BLOB-объекта** и набор hello блока размером too4 МБ, что вполне достаточно для этого учебника.

    ![отправка файла большого двоичного объекта](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Нажмите кнопку hello **отправить** кнопку в нижней части hello колонка hello.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Добавить модель анализа мнений hello из коллекции аналитики Cortana hello

Теперь, когда данные образца hello в большом двоичном объекте, можно включить модели анализа мнений hello в коллекции Cortana аналитики.

1. Go toohello [мнений прогнозной модели analytics](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) страницы в коллекции Cortana аналитики hello.  

2. Щелкните **Открыть в Studio**.  
   
   ![Машинное обучение и Stream Analytics, открытие Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Войдите в рабочую область toohello toogo. Выберите расположение.

4. Нажмите кнопку **запуска** hello нижней части страницы приветствия. Здравствуйте выполнения процесса, который занимает около минуты.

   ![выполнение эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. После успешного выполнения процесса hello выберите **развертывание веб-службы** hello нижней части страницы приветствия.

   ![развертывание эксперимента как веб-службы в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate, hello модель analytics — Готово toouse мнений щелкните hello **тест** кнопки. Введите текст "Мне нравится Майкрософт". 

   ![проверка эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Если hello тест работает, появится примерно toohello результат, следующий пример:

   ![результаты проверки в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. В hello **приложения** столбец, щелкните hello **Excel 2010 или более ранних книги** toodownload ссылку книги Excel. Hello книга содержит ключ hello API и URL-адрес hello, необходимо более поздней версии tooset задание Stream Analytics hello.

    ![Машинное обучение и Stream Analytics, сводка](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Создать задание Stream Analytics, которое использует модель машинного обучения hello

Теперь можно создать задание Stream Analytics, считывающий твиты образец hello из hello CSV-файла в хранилище больших двоичных объектов. 

### <a name="create-hello-job"></a>Создание задания hello

1. Go toohello [портал Azure](https://portal.azure.com).  

2. Щелкните **Создать** > **"Интернет вещей"** > **Задание Stream Analytics**. 

   ![Azure портала путь для получения tooa новое задание Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Имя задания hello `azure-sa-ml-demo`укажите подписки, укажите существующую группу ресурсов или создайте новый и выберите расположение hello для задания hello.

   ![указание параметров для нового задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Настройка задания ввода hello
Задание Hello получает входные данные из CSV-файла hello, что был загружен ранее tooblob хранилища.

1. После задания hello будет создана, в разделе **топологии задания** в колонке задания hello щелкните hello **входов** поле.  
   
   ![Поле "Входные данные" в колонке задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. В hello **входов** колонка, щелкните **+ добавить**.

   ![Кнопка для добавления задания Stream Analytics ввода toohello «добавить»](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Заполните hello **вводимые** колонка со следующими значениями:

    * **Входной псевдоним**: hello используйте имя `datainput`.
    * **Тип источника**: выберите **Поток данных**.
    * **Источник**: выберите **Хранилище BLOB-объектов**.
    * **Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**. 
    * **Учетная запись хранения**: Выберите учетную запись хранения hello, созданную ранее.
    * **Контейнер**: Выберите hello контейнера, созданную ранее (`azuresamldemoblob`).
    * **Формат сериализации событий**: выберите **CSV**.

    ![Параметры для новых входных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Щелкните **Создать**.

### <a name="configure-hello-job-output"></a>Настройка выходных данных задания hello
Hello задания отправляет результаты toohello же хранилище, где он получает входные больших двоичных объектов. 

1. В разделе **топологии задания** в колонке задания hello щелкните hello **выходов** поле.  
  
   ![Создание новых выходных данных для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. В hello **выходов** колонка, щелкните **+ добавить**и затем добавить выход с псевдонимом hello `datamloutput`. 

3. Для поля **Приемник** выберите **Хранилище BLOB-объектов**. Затем заполните остальные hello hello выходных параметров с помощью hello одинаковые значения, которые используются для хранения больших двоичных объектов hello для входа:

    * **Учетная запись хранения**: Выберите учетную запись хранения hello, созданную ранее.
    * **Контейнер**: Выберите hello контейнера, созданную ранее (`azuresamldemoblob`).
    * **Формат сериализации событий**: выберите **CSV**.

   ![Параметры для новых выходных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Щелкните **Создать**.   


### <a name="add-hello-machine-learning-function"></a>Добавление функции машинного обучения hello 
Ранее вы опубликовали tooa веб-службы машинного обучения модели. В нашем сценарии анализа потока выполнения задания hello отправляет твит каждого образца из входного toohello hello веб-службы для анализа мнений. веб-службы машинного обучения Hello возвращает мнений (`positive`, `neutral`, или `negative`) и вероятность твит hello, положительным. 

В этом разделе учебника hello определить функцию в задание анализа потока hello. функции Hello можно вызванный toosend твит toohello веб-службы и вернуть ответ hello. 

1. Убедитесь, что у вас есть hello ключ веб-службе URL-адрес и API-интерфейса, загруженный ранее в книге Excel hello.

2. Возвращает колонку Обзор toohello задания.

3. В разделе **Параметры** выберите **Функции**, а затем нажмите кнопку **Добавить**.

   ![Добавить задание Stream Analytics toohello функции](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Введите `sentiment` как hello функцией псевдоним и заполнить rest hello колонка hello, используя следующие значения:

    * **Тип функции**: выберите **Машинное обучение Azure**.
    * **Метод импорта**: выберите **Импортировать из другой подписки**. Это дает возможность tooenter hello и URL-адрес и ключ.
    * **URL-адрес**: вставить в hello URL веб-службы.
    * **Ключ**: вставить в ключе hello API.
  
    ![Параметры для добавления задания Stream Analytics toohello функции машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Щелкните **Создать**.

### <a name="create-a-query-tootransform-hello-data"></a>Создание запроса данных hello tootransform

Stream Analytics использует вход hello tooexamine декларативный, основанный на SQL запроса и его обработки. В этом разделе создайте запрос, который считывает каждый твит из входных данных, а затем вызывает анализ мнений tooperform функции машинного обучения hello. запрос Hello затем отправляет результат toohello hello выходных данных определенного (хранилище больших двоичных объектов).

1. Возвращает колонку Обзор toohello задания.

2.  В разделе **топологии задания**, нажмите кнопку hello **запроса** поле.

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Введите приветствия при следующем запросе:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    Hello запрос вызывает функцию hello, созданную ранее (`sentiment`) в анализ мнений tooperform заказа для каждого твит во входном файле hello. 

4. Нажмите кнопку **Сохранить** toosave hello запроса.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Запустить задание Stream Analytics hello и проверьте выходные данные hello

Теперь вы можете запустить задание Stream Analytics hello.

### <a name="start-hello-job"></a>Запустить задание hello
1. Возвращает колонку Обзор toohello задания.

2. Нажмите кнопку **запустить** hello верхней части колонки hello.

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. В hello **запуска задания**выберите **настраиваемый**и выберите один день предыдущего toowhen загруженный хранилища tooblob файл CSV hello. После этого нажмите кнопку **Запуск**.  


### <a name="check-hello-output"></a>Проверьте выходные данные hello
1. Let hello задания, выполняемого на несколько минут, пока не увидите действия в hello **мониторинг** поле. 

2. Если у вас есть средство, обычно используемое содержимое hello tooexamine хранилища больших двоичных объектов, использовать этот инструмент tooexamine hello `azuresamldemoblob` контейнера. Кроме того hello шагов в hello портала Azure:

    1. На портале hello найти hello `samldemo` хранилища учетную запись, а в пределах учетной записи hello, найти hello `azuresamldemoblob` контейнера. Вы видите два файла в контейнере hello: hello файл, содержащий твиты образец hello и CSV-файла, созданные задания Stream Analytics hello.
    2. Щелкните правой кнопкой мыши файл создан hello, а затем выберите **загрузить**. 

   ![Скачивание выходных данных задания в виде CSV-файла из хранилища BLOB-объектов](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Привет открыть созданный CSV-файла. Можно наблюдать нечто похожее на следующий пример hello:  
   
   ![Машинное обучение и Stream Analytics, просмотр CSV-файла](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Просмотр метрик
Вы можете также просматривать метрики, связанные с функциями Машинного обучения Azure. Следующая функция метрик Hello отображаются в hello **мониторинг** поле в колонке hello задания:

* **Функции запросов** указывает hello число запросов, отправленных tooa веб-службы машинного обучения.  
* **Функция событий** указывает номер события в запросе hello hello. По умолчанию каждый запрос tooa веб-службы машинного обучения содержит до too1 000 событий.  


## <a name="next-steps"></a>Дальнейшие действия

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Интеграция машинного обучения в Stream Analytics](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)



