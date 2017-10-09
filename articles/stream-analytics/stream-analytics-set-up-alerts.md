---
title: "aaaSet предупреждений для запросов в Stream Analytics | Документы Microsoft"
description: "Общая информация об оповещениях Stream Analytics"
keywords: "настройка оповещений"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Настройка оповещений для заданий Azure Stream Analytics
## <a name="introduction-monitor-page"></a>Введение: страница мониторинга
Можно выполнить настройку tootrigger предупреждения оповещение достижении условие, которое указывается метрики. Например можно настроить оповещение для условия hello следующим образом:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Правила можно настроить на метрики через портал hello, или можно настроить [программно](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) данных журналов операций.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Настройка оповещений в hello портал Azure
1. Откройте задания Stream Analytics hello нужные toocreate оповещение для hello портал Azure. 

2. В hello **задания** колонка, щелкните hello **мониторинг** раздела.  

3. В hello **метрика** колонка, щелкните hello **добавить оповещение** команды.

      ![Настройка портала Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Введите имя и описание.

5. Используйте hello селекторы toodefine hello условие, в какие hello будет отправлено предупреждение.

6. Приводятся сведения о куда hello предупреждение.

      ![Настройка оповещений для заданий Azure Streaming Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Дополнительные сведения о настройке предупреждений в hello портал Azure в разделе [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-get-started.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

