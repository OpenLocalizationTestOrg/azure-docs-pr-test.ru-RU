---
title: "руководство по aaaTroubleshooting для Azure Stream Analytics | Документы Microsoft"
description: "Как tootroubleshoot ваше задание Stream Analytics"
keywords: "руководство по устранению неполадок"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Руководство по устранению неполадок для Azure Stream Analytics

Устранение неполадок Azure Stream Analytics может отображаться toobe более сложных усилий на первый взгляд. После работы с большим числом пользователей, мы создали этот процесс hello оптимизировать toohelp руководства и удалите hello догадки о входов, выходов, запросы и функции.

## <a name="troubleshoot-your-stream-analytics-job"></a>Устранение неполадок в задании Stream Analytics

Для получения наилучших результатов при устранении неполадок в задание Stream Analytics используйте hello, следование правилам:

1.  Проверьте подключение:
    - Проверьте подключение tooinputs и выходные данные с помощью hello **проверить подключение** кнопка для каждого входа и выхода.

2.  Проверьте входные данные:
    - tooverify входных данных, поступающих в концентратор событий, используйте [обозревателя Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure концентратора событий (если используется концентратора событий ввода).  
    - Используйте hello [ **образец данных** ](stream-analytics-sample-data-input.md) кнопку для каждого входа и загрузку данных hello выборки входных данных.
    - Проверить форму hello образец данных toounderstand hello данных hello: hello схемы и hello [типы данных](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Проверьте запрос:
    - На hello **запроса** используйте hello **тестирования** кнопку tootest hello запроса и использовать образцы данных загружаются hello слишком[проверка hello запроса](stream-analytics-test-query.md). Просмотрите все ошибки и повторите попытку toocorrect их.
    - Если вы используете [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), убедитесь, что события hello отметки времени больше, чем hello [время начала задания](stream-analytics-out-of-order-and-late-events.md).

4.  Выполните отладку запроса:
    - Перестройте hello запрос последовательно из сложные агрегаты toomore простой инструкции select с помощью действия. использовать toobuild копирование логику запроса hello шаг за шагом, [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) предложения.
    - Используйте [SELECT INTO](stream-analytics-select-into.md) toodebug действия запроса.

5.  Исключите типичные проблемы, например:
    - Объект [ **ГДЕ** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) предложение в запросе hello отфильтровываются все события, предотвращая создаваемого никаких выходных данных.
    - При использовании функции окна, дождитесь toosee длительность всего содержимого окна hello выходные данные из запроса hello.
    - Hello отметки времени для событий предшествует времени начала задания hello и, таким образом, события отбрасываются.

6.  Используйте упорядочивание событий:
    - Если все hello предыдущие шаги работал правильно, переходите toohello **параметры** и выберите [ **воспроизведении порядок возникновения событий**](stream-analytics-out-of-order-and-late-events.md). Убедитесь, что эта политика настроена для требуемых элементов сценария. политика Hello *не* применяется при использовании hello **тест** кнопку tootest hello запроса. Этот результат является одним из различий между тестирование в браузере и запуск задания hello в рабочей среде.

7.  Выполните отладку с использованием метрик:
    - Если получить выходные данные после hello Ожидаемая длительность, (на основе hello запроса), попробуйте следующие hello.
        - Посмотрите на [ **мониторинг метрик** ](stream-analytics-monitoring.md) на hello **монитор** вкладки. Поскольку hello значения суммируются, метрики hello задерживаются на несколько минут.
            - Если входных событий > 0, hello задания — может tooread входных данных. Если значение параметра "Входные события" меньше 0, сделайте следующее:
                - toosee ли источник данных hello содержит допустимые данные, проверьте его с помощью [обозревателя Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Эта проверка применяется, если задание hello использует концентратора событий в качестве входных данных.
                - Проверьте наличие toosee формат сериализации данных hello и кодировки данных соответствуют ожидаемым.
                - Если задание hello использует концентратора событий, проверьте наличие toosee hello тело сообщения hello *Null*.
            - Если ошибки преобразования данных может > 0 и экстремума выполняться hello следующие условия:
                - Hello задания могут быть может toode-сериализации событий hello.
                - Hello схема событий может не совпадать с определенных hello или Ожидаемая схема событий hello в запросе hello.
                - типы данных Hello некоторых hello полями hello события могут не соответствовать ожиданиям.
            - Если ошибки времени выполнения > 0, это означает hello задания может получать данные hello, но выдает ошибки при обработке запроса hello.
                - ошибки toofind hello, последовательно выберите toohello [журналы аудита](../azure-resource-manager/resource-group-audit.md) и фильтрацию по *сбой* состояния.
            - Если InputEvents > 0 и OutputEvents = 0, означает, что одно из следующих hello имеет значение true:
                - В результате обработки исходящие события не получены.
                - События или его поля могут быть повреждены, и выходные события после обработки запроса не получены.
                - Задание Hello был toohello данных не удается toopush [приемником потока](stream-analytics-select-into.md) в целях подключения или проверки подлинности.
        - В hello всех упомянутых выше случаях ошибка операции, сообщения журнала приводятся дополнительные сведения, включая выполняемых, за исключением случаев, когда логику запроса hello исключены все события. Если hello обработки нескольких событий приводит к возникновению ошибки, регистрирует журналы hello первые три сообщения об ошибках из того же типа, в течение 10 минут tooOperations hello Stream Analytics. Затем дополнительные сообщения об идентичных ошибках скрываются, и появляется сообщение о том, что ошибки возникают слишком быстро, поэтому сообщения о них скрываются.

8. Выполните отладку с помощью журналов аудита и диагностики:
    - Используйте [журналы аудита](../azure-resource-manager/resource-group-audit.md)и ошибки фильтра tooidentify и отладки.
    - Используйте [журналы диагностики задания](stream-analytics-job-diagnostic-logs.md) ошибки tooidentify и отладки.

9. Проверьте выходные данные hello:
    - Когда hello задание находится в состоянии *под управлением*, в зависимости от длительности hello, оговорено в запросе hello вывод hello в источнике данных приемник hello.
    - Если невозможно просмотреть выходные данные, которые будут tooa специальные выходные данные типа, перенаправлять их tooan тип выходных данных, менее сложна, такие как BLOB-объект Azure. С помощью обозревателя хранилищ, проверьте наличие toosee hello выходные данные будут видны. Кроме того проверьте ли ограничения регулирования с выхода hello препятствуют получению данных.

10. Используйте анализ потока данных с помощью метрик схемы заданий:
    - потока данных tooanalyze и идентифицировать проблемы, используйте hello [задания диаграмма с метриками](stream-analytics-job-diagram-with-metrics.md).

11. Отправьте запрос в службу поддержки:
    - Наконец Если ничего не поможет, откройте обращение в службу поддержки корпорации Майкрософт с помощью hello SubscriptionID, содержащий задание.

## <a name="get-help"></a>Получение справки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
