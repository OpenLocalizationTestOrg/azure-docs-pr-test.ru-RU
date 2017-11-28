---
title: "Добавление соединителя Yammer в Azure Logic Apps | Документация Майкрософт"
description: "Обзор соединителя Yammer с параметрами API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="8a7b3-103">Начало работы с соединителем Yammer</span><span class="sxs-lookup"><span data-stu-id="8a7b3-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="8a7b3-104">Вы можете подключаться к Yammer для доступа к беседам в корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="8a7b3-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="8a7b3-105">С помощью Yammer вы можете:</span><span class="sxs-lookup"><span data-stu-id="8a7b3-105">With Yammer, you can:</span></span>

* <span data-ttu-id="8a7b3-106">формировать бизнес-процессы на основе данных, получаемых из Yammer;</span><span class="sxs-lookup"><span data-stu-id="8a7b3-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="8a7b3-107">использовать триггеры при поступлении нового сообщения в группе или веб-канале, на который вы подписаны;</span><span class="sxs-lookup"><span data-stu-id="8a7b3-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="8a7b3-108">использовать действия для публикации сообщений, получения всех сообщений и т. д.</span><span class="sxs-lookup"><span data-stu-id="8a7b3-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="8a7b3-109">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="8a7b3-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="8a7b3-110">Например, при появлении нового сообщения вы можете отправлять сообщения электронной почты с помощью Office 365.</span><span class="sxs-lookup"><span data-stu-id="8a7b3-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="8a7b3-111">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8a7b3-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="8a7b3-112">Создание подключения к Yammer</span><span class="sxs-lookup"><span data-stu-id="8a7b3-112">Create a connection to Yammer</span></span>
<span data-ttu-id="8a7b3-113">Чтобы использовать соединитель Yammer, сначала нужно создать **подключение**, а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="8a7b3-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="8a7b3-114">Свойство</span><span class="sxs-lookup"><span data-stu-id="8a7b3-114">Property</span></span> | <span data-ttu-id="8a7b3-115">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8a7b3-115">Required</span></span> | <span data-ttu-id="8a7b3-116">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="8a7b3-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a7b3-117">Маркер</span><span class="sxs-lookup"><span data-stu-id="8a7b3-117">Token</span></span> |<span data-ttu-id="8a7b3-118">Да</span><span class="sxs-lookup"><span data-stu-id="8a7b3-118">Yes</span></span> |<span data-ttu-id="8a7b3-119">Указание учетных данных Yammer</span><span class="sxs-lookup"><span data-stu-id="8a7b3-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="8a7b3-120">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="8a7b3-120">Connector-specific details</span></span>

<span data-ttu-id="8a7b3-121">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="8a7b3-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8a7b3-122">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="8a7b3-122">More connectors</span></span>
<span data-ttu-id="8a7b3-123">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8a7b3-123">Go back to the [APIs list](apis-list.md).</span></span>