---
title: "Соединитель RSS в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Соединитель RSS позволяет пользователям публиковать и извлекать элементы веб-канала. Он также позволяет пользователям активировать операции при публикации нового элемента в веб-канале."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: a10a6277-ed29-4e68-a881-ccdad6fd0ad8
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 308d78550e9e60303b70d591eb4e6bfff3e49ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-rss-connector"></a><span data-ttu-id="12b04-105">Начало работы с соединителем RSS</span><span class="sxs-lookup"><span data-stu-id="12b04-105">Get started with the RSS connector</span></span>
<span data-ttu-id="12b04-106">RSS — это популярный формат веб-синдикации, используемый для публикации часто обновляемого содержимого (записей блогов и заголовков новостей).</span><span class="sxs-lookup"><span data-stu-id="12b04-106">RSS is a popular web syndication format used to publish frequently updated content – like blog entries and news headlines.</span></span>  <span data-ttu-id="12b04-107">Многие издатели содержимого предоставляют RSS-канал, чтобы пользователи могли на него подписаться.</span><span class="sxs-lookup"><span data-stu-id="12b04-107">Many content publishers provide an RSS feed to allow users to subscribe to it.</span></span>  <span data-ttu-id="12b04-108">Соединитель RSS можно использовать для извлечения сведений о канале и активации потоков при публикации новых элементов в RSS-канале.</span><span class="sxs-lookup"><span data-stu-id="12b04-108">Use the RSS connector to retrieve feed information and trigger flows when new items are published in an RSS feed.</span></span>

<span data-ttu-id="12b04-109">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="12b04-109">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-rss"></a><span data-ttu-id="12b04-110">Создание подключения к RSS</span><span class="sxs-lookup"><span data-stu-id="12b04-110">Create a connection to RSS</span></span>
> [!INCLUDE [Steps to create a connection to an RSS feed](../../includes/connectors-create-api-rss.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="12b04-111">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="12b04-111">Connector-specific details</span></span>

<span data-ttu-id="12b04-112">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/rss/).</span><span class="sxs-lookup"><span data-stu-id="12b04-112">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/rss/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="12b04-113">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="12b04-113">More connectors</span></span>
<span data-ttu-id="12b04-114">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="12b04-114">Go back to the [APIs list](apis-list.md).</span></span>