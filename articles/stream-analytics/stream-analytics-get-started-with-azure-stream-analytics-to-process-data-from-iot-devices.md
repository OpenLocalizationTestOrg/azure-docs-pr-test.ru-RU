---
title: "aaaIoT потоки данных в режиме реального времени и Azure Stream Analytics | Документы Microsoft"
description: "Теги и потоки данных датчиков IoT: обработка данных с использованием Stream Analytics в режиме реального времени"
keywords: "решение IoT, начало работы с IoT"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Начало работы с данными tooprocess Azure Stream Analytics с устройств IoT
В этом учебнике вы узнаете, как toocreate логика потока обработки toogather данные управляемых устройств Интернета вещей (IoT). Мы будем использовать реального мира, toodemonstrate вариантов Интернета вещей (IoT) используется как toobuild решение быстро и экономически.

## <a name="prerequisites"></a>Предварительные требования
* [Подписка Azure.](https://azure.microsoft.com/pricing/free-trial/)
* пример запроса и файлов данных, который можно скачать на сайте [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Сценарий
Contoso, являющийся компании в пространстве промышленное автоматическое hello, полностью автоматизировать его производственного процесса. механизмы Hello в это предприятие имеет датчиков, способные порождение потоков данных в режиме реального времени. В этом случае руководитель floor рабочей хочет toohave в реальном времени информацию из данных toolook hello датчика для шаблонов и предпринять действия на них. Мы будем использовать hello язык запросов Stream Analytics (SAQL) через интересующие шаблоны данных датчика toofind hello из hello входящего потока данных.

В этой статье описываются данные, созданные с помощью устройства Texas Instruments SensorTag.

![Texas Instruments SensorTag](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

Hello полезных данных hello в формате JSON и выглядит hello следующим образом:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

В реальном сценарии у вас могут быть сотни таких датчиков, создающих события в виде потока. В идеальном случае устройство шлюза запустит код toopush эти события слишком[концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) или [центры IoT Azure](https://azure.microsoft.com/services/iot-hub/). Задание Stream Analytics следует принять эти события из концентраторов событий и выполнять запросы в режиме реального времени к hello потоков. Затем можно отправлять tooone результаты hello объекта hello [поддерживается выходов](stream-analytics-define-outputs.md).

Для удобства в этом руководстве по началу работы приведен пример файла данных, полученных с реальных устройств SensorTag. Можно выполнять запросы по данным образец hello и просмотреть результаты. В последующих руководства вы узнаете, как tooconnect вашей tooinputs и выходные данные задания и развертывать их toohello службы Azure.

## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics
1. В hello [портал Azure](http://portal.azure.com), нажмите кнопку hello "плюс", а затем введите **STREAM ANALYTICS** окна toohello hello текста справа. Выберите **задания Stream Analytics** в списке результатов hello.
   
    ![Создание нового задания Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Введите уникальное имя и проверьте hello подписки hello правильный выбор для задания. Затем создайте новую группу ресурсов или выберите существующую в вашей подписке.
3. После этого выберите расположение для вашего задания. Скорость обработки и сокращения затрат в передаче данных, выбрав hello же расположении, что группа ресурсов hello и учетной записи хранения предполагаемого рекомендуется.
   
    ![Создание нового задания Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Для каждого региона необходимо создать только одну учетную запись хранения. Она будет совместно использоваться для всех заданий Stream Analytics, созданных в этом регионе.
   > 
   > 
4. Установите поле tooplace hello задания на информационной панели и нажмите кнопку **создать**.
   
    ![выполняется создание задания](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Вы увидите «начато развертывание...» отображается в правой верхней hello окна браузера. Скоро это приведет к изменению окна завершения tooa как показано ниже.
   
    ![выполняется создание задания](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Создание запроса Azure Stream Analytics
После задания создания tooopen времени его и построения запроса. Задание можно легко получить, щелкнув плитку hello для него.

![Плитка задания](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

В hello **топологии задания** области выберите hello **ЗАПРОСА** поле toogo toohello редактора запросов. Hello **ЗАПРОСА** редактор позволяет tooenter T-SQL-запрос, который выполняет преобразование «hello» по hello данных входящего события.

![Поле запроса](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Запрос: архивация необработанных данных
Hello простой формой запроса является запрос к серверу архивирует tooits всех входных данных, указанных выходных данных. Загрузить образец файла данных hello из [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa расположении на компьютере. 

1. Вставьте hello запрос из файла PassThrough.txt hello. 
   
    ![Проверка входного потока](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Нажмите кнопку Далее tooyour входных данных hello тремя точками и выберите **отправьте демонстрационные данные из файла** поле.
   
    ![Проверка входного потока](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Откроется область hello прямо в результате, в нем выберите hello HelloWorldASA InputStream.json в файле данных из загруженного папки и нажмите кнопку **ОК** hello нижней части панели hello.
   
    ![Проверка входного потока](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Нажмите кнопку hello **тестирования** шестеренки в hello верхней левой области окна hello и обработки запроса теста к hello образец набора данных. Окно результатов будет открыта ниже запроса hello Обработка завершена.
   
    ![Результаты проверки](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Запроса: Hello данных на основе условия фильтрации
Давайте попробуем toofilter hello результаты на основе условия. Мы хотели бы tooshow результаты только для тех событий, полученных от «sensorA». Hello запросов — в файле Filtering.txt hello.

![Фильтрация потока данных](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Обратите внимание, что hello регистр запросов сравнивает строковое значение. Нажмите кнопку hello **тест** шестеренки tooexecute hello запрос еще раз. Hello запрос должен возвращать 389 строк из 1860 события.

![Результаты второго вывода при проверке запроса](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Запрос: Предупреждения tootrigger рабочий процесс
Теперь давайте детализируем наш запрос. Для каждого типа датчика мы toomonitor средней температуры за 30 секунд и отобразить результаты только в том случае, если средней температуры hello превышает 100 градусов. Мы напишем ниже hello запроса и нажмите кнопку **тест** toosee hello результаты. Hello запросов — в файле ThresholdAlerting.txt hello.

![Запрос с 30-секундным фильтром](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Вы увидите результаты, содержащие только 245 строк и имен датчиков где среднее hello температур превышает 100. Этот запрос группирует hello поток событий, **dspl**, — имя датчика hello, более **"Переворачивающееся" окно** 30 секунд. Темпоральные запросы должно быть указано как мы хотим tooprogress времени. С помощью hello **TIMESTAMP BY** предложение, мы указали hello **OUTPUTTIME** раз tooassociate столбца с всех временных вычислений. Дополнительные сведения, прочтите статьи MSDN hello о [управление временем](https://msdn.microsoft.com/library/azure/mt582045.aspx) и [Ранжирующие функции](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Запрос: обнаружение отсутствия событий
Как мы пишут toofind запроса отсутствия входных событий? Давайте найти hello время последнего, что датчик отправил данные и затем не отправил события для hello следующей минуты. Hello запросов — в файле AbsenseOfEvent.txt hello.

![Обнаружение отсутствия событий](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Здесь мы используем **LEFT OUTER** join toohello и те же данные потока (самосоединение). При **внутреннем соединении** результат возвращается, только если обнаружено совпадение.  Для **LEFT OUTER** соединения, если события из hello слева от оператора hello соединения не совпадает, который имеет значение NULL для всех hello столбцы hello справа от оператора возвращается строка. Этот метод является полезным toofind отсутствие событий. Дополнительные сведения об условии [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx) см. в документации MSDN.

## <a name="conclusion"></a>Заключение
Hello этот учебник предназначен toodemonstrate отображением результатов различных запросов язык запросов Stream Analytics toowrite и см. в браузере hello. Тем не менее, это только начало работы. С помощью Stream Analytics можно сделать множество других действий. Stream Analytics поддерживает множество входов и выходов и можно даже использовать функции в машинном обучении Azure toomake его надежное средство для анализа потоков данных. Дополнительные сведения о Stream Analytics tooexplore можно запустить с помощью наших [карта обучения](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Дополнительные сведения о том, как запросы toowrite, узнайте, как статья hello [распространенными шаблонами запросов](stream-analytics-stream-analytics-query-patterns.md).

