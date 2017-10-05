---
title: "Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов веб-перехватчиков | Документация Майкрософт"
description: "Узнайте, как в Azure ограничивается количество возможных SMS, сообщений электронной почты или уведомлений веб-перехватчика из группы действий."
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
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="77467-103">Ограничение частоты отправки SMS, сообщений электронной почты и вызовов веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="77467-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="77467-104">Ограничение частоты означает приостановку уведомлений, которые слишком часто отправляются на указанный номер телефона или адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="77467-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="77467-105">Ограничение скорости гарантирует управляемость и действенность оповещений.</span><span class="sxs-lookup"><span data-stu-id="77467-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="77467-106">Правила для сообщений SMS и электронной почты не отличаются.</span><span class="sxs-lookup"><span data-stu-id="77467-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="77467-107">Порог частоты:</span><span class="sxs-lookup"><span data-stu-id="77467-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="77467-108">**SMS**: 10 сообщений в час.</span><span class="sxs-lookup"><span data-stu-id="77467-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="77467-109">**Электронная почта**: 100 сообщений в час.</span><span class="sxs-lookup"><span data-stu-id="77467-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="77467-110">Правила ограничения частоты</span><span class="sxs-lookup"><span data-stu-id="77467-110">Rate limit rules</span></span>
- <span data-ttu-id="77467-111">Нужный номер телефона или адрес электронной почты ограничивается, если частота превысит пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="77467-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="77467-112">Номер телефона или адрес электронной почты может быть частью групп действий в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="77467-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="77467-113">Ограничение частоты применяется ко всем подпискам</span><span class="sxs-lookup"><span data-stu-id="77467-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="77467-114">по достижении порогового значения, даже если сообщения отправляются из нескольких подписок.</span><span class="sxs-lookup"><span data-stu-id="77467-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="77467-115">Если для номера телефона или адреса электронной почты ограничена частота, отправляется уведомление, в котором сообщается об ограничении скорости.</span><span class="sxs-lookup"><span data-stu-id="77467-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="77467-116">Уведомление сообщает также, когда истекает срок действия ограничения частоты.</span><span class="sxs-lookup"><span data-stu-id="77467-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="77467-117">Ограничение частоты вызовов веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="77467-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="77467-118">Для вызовов веб-перехватчика нет ограничения частоты.</span><span class="sxs-lookup"><span data-stu-id="77467-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77467-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77467-119">Next steps</span></span> ##
* <span data-ttu-id="77467-120">Дополнительные сведения о поведении SMS-оповещений в группе действий см. в [этой статье](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="77467-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="77467-121">Изучите [обзор оповещений журнала действий](monitoring-overview-alerts.md) и узнайте, как получать оповещения.</span><span class="sxs-lookup"><span data-stu-id="77467-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="77467-122">Узнайте, как [настроить оповещения при поступлении уведомлений о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="77467-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
