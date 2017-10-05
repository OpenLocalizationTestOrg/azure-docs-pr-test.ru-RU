---
title: "Добавление соединителя Facebook в приложения логики | Документация Майкрософт"
description: "Обзор соединителя Facebook с параметрами интерфейса API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: e10a30ccef3e81cb3d7749696453d82b8958d076
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-facebook-connector"></a><span data-ttu-id="dd5f3-103">Начало работы с соединителем Facebook</span><span class="sxs-lookup"><span data-stu-id="dd5f3-103">Get started with the Facebook connector</span></span>
<span data-ttu-id="dd5f3-104">Подключение к Facebook позволяет оставлять публикации в хронике, получать канал страниц и выполнять другие действия.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-104">Connect to Facebook and post to a timeline, get a page feed, and more.</span></span> <span data-ttu-id="dd5f3-105">С помощью Facebook можно:</span><span class="sxs-lookup"><span data-stu-id="dd5f3-105">With Facebook, you can:</span></span>

* <span data-ttu-id="dd5f3-106">формировать бизнес-процессы на основе данных, получаемых из Facebook;</span><span class="sxs-lookup"><span data-stu-id="dd5f3-106">Build your business flow based on the data you get from Facebook.</span></span> 
* <span data-ttu-id="dd5f3-107">использовать триггер при получении новой публикации;</span><span class="sxs-lookup"><span data-stu-id="dd5f3-107">Use a trigger when a new post is received.</span></span>
* <span data-ttu-id="dd5f3-108">использовать действия, оставляющие публикации в хронике, получающие канал страниц и выполняющие другие действия.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-108">Use actions that post to your timeline, get a page feed, and more.</span></span> <span data-ttu-id="dd5f3-109">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="dd5f3-110">Например, можно настроить трансляцию всех публикаций, которые появляются в хронике, в Twitter.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-110">For example, when there is a new post on your timeline, you can take that post and push it to your Twitter feed.</span></span> 

<span data-ttu-id="dd5f3-111">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dd5f3-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-facebook"></a><span data-ttu-id="dd5f3-112">Создание подключения к Facebook</span><span class="sxs-lookup"><span data-stu-id="dd5f3-112">Create a connection to Facebook</span></span>
<span data-ttu-id="dd5f3-113">При добавлении соединителя в приложения логики эти приложения необходимо авторизовать для подключения к Facebook.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-113">When you add this connector to your logic apps, you must authorize logic apps to connect to your Facebook.</span></span>

1. <span data-ttu-id="dd5f3-114">Вход в учетную запись Facebook</span><span class="sxs-lookup"><span data-stu-id="dd5f3-114">Sign in to your Facebook account</span></span>
2. <span data-ttu-id="dd5f3-115">Выберите **Авторизовать**и разрешите приложениям логики подключаться к Facebook и использовать его.</span><span class="sxs-lookup"><span data-stu-id="dd5f3-115">Select **Authorize**, and allow your logic apps to connect and use your Facebook.</span></span> 

> [!INCLUDE [Steps to create a connection to Facebook](../../includes/connectors-create-api-facebook.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="dd5f3-116">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="dd5f3-116">Connector-specific details</span></span>

<span data-ttu-id="dd5f3-117">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/facebook/).</span><span class="sxs-lookup"><span data-stu-id="dd5f3-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/facebook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="dd5f3-118">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="dd5f3-118">More connectors</span></span>
<span data-ttu-id="dd5f3-119">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="dd5f3-119">Go back to the [APIs list](apis-list.md).</span></span>