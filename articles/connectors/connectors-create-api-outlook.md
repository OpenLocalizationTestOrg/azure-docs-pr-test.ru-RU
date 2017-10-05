---
title: "Соединитель Outlook.com в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Соединитель Outlook.com позволяет управлять электронной почтой, календарями и контактами. С его помощью можно выполнять различные действия, такие как отправка сообщения электронной почты, планирование встреч, добавление контактов и т. д."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="daf07-105">Начало работы с соединителем Outlook.com</span><span class="sxs-lookup"><span data-stu-id="daf07-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="daf07-106">Соединитель Outlook.com позволяет управлять электронной почтой, календарями и контактами.</span><span class="sxs-lookup"><span data-stu-id="daf07-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="daf07-107">С его помощью можно выполнять различные действия, такие как отправка сообщения электронной почты, планирование встреч, добавление контактов и т. д.</span><span class="sxs-lookup"><span data-stu-id="daf07-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="daf07-108">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="daf07-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="daf07-109">Создание подключения к Outlook.com</span><span class="sxs-lookup"><span data-stu-id="daf07-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="daf07-110">Для создания приложений логики с помощью Outlook.com необходимо создать **подключение**, а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="daf07-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="daf07-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="daf07-111">Property</span></span> | <span data-ttu-id="daf07-112">Обязательно</span><span class="sxs-lookup"><span data-stu-id="daf07-112">Required</span></span> | <span data-ttu-id="daf07-113">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="daf07-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="daf07-114">Маркер</span><span class="sxs-lookup"><span data-stu-id="daf07-114">Token</span></span> |<span data-ttu-id="daf07-115">Да</span><span class="sxs-lookup"><span data-stu-id="daf07-115">Yes</span></span> |<span data-ttu-id="daf07-116">Укажите учетные данные Outlook.com</span><span class="sxs-lookup"><span data-stu-id="daf07-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="daf07-117">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="daf07-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="daf07-118">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="daf07-118">Connector-specific details</span></span>

<span data-ttu-id="daf07-119">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="daf07-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="daf07-120">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="daf07-120">More connectors</span></span>
<span data-ttu-id="daf07-121">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="daf07-121">Go back to the [APIs list](apis-list.md).</span></span>