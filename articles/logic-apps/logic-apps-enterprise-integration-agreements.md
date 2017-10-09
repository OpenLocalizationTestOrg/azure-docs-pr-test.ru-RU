---
title: "aaaAgreements для связи B2B - приложения логики Azure | Документы Microsoft"
description: "Создание соглашений, чтобы партнеры могут взаимодействовать в сценариях B2B для приложения логики Azure и hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 499edcbab1cd67fbc169e393c3cad7b81658a250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="8985c-103">Партнерские соглашения для обмена данными в сценариях B2B с использованием Azure Logic Apps и пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="8985c-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="8985c-104">Соглашения позволяют бизнес-сущности связи без проблем с использованием стандартных протоколов и лежат hello для бизнес-взаимодействия (B2B).</span><span class="sxs-lookup"><span data-stu-id="8985c-104">Agreements let business entities communicate seamlessly using industry standard protocols and are hello cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="8985c-105">При включении сценарии B2B для логики приложений с помощью hello пакет интеграции Enterprise, соглашение имеет схему связи между торговыми партнерами B2B.</span><span class="sxs-lookup"><span data-stu-id="8985c-105">When enabling B2B scenarios for logic apps with hello Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="8985c-106">Это соглашение основан на hello связи, которые партнеры hello слишком установления и протокол или на уровне транспорта.</span><span class="sxs-lookup"><span data-stu-id="8985c-106">This agreement is based on hello communications that hello partners want too establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="8985c-107">Интеграция Enterprise поддерживает три стандарта протокола или транспорта:</span><span class="sxs-lookup"><span data-stu-id="8985c-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="8985c-108">AS2</span><span class="sxs-lookup"><span data-stu-id="8985c-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="8985c-109">X12</span><span class="sxs-lookup"><span data-stu-id="8985c-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="8985c-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="8985c-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="8985c-111">Для чего используются соглашения</span><span class="sxs-lookup"><span data-stu-id="8985c-111">Why use agreements</span></span>

<span data-ttu-id="8985c-112">Ниже перечислены некоторые преимущества, связанные с использованием соглашений.</span><span class="sxs-lookup"><span data-stu-id="8985c-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="8985c-113">Включает различные компании и организации tooexchange информацию о хорошо известных формат.</span><span class="sxs-lookup"><span data-stu-id="8985c-113">Enables different organizations and businesses tooexchange information in a well-known format.</span></span>
* <span data-ttu-id="8985c-114">Повышает эффективность при проведении транзакций "бизнес-бизнес".</span><span class="sxs-lookup"><span data-stu-id="8985c-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="8985c-115">Легко toocreate управлять и использовать при создании приложения интеграции enterprise</span><span class="sxs-lookup"><span data-stu-id="8985c-115">Easy toocreate, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-toocreate-agreements"></a><span data-ttu-id="8985c-116">Как toocreate соглашений</span><span class="sxs-lookup"><span data-stu-id="8985c-116">How toocreate agreements</span></span>

* [<span data-ttu-id="8985c-117">Создание соглашения AS2</span><span class="sxs-lookup"><span data-stu-id="8985c-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="8985c-118">Создание соглашения X12</span><span class="sxs-lookup"><span data-stu-id="8985c-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="8985c-119">Создание соглашения EDIFACT</span><span class="sxs-lookup"><span data-stu-id="8985c-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-toouse-an-agreement"></a><span data-ttu-id="8985c-120">Как toouse соглашения</span><span class="sxs-lookup"><span data-stu-id="8985c-120">How toouse an agreement</span></span>

<span data-ttu-id="8985c-121">Вы можете создавать [приложения логики](logic-apps-what-are-logic-apps.md "Дополнительные сведения о приложениях логики") с возможностями B2B, используя созданные вами соглашения.</span><span class="sxs-lookup"><span data-stu-id="8985c-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-tooedit-an-agreement"></a><span data-ttu-id="8985c-122">Как tooedit соглашения</span><span class="sxs-lookup"><span data-stu-id="8985c-122">How tooedit an agreement</span></span>

<span data-ttu-id="8985c-123">Любое соглашение можно изменить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8985c-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="8985c-124">Выберите учетную запись интеграции hello, имеется соглашение hello, требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="8985c-124">Select hello integration account that has hello agreement you want tooupdate.</span></span>

2. <span data-ttu-id="8985c-125">Выберите hello **соглашения** плитки.</span><span class="sxs-lookup"><span data-stu-id="8985c-125">Choose hello **Agreements** tile.</span></span>

3. <span data-ttu-id="8985c-126">На hello **соглашения** колонки, выберите hello соглашения.</span><span class="sxs-lookup"><span data-stu-id="8985c-126">On hello **Agreements** blade, select hello agreement.</span></span>

4. <span data-ttu-id="8985c-127">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="8985c-127">Choose **Edit**.</span></span> <span data-ttu-id="8985c-128">Внесите нужные изменения.</span><span class="sxs-lookup"><span data-stu-id="8985c-128">Make your changes.</span></span>

5. <span data-ttu-id="8985c-129">Выберите изменения, toosave **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8985c-129">toosave your changes, choose **OK**.</span></span>

## <a name="how-toodelete-an-agreement"></a><span data-ttu-id="8985c-130">Как toodelete соглашения</span><span class="sxs-lookup"><span data-stu-id="8985c-130">How toodelete an agreement</span></span>

<span data-ttu-id="8985c-131">Любое соглашение можно удалить. Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="8985c-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="8985c-132">Выберите учетную запись интеграции hello, имеется соглашение hello, требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="8985c-132">Select hello integration account that has hello agreement you want toodelete.</span></span>
2. <span data-ttu-id="8985c-133">Выберите hello **соглашения** плитки.</span><span class="sxs-lookup"><span data-stu-id="8985c-133">Choose hello **Agreements** tile.</span></span>
3. <span data-ttu-id="8985c-134">На hello **соглашения** колонки, выберите hello соглашения.</span><span class="sxs-lookup"><span data-stu-id="8985c-134">On hello **Agreements** blade, select hello agreement.</span></span>
4. <span data-ttu-id="8985c-135">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="8985c-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="8985c-136">Подтвердите toodelete hello выбранного соглашения.</span><span class="sxs-lookup"><span data-stu-id="8985c-136">Confirm that you want toodelete hello selected agreement.</span></span>

    <span data-ttu-id="8985c-137">Hello соглашений колонке больше не отображается hello удалить соглашения.</span><span class="sxs-lookup"><span data-stu-id="8985c-137">hello Agreements blade no longer shows hello deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8985c-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8985c-138">Next steps</span></span>
* [<span data-ttu-id="8985c-139">Создание соглашения AS2</span><span class="sxs-lookup"><span data-stu-id="8985c-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
