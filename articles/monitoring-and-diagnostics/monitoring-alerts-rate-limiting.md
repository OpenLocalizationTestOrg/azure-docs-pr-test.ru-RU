---
title: "aaaRate ограничения для SMS-сообщений электронной почты и веб-перехватчиков | Документы Microsoft"
description: "Понимать, каким образом Azure ограничивает hello число возможных SMS, электронную почту или веб-перехватчика уведомлений из группы действие."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="80666-103">Ограничение частоты отправки SMS, сообщений электронной почты и вызовов веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="80666-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="80666-104">Ограничение скорости является приостановку уведомления происходит, когда слишком много уведомления отправляются tooa определенного телефонный номер или адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="80666-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="80666-105">Ограничение скорости гарантирует управляемость и действенность оповещений.</span><span class="sxs-lookup"><span data-stu-id="80666-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="80666-106">Hello правила для SMS и адрес электронной почты: hello таким же.</span><span class="sxs-lookup"><span data-stu-id="80666-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="80666-107">Пороговое значение скорости Hello является:</span><span class="sxs-lookup"><span data-stu-id="80666-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="80666-108">**SMS**: 10 сообщений в час.</span><span class="sxs-lookup"><span data-stu-id="80666-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="80666-109">**Электронная почта**: 100 сообщений в час.</span><span class="sxs-lookup"><span data-stu-id="80666-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="80666-110">Правила ограничения частоты</span><span class="sxs-lookup"><span data-stu-id="80666-110">Rate limit rules</span></span>
- <span data-ttu-id="80666-111">Нужный номер телефона или электронной почты — скорость, когда он получает больше сообщений, чем позволяет hello пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="80666-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="80666-112">Номер телефона или адрес электронной почты может быть частью групп действий в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="80666-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="80666-113">Ограничение частоты применяется ко всем подпискам</span><span class="sxs-lookup"><span data-stu-id="80666-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="80666-114">Оно применяется, как только достигается пороговое значение hello, даже если сообщения отправляются из нескольких подписок.</span><span class="sxs-lookup"><span data-stu-id="80666-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="80666-115">Когда номер телефона или электронной почты — скорость, ограниченный, дополнительные уведомление отправляется toocommunicate hello ограничения скорости.</span><span class="sxs-lookup"><span data-stu-id="80666-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="80666-116">Hello уведомлений, состояния, когда hello интенсивность ограничения срока действия.</span><span class="sxs-lookup"><span data-stu-id="80666-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="80666-117">Ограничение частоты вызовов веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="80666-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="80666-118">Для вызовов веб-перехватчика нет ограничения частоты.</span><span class="sxs-lookup"><span data-stu-id="80666-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80666-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80666-119">Next steps</span></span> ##
* <span data-ttu-id="80666-120">Дополнительные сведения о поведении SMS-оповещений в группе действий см. в [этой статье](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="80666-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="80666-121">Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md)и узнайте, как tooreceive предупреждения.</span><span class="sxs-lookup"><span data-stu-id="80666-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="80666-122">Узнайте, каким образом слишком[настроить оповещения при изменении отправленных уведомление о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="80666-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
