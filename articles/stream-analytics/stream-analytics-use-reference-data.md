---
title: "aaaUse поиск данных и таблицы ссылок в Stream Analytics | Документы Microsoft"
description: "Использование ссылочных данных в запросе Stream Analytics"
keywords: "таблица подстановки, ссылочные данные"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Использование ссылочных данных и таблиц подстановки во входном потоке Stream Analytics
Справочные данные (также называется таблицей подстановки) — это конечное набора данных, который является статическим или замедление изменение по своей природе, при использовании tooperform уточняющего запроса или toocorrelate потока данных. toomake использование ссылочных данных в задание Azure Stream Analytics, обычно используется [присоединения эталонных данных](https://msdn.microsoft.com/library/azure/dn949258.aspx) в запросе. Stream Analytics использует хранилище больших двоичных объектов Azure как hello уровень хранения для ссылочных данных и со ссылкой фабрики данных Azure данные могут быть преобразованные или скопированный tooAzure хранилища больших двоичных объектов, для использования в качестве ссылочных данных из [любое количество облачных и локальных хранилищ данных](../data-factory/data-factory-data-movement-activities.md). Ссылочные данные моделируется как последовательность больших двоичных объектов (определен во входной конфигурации hello) по возрастанию hello даты и времени в имени большого двоичного объекта hello. Он **только** поддерживает добавление toohello конец последовательности hello, используя даты и времени **больше** чем Здравствуйте, указанной в последовательности hello последнего hello BLOB-объекта.

Stream Analytics имеет **ограничение в 100 МБ на BLOB-объект** , но задания может обрабатывать несколько ссылок больших двоичных объектов с помощью hello **шаблон пути** свойство.


## <a name="configuring-reference-data"></a>Настройка ссылочных данных
tooconfigure вашей ссылочных данных, необходимо сначала toocreate входа типа **ссылочных данных**. в следующей таблице Hello описание каждого свойства, которые понадобятся tooprovide при создании hello входных справочных данных с ее описанием:


<table>
<tbody>
<tr>
<td>Имя свойства</td>
<td>Описание</td>
</tr>
<tr>
<td>Псевдоним входных данных</td>
<td>Понятное имя, которое будет использоваться в tooreference запроса задания hello это ввода.</td>
</tr>
<tr>
<td>Учетная запись хранения</td>
<td>Имя учетной записи хранения hello, где расположены BLOB-объектов Hello. Если он находится в hello той же подписке, ваше задание Stream Analytics можно выбрать его из раскрывающегося списка hello.</td>
</tr>
<tr>
<td>Ключ учетной записи хранения</td>
<td>Hello секретный ключ, связанный с учетной записью хранения hello. Автоматически это заполняется, если учетная запись хранения hello в hello той же подписке, задание Stream Analytics.</td>
</tr>
<tr>
<td>Контейнер хранилища</td>
<td>Контейнеры обеспечивают логическое группирование больших двоичных объектов, хранящихся в hello службы BLOB-объектов Microsoft Azure. При передаче большого двоичного объекта toohello службы BLOB-объектов, необходимо указать контейнер для объекта.</td>
</tr>
<tr>
<td>Шаблон пути</td>
<td>использовать путь Hello toolocate BLOB-объектов в указанном контейнере hello. В пути hello можно выбрать один или несколько экземпляров следующих двух переменных hello toospecify:<BR>{date}, {time}<BR>Пример 1: products/{date}/{time}/product-list.csv<BR>Пример 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Формат даты (необязательное свойство)</td>
<td>При использовании {date} в шаблон пути, указанном вами hello hello формат даты, в котором упорядочены BLOB-объектов можно выбрать из раскрывающегося списка hello поддерживаемых форматов.<BR>Например: ГГГГ/ММ/ДД, ММ/ДД/ГГГГ и т. д.</td>
</tr>
<tr>
<td>Формат времени (необязательное свойство)</td>
<td>При использовании {time} в шаблон пути, указанном вами hello hello формат времени, в котором упорядочены BLOB-объектов можно выбрать из раскрывающегося списка hello поддерживаемых форматов.<BR>Примеры: ЧЧ, ЧЧ/мм или ЧЧ-мм.</td>
</tr>
<tr>
<td>Формат сериализации событий</td>
<td>убедиться, что ваши запросы работают hello должным образом, Stream Analytics toomake должен tooknow формат сериализации, который вы используете для входных потоков данных. Форматы hello поддерживается ссылочных данных: CSV и JSON.</td>
</tr>
<tr>
<td>Кодирование</td>
<td>UTF-8 является hello поддерживается только формат кодировки в данный момент</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Создание ссылочных данных по расписанию
Если ссылка данных отличается от набора медленно изменяющихся данных, указав шаблон пути во входной конфигурации hello, с помощью hello {date} и {time} подстановки токенов включена поддержка обновления ссылочных данных. Stream Analytics забирает hello обновить ссылку данных определения на основе этого шаблона пути. Например, шаблон `sample/{date}/{time}/products.csv` формат даты **«Гггг-мм-дд»** и формат времени **«Чч мм»** toopick Stream Analytics, копирование большого двоичного объекта обновлен hello указывает, что `sample/2015-04-16/17-30/products.csv` в 5:30 апреля Шестнадцатый, 2015 часовом поясе UTC.

> [!NOTE]
> В настоящее время заданий Stream Analytics искать обновления hello большого двоичного объекта только в том случае, если время машины hello увеличивается время toohello, закодированное в имени большого двоичного объекта hello. Например, задание hello будет искать `sample/2015-04-16/17-30/products.csv` как только возможно, но не ранее чем 17:30:00 16 апреля 2015 г. UTC часового пояса. Он будет *никогда не* искать большой двоичный объект с более ранних, чем hello последним, обнаруженный кодировке выполнения.
> 
> Например:  После задания hello находит hello больших двоичных объектов `sample/2015-04-16/17-30/products.csv` игнорирует все файлы в кодировке дата предшествует 17:30:00 16 апреля 2015 г. таким образом, если позднее поступающих `sample/2015-04-16/17-25/products.csv` BLOB-объектов возвращает созданные в hello же контейнер hello задание не будет его использовать.
> 
> Аналогично Если `sample/2015-04-16/17-30/products.csv` создается только в 22:03:00 16 апреля 2015 г., но BLOB-объекты с более ранней дате не присутствует в контейнере hello, hello задания будет использовать этот файл, начиная с 10:03 по 16 апреля 2015 г. и использовать hello предыдущих ссылочных данных до этого момента.
> 
> Toothis исключение — когда задание hello необходимы данные процесса toore назад во времени или при первом запуске задания hello. Во время запуска, задание времени hello ищет последних blob hello произведено до задания hello указано время начала. Для этого tooensure, что **непустой** ссылаться на набор данных, когда запускается задание hello. Если не удается найти одно, задание hello отображает hello после диагностики: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Фабрика данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) может быть используется tooorchestrate hello задачу создания hello обновить большие двоичные объекты, необходимые для определения данных Stream Analytics tooupdate ссылки. Фабрика данных — службы интеграции облачных данных, которая координирует и автоматизирует процессы hello перемещения и преобразования данных. Фабрика данных поддерживает [подключение tooa большое число на основе облака и локальных хранилищ данных](../data-factory/data-factory-data-movement-activities.md) и легко перемещения данных по регулярному расписанию, можно указать. Дополнительные сведения и пошаговые инструкции о том, как tooset копирование фабрики данных конвейера toogenerate ссылочных данных для Stream Analytics, который обновляет на это заранее определенное расписание, ознакомьтесь с этой [GitHub пример](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Советы по обновлению ссылочных данных
1. Перезапись ссылку данных больших двоичных объектов не приведет к BLOB-объектов hello tooreload Stream Analytics и в некоторых случаях это может привести к toofail задания hello. Рекомендуется Hello способом toochange ссылочных данных является tooadd новый большой двоичный объект, с помощью того же контейнера и путь к шаблону определен во входных данных задания hello hello и использовать даты и времени **больше** чем Здравствуйте, указанной в последовательности hello последнего hello BLOB-объекта.
2. Ссылка данных BLOB-объектов **не** упорядочены по времени «Последнее изменение» hello большого двоичного объекта, но только по hello времени и даты, указанной в hello имя большого двоичного объекта, с помощью hello {date} и {time} подстановки.
3. В нескольких случаях задания обращаются к данным за прошедшие периоды, поэтому изменять или удалять большие двоичные объекты ссылочных данных нельзя.

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
Было введено tooStream Analytics, управляемой службы для потоковой передачи анализ данных из Интернета вещей hello. toolearn больше об этой службе см.:

* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
