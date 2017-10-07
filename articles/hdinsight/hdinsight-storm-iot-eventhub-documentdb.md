---
title: "aaaProcess vehicle датчиков с Apache Storm на HDInsight | Документы Microsoft"
description: "Узнайте, как tooprocess vehicle датчиков из концентраторов событий с помощью Apache Storm на HDInsight. Добавление модели данных из базы данных Azure Cosmos и хранения toostorage выходных данных."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Обработка данных с датчиков автомобилей из концентраторов событий Azure с использованием средств Apache Storm в HDInsight.

Узнайте, как tooprocess vehicle датчиков из концентраторов событий Azure с помощью Apache Storm на HDInsight. Этот пример считывает данные датчика из концентраторов событий Azure, обогащает hello данных с помощью ссылки на данные, хранящиеся в базе данных Azure Cosmos. Hello данные хранятся в хранилище Azure с помощью hello системы файла Hadoop (HDFS).

![HDInsight и hello схема архитектуры Интернета вещей (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Обзор

Добавление датчиков toovehicles позволяет toopredict неполадок оборудования, на основе исторических данных тенденций. Она также позволяет усовершенствования toomake toofuture версии на основе анализа шаблонов использования. Должен быть доступ tooquickly и эффективно hello данных из всех автомобилей Чтобы загрузить в Hadoop может произойти обработка MapReduce. Кроме того вы можете toodo анализа для путей критический сбой (температуры ядра, brakes, т. д.) в режиме реального времени.

Концентраторы событий Azure построен toohandle hello значительный объем данных, созданные датчиков. Apache Storm можно использовать tooload и hello обработки данных перед их передачей в HDFS.

## <a name="solution"></a>Решение

Данные телеметрии, связанные с температурой двигателя и окружающей среды, и также со скоростью автомобиля, фиксируются датчиками Данных затем отправляется концентраторов tooEvent вместе с номер идентификации hello car транспортного средства (VIN) и отметкой времени. Оттуда Storm топология, работающая на Apache Storm в кластере HDInsight считывает данные hello, обрабатывает его и сохраняет его в HDFS.

Во время обработки hello VIN является используется tooretrieve сведения о модели из базы данных Cosmos. Эти данные добавляется в поток данных toohello перед сохранением.

Hello компоненты, используемые в hello Storm топологии являются:

* **EventHubSpout** : считывает данные из концентраторов событий Azure.
* **TypeConversionBolt** -преобразует hello строки JSON из концентраторов событий в кортеж, содержащий следующие данные датчика hello:
    * engineTemperature
    * температура окружающей среды;
    * Speed
    * VIN
    * Timestamp
* **DataReferencBolt** -ищет hello vehicle модели из Cosmos базу данных, используя hello VIN
* **WasbStoreBolt** -магазины hello tooHDFS данных (хранилище Azure)

Следующие изображения Hello является схема этого решения:

![топология Storm](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Реализация

Завершенный автоматизированным решением, для этого сценария доступна как часть hello [HDInsight-Storm-примеры](https://github.com/hdinsight/hdinsight-storm-examples) репозитория в GitHub. toouse в этом примере, повторите шаги hello в hello [IoTExample файл README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Дальнейшие действия

Другие примеры топологий Storm см. в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).

