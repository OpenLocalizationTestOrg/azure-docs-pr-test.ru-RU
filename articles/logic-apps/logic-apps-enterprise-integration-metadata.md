---
title: "Интеграция aaaManage учетной записи метаданных артефакта - приложения логики Azure | Документы Microsoft"
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
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="e33c0-103">Управление метаданными артефактов в учетных записях интеграции для приложений логики</span><span class="sxs-lookup"><span data-stu-id="e33c0-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="e33c0-104">Вы можете определять пользовательские метаданные для артефактов в учетных записях интеграции и извлекать эти метаданные в среде выполнения приложений логики.</span><span class="sxs-lookup"><span data-stu-id="e33c0-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="e33c0-105">Например, можно указать метаданные для артефактов (партнеры, соглашения, схемы, сопоставления и др.) и сохранить все метаданные с помощью пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="e33c0-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="e33c0-106">В настоящее время артефактов не может создать метаданные через пользовательский Интерфейс, но можно использовать API-интерфейс REST toocreate метаданных.</span><span class="sxs-lookup"><span data-stu-id="e33c0-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="e33c0-107">Выберите tooadd метаданных при создании или выберите в hello Azure портал партнера, соглашения или схемы **изменить как JSON**.</span><span class="sxs-lookup"><span data-stu-id="e33c0-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="e33c0-108">tooretrieve артефактов метаданных в логику приложения, можно использовать средство просмотра артефакта учетной записи интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="e33c0-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="e33c0-109">Добавить метаданные tooartifacts в учетные записи службы интеграции</span><span class="sxs-lookup"><span data-stu-id="e33c0-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="e33c0-110">Создайте [учетную запись интеграции](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="e33c0-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="e33c0-111">Добавьте учетную запись интеграции tooyour артефакта, например, [партнера](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [соглашение](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), или [схемы](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="e33c0-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="e33c0-112">Выберите артефакт hello, выберите **изменить как JSON**и введите сведения о метаданных.</span><span class="sxs-lookup"><span data-stu-id="e33c0-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Ввод метаданных](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="e33c0-114">Извлечение метаданных из артефактов для приложений логики</span><span class="sxs-lookup"><span data-stu-id="e33c0-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="e33c0-115">Создайте [приложение логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e33c0-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="e33c0-116">Создание [ссылку из вашей учетной записи интеграции логики приложения tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e33c0-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="e33c0-117">В конструкторе логики приложения, добавить триггер как *запроса* или *HTTP* tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="e33c0-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="e33c0-118">Выберите **Следующий шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="e33c0-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="e33c0-119">Выполните поиск по слову *интеграции*, чтобы найти и выбрать **Учетная запись интеграции > Поиск артефакта учетной записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="e33c0-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Выбор функции "Поиск артефакта учетной записи интеграции"](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="e33c0-121">Выберите hello **тип артефакта**и укажите hello **имя артефакта**.</span><span class="sxs-lookup"><span data-stu-id="e33c0-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Выбор типа артефакта и указание имени артефакта](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="e33c0-123">Пример: извлечение метаданных партнера</span><span class="sxs-lookup"><span data-stu-id="e33c0-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="e33c0-124">Метаданные партнера содержат такие сведения о `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="e33c0-124">Partner metadata has these `routingUrl` details:</span></span>

![Поиск в метаданных партнера сведений о routingURL](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="e33c0-126">В приложении логики добавьте триггер, действие **Учетная запись интеграции > Поиск артефакта учетной записи интеграции** для партнера, а затем — **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e33c0-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Добавление триггера, артефакта подстановки и приложения логики tooyour «HTTP»](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="e33c0-128">hello tooretrieve URI, последовательно tooCode представление логики приложения.</span><span class="sxs-lookup"><span data-stu-id="e33c0-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="e33c0-129">Определение приложения логики должно выглядеть примерно как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="e33c0-129">Your logic app definition should look like this example:</span></span>

    ![Поиск](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="e33c0-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e33c0-131">Next steps</span></span>
* [<span data-ttu-id="e33c0-132">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="e33c0-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
