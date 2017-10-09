---
title: "с помощью операции и служба журналов в Stream Analytics aaaDebug | Документы Microsoft"
description: "Поток как toouse аналитика журналов операций"
keywords: "журналы служб"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Основные сведения о службе Stream Analytics и журналах операций
Всех служб Azure, оперативной питания ведения журнала сообщений toousers toorecord сведений о связанных с toomanagement операций. В Azure Stream Analytics эти сведения можно использовать для отладки, такие как просмотр состояния задания, ход выполнения задания и сбой сообщения tootrack hello ход выполнения задания по времени, из начала tooprocessing toooutput.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Найти журналы операций на портале управления Azure hello
Доступ к журналам операций можно получить одним из двух способов.  

* Панель мониторинга задания Stream Analytics hello  
* Службы управления Azure классическом портале hello  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Панель мониторинга задания Stream Analytics hello
Ссылка toohello соответствующие журналы задания Stream Analytics отображаются на вкладке панели мониторинга hello задания. Если щелкнуть эту ссылку, установит hello фильтры таким образом, что в нем отображаются последние журналы для этого конкретного задания.

  ![Выбор журналов служб управления](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Службы управления
toomanually перейдите журналы операций toohello Stream Analytics и других служб Azure в классическом портале hello:

1. Щелкните **служб управления** в hello [Azure классический портал](https://manage.windowsazure.com).
2. Выберите **Stream Analytics** для **тип** и имя hello hello задания для **имя службы**.  
   
   ![Выбор Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Найти журналы аудита в hello портал Azure
toofind операционные журналы для задания Stream Analytics в hello портала Azure щелкните **Обзор** , а затем выберите **журналы аудита**.

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Откроется колонка событий из hello последние 7 дней для всех ресурсов в вашей подписке.  Можно отфильтровать такие события toosee, укажите тип или промежуток времени, щелкнув hello **фильтра** команды.

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Получение подробных сведений журнала
Можно отфильтровать диапазон времени и состояние tooview hello журналы для задания.

На портале управления Azure hello, нажмите кнопку hello **сведения** кнопку внизу hello tooview окно hello подробной информации о выбранном событии. 

  ![Выбор сведений](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

В hello портал Azure, щелкните запись журнала toosee hello подробные события внутри него.

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

После этого можно открыть hello **сведений** колонки, щелкнув событие hello.

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Отладка невыполненного задания
На портале управления Azure hello щелкните значок поиска hello и введите «сбой». Это позволит получить все журналы с ошибками. 

  ![Отладка задания с ошибкой](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

В hello портал Azure, можно фильтровать по уровень сообщения tooview **критическое** события.

  ![Отладка на портале Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Можно выбрать любой из ошибок hello и щелкнуть hello **сведения** Дополнительные сведения об ошибке hello.  Некоторые сообщения об ошибках также предоставляют сведения о как toomitigate hello проблему. 

  ![Сведения об операции](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

При необходимости toocontact [поддержки](https://azure.microsoft.com/support/options/) или предоставить авторам toohello сведения через hello [форум MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), имейте в виду hello сведения об операции, в частности hello **идентификатор корреляции**. 

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

