---
title: "Кодирование сообщений AS2 в Azure Logic Apps | Документация Майкрософт"
description: "Использование кодировщика AS2 (входит в пакет интеграции Enterprise) в Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="d747e-103">Кодирование сообщений AS2 для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="d747e-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="d747e-104">Чтобы обеспечить безопасность и надежность при передаче сообщений, используйте соединитель кодирования сообщений AS2.</span><span class="sxs-lookup"><span data-stu-id="d747e-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="d747e-105">Этот соединитель выполняет цифровое подписывание, расшифровку и подтверждение через уведомления о состоянии сообщений (MDN), что также предусматривает невозможность отказа.</span><span class="sxs-lookup"><span data-stu-id="d747e-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d747e-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d747e-106">Before you start</span></span>

<span data-ttu-id="d747e-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="d747e-107">Here's the items you need:</span></span>

* <span data-ttu-id="d747e-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="d747e-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d747e-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="d747e-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d747e-110">Для работы с соединителем для кодирования сообщений AS2 потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="d747e-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="d747e-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="d747e-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d747e-112">В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).</span><span class="sxs-lookup"><span data-stu-id="d747e-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="d747e-113">Кодирование сообщений AS2</span><span class="sxs-lookup"><span data-stu-id="d747e-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="d747e-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d747e-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d747e-115">В соединителе кодирования сообщений AS2 нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="d747e-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d747e-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="d747e-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="d747e-117">В поле поиска введите "AS2" для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d747e-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="d747e-118">Выберите **AS2 — Encode AS2 message** (AS2 — кодирование сообщения AS2).</span><span class="sxs-lookup"><span data-stu-id="d747e-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Поиск по запросу "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="d747e-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="d747e-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="d747e-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="d747e-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![установка подключения к учетной записи интеграции](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="d747e-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="d747e-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d747e-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="d747e-124">Property</span></span> | <span data-ttu-id="d747e-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="d747e-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d747e-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="d747e-126">Connection Name *</span></span> |<span data-ttu-id="d747e-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="d747e-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d747e-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="d747e-128">Integration Account *</span></span> |<span data-ttu-id="d747e-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="d747e-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d747e-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="d747e-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="d747e-131">Когда все будет готово, данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="d747e-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="d747e-132">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d747e-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![Сведения для подключения учетной записи интеграции](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="d747e-134">Создав подключения, как показано в следующем примере, введите данные в поля **AS2-From identifiers** (AS2 — от идентификаторов) , **AS2-To identifiers** (AS2 — к идентификаторам) в соответствии с соглашением, а также заполните поле **Body** (Текст), предназначенное для полезных данных сообщения.</span><span class="sxs-lookup"><span data-stu-id="d747e-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![заполнение обязательных полей](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="d747e-136">Сведения о кодировщике AS2</span><span class="sxs-lookup"><span data-stu-id="d747e-136">AS2 encoder details</span></span>

<span data-ttu-id="d747e-137">Соединитель кодирования AS2 выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d747e-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="d747e-138">Обработка заголовков AS2 и HTTP.</span><span class="sxs-lookup"><span data-stu-id="d747e-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="d747e-139">Подписывание исходящих сообщений (если настроено).</span><span class="sxs-lookup"><span data-stu-id="d747e-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="d747e-140">Кодирование исходящих сообщений (если настроено).</span><span class="sxs-lookup"><span data-stu-id="d747e-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="d747e-141">Сжатие сообщения (если настроено).</span><span class="sxs-lookup"><span data-stu-id="d747e-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="d747e-142">Пробное использование примера</span><span class="sxs-lookup"><span data-stu-id="d747e-142">Try this sample</span></span>

<span data-ttu-id="d747e-143">Чтобы попробовать развернуть полностью рабочее приложение логики и пример сценария AS2, см. [шаблон и сценарий приложения логики AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="d747e-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="d747e-144">Просмотр Swagger</span><span class="sxs-lookup"><span data-stu-id="d747e-144">View the swagger</span></span>
<span data-ttu-id="d747e-145">Ознакомьтесь с [дополнительными сведениями о Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="d747e-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d747e-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d747e-146">Next steps</span></span>
[<span data-ttu-id="d747e-147">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="d747e-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise") 

