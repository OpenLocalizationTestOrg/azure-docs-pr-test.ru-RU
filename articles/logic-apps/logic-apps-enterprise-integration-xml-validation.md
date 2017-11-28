---
title: "aaaValidate XML - приложения логики Azure | Документы Microsoft"
description: "Проверка XML с помощью схем для сценариев приложения логики Azure и B2B с помощью hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="c3a57-103">Проверка XML для интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c3a57-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="c3a57-104">Часто в сценарии B2B hello партнеров в соглашении убедитесь обмена сообщений hello допустимы, до начала обработки данных.</span><span class="sxs-lookup"><span data-stu-id="c3a57-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="c3a57-105">Документы с предварительно определенной схемой можно проверить с помощью hello проверки XML hello использование соединителя в пакет интеграции Enterprise hello.</span><span class="sxs-lookup"><span data-stu-id="c3a57-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="c3a57-106">Проверить документ с соединителем hello Проверка XML</span><span class="sxs-lookup"><span data-stu-id="c3a57-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="c3a57-107">Создание логики приложения, и [связать учетную запись для интеграции toohello приложения hello](../logic-apps/logic-apps-enterprise-integration-accounts.md "узнать toolink tooa логики интеграции учетной записи приложения") , содержащее схему hello, требуется toouse для проверки XML-данных.</span><span class="sxs-lookup"><span data-stu-id="c3a57-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="c3a57-108">Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="c3a57-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="c3a57-109">tooadd hello **проверки XML** действия, выберите **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="c3a57-110">Введите все hello toohello действия, который вы хотите toofilter *xml* в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="c3a57-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="c3a57-111">Выберите действие **Проверка XML**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="c3a57-112">Выберите toospecify hello XML-содержимое, которое следует toovalidate, **СОДЕРЖИМОГО**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="c3a57-113">Выберите тег текст hello в качестве содержимого, которое следует toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="c3a57-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="c3a57-114">требуется toouse проверки hello предыдущей схемы hello toospecify *содержимого* ввода, выберите **имя СХЕМЫ**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="c3a57-115">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="c3a57-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="c3a57-116">Вы закончили работу с настройкой соединителя проверки.</span><span class="sxs-lookup"><span data-stu-id="c3a57-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="c3a57-117">В приложении реального мира может потребоваться toostore hello проверки данных в бизнес-приложения (LOB), например SalesForce.</span><span class="sxs-lookup"><span data-stu-id="c3a57-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="c3a57-118">toosend Здравствуйте tooSalesforce проверенные выходных данных, добавить действие.</span><span class="sxs-lookup"><span data-stu-id="c3a57-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="c3a57-119">tootest действие проверки, создадим конечную точку toohello HTTP запроса.</span><span class="sxs-lookup"><span data-stu-id="c3a57-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3a57-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3a57-120">Next steps</span></span>
[<span data-ttu-id="c3a57-121">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c3a57-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")   

