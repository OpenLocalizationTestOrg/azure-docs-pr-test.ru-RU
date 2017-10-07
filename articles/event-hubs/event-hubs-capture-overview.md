---
title: "aaaOverview из записи концентраторов событий Azure | Документы Microsoft"
description: "Запись телеметрических данных с помощью записи концентраторов событий."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Запись концентраторов событий Azure

Записать Azure концентраторов событий позволяет hello доставки tooautomatically потоковой передачи данных в концентраторы событий tooan [хранилища больших двоичных объектов Azure](https://azure.microsoft.com/services/storage/blobs/) или [хранилища Озера данных Azure](https://azure.microsoft.com/services/data-lake-store/) добавить учетную запись по своему усмотрению с hello гибкость указания времени или размер интервала. Настройка отслеживания очень быстро, существуют не toorun расходы на администрирование, он и он автоматически масштабируется с концентраторами событий [единиц производительности](event-hubs-features.md#capacity). Записать концентраторов событий является наиболее простым способом tooload hello потоковой передачи данных в Azure, а также позволяет toofocus обработки данных, а не система отслеживания измененных данных.

Записать концентраторов событий позволяет tooprocess в режиме реального времени и пакетные конвейеры на hello того же потока. благодаря чему вы можете создавать решения, масштабируемые по мере необходимости. Вы создаете системах на базе пакета сегодня с глазу для будущей обработки в режиме реального времени или вы хотите tooadd эффективный путь холодного tooan существующее в реальном времени решение, записать концентраторов событий упрощает работу с потоковой передачи данных.

## <a name="how-event-hubs-capture-works"></a>Принцип работы записи концентраторов событий

Концентраторы событий является буфером устойчивых время хранения для входящих данных телеметрии, аналогичные tooa распределенных журнала. tooscaling ключа Hello в концентраторы событий — hello [модели](event-hubs-features.md#partitions). Каждая секция — это независимый сегмент данных, потребление которого осуществляется отдельно. Со временем эти данные устаревают, off на основании hello заданного срока хранения. поэтому определенный концентратор событий никогда не заполняется полностью.

Захвата концентраторов событий позволяет вам toospecify учетной записи хранилища больших двоичных объектов Azure и контейнер или учетной записи хранилища Озера данных Azure, которая используется toostore hello собранных данных. Эти учетные записи могут находиться в hello же регионе, как концентратора событий или в другой области, добавление toohello гибкость функция сбора концентраторов событий hello.

Собранные данные записываются в формате [Apache Avro][Apache Avro] — сжатый быстрый двоичный формат, обеспечивающий эффективную структуру данных за счет встроенной схемы. Этот формат широко используется в экосистеме Hadoop hello, Stream Analytics и фабрики данных Azure. Работа с Avro более подробно описана далее в этой статье.

### <a name="capture-windowing"></a>Управление окнами в записи

Записать концентраторов событий позволяет tooset копирование захват toocontrol окна. Это окно будет минимальный размер и время конфигурации с «первый wins политики «это означает, что операции записи, hello пределов обнаружил триггер. При наличии пятнадцать минут 100 МБ окна сбора данных и отправки 1 МБ в секунду, hello размер окна триггеры перед hello временного окна. Каждая секция захватывает независимо друг от друга и записывает завершенного большого двоичного объекта на момент hello захвата, с именем hello времени, на какие hello обнаружена интервал захвата. соглашение об именовании хранилища Hello выглядит следующим образом:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Единицы масштабирования toothroughput

Трафик концентраторов событий контролируется с помощью [единиц пропускной способности](event-hubs-features.md#capacity). Одна единица пропускной способности разрешает передачу до 1 МБ/с или 1000 событий/с для входящих данных или до 2 МБ/с или 2000 событий/с для исходящих данных. Для концентраторов событий (цен. категория "Стандартный") можно настроить от 1 до 20 единиц пропускной способности. Кроме того, можно отправить запрос на увеличение квоты в [службу поддержки][support request]. Использование единиц пропускной способности свыше приобретенного количества регулируется. Записать концентраторов событий копирует данные напрямую из внутреннего хранилища концентраторов событий hello, обход квоты исходящих единицы пропускной способности и сохранение на исходящие данные для других модулей чтения обработки, например Stream Analytics или Spark.

После настройки функция записи концентраторов событий автоматически запускается при отправке первого события и продолжает работать. toomake, облегчить работу вашей последующей обработки tooknow работы процесса hello концентраторов событий записывает пустые файлы при нет данных. Этот процесс обеспечивает прогнозируемую периодичность и позволяет получить маркер, необходимый для пакетных обработчиков.

## <a name="setting-up-event-hubs-capture"></a>Настройка записи концентраторов событий

Можно настроить записи время hello события концентратора создания с помощью hello [портал Azure](https://portal.azure.com), или с помощью шаблонов диспетчера ресурсов Azure. Дополнительные сведения см. в разделе hello в следующих статьях:

- [Разрешить отслеживание концентраторов событий с помощью портала Azure hello](event-hubs-capture-enable-through-portal.md)
- [Создание пространства имен концентраторов событий с концентратором событий и включение записи с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Исследование hello собранных файлов и работа с Avro

Записать концентраторов событий создает файлы в формате Avro, как указано на hello настроить интервал времени. Эти файлы можно просмотреть в любом инструменте, например в [Azure Storage Explorer][Azure Storage Explorer]. Вы можете загрузить hello файлы локально toowork на них.

Hello файлы, созданные системой отслеживания концентраторов событий имеют следующие схемы Avro hello.

![][3]

Можно легко tooexplore Avro файлы с помощью hello [средства Avro] [ Avro Tools] jar с Apache. Загрузив этот JAR-файл, можно просмотреть схемы hello конкретного файла, Avro, выполнив следующую команду hello:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Эта команда возвращает следующее:

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Можно также использовать формат Avro средства tooconvert hello файла tooJSON и выполнять другие операции по обработке.

tooperform более сложных обработки, загрузите и установите Avro для выбора платформы. На момент написания этой статьи hello, существуют реализации для C, C++, C\#, Java, NodeJS, Perl, PHP, Python и Ruby.

Apache Avro предоставляет руководства по началу работы для платформ [Java][Java] и [Python][Python]. Можно также прочитать hello [Приступая к работе с захвата концентраторов событий](event-hubs-capture-python.md) статьи.

## <a name="how-event-hubs-capture-is-charged"></a>Выставление счета за запись концентраторов событий

Записать концентраторов событий измеряется аналогично toothroughput единицы: как почасовой издержки. Hello взимается прямо пропорционально toohello количество единиц производительности, приобретенных для пространства имен hello. Как единицы увеличиваются и уменьшаются, метрах захвата концентраторов событий увеличения и уменьшения tooprovide сопоставления производительности. Hello метрах возникают вместе. Дополнительные сведения о ценах см. на странице цен на [концентраторы событий](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Дальнейшие действия

Записать концентраторов событий — hello простым способом tooget данные в Azure. С помощью знакомых средств и платформ (Azure Data Lake, фабрики данных Azure и Azure HDInsight) можно выполнять необходимую пакетную обработку и другие операции анализа в любом масштабе.

На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Отправка событий в концентраторы событий Azure с помощью платформы .NET Framework](event-hubs-dotnet-framework-getstarted-send.md)
* Полный [пример приложения, использующего концентраторы событий][sample application that uses Event Hubs]
* [Обзор концентраторов событий Azure][Event Hubs overview].

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
