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
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="5f4a5-104">Настройка оповещений для заданий Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="5f4a5-105">Введение: страница мониторинга</span><span class="sxs-lookup"><span data-stu-id="5f4a5-105">Introduction: Monitor page</span></span>
<span data-ttu-id="5f4a5-106">Можно выполнить настройку tootrigger предупреждения оповещение достижении условие, которое указывается метрики.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="5f4a5-107">Например можно настроить оповещение для условия hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5f4a5-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="5f4a5-108">Правила можно настроить на метрики через портал hello, или можно настроить [программно](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) данных журналов операций.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="5f4a5-109">Настройка оповещений в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5f4a5-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="5f4a5-110">Откройте задания Stream Analytics hello нужные toocreate оповещение для hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="5f4a5-111">В hello **задания** колонка, щелкните hello **мониторинг** раздела.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="5f4a5-112">В hello **метрика** колонка, щелкните hello **добавить оповещение** команды.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Настройка портала Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="5f4a5-114">Введите имя и описание.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="5f4a5-115">Используйте hello селекторы toodefine hello условие, в какие hello будет отправлено предупреждение.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="5f4a5-116">Приводятся сведения о куда hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="5f4a5-116">Provide information about where hello alert should go.</span></span>

      ![Настройка оповещений для заданий Azure Streaming Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="5f4a5-118">Дополнительные сведения о настройке предупреждений в hello портал Azure в разделе [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="5f4a5-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="5f4a5-119">Получение справки</span><span class="sxs-lookup"><span data-stu-id="5f4a5-119">Get help</span></span>
<span data-ttu-id="5f4a5-120">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5f4a5-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f4a5-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f4a5-121">Next steps</span></span>
* [<span data-ttu-id="5f4a5-122">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5f4a5-123">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="5f4a5-124">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5f4a5-125">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5f4a5-126">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4a5-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

