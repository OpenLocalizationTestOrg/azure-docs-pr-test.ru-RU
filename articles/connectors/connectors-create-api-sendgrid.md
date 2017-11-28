---
title: "SendGrid | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Поставщик подключений SendGrid позволяет отправлять электронную почту и управлять списками получателей."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="50d6a-104">Начало работы с соединителем SendGrid</span><span class="sxs-lookup"><span data-stu-id="50d6a-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="50d6a-105">Поставщик подключений SendGrid позволяет отправлять электронную почту и управлять списками получателей.</span><span class="sxs-lookup"><span data-stu-id="50d6a-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="50d6a-106">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="50d6a-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="50d6a-107">Создание подключения к SendGrid</span><span class="sxs-lookup"><span data-stu-id="50d6a-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="50d6a-108">Для создания приложений логики с помощью SendGrid необходимо создать **подключение**, а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="50d6a-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="50d6a-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="50d6a-109">Property</span></span> | <span data-ttu-id="50d6a-110">Обязательно</span><span class="sxs-lookup"><span data-stu-id="50d6a-110">Required</span></span> | <span data-ttu-id="50d6a-111">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="50d6a-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50d6a-112">ApiKey</span><span class="sxs-lookup"><span data-stu-id="50d6a-112">ApiKey</span></span> |<span data-ttu-id="50d6a-113">Да</span><span class="sxs-lookup"><span data-stu-id="50d6a-113">Yes</span></span> |<span data-ttu-id="50d6a-114">Укажите ключ API SendGrid</span><span class="sxs-lookup"><span data-stu-id="50d6a-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="50d6a-115">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров.</span><span class="sxs-lookup"><span data-stu-id="50d6a-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="50d6a-116">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="50d6a-116">Connector-specific details</span></span>

<span data-ttu-id="50d6a-117">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/sendgrid/).</span><span class="sxs-lookup"><span data-stu-id="50d6a-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="50d6a-118">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="50d6a-118">More connectors</span></span>
<span data-ttu-id="50d6a-119">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="50d6a-119">Go back to the [APIs list](apis-list.md).</span></span>