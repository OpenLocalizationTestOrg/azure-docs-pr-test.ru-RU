---
title: "Добавление соединителя Twilio в Azure Logic Apps | Документация Майкрософт"
description: "Обзор соединителя Twilio с параметрами API REST"
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
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="50f19-103">Начало работы с соединителем Twilio</span><span class="sxs-lookup"><span data-stu-id="50f19-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="50f19-104">Подключитесь к Twilio для отправки и получения глобальных SMS-, MMS- и IP-сообщений.</span><span class="sxs-lookup"><span data-stu-id="50f19-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="50f19-105">С помощью Twilio вы можете:</span><span class="sxs-lookup"><span data-stu-id="50f19-105">With Twilio, you can:</span></span>

* <span data-ttu-id="50f19-106">формировать бизнес-процессы на основе данных, получаемых из Twilio;</span><span class="sxs-lookup"><span data-stu-id="50f19-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="50f19-107">использовать действия для получения сообщений, вывода списка сообщений и выполнения многих других задач.</span><span class="sxs-lookup"><span data-stu-id="50f19-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="50f19-108">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="50f19-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="50f19-109">Например, новое полученное сообщение Twilio можно использовать в рабочем процессе служебной шины.</span><span class="sxs-lookup"><span data-stu-id="50f19-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="50f19-110">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="50f19-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="50f19-111">Создание подключения к Twilio</span><span class="sxs-lookup"><span data-stu-id="50f19-111">Create a connection to Twilio</span></span>
<span data-ttu-id="50f19-112">При добавлении этого соединителя в приложения логики введите указанные ниже значения Twilio:</span><span class="sxs-lookup"><span data-stu-id="50f19-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="50f19-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="50f19-113">Property</span></span> | <span data-ttu-id="50f19-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="50f19-114">Required</span></span> | <span data-ttu-id="50f19-115">Описание</span><span class="sxs-lookup"><span data-stu-id="50f19-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50f19-116">Идентификатор учетной записи</span><span class="sxs-lookup"><span data-stu-id="50f19-116">Account ID</span></span> |<span data-ttu-id="50f19-117">Да</span><span class="sxs-lookup"><span data-stu-id="50f19-117">Yes</span></span> |<span data-ttu-id="50f19-118">Введите идентификатор своей учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="50f19-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="50f19-119">Маркер доступа</span><span class="sxs-lookup"><span data-stu-id="50f19-119">Access Token</span></span> |<span data-ttu-id="50f19-120">Да</span><span class="sxs-lookup"><span data-stu-id="50f19-120">Yes</span></span> |<span data-ttu-id="50f19-121">Введите свой маркер доступа Twilio</span><span class="sxs-lookup"><span data-stu-id="50f19-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="50f19-122">Если у вас нет маркера доступа Twilio, см. статью об [удостоверениях пользователей и маркерах доступа](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="50f19-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="50f19-123">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="50f19-123">Connector-specific details</span></span>

<span data-ttu-id="50f19-124">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="50f19-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="50f19-125">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="50f19-125">More connectors</span></span>
<span data-ttu-id="50f19-126">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="50f19-126">Go back to the [APIs list](apis-list.md).</span></span>