---
title: "Декодирование сообщений AS2 — Azure Logic Apps | Документация Майкрософт"
description: "Использование декодера AS2, входящего в пакет интеграции Enterprise для Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="a49cf-103">Декодирование сообщений AS2 для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a49cf-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="a49cf-104">Чтобы обеспечить безопасность и надежность при передаче сообщений, используйте соединитель декодирования сообщений AS2.</span><span class="sxs-lookup"><span data-stu-id="a49cf-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="a49cf-105">Этот соединитель выполняет цифровое подписывание, расшифровку и подтверждение через уведомления о состоянии сообщений (MDN).</span><span class="sxs-lookup"><span data-stu-id="a49cf-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a49cf-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a49cf-106">Before you start</span></span>

<span data-ttu-id="a49cf-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="a49cf-107">Here's the items you need:</span></span>

* <span data-ttu-id="a49cf-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="a49cf-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a49cf-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="a49cf-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a49cf-110">Для работы с соединителем декодирования сообщений AS2 потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="a49cf-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="a49cf-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="a49cf-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a49cf-112">В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).</span><span class="sxs-lookup"><span data-stu-id="a49cf-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="a49cf-113">Декодирование сообщений AS2</span><span class="sxs-lookup"><span data-stu-id="a49cf-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="a49cf-114">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a49cf-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a49cf-115">В соединителе декодирования сообщений AS2 нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="a49cf-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a49cf-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a49cf-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="a49cf-117">В поле поиска введите "AS2" для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="a49cf-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="a49cf-118">Выберите **AS2 — Decode AS2 message** (AS2 — декодирование сообщения AS2).</span><span class="sxs-lookup"><span data-stu-id="a49cf-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Поиск по запросу "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="a49cf-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="a49cf-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="a49cf-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="a49cf-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Создание подключения к системе интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="a49cf-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="a49cf-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a49cf-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="a49cf-124">Property</span></span> | <span data-ttu-id="a49cf-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="a49cf-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a49cf-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="a49cf-126">Connection Name *</span></span> |<span data-ttu-id="a49cf-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="a49cf-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a49cf-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="a49cf-128">Integration Account *</span></span> |<span data-ttu-id="a49cf-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="a49cf-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a49cf-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="a49cf-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="a49cf-131">Когда все будет готово, данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="a49cf-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="a49cf-132">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a49cf-132">To finish creating your connection, choose **Create**.</span></span>

    ![Сведения для подключения учетной записи интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="a49cf-134">После создания подключения, как показано в этом примере, выберите **Текст** и **Заголовки** в выходных данных запроса.</span><span class="sxs-lookup"><span data-stu-id="a49cf-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![подключение к системе интеграции создано](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="a49cf-136">Например:</span><span class="sxs-lookup"><span data-stu-id="a49cf-136">For example:</span></span>

    ![Выберите текст и заголовки из выходных данных запроса](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="a49cf-138">Сведения о декодере AS2</span><span class="sxs-lookup"><span data-stu-id="a49cf-138">AS2 decoder details</span></span>

<span data-ttu-id="a49cf-139">Соединитель декодирования AS2 выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a49cf-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="a49cf-140">обрабатывает заголовки AS2 и HTTP;</span><span class="sxs-lookup"><span data-stu-id="a49cf-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="a49cf-141">проверяет подпись (если настроено);</span><span class="sxs-lookup"><span data-stu-id="a49cf-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="a49cf-142">расшифровывает сообщения (если настроено);</span><span class="sxs-lookup"><span data-stu-id="a49cf-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="a49cf-143">распаковывает сообщения (если настроено);</span><span class="sxs-lookup"><span data-stu-id="a49cf-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="a49cf-144">сопоставляет полученный MDN с первоначальным исходящим сообщением;</span><span class="sxs-lookup"><span data-stu-id="a49cf-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="a49cf-145">обновляет и сопоставляет записи в базе данных неотрекаемости;</span><span class="sxs-lookup"><span data-stu-id="a49cf-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="a49cf-146">сохраняет записи отчетов о состоянии AS2;</span><span class="sxs-lookup"><span data-stu-id="a49cf-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="a49cf-147">кодирует методом base64 содержимое полезных выходных данных;</span><span class="sxs-lookup"><span data-stu-id="a49cf-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="a49cf-148">определяет, требуется ли MDN, а также синхронность или асинхронность MDN, исходя из установленной в соглашении AS2 конфигурации;</span><span class="sxs-lookup"><span data-stu-id="a49cf-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="a49cf-149">создает синхронное или асинхронное MDN (в зависимости от конфигурации соглашения);</span><span class="sxs-lookup"><span data-stu-id="a49cf-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="a49cf-150">задает маркеры корреляции и свойства для MDN.</span><span class="sxs-lookup"><span data-stu-id="a49cf-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="a49cf-151">Пробное использование примера</span><span class="sxs-lookup"><span data-stu-id="a49cf-151">Try this sample</span></span>

<span data-ttu-id="a49cf-152">Чтобы попробовать развернуть полностью рабочее приложение логики и пример сценария AS2, см. [шаблон и сценарий приложения логики AS2](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="a49cf-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="a49cf-153">Просмотр Swagger</span><span class="sxs-lookup"><span data-stu-id="a49cf-153">View the swagger</span></span>
<span data-ttu-id="a49cf-154">Ознакомьтесь с [дополнительными сведениями о Swagger](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="a49cf-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a49cf-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a49cf-155">Next steps</span></span>
[<span data-ttu-id="a49cf-156">Обзор Пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a49cf-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

