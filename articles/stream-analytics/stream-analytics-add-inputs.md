---
title: "aaaAdd данных ввода заданий Stream Analytics tooyour | Документы Microsoft"
description: "Узнайте, как toohook копирование tooyour источника данных Stream Analytics задания как потоковой передачи входных данных из хранилища больших двоичных данных концентраторов событий или ссылку."
keywords: "входные данные, потоковые данные"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Добавить потоковой передачи данных входные или ссылочные данные tooa задания Stream Analytics
Узнайте, как toohook копирование tooyour источника данных Stream Analytics задания как потоковой передачи входных данных из концентраторов событий или ссылка данные из хранилища больших двоичных объектов.

Azure Stream Analytics задания могут быть подключенным tooone входные данные или несколько, каждый из которых определения существующего источника данных соединения tooan. Как данные передаются источнику данных toothat, потребляемых задания Stream Analytics hello и обрабатываются в режиме реального времени, как потоковые данные. Stream Analytics поддерживает качественную интеграцию с [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) и [хранилища больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) как внутри, так и за пределами задания hello подписки.

Эта статья является этапом hello [план обучения для Stream Analytics](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Входные данные: потоковые данные и ссылочные данные
В службе Stream Analytics используют два отдельных типа входных данных: потоки данных и эталонные данные.

* **Потоки данных**: заданий Stream Analytics должен включать по крайней мере один данных потока ввода toobe использована и преобразована заданием hello. В качестве источников входных потоковых данных могут выступать хранилище больших двоичных объектов Azure и концентраторы событий Azure. Концентраторы событий Azure, используемых toocollect потоки событий из подключенных устройств, служб и приложений. Для приема массовых данных  в качестве потока можно использовать хранилище больших двоичных объектов Azure.  
* **Эталонные данные**: служба Stream Analytics поддерживает второй тип вспомогательных входных данных, которые называются эталонными.  В противоположность toodata на ходу эти данные являются статическими или снижающее производительность изменение.  Обычно используется для выполнения поисков и взаимосвязи с toocreate потоков данных на более широком наборе данных.  Хранилища больших двоичных объектов Azure в настоящее время является источника входных данных hello поддерживается только для ссылочных данных.  

tooadd задание Stream Analytics ввода tooyour:

1. В hello портала Azure щелкните **входов** и нажмите кнопку **Добавление входных данных** в задание Stream Analytics.
   
    ![Классический портал Azure — добавление входных данных.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    В hello портала Azure щелкните hello **входов** плитки в задание Stream Analytics.  
   
    ![Портал Azure — добавление входных данных.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Укажите тип Привет вводимых hello: либо **потока данных** или **ссылочные данные**.
   
    ![Добавить hello правильные данные ввода, потоковый или ссылки](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Добавить hello правильные данные ввода, потоковый или ссылки](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. При создании ввода потока данных, укажите тип источника hello для входа hello.  Так как в настоящее время поддерживается только хранилище больших двоичных объектов, при создании эталонных данных этот шаг можно пропустить.
   
    ![Добавление источника потока данных](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Добавление источника потока данных](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Введите понятное имя для этого входного в hello входной псевдоним.  Это имя будет использоваться в запросе в задание позже на входе toohello toorefer.
   
    Заполните остальные hello hello необходимые свойства tooconnect tooyour в источнике данных соединения. Эти поля зависят от типа входных данных и источника и подробно описаны [здесь](stream-analytics-create-a-job.md).  
   
    ![Добавление входных данных концентратора событий](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Укажите параметры сериализации hello hello входных данных.
   
   * toomake убедиться, что ваши запросы работают hello так, как ожидалось, укажите hello **формат сериализации событий** входящих данных.  Поддерживаемые форматы сериализации: JSON, CSV и Avro.
   * Проверьте hello **кодировка** hello данных.  UTF-8 является hello поддерживается только формат кодировки в данный момент.
     
     ![Параметры сериализации данных для входных данных hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Параметры сериализации данных для входных данных hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. После завершения создания входных hello, Stream Analytics будет проверять возможность подключения toohello источника входных данных.  Состояние hello hello операции подключения теста можно просмотреть в концентраторе уведомлений hello.
   
    ![Проверка соединения объекта hello потокового ввода данных](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Проверка соединения объекта hello потокового ввода данных](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Получение справки по потоковой передаче входных данных
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

