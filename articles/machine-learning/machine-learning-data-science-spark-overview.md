---
title: "aaaOverview процесса обработки и анализа данных с помощью Spark на Azure HDInsight | Документы Microsoft"
description: "набор средств Spark MLlib Hello переводит существенное машинного обучения моделирования возможности распределенного toohello HDInsight среды."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Общие сведения об обработке и анализе данных с помощью платформы Spark в Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Этот набор разделов показано, как задачи toouse HDInsight Spark toocomplete общие обработки и анализа данных, такие как приема данных, конструируются, моделирования и вычисления моделей. Hello данные, используемые приводится образец hello 2013 NYC такси маршрута и тариф авиакомпании набора данных. Hello моделей, построенных включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев. Hello также показано, как toostore эти модели в Azure BLOB-объектов хранилища (WASB) и как tooscore и оценить их прогнозирования производительности. В более расширенных разделах рассматриваются способы обучения моделей с помощью перекрестной проверки и перебора гиперпараметров. В этом обзорном разделе также ссылается hello разделы, описывающие, каким образом tooset копирование hello кластера Spark, необходимые шаги hello toocomplete hello пошаговых руководств, приведенных. 

## <a name="spark-and-mllib"></a>Spark и MLlib
[Spark](http://spark.apache.org/) платформу параллельной обработки с открытым исходным кодом, поддерживающий в памяти обрабатывает tooboost hello производительность приложений для анализа больших данных. Подсистема обработки Spark Hello, созданную для скорости, простоте использования и сложные analytics. Возможности распределенных вычислений в памяти Spark лучше всего подходит для hello итеративный алгоритмы, используемые в вычислениях машины обучения и диаграммы. [MLlib](http://spark.apache.org/mllib/) Spark в масштабируемой машины обучения библиотека, которая переводит hello алгоритмической моделирования возможности toothis распределенной среде. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure размещается предложения из Spark с открытым исходным кодом. Она также включает поддержку **записные книжки Jupyter PySpark** на кластере Spark hello, можно запустить Spark SQL интерактивной обработки запросов для преобразования, фильтрации и наглядное представление данных, хранящихся в больших двоичных объектов Azure (WASB). PySpark — hello API Python для Spark. фрагменты кода Hello, которые обеспечивают hello и Показать hello соответствующие графики toovisualize hello данные здесь выполняются в записные книжки Jupyter установлен в кластерах Spark hello. шаги моделирования Hello в этих разделах содержат код, который показывает, как tootrain, вычисления, сохранения и использования каждого типа модели. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Настройка кластеров Spark и записных книжек Jupyter
Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6. Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0. Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их. Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark. Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь. Для удобства ниже приведены hello ссылки записные книжки Jupyter toohello для 1.6 Spark (выполняются в ядро pySpark hello hello server книжке Jupyter toobe) и 2.0 Spark (toobe запуска ядра pySpark3 hello объекта hello книжке Jupyter сервера).

### <a name="spark-16-notebooks"></a>Записные книжки для Spark 1.6
Эти портативные компьютеры являются toobe запуска ядра pySpark hello из блокнота jupyter.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): содержит сведения о том, как просмотр данных tooperform, моделирование и оценка с несколько разных алгоритмов.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит разделы в записной книжке №1 и варианты моделей с использованием настройки гиперпараметров и перекрестной проверки.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): показано, как toooperationalize сохраненную модель с помощью Python в HDInsight кластеров.

### <a name="spark-20-notebooks"></a>Записные книжки для Spark 2.0
Эти портативные компьютеры являются toobe запуска ядра pySpark3 hello из блокнота jupyter.

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): этот файл содержит сведения о как tooperform Просмотр данных, моделирования и оценки в Spark 2.0 кластеры, использующие hello trip такси NYC и набор данных тариф авиакомпании, описано [здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Записной книжки может быть хорошей отправной точкой для быстрого исследования кода hello, предоставленные для Spark 2.0. Для подробных записной книжки анализирует hello такси NYC данных, см. Далее записной книжки hello в этом списке. См. примечания hello ниже, сравнивающие эти портативные компьютеры. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello trip такси NYC и тариф авиакомпании набор данных описывается [ Здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello хорошо известных авиакомпании на время отправления набор данных на основе 2011 г. и 2012. Мы интегрировать dataset авиакомпании hello hello аэропорта погоды данных (например, windspeed, температуры, высота над уровнем моря т. д.) предыдущих toomodeling, эти функции погоды могут быть включены в модель hello.

<!-- -->

> [!NOTE]
> набор данных авиакомпании Hello был добавлен toohello Spark 2.0 записных книжек toobetter иллюстрируют использование hello алгоритмы классификации. См. следующие ссылки на сведения о набора данных на время отправления авиакомпании и набора данных погоды hello.

>- Данные о расписании вылетов авиакомпании: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Данные о погоде в аэропортах: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
записных книжек Spark 2.0 Hello на такси NYC hello и наборы авиакомпании рейса задержка данных может занять 10 минут или более toorun (в зависимости от размера hello кластер HDI). Hello первой записной книжки в hello над списком показаны различные аспекты hello исследования данных, визуализации и машинного Обучения моделей обучения в записной книжке, занимает меньше времени toorun уменьшается NYC набора данных, в которой hello такси и тариф авиакомпании файлы были предварительно присоединены к домену: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) записной книжки принимает более короткое время toofinish (2-3 минуты) и может быть это хорошая отправная точка для быстро анализ кода hello у нас есть обеспечивает Spark 2.0. 

<!-- -->

Рекомендации по ввода в эксплуатацию hello Spark 2.0 модели и модели потребления для оценки разделе hello [документа Spark 1.6 на потребление](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) пример структурирование hello шаги. toouse это 2.0 Spark, замените файл кода hello Python с [этот файл](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Предварительные требования
Hello следующих процедур, связанных tooSpark 1.6. Для версии Spark 2.0 hello записных книжек hello используйте описанные и связанных toopreviously. 

1. У вас должна быть подписка Azure. Если у вас ее нет, см. статью [о получении бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. необходимо toocomplete кластера Spark 1.6 в данном пошаговом руководстве. hello следуйте инструкциям в разделе toocreate, [приступить к работе: создание Apache Spark на Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). тип кластера Hello и версии указан из hello **Выбор типа кластера** меню. 

![Настройка кластера](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Раздел, показывающий выполнение задач по toouse toocomplete Scala, а не Python для процесса обработки и анализа данных с начала до конца, в разделе hello [обработки и анализа данных с помощью Scala с Spark на Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Hello такси 2013 NYC данных
Hello Trip такси NYC данных составляет около 20 ГБ файлы сжатых значений с разделителями запятыми (CSV) (~ 48 ГБ несжатого), включающего в себя более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута. Каждой записи маршрута включены отгрузки hello и истощение и времени, анонимные hack (драйвер) номер соглашения и номер medallion (уникальный идентификатор элемента такси). данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:

1. Hello «trip_data» CSV-файлы содержат обработки таких сведений, как количество пассажиров, взять и указывает dropoff, быть длительность и длина пути. Вот несколько примеров записей:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. CSV-файлы «trip_fare» Hello содержат подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты. Вот несколько примеров записей:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Образец 0,1% эти файлы и присоединены к домену hello trip перешли\_данных и обработки\_успешного CVS файлы в toouse один набор данных как hello входного набора данных в этом пошаговом руководстве. Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из полей hello: medallion hack\_лицензии и раскладки\_даты и времени. Каждая запись hello набор данных содержит следующие атрибуты, представляющий маршрут такси NYC hello:

| Поле | Краткое описание |
| --- | --- |
| medallion |Обезличенный медальон такси (уникальный идентификатор такси) |
| hack_license |Обезличенный номер лицензии такси |
| vendor_id |Идентификатор поставщика услуг такси |
| rate_code |Тариф на такси в Нью-Йорке |
| store_and_fwd_flag |Отметка записи и дальнейшей передачи |
| pickup_datetime |Дата и время посадки пассажира |
| dropoff_datetime |Дата и время высадки пассажира |
| pickup_hour |Час посадки пассажира |
| pickup_week |Взять неделя года hello |
| weekday |День недели (диапазон 1–7) |
| passenger_count |Количество пассажиров во время поездки на такси |
| trip_time_in_secs |Длительность поездки в секундах |
| trip_distance |Расстояние поездки в милях |
| pickup_longitude |Долгота места посадки пассажира |
| pickup_latitude |Широта места посадки пассажира |
| dropoff_longitude |Долгота высадки пассажира |
| dropoff_latitude |Широта высадки пассажира |
| direct_distance |Расстояние по прямой между местами посадки и высадки |
| payment_type |Тип оплаты (наличные, кредитная карта и т. д.) |
| fare_amount |Сумма к оплате |
| surcharge |Доплата |
| mta_tax |Налог MTA |
| tip_amount |Сумма чаевых |
| tolls_amount |Дорожные пошлины |
| total_amount |Общая сумма |
| tipped |Чаевые (0 — нет, 1 — да) |
| tip_class |Класс чаевых (0: 0 долларов, 1: 0–5 долларов, 2: 6–10 долларов, 3: 11–20 долларов, 4: >20 долларов) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Выполнять код из записной книжке Jupyter на кластере Spark hello
Вы можете запустить hello книжке Jupyter из hello портал Azure. Найдите свой кластер Spark на информационной панели и щелкните его tooenter страницы управления для кластера. Щелкните записной книжки tooopen hello, связанные с кластера Spark hello, **панели мониторинга кластера** -> **книжке Jupyter** .

![Панели мониторинга кластера](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

Можно также просмотреть слишком***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello записные книжки Jupyter. Замените этот URL-адресе ИМЯ_КЛАСТЕРА hello hello имя свой кластер. Вам необходим пароль hello для записных книжек hello tooaccess учетной записи администратора.

![Просмотр записных книжек Jupyter](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Выберите PySpark toosee каталога, который содержит несколько примеров предварительно упакованные ноутбуки, использующие hello PySpark API.hello портативные компьютеры, содержащие hello образцы кода для этого набора Spark раздела можно найти по адресу [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Вы можете отправить записных книжек hello непосредственно из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) блокнота jupyter toohello на кластере Spark. На домашней странице hello вашей Jupyter, нажмите кнопку hello **отправить** кнопку в правой части экрана приветствия hello. Откроется окно проводника. Здесь можно вставить hello GitHub (необработанное содержимое) URL-адрес hello записной книжки и нажмите кнопку **откройте**. 

Вы увидите hello имя файла в список файлов Jupyter с **отправить** еще раз. Нажмите кнопку **Отправить** . Теперь импорта записной книжки hello. Повторите эти шаги tooupload hello других записных книжек из этого пошагового руководства.

> [!TIP]
> Щелкнуть правой кнопкой мыши hello ссылок в браузере и выберите **Копировать ссылку** tooget hello github необработанный URL-адрес содержимого. Этот URL-адрес можно вставить в hello отправить Jupyter explorer диалоговое окно файла.
> 
> 

Теперь вы можете:

* Просмотреть кода hello, щелкнув записной книжки hello.
* выполнить отдельную ячейку, нажав клавиши **SHIFT+ВВОД**;
* Запустите всей записной книжки hello, щелкнув **ячейки** -> **запуска**.
* Используйте автоматическое визуализацию hello запросов.

> [!TIP]
> Hello PySpark ядра автоматически визуализирует hello вывод запросов SQL (HiveQL). Hello tooselect вариант среди различных типов визуализации (таблицы, круговая, строки, области или панели), получают с помощью hello **тип** кнопок меню в записной книжке hello:
> 
> 

![Кривая ROC логистической регрессии для универсального подхода](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Что дальше?
Теперь, настраиваются с кластером HDInsight Spark и переданы записные книжки Jupyter hello, все готово toowork через hello разделы, соответствующие toohello три PySpark блокнота. Они показывают как tooexplore данных и как затем toocreate и использования моделей. Расширенный просмотр данных и моделирование записной книжки показано как Hello tooinclude свертки перекрестной проверки, hyper параметр и вычисления моделей. 

**Просмотр данных и моделирование с помощью Spark:** изучение набора данных hello и создать, оценки и оценивать hello моделей машинного обучения, прохождение hello [создания двоичных классификационных и регрессионных моделей данных с hello Spark Набор средств MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) раздела.

**Модели потребления:** toolearn tooscore hello классификационных и регрессионных моделей создан в этом разделе в статье [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).

**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).

