---
title: "Проверка XML в Azure Logic Apps | Документация Майкрософт"
description: "Проверка XML с помощью схем для Azure Logic Apps и сценариев B2B с использованием пакета интеграции Enterprise"
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
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="fa298-103">Проверка XML для интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="fa298-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="fa298-104">Часто в сценариях B2B партнерам, участвующим в соглашении, необходимо убедиться в допустимости сообщений, которыми они обмениваются. И это нужно сделать до начала обработки данных.</span><span class="sxs-lookup"><span data-stu-id="fa298-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="fa298-105">В пакете интеграции Enterprise можно использовать соединитель проверки XML, чтобы проверять документы на соответствие предопределенной схеме.</span><span class="sxs-lookup"><span data-stu-id="fa298-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="fa298-106">Проверка документа с помощью соединителя проверки XML</span><span class="sxs-lookup"><span data-stu-id="fa298-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="fa298-107">Создайте приложение логики и [свяжите его с учетной записью интеграции](../logic-apps/logic-apps-enterprise-integration-accounts.md "Дополнительные сведения о связывании учетной записи интеграции с приложением логики"), которая содержит схему для проверки данных XML.</span><span class="sxs-lookup"><span data-stu-id="fa298-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="fa298-108">Добавьте триггер **Request - When an HTTP request is received** (Запрос: при получении HTTP-запроса) в свое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="fa298-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="fa298-109">Добавьте действие **Проверка XML**, щелкнув **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="fa298-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="fa298-110">Введите *xml* в поле поиска, чтобы отфильтровать все действия и оставить только необходимые.</span><span class="sxs-lookup"><span data-stu-id="fa298-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="fa298-111">Выберите действие **Проверка XML**.</span><span class="sxs-lookup"><span data-stu-id="fa298-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="fa298-112">Чтобы указать содержимое XML, которое будет проверено, выберите **Содержимое**.</span><span class="sxs-lookup"><span data-stu-id="fa298-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="fa298-113">Выберите тег body в качестве содержимого, которое будет проверено.</span><span class="sxs-lookup"><span data-stu-id="fa298-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="fa298-114">Чтобы определить схему для проверки ввода предыдущего *содержимого*, выберите **Имя схемы**.</span><span class="sxs-lookup"><span data-stu-id="fa298-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="fa298-115">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="fa298-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="fa298-116">Вы закончили работу с настройкой соединителя проверки.</span><span class="sxs-lookup"><span data-stu-id="fa298-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="fa298-117">В реальном приложении вам нужно будет передать проверенные данные в бизнес-приложение (например, SalesForce).</span><span class="sxs-lookup"><span data-stu-id="fa298-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="fa298-118">Чтобы отправить проверенные выходные данные в Salesforce, добавьте действие.</span><span class="sxs-lookup"><span data-stu-id="fa298-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="fa298-119">Теперь можно протестировать действие проверки, выполнив запрос к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="fa298-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa298-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa298-120">Next steps</span></span>
[<span data-ttu-id="fa298-121">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="fa298-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise")   

