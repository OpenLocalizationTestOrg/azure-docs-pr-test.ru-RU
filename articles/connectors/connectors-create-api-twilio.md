---
title: "aaaAdd hello соединитель Twilio в свои приложения логики Azure | Документы Microsoft"
description: "Общие сведения о hello Twilio соединителя с параметрами REST API"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="a97ee-103">Начало работы с соединителем Twilio hello</span><span class="sxs-lookup"><span data-stu-id="a97ee-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="a97ee-104">Подключение tooTwilio toosend и получение глобального IP, SMS и MMS сообщений.</span><span class="sxs-lookup"><span data-stu-id="a97ee-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="a97ee-105">С помощью Twilio вы можете:</span><span class="sxs-lookup"><span data-stu-id="a97ee-105">With Twilio, you can:</span></span>

* <span data-ttu-id="a97ee-106">Создать поток вашего бизнеса, на основе hello данных, получаемых из Twilio.</span><span class="sxs-lookup"><span data-stu-id="a97ee-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="a97ee-107">использовать действия для получения сообщений, вывода списка сообщений и выполнения многих других задач.</span><span class="sxs-lookup"><span data-stu-id="a97ee-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="a97ee-108">Эти действия получить ответ и внесите hello выходные данные для других действий.</span><span class="sxs-lookup"><span data-stu-id="a97ee-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="a97ee-109">Например, новое полученное сообщение Twilio можно использовать в рабочем процессе служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a97ee-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="a97ee-110">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a97ee-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="a97ee-111">Создание tooTwilio подключения</span><span class="sxs-lookup"><span data-stu-id="a97ee-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="a97ee-112">При добавлении этого соединителя tooyour логику приложения, введите следующие значения Twilio hello:</span><span class="sxs-lookup"><span data-stu-id="a97ee-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="a97ee-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="a97ee-113">Property</span></span> | <span data-ttu-id="a97ee-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a97ee-114">Required</span></span> | <span data-ttu-id="a97ee-115">Описание</span><span class="sxs-lookup"><span data-stu-id="a97ee-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a97ee-116">Идентификатор учетной записи</span><span class="sxs-lookup"><span data-stu-id="a97ee-116">Account ID</span></span> |<span data-ttu-id="a97ee-117">Да</span><span class="sxs-lookup"><span data-stu-id="a97ee-117">Yes</span></span> |<span data-ttu-id="a97ee-118">Введите идентификатор своей учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="a97ee-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="a97ee-119">Маркер доступа</span><span class="sxs-lookup"><span data-stu-id="a97ee-119">Access Token</span></span> |<span data-ttu-id="a97ee-120">Да</span><span class="sxs-lookup"><span data-stu-id="a97ee-120">Yes</span></span> |<span data-ttu-id="a97ee-121">Введите свой маркер доступа Twilio</span><span class="sxs-lookup"><span data-stu-id="a97ee-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="a97ee-122">Если у вас нет маркера доступа Twilio, см. статью об [удостоверениях пользователей и маркерах доступа](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="a97ee-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="a97ee-123">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="a97ee-123">Connector-specific details</span></span>

<span data-ttu-id="a97ee-124">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="a97ee-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a97ee-125">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="a97ee-125">More connectors</span></span>
<span data-ttu-id="a97ee-126">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a97ee-126">Go back toohello [APIs list](apis-list.md).</span></span>
