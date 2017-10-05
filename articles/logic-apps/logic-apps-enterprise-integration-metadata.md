---
title: "Управление метаданными артефактов учетной записи интеграции в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как добавлять и извлекать метаданные артефактов учетных записей интеграции для Azure Logic Apps."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="1469b-103">Управление метаданными артефактов в учетных записях интеграции для приложений логики</span><span class="sxs-lookup"><span data-stu-id="1469b-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="1469b-104">Вы можете определять пользовательские метаданные для артефактов в учетных записях интеграции и извлекать эти метаданные в среде выполнения приложений логики.</span><span class="sxs-lookup"><span data-stu-id="1469b-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="1469b-105">Например, можно указать метаданные для артефактов (партнеры, соглашения, схемы, сопоставления и др.) и сохранить все метаданные с помощью пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="1469b-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="1469b-106">В настоящее время артефакты не могут создавать метаданные через пользовательский интерфейс, но вы можете использовать для этого интерфейсы REST API.</span><span class="sxs-lookup"><span data-stu-id="1469b-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="1469b-107">Чтобы добавить метаданные при создании или выборе партнера, соглашения или схемы на портале Azure, выберите **Редактирование в качестве JSON**.</span><span class="sxs-lookup"><span data-stu-id="1469b-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="1469b-108">Чтобы извлечь метаданные артефактов в приложениях логики, можно использовать функцию "Поиск артефакта учетной записи интеграции".</span><span class="sxs-lookup"><span data-stu-id="1469b-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="1469b-109">Добавление метаданных в артефакты учетных записей интеграции</span><span class="sxs-lookup"><span data-stu-id="1469b-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="1469b-110">Создайте [учетную запись интеграции](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="1469b-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="1469b-111">Добавьте в учетную запись интеграции артефакт, такой как [партнер](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [соглашение](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) или [схема](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="1469b-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="1469b-112">Выберите артефакт, затем выберите **Редактирование в качестве JSON** и введите сведения о метаданных.</span><span class="sxs-lookup"><span data-stu-id="1469b-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Ввод метаданных](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="1469b-114">Извлечение метаданных из артефактов для приложений логики</span><span class="sxs-lookup"><span data-stu-id="1469b-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="1469b-115">Создайте [приложение логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1469b-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="1469b-116">Затем [свяжите приложение логики с учетной записью интеграции](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="1469b-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="1469b-117">В конструкторе приложений логики добавьте в свое приложение логики триггер (*Запрос* или *HTTP*).</span><span class="sxs-lookup"><span data-stu-id="1469b-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="1469b-118">Выберите **Следующий шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="1469b-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="1469b-119">Выполните поиск по слову *интеграции*, чтобы найти и выбрать **Учетная запись интеграции > Поиск артефакта учетной записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="1469b-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Выбор функции "Поиск артефакта учетной записи интеграции"](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="1469b-121">Выберите **Типа артефакта** и укажите **Имя артефакта**.</span><span class="sxs-lookup"><span data-stu-id="1469b-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Выбор типа артефакта и указание имени артефакта](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="1469b-123">Пример: извлечение метаданных партнера</span><span class="sxs-lookup"><span data-stu-id="1469b-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="1469b-124">Метаданные партнера содержат такие сведения о `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="1469b-124">Partner metadata has these `routingUrl` details:</span></span>

![Поиск в метаданных партнера сведений о routingURL](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="1469b-126">В приложении логики добавьте триггер, действие **Учетная запись интеграции > Поиск артефакта учетной записи интеграции** для партнера, а затем — **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="1469b-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Добавление в приложение логики триггера, поиска артефакта и HTTP](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="1469b-128">Чтобы получить универсальный код ресурса (URI), перейдите в представление кода своего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1469b-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="1469b-129">Определение приложения логики должно выглядеть примерно как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="1469b-129">Your logic app definition should look like this example:</span></span>

    ![Поиск](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="1469b-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1469b-131">Next steps</span></span>
* [<span data-ttu-id="1469b-132">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="1469b-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
