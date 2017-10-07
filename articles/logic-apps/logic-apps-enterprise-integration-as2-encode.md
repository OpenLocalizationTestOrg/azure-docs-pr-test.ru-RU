---
title: "сообщения aaaEncode AS2 - приложения логики Azure | Документы Microsoft"
description: "Как toouse hello кодировщика AS2 в hello пакет интеграции Enterprise для приложения логики Azure"
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="c46f4-103">Кодирование сообщения AS2 для приложения логики Azure с помощью hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c46f4-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="c46f4-104">tooestablish безопасность и надежность при передаче сообщений, использовать соединитель сообщение hello кодирования AS2.</span><span class="sxs-lookup"><span data-stu-id="c46f4-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="c46f4-105">Этот соединитель обеспечивает цифровой подписи, шифрования и подтверждений через сообщения метода обработки уведомления (MDN), что также приводит toosupport для Неотказуемость.</span><span class="sxs-lookup"><span data-stu-id="c46f4-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c46f4-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c46f4-106">Before you start</span></span>

<span data-ttu-id="c46f4-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="c46f4-107">Here's hello items you need:</span></span>

* <span data-ttu-id="c46f4-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="c46f4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="c46f4-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="c46f4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="c46f4-110">Необходимо иметь соединителя интеграции кодирования AS2 hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="c46f4-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="c46f4-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="c46f4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="c46f4-112">В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).</span><span class="sxs-lookup"><span data-stu-id="c46f4-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="c46f4-113">Кодирование сообщений AS2</span><span class="sxs-lookup"><span data-stu-id="c46f4-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="c46f4-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c46f4-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="c46f4-115">Соединитель сообщения AS2 кодирования Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="c46f4-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="c46f4-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="c46f4-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="c46f4-117">В поле поиска hello введите «AS2» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="c46f4-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="c46f4-118">Выберите **AS2 — Encode AS2 message** (AS2 — кодирование сообщения AS2).</span><span class="sxs-lookup"><span data-stu-id="c46f4-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Поиск по запросу "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="c46f4-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="c46f4-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="c46f4-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c46f4-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Создайте учетную запись toointegration подключения](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="c46f4-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="c46f4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="c46f4-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="c46f4-124">Property</span></span> | <span data-ttu-id="c46f4-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="c46f4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="c46f4-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="c46f4-126">Connection Name *</span></span> |<span data-ttu-id="c46f4-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="c46f4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="c46f4-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="c46f4-128">Integration Account *</span></span> |<span data-ttu-id="c46f4-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="c46f4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="c46f4-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="c46f4-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="c46f4-131">После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="c46f4-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="c46f4-132">toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="c46f4-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Сведения для подключения учетной записи интеграции](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="c46f4-134">После создания подключения, как показано в следующем примере, введите данные для **AS2-из**, **AS2 tooidentifiers** согласно настройкам в лицензионном соглашении и **текст**, который является полезные данные сообщения Hello.</span><span class="sxs-lookup"><span data-stu-id="c46f4-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![заполнение обязательных полей](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="c46f4-136">Сведения о кодировщике AS2</span><span class="sxs-lookup"><span data-stu-id="c46f4-136">AS2 encoder details</span></span>

<span data-ttu-id="c46f4-137">Соединитель кодирования AS2 Hello выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c46f4-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="c46f4-138">Обработка заголовков AS2 и HTTP.</span><span class="sxs-lookup"><span data-stu-id="c46f4-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="c46f4-139">Подписывание исходящих сообщений (если настроено).</span><span class="sxs-lookup"><span data-stu-id="c46f4-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="c46f4-140">Кодирование исходящих сообщений (если настроено).</span><span class="sxs-lookup"><span data-stu-id="c46f4-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="c46f4-141">Сжимает приветственное сообщение (если настроено)</span><span class="sxs-lookup"><span data-stu-id="c46f4-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="c46f4-142">Пробное использование примера</span><span class="sxs-lookup"><span data-stu-id="c46f4-142">Try this sample</span></span>

<span data-ttu-id="c46f4-143">развертывания полностью логику приложения и образец сценария AS2, tootry разделе hello [AS2 шаблон логику приложения и сценария](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="c46f4-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="c46f4-144">Представление hello swagger</span><span class="sxs-lookup"><span data-stu-id="c46f4-144">View hello swagger</span></span>
<span data-ttu-id="c46f4-145">В разделе hello [swagger сведения](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="c46f4-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c46f4-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c46f4-146">Next steps</span></span>
[<span data-ttu-id="c46f4-147">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c46f4-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

