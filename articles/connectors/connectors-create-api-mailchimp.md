---
title: "Соединитель MailChimp в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. MailChimp — это служба SaaS, которая позволяет компаниям управлять маркетинговыми мероприятиями по электронной почте, включая отправку маркетинговых сообщений электронной почты, автоматических сообщений и целевых кампаний, и автоматизировать их."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 36559de2-94f0-4355-b492-2926dfc56486
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 46de91881f84183d0359755f49a115e712a7033b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-mailchimp-connector"></a><span data-ttu-id="f725d-104">Начало работы с соединителем MailChimp</span><span class="sxs-lookup"><span data-stu-id="f725d-104">Get started with the MailChimp connector</span></span>
<span data-ttu-id="f725d-105">MailChimp — это служба SaaS, которая позволяет компаниям управлять маркетинговыми мероприятиями по электронной почте, включая отправку маркетинговых сообщений электронной почты, автоматических сообщений и целевых кампаний, и автоматизировать их.</span><span class="sxs-lookup"><span data-stu-id="f725d-105">MailChimp is a SaaS service that allows businesses to manage and automate email marketing activities, including sending marketing emails, automated messages and targeted campaigns.</span></span>

<span data-ttu-id="f725d-106">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f725d-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-mailchimp"></a><span data-ttu-id="f725d-107">Создание подключения к MailChimp</span><span class="sxs-lookup"><span data-stu-id="f725d-107">Create a connection to MailChimp</span></span>
<span data-ttu-id="f725d-108">Для создания приложений логики с помощью MailChimp необходимо создать **подключение**, а затем указать данные для следующих свойств.</span><span class="sxs-lookup"><span data-stu-id="f725d-108">To create Logic apps with MailChimp, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="f725d-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="f725d-109">Property</span></span> | <span data-ttu-id="f725d-110">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f725d-110">Required</span></span> | <span data-ttu-id="f725d-111">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="f725d-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f725d-112">Маркер</span><span class="sxs-lookup"><span data-stu-id="f725d-112">Token</span></span> |<span data-ttu-id="f725d-113">Да</span><span class="sxs-lookup"><span data-stu-id="f725d-113">Yes</span></span> |<span data-ttu-id="f725d-114">Укажите учетные данные MailChimp</span><span class="sxs-lookup"><span data-stu-id="f725d-114">Provide MailChimp Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to MailChimp](../../includes/connectors-create-api-mailchimp.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="f725d-115">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="f725d-115">Connector-specific details</span></span>

<span data-ttu-id="f725d-116">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/mailchimp/).</span><span class="sxs-lookup"><span data-stu-id="f725d-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mailchimp/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f725d-117">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="f725d-117">More connectors</span></span>
<span data-ttu-id="f725d-118">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f725d-118">Go back to the [APIs list](apis-list.md).</span></span>