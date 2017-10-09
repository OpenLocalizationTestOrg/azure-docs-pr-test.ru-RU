---
title: "Углубленное aaaDeep прогнозирования vehicle работоспособности и управление им привычки - Azure | Документы Microsoft"
description: "Использовать возможности hello toogain Cortana аналитики в реальном времени и прогнозной аналитики на автомобиль работоспособности и пешком привычки."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Аналитика решения транспортных средств телеметрии репертуара: глубокое погружение в решение hello
Это **меню** связывает этот репертуара toohello разделы: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Этот раздел детализируется углублением каждого из этапов hello, используемые в hello архитектура решения инструкции и указания для настройки. 

## <a name="data-sources"></a>Источники данных
Hello решение использует два различных источников данных:

* **имитированные сигналы автомобиля и набор диагностических данных** ; 
* **каталог автомобилей.**

В это решение входит симулятор телематики автомобиля. Он выдает диагностических сведений и уведомляет соответствующее состояние toohello hello vehicle и toohello пешком шаблон в определенный момент времени. Нажмите кнопку [симулятор Vehicle Telematics](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **решение Visual Studio Vehicle Telematics симулятор** для настройки в соответствии с вашими требованиями. каталог vehicle Hello содержит сопоставление toomodel VIN эталонного набора данных.

![Симулятор телематики автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Рис. 1. Симулятор телематики автомобиля*

Это формата JSON набора данных, содержащий hello следующие схемы.

| столбец | Описание | Значения |
| --- | --- | --- |
| VIN |Случайно сгенерированный идентификационный номер автомобиля |Его можно получить из главного списка 10 000 случайно сгенерированных идентификационных номеров автомобилей |
| outsideTemperature |Hello за пределами температуры, где пешком hello vehicle |Случайно сгенерированное число от 0 до 100 |
| engineTemperature |Hello температуру ядра hello vehicle |Случайно сгенерированное число от 0 до 500 |
| Speed |скорость Hello, влияющие на какие hello транспортного средства |Случайно сгенерированное число от 0 до 100 |
| fuel |уровень топлива Hello hello vehicle |Случайно сгенерированное число от 0 до 100 (указывает уровень топлива в процентах) |
| engineoil |уровень нефти engine Hello hello vehicle |Случайно сгенерированное число от 0 до 100 (указывает уровень моторного масла в процентах) |
| Давление в шинах |загрузку велосипеда Hello hello vehicle |Случайно сгенерированное число от 0 до 50 (указывает уровень давления в шинах в процентах) |
| odometer |считывание одометра Hello hello vehicle |Случайно сгенерированное число от 0 до 200 000 |
| accelerator_pedal_position |Hello сочетаний клавиш педали положение hello vehicle |Случайно сгенерированное число от 0 до 100 (указывает уровень, соответствующий положению педали газа, в процентах) |
| parking_brake_status |Указывает ли hello vehicle выполнены в нерабочем или нет |Значение true или false |
| headlamp_status |Указывает, где Прожектор hello на или нет |Значение true или false |
| brake_pedal_status |Указывает, нажата ли педаль тормоза hello |Значение true или false |
| transmission_gear_position |положение шестеренки передачи Hello hello vehicle |Состояния: first, second, third, fourth, fifth, sixth, seventh, eighth |
| ignition_status |Указывает, является ли hello vehicle запущенной или остановленной |Значение true или false |
| windshield_wiper_status |Указывает, включено ли wiper ветровое hello |Значение true или false |
| ABS |Указывает, включена ли антиблокировочная система тормозов |Значение true или false |
| Timestamp |Hello отметка времени, когда создается точка данных hello |Дата |
| City |расположение Hello hello vehicle |В этом решении представлены 4 города: Бельвью, Редмонд, Саммамиш и Сиэтл |

Hello vehicle модели эталонный набор данных содержит сопоставление модели VIN toohello. 

| VIN | Модель |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Седан |
| 8J0U8XCPRGW4Z3NQE |Гибридная среда |
| WORG68Z2PLTNZDBI7 |Семейный седан |
| JTHMYHQTEPP4WBMRN |Седан |
| W9FTHG27LZN1YWO0Y |Гибридная среда |
| MHTP9N792PHK08WJM |Семейный седан |
| EI4QXI2AXVQQING4I |Седан |
| 5KKR2VB4WHQH97PF8 |Гибридная среда |
| W9NSZ423XZHAONYXB |Семейный седан |
| 26WJSGHX4MA5ROHNL |Автомобиль с откидным верхом |
| GHLUB6ONKMOSI7E77 |Автомобиль с кузовом «универсал» |
| 9C2RHVRVLMEJDBXLP |Малогабаритный автомобиль |
| BRNHVMZOUJ6EOCP32 |Небольшой внедорожник |
| VCYVW0WUZNBTM594J |Спортивный автомобиль |
| HNVCE6YFZSA5M82NY |Внедорожник среднего размера |
| 4R30FOR7NUOBL05GJ |Автомобиль с кузовом «универсал» |
| WYNIIY42VKV6OQS1J |Большой внедорожник |
| 8Y5QKG27QET1RBK7I |Большой внедорожник |
| DF6OX2WSRA6511BVG |Двухместный легковой автомобиль |
| Z2EOZWZBXAEW3E60T |Седан |
| M4TV6IEALD5QDS3IR |Гибридная среда |
| VHRA1Y2TGTA84F00H |Семейный седан |
| R0JAUHT1L1R3BIKI0 |Седан |
| 9230C202Z60XX84AU |Гибридная среда |
| T8DNDN5UDCWL7M72H |Семейный седан |
| 4WPYRUZII5YV7YA42 |Седан |
| D1ZVY26UV2BFGHZNO |Гибридная среда |
| XUF99EW9OIQOMV7Q7 |Семейный седан |
| 8OMCL3LGI7XNCC21U |Автомобиль с откидным верхом |
| ……. | |

### <a name="references"></a>Ссылки
[Решение Visual Studio "Симулятор телематики автомобиля"](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Концентратор событий Azure](https://azure.microsoft.com/services/event-hubs/)

[Фабрика данных Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Прием
Комбинация концентраторов событий Azure Stream Analytics и фабрики данных является hello vehicle использовать tooingest сигналов, hello события диагностики и в режиме реального времени и пакетной аналитике. Все эти компоненты создаются и настраиваются как часть развертывания решения hello. 

### <a name="real-time-analysis"></a>Анализ в режиме реального времени
Hello события, создаваемые hello симулятор Telematics Vehicle публикуются toohello концентратора событий с помощью пакета SDK концентратор событий "hello". Задание Stream Analytics Hello принимает эти события из концентратора событий hello и процессы hello данные в реальном времени tooanalyze hello vehicle работоспособности. 

![Панель мониторинга концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Рис. 4. Панель мониторинга концентратора событий*

![Обработка данных заданием Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Рис. 5. Обработка данных заданием Stream Analytics*

Задание Stream Analytics Hello;

* принимает данные из hello концентратора событий 
* выполняется соединение с hello ссылка toomap hello vehicle VIN toohello соответствующей модели данных 
* сохраняет эти данные в хранилище BLOB-объектов для расширенного пакетного анализа. 

приветствия при следующем запросе Stream Analytics является данных используется toopersist hello в хранилище больших двоичных объектов. 

![Запрос задания Stream Analytics для приема данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Рис. 6. Запрос задания Stream Analytics для приема данных*

### <a name="batch-analysis"></a>Пакетный анализ
Для расширенного пакетного анализа необходимо создать дополнительное количество имитированных сигналов автомобиля и набор диагностических данных. Это обязательный tooensure тома хорошо репрезентативных данных для пакетной обработки. Для этой цели используется конвейер с именем «PrepareSampleDataPipeline» в рабочий процесс toogenerate hello фабрики данных Azure за один год имитацию vehicle сигналов и набор диагностических данных. Нажмите кнопку [фабрики данных пользовательского действия](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello пользовательское действие DotNet решения Visual Studio для настройки фабрики данных на основе требований. 

![Подготовка образца данных для рабочего процесса пакетной обработки](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Рис. 7. Подготовка образца данных для рабочего процесса пакетной обработки*

конвейер Hello состоит из пользовательских .net ADF действия, здесь показаны:

![Действие PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Рис. 8. PrepareSampleDataPipeline*

После конвейера hello выполняется успешно и набор данных «RawCarEventsTable» помечен «Готово», один год стоит имитацию vehicle сигналов и диагностических данных создаются. Вы видите следующее hello папок и файлов, созданных в учетной записи хранения в контейнере «connectedcar» hello:

![Выходные данные PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Рис. 9. Выходные данные PrepareSampleDataPipeline*

### <a name="references"></a>Ссылки
[Пакет SDK концентратора событий Azure для приема потока](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md)
[Использование настраиваемых действий в конвейере фабрики данных Azure](../data-factory/data-factory-use-custom-activities.md)

[Решение Visual Studio "Действие DotNet фабрики данных Azure" для подготовки примера данных](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Разделение набора данных hello
сигналы необработанные полуструктурированные vehicle Hello и набор диагностических данных секционируются на этапе подготовки данных hello в формат года и МЕСЯЦА. Такое секционирование обеспечивает более эффективно опрашивать и масштабируемых долговременного хранения, позволяя сбоя переход из одного большого двоичного объекта учетной записи toohello Далее hello первой учетной записи может заполниться до конца. 

>[!NOTE] 
>Этот шаг в решении hello является применимо только toobatch обработки.

Управление входными и выходными данными:

* Hello **выходных данных** (с меткой *PartitionedCarEventsTable*) toobe сохраняется длительное время как hello фундаментальные / «rawest» формы данных в hello клиента» Озера данных». 
* Hello **входные данные** конвейера toothis бы обычно удаляется как hello выходных данных имеет toohello полноценная входных данных — просто хранится (секционировать) лучше для последующего использования.

![Рабочий процесс секционирования событий автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Рис. 10. Рабочий процесс секционирования событий автомобиля*

Hello необработанные данные секционируются с использованием действия Hive HDInsight в «PartitionCarEventsPipeline». Hello образец данных, созданного на шаге 1 за год, секционирована по года и МЕСЯЦА. Hello разделы являются используется toogenerate vehicle сигналов и диагностических данных для каждого месяца (всего 12 разделов) года. 

![Действие PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Рис. 11. PartitionCarEventsPipeline*

***Сценарий Hive PartitionConnectedCarEvents***

Hello следующий сценарий Hive, с именем «partitioncarevents.hql» используется для секционирования и находится в папке «\demo\src\connectedcar\scripts» hello hello загружен zip. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.

![Секционированные выходные данные](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Рис. 12. Секционированные выходные данные*

Hello данных теперь оптимизирован, управляемость и готов для дальнейшей обработки toogain широкие возможности пакета аналитики. 

## <a name="data-analysis"></a>Анализ данных
В этом разделе, показано, как расширенный toocombine Azure Stream Analytics, машинного обучения Azure, фабрики данных Azure и Azure HDInsight для форматированного привычки аналитика на автомобиль работоспособности и управление им. Здесь содержатся три подраздела:

1. **Машинное Обучение**: в этом подразделе рассказывается о эксперимента обнаружение аномалий hello, мы использовали в это решение toopredict автомобилей, требующие обслуживания, обслуживания и средств, требующие попыток из-за проблем с toosafety.
2. **В режиме реального времени анализа**: в этом подразделе содержит сведения о аналитики hello в реальном времени с помощью hello язык запросов Stream Analytics и ввод в эксплуатацию hello машинного обучения поэкспериментировать в режиме реального времени с помощью пользовательского приложения.
3. **Анализ пакета**: этот подраздел содержит сведения, касающиеся hello, преобразования и обработки данных пакета hello, с помощью Azure HDInsight и машинного обучения Azure, введенную фабрикой данных Azure.

### <a name="machine-learning"></a>Машинное обучение
Наша цель — toopredict hello автомобилей, требующие обслуживания или отзыв на основе определенных состоянием статистики. Корпорация Microsoft hello, следуя предположения

* Если один из следующих трех условий hello верны, требуют hello автомобилей **обслуживания обслуживания**:
  
  * низкое давление в шине;
  * низкий уровень моторного масла;
  * высокая температура двигателя.
* Если одно из следующих условий hello имеют значение true, возможно, hello автомобилей **проблему безопасности** и требуют **отзыва**:
  
  * высокая температура двигателя, но низкая наружная температура;
  * низкая температура двигателя, но высокая наружная температура.

В зависимости от требований предыдущих hello, мы создали аномалий toodetect две отдельные модели, один для обнаружения транспортного средства обслуживания и один для обнаружения транспортного средства повторного вызова. В обоих этих моделей hello встроенный алгоритм анализа главных компонентов (PCA) используется для обнаружения аномалий. 

**Модель определения необходимости в обслуживании**

Если один из трех индикаторов - нагрузка для велосипеда, нефти engine или температуры ядра - удовлетворяет его соответствующие условию, модель обнаружения обслуживания hello сообщает аномалий. В результате нам требуется только tooconsider эти три переменные для построения модели hello. В нашем эксперименты в машинном обучении Azure, сначала используется **Выбор столбцов в наборе данных** модуль tooextract эти три переменные. Далее мы используем hello аномалий на основе PCA обнаружения модуль toobuild hello модель обнаружения аномалий. 

Анализ главных компонентов (PCA) — это общепринятая методика машинного обучения, который может быть применен toofeature выбора, классификации и аномалий обнаружения. Этот тип анализа предусматривает преобразование набора сценариев с предположительно коррелированными переменными в набор значений, которые называются основными компонентами. Идея ключа Hello моделирования на основе PCA данные tooproject на нижнем мерный пространство, чтобы компоненты и аномалии, можно легко определить.

Для каждого нового входного слишком hello модель обнаружения, обнаружения аномалий hello сначала вычисляет его проекции на собственных векторов hello, а затем вычисляет hello нормализовать реконструкции ошибки. Нормализованный ошибки, оценка аномалий hello. Ошибка выше hello Hello, hello более hello экземпляр является. 

В проблема обнаружения обслуживания hello каждая запись можно считать, что точки в пространстве с 3-мерная определяется велосипеда давление, engine нефти и температуры ядра координатами. toocapture эти аномалии мы проекта hello исходных данных в пространстве объемного hello на двухмерного пространство с помощью PCA. Таким образом рекомендуется задать для параметра hello количество компонентов toouse в PCA toobe 2. Этот параметр играет важную роль в обнаружении аномалий на основе анализа главных компонентов. Спроецировав данные с использованием этого анализа, определить соответствующие аномалии намного проще.

**Модель обнаружения аномалий выборка** в модели обнаружения аномалий выборка hello, мы используем hello Выбор столбцов в наборе данных и аномалий на основе PCA модулей обнаружения аналогичным образом. В частности, мы сначала извлечь три переменные - температуры ядра, вне температуры и скорости — с помощью hello **Выбор столбцов в наборе данных** модуля. Также мы включаем скорость hello переменной, поскольку обычно является температуры ядра hello коррелированных toohello скорости. Далее мы используем данные hello tooproject модуля обнаружения аномалий на основе PCA из 3-мерная пространства hello на двухмерного пространство. удовлетворяются условия отзыва Hello и hello vehicle требует повторного вызова при температуры ядра и внешними температуры высокой отрицательно связаны. Используя алгоритм обнаружения аномалий на основе PCA, можно свести аномалий hello после выполнения PCA. 

При обучении любой модели, нам нужна обычные данные toouse, которая не требует обслуживания или отзыве как модель обнаружения аномалий на основе PCA hello tootrain hello входных данных. В hello оценки экспериментов мы используем toodetect модели обнаружения аномалий hello обучена ли hello vehicle требуется обслуживание или отзыва. 

### <a name="real-time-analysis"></a>Анализ в режиме реального времени
использовать следующие SQL запросов Stream Analytics Hello tooget hello среднее всех hello важным средством таких параметров, как vehicle скорость, уровень топлива, температуры ядра, одометра чтения, нехватку велосипеда, нефти уровня ядра и другим пользователям. Hello средние значения, используемые toodetect аномалий, выдавать предупреждения, а также определить hello общей работоспособности условий эксплуатации в определенном регионе автомобилей и сопоставить его toodemographics. 

![Запрос Stream Analytics для обработки в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Рис. 13. Запрос Stream Analytics для обработки в реальном времени*

Средние значения все hello вычисляются TumblingWindow 3 секунды. Мы применили TubmlingWindow, так как необходимо использовать непересекающиеся последовательные интервалы времени. 

Щелкните toolearn Дополнительные сведения о всеми возможностями «Над окнами» hello в Azure Stream Analytics [управления окнами (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Прогнозирование в режиме реального времени**

Приложение включен в состав решения toooperationalize hello машинного обучения модели hello в реальном времени. Это приложение, называется «RealTimeDashboardApp» создается и настраивается в ходе развертывания решения hello. приложение Hello выполняет hello следующее:

1. Выполняет прослушивание экземпляр tooan концентратора событий, где Stream Analytics публикация hello событий в шаблоне постоянно. ![Запросов Stream Analytics для публикации данных hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *рис. 14 – запросов Stream Analytics для публикации данных tooan hello вывода экземпляра концентратора событий* 
2. Для каждого события, которое получает это приложение: 
   
   * Процессы hello данные с помощью машины оценки запроса-ответа обучения (RR) конечной точки. Конечная точка Hello записей Ресурсов, автоматически публикуется как часть развертывания hello.
   * выходные данные записи Ресурсов Hello — опубликованных tooa набора данных Power BI с помощью принудительной hello API-интерфейсы.

Этот шаблон также является применимо tooscenarios, в котором нужно toointegrate строке из бизнес-приложения с потоком hello аналитика в реальном времени, для сценариев, таких как оповещения, уведомления и обмена сообщениями.

Нажмите кнопку [RealtimeDashboardApp загрузки](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello решения RealtimeDashboardApp Visual Studio для настройки. 

**hello tooexecute приложении панели мониторинга в реальном времени**
1. Извлеките его и сохраните на локальном компьютере ![Папка RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Рис. 16. Папка RealtimeDashboardApp*  
2. Выполните приложение hello RealtimeDashboardApp.exe
3. Укажите действительные учетные данные Power BI, войдите и нажмите кнопку "Принять". ![Панель мониторинга в реальном времени приложения вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Приложение с панелью мониторинга в реальном времени окончания tooPower входа бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Рисунок 17 — RealtimeDashboardApp: Вход tooPower бизнес-Аналитики*

>[!NOTE] 
>Если вы хотите tooflush набора данных Power BI hello, выполните hello RealtimeDashboardApp с параметром «flushdata» hello: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Пакетный анализ
Hello цель — tooshow как Contoso моторов использует hello вычислений Azure возможности tooharness больших данных toogain подробные сведения о на шаблон, использование поведения и работоспособности автомобиля. Это позволяет:

* Повышение качества hello и сделать его дешевле, предоставляя аналитические данные на привычки и топливо эффективный определяющим поведения
* Ознакомьтесь с заранее клиентов и определяющим шаблонов toogovern бизнес-решения и предоставьте hello лучше всего в класс продукты и услуги

В данном решении мы ожидаем hello следующие метрики:

1. **Агрессивная пешком поведение**: Определяет тренд hello hello моделей, расположения, определяющим условия и время средств анализа toogain год hello агрессивной определяющим шаблонов. Contoso Motors сможет использовать ее в маркетинговых кампаниях, чтобы предлагать новые персонализированные функции и умное страхование.
2. **Задают ритм для эффективного определяющим поведение**: Определяет тренд hello hello моделей, расположения, определяющим условия и время hello аналитики toogain год на топливо эффективный определяющим шаблонов. Contoso моторов можно использовать эти знания для маркетинговых кампаний, пешком новые функции и упреждающее отчетов toohello драйверы для стоимости начала и среде понятное определяющим привычки. 
3. **Отозвать моделей**: Определяет моделей требуется отзывы, ввод в эксплуатацию эксперимента машинного обучения для обнаружения аномалий hello

Давайте посмотрим hello Дополнительные сведения о каждой из этих метрик

**Шаблон агрессивного вождения**

Hello секционированы vehicle сигналов и диагностических данных обрабатываются в конвейере hello с именем «AggresiveDrivingPatternPipeline» с использованием моделей hello toodetermine Hive, расположение, автомобиль, пешком условия и другие параметры, которые видно агрессивной определяющим шаблон.

![Рабочий процесс для шаблона агрессивного вождения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Рис. 18. Рабочий процесс для шаблона агрессивного вождения*


***Запрос Hive для шаблона агрессивного вождения***

Hello скрипта Hive с именем «aggresivedriving.hql», используемое для анализа агрессивной определяющим условие шаблон находится в папке «\demo\src\connectedcar\scripts» hello загружен zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Она использует сочетание hello автомобилей передачи шестеренки позиции, педали состояние тормоза и скорость toodetect бы безрассудным/агрессивной пешком поведение в зависимости от тормозным шаблон с высокой скоростью. 

После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.

![Выходные данные AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Рис. 19. Выходные данные AggressiveDrivingPatternPipeline*

**Шаблон вождения для экономии топлива**

Hello секционированы vehicle сигналов и диагностических данных обрабатываются в конвейере hello с именем «FuelEfficientDrivingPatternPipeline». Куст — моделей используется toodetermine hello, расположение, vehicle, определяющим условия и другие свойства, которые демонстрировал топливо эффективный определяющим.

![Шаблон вождения для экономии топлива](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Рис. 20. Рабочий процесс для шаблона вождения, позволяющего экономить топливо*

***Запрос Hive для шаблона вождения, позволяющего экономить топливо***

Hello скрипта Hive с именем «fuelefficientdriving.hql», используемое для анализа агрессивной определяющим условие шаблон находится в папке «\demo\src\connectedcar\scripts» hello загружен zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Он использует сочетание hello передачи шестеренки положение автомобилей, тормоза педали состояния, скорость и сочетаний клавиш педали позиции toodetect топливо эффективный определяющим поведение на основании ускорение, тормозным, и ускорить шаблонов. 

После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.

![Выходные данные FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Рис. 21. Выходные данные FuelEfficientDrivingPatternPipeline*

**Прогнозы для отзыва**

Подготовленная и опубликованы как веб-службы в ходе развертывания решения hello Hello эксперимента машинного обучения. Hello массовой оценки конечной точки используется в этом рабочем процессе, регистрируются в качестве данных связанной службы фабрики и введенную, используя действие оценки пакета фабрики данных.

![Конечная точка машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Рис. 22. Конечная точка машинного обучения, зарегистрированная в качестве связанной службы в фабрике данных*

Hello зарегистрированной связанной службы используется в hello DetectAnomalyPipeline tooscore hello данных с помощью модели обнаружения аномалий hello. 

![Пакетная оценка в фабрике данных в рамках Машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Рис. 23. Пакетная оценка в фабрике данных в рамках Машинного обучения Azure* 

Существуют несколько шагов, выполненных в этом конвейере для подготовки данных, чтобы его можно введенную с hello массовой оценки веб-службы. 

![DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Рис. 24. DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей* 

***Запрос Hive для обнаружения аномалий***

После завершения оценки hello действие HDInsight — используется tooprocess и hello статистические данные, которые классифицируются как аномалии hello модели с оценкой вероятности 0.60 или выше.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.

![Выходные данные DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Рис. 25. Выходные данные DetectAnomalyPipeline*

## <a name="publish"></a>Опубликовать

### <a name="real-time-analysis"></a>Анализ в режиме реального времени
Один из запросов hello в задании Stream Analytics hello публикует выход tooan hello события экземпляра концентратора событий. 

![Задание Stream Analytics публикует выход tooan экземпляра концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Рис. 26 — задание Stream Analytics публикует выход tooan экземпляра концентратора событий*

![Stream Analytics запроса toopublish toohello вывода экземпляра концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Рис. 27 — экземпляр концентратора событий вывода toohello toopublish запросов Stream Analytics*

Этот поток событий используются hello RealTimeDashboardApp, включенный в решении hello. Это приложение использует hello машины обучения запрос-ответ веб-службы для оценки в режиме реального времени и публикует hello результирующие данные tooa Power BI набор данных для потребления. 

### <a name="batch-analysis"></a>Пакетный анализ
результаты Hello hello пакета и в режиме реального времени обработки, toohello опубликованных таблиц базы данных SQL Azure для потребления. Hello Azure SQL Server, базы данных и таблицы hello автоматически создаются как часть сценария установки hello. 

![Результаты пакетной обработки скопировать рабочий процесс Киоск toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Рис. 28 – пакетной обработки toodata Киоск результаты копирование рабочего процесса*

![Задание Stream Analytics публикует toodata киоска](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Рис. 29 — задание Stream Analytics публикует toodata киоска*

![Настройка киоска данных в задании Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Рис. 30. Настройка киоска данных в задании Stream Analytics*

## <a name="consume"></a>Использование
Power BI предоставляет для этого решения расширенную панель мониторинга, предназначенную для визуализации данных в режиме реального времени и прогнозной аналитики. 

Подробные инструкции по настройке hello Power BI отчеты и панели мониторинга hello, щелкните здесь. Окончательный мониторинга Hello выглядит следующим образом:

![Информационная панель Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Рис. 31. Информационная панель Power BI*

## <a name="summary"></a>Сводка
Этот документ содержит подробные детализация hello решения для анализа телеметрии автомобиля. Здесь показан шаблон лямбда-архитектуры для анализа в режиме реального времени и пакетного анализа с прогнозами и действиями. Эта схема применяется tooa разнообразные варианты использования, которые требуют Горячий путь (в реальном времени) и аналитика холодного путь (пакет). 

