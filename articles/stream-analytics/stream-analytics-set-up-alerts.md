---
title: "Настройка оповещений для запросов в Stream Analytics | Документация Майкрософт"
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
ms.openlocfilehash: 75b1b256eea7295f5a464996e2f34ae301c715fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="f35f6-104">Настройка оповещений для заданий Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="f35f6-105">Введение: страница мониторинга</span><span class="sxs-lookup"><span data-stu-id="f35f6-105">Introduction: Monitor page</span></span>
<span data-ttu-id="f35f6-106">Оповещения можно настроить на отображение в случае, если метрика достигнет указанного состояния.</span><span class="sxs-lookup"><span data-stu-id="f35f6-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="f35f6-107">Например, оповещение для условия можно настроить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f35f6-107">For example, you might set up an alert for a condition like the following:</span></span>

`If there are zero input events in the last 5 minutes, send email notification to sa-admin@example.com`

<span data-ttu-id="f35f6-108">Правила на основе метрик можно настраивать через портал либо [программным путем](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) , используя данные в журналах операций.</span><span class="sxs-lookup"><span data-stu-id="f35f6-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-the-azure-portal"></a><span data-ttu-id="f35f6-109">Настройка оповещений на портале Azure</span><span class="sxs-lookup"><span data-stu-id="f35f6-109">Set up alerts in the Azure portal</span></span>
1. <span data-ttu-id="f35f6-110">На портале Azure откройте задание Stream Analytics, для которого требуется создать оповещение.</span><span class="sxs-lookup"><span data-stu-id="f35f6-110">In the Azure portal, open the Stream Analytics job you want to create an alert for.</span></span> 

2. <span data-ttu-id="f35f6-111">В колонке **Задание** щелкните раздел **Мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="f35f6-111">In the **Job** blade, click the **Monitoring** section.</span></span>  

3. <span data-ttu-id="f35f6-112">В колонке **Метрика** выберите команду **Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="f35f6-112">In the **Metric** blade, click the **Add alert** command.</span></span>

      ![Настройка портала Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="f35f6-114">Введите имя и описание.</span><span class="sxs-lookup"><span data-stu-id="f35f6-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="f35f6-115">Используйте селекторы для определения условий, при которых будут отправляться оповещения.</span><span class="sxs-lookup"><span data-stu-id="f35f6-115">Use the selectors to define the condition under which the alert will be sent.</span></span>

6. <span data-ttu-id="f35f6-116">Предоставьте сведения о том, куда следует отправлять оповещения.</span><span class="sxs-lookup"><span data-stu-id="f35f6-116">Provide information about where the alert should go.</span></span>

      ![Настройка оповещений для заданий Azure Streaming Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="f35f6-118">Дополнительные сведения о настройке оповещений на портале Azure см. в статье [Получение уведомлений](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="f35f6-118">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="f35f6-119">Получение справки</span><span class="sxs-lookup"><span data-stu-id="f35f6-119">Get help</span></span>
<span data-ttu-id="f35f6-120">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f35f6-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f35f6-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f35f6-121">Next steps</span></span>
* [<span data-ttu-id="f35f6-122">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-122">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f35f6-123">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="f35f6-124">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f35f6-125">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f35f6-126">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f35f6-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

