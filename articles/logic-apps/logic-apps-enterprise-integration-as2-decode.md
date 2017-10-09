---
title: "сообщения aaaDecode AS2 - приложения логики Azure | Документы Microsoft"
description: "Как toouse hello декодер AS2 в hello пакет интеграции Enterprise для приложения логики Azure"
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
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="47822-103">Декодирование сообщения AS2 для приложения логики Azure с hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="47822-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="47822-104">tooestablish безопасность и надежность при передаче сообщений, использовать соединитель сообщение hello декодировать AS2.</span><span class="sxs-lookup"><span data-stu-id="47822-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="47822-105">Этот соединитель выполняет цифровое подписывание, расшифровку и подтверждение через уведомления о состоянии сообщений (MDN).</span><span class="sxs-lookup"><span data-stu-id="47822-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="47822-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="47822-106">Before you start</span></span>

<span data-ttu-id="47822-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="47822-107">Here's hello items you need:</span></span>

* <span data-ttu-id="47822-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="47822-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="47822-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="47822-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="47822-110">Необходимо иметь соединителя интеграции декодировать AS2 hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="47822-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="47822-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="47822-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="47822-112">В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).</span><span class="sxs-lookup"><span data-stu-id="47822-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="47822-113">Декодирование сообщений AS2</span><span class="sxs-lookup"><span data-stu-id="47822-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="47822-114">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="47822-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="47822-115">Соединитель сообщения AS2 декодировать Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="47822-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="47822-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="47822-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="47822-117">В поле поиска hello введите «AS2» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="47822-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="47822-118">Выберите **AS2 — Decode AS2 message** (AS2 — декодирование сообщения AS2).</span><span class="sxs-lookup"><span data-stu-id="47822-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Поиск по запросу "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="47822-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="47822-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="47822-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="47822-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Создание подключения к системе интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="47822-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="47822-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="47822-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="47822-124">Property</span></span> | <span data-ttu-id="47822-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="47822-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="47822-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="47822-126">Connection Name *</span></span> |<span data-ttu-id="47822-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="47822-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="47822-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="47822-128">Integration Account *</span></span> |<span data-ttu-id="47822-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="47822-129">Enter a name for your integration account.</span></span> <span data-ttu-id="47822-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="47822-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="47822-131">После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="47822-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="47822-132">toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="47822-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Сведения для подключения учетной записи интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="47822-134">После создания подключения, как показано в следующем примере, выберите **текст** и **заголовки** с hello запрашивать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="47822-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![подключение к системе интеграции создано](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="47822-136">Например:</span><span class="sxs-lookup"><span data-stu-id="47822-136">For example:</span></span>

    ![Выберите текст и заголовки из выходных данных запроса](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="47822-138">Сведения о декодере AS2</span><span class="sxs-lookup"><span data-stu-id="47822-138">AS2 decoder details</span></span>

<span data-ttu-id="47822-139">Соединитель декодировать AS2 Hello выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="47822-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="47822-140">обрабатывает заголовки AS2 и HTTP;</span><span class="sxs-lookup"><span data-stu-id="47822-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="47822-141">Проверяет подпись hello (если настроено)</span><span class="sxs-lookup"><span data-stu-id="47822-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="47822-142">Расшифровывает сообщений hello (если настроено)</span><span class="sxs-lookup"><span data-stu-id="47822-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="47822-143">Распаковывает приветственное сообщение (если настроено)</span><span class="sxs-lookup"><span data-stu-id="47822-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="47822-144">Согласование полученных MDN с исходной исходящего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="47822-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="47822-145">Обновляет и сопоставляет записей в неотказуемой базе данных hello</span><span class="sxs-lookup"><span data-stu-id="47822-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="47822-146">сохраняет записи отчетов о состоянии AS2;</span><span class="sxs-lookup"><span data-stu-id="47822-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="47822-147">Hello вывода полезных данных состоит в кодировке base64</span><span class="sxs-lookup"><span data-stu-id="47822-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="47822-148">Определяет ли уведомление MDN является обязательным и ли hello MDN должны синхронной или асинхронной на основе конфигурации в соглашении AS2</span><span class="sxs-lookup"><span data-stu-id="47822-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="47822-149">создает синхронное или асинхронное MDN (в зависимости от конфигурации соглашения);</span><span class="sxs-lookup"><span data-stu-id="47822-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="47822-150">Задает токенов корреляции hello и свойства для hello MDN</span><span class="sxs-lookup"><span data-stu-id="47822-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="47822-151">Пробное использование примера</span><span class="sxs-lookup"><span data-stu-id="47822-151">Try this sample</span></span>

<span data-ttu-id="47822-152">развертывания полностью логику приложения и образец сценария AS2, tootry разделе hello [AS2 шаблон логику приложения и сценария](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="47822-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="47822-153">Представление hello swagger</span><span class="sxs-lookup"><span data-stu-id="47822-153">View hello swagger</span></span>
<span data-ttu-id="47822-154">В разделе hello [swagger сведения](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="47822-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="47822-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47822-155">Next steps</span></span>
[<span data-ttu-id="47822-156">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="47822-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

