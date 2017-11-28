---
title: "Соглашения для обмена данными в сценариях B2B с использованием Azure Logic Apps | Документация Майкрософт"
description: "Создание соглашений, благодаря которым партнеры могут взаимодействовать, реализуя сценарии B2B с помощью Azure Logic Apps и пакета интеграции Enterprise"
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
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="5ca39-103">Партнерские соглашения для обмена данными в сценариях B2B с использованием Azure Logic Apps и пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="5ca39-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="5ca39-104">Соглашения являются основой взаимодействий "бизнес — бизнес" (B2B), так как они позволяют бизнес-сущностям легко обмениваться данными с помощью стандартных протоколов.</span><span class="sxs-lookup"><span data-stu-id="5ca39-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="5ca39-105">В контексте реализации сценариев В2В с помощью интеграции Enterprise соглашение — это договоренность о взаимодействии "бизнес — бизнес" между торговыми партнерами.</span><span class="sxs-lookup"><span data-stu-id="5ca39-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="5ca39-106">Соглашение основывается на взаимодействии, которое устанавливается между двумя партнерами с учетом стандартов транспорта или протокола.</span><span class="sxs-lookup"><span data-stu-id="5ca39-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="5ca39-107">Интеграция Enterprise поддерживает три стандарта протокола или транспорта:</span><span class="sxs-lookup"><span data-stu-id="5ca39-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="5ca39-108">AS2</span><span class="sxs-lookup"><span data-stu-id="5ca39-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="5ca39-109">X12</span><span class="sxs-lookup"><span data-stu-id="5ca39-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="5ca39-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="5ca39-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="5ca39-111">Для чего используются соглашения</span><span class="sxs-lookup"><span data-stu-id="5ca39-111">Why use agreements</span></span>

<span data-ttu-id="5ca39-112">Ниже перечислены некоторые преимущества, связанные с использованием соглашений.</span><span class="sxs-lookup"><span data-stu-id="5ca39-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="5ca39-113">Возможность для разных организаций и компаний обмениваться данными в привычном формате.</span><span class="sxs-lookup"><span data-stu-id="5ca39-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="5ca39-114">Повышает эффективность при проведении транзакций "бизнес-бизнес".</span><span class="sxs-lookup"><span data-stu-id="5ca39-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="5ca39-115">Быстрое создание, использование и администрирование приложений интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5ca39-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="5ca39-116">Как создать соглашение</span><span class="sxs-lookup"><span data-stu-id="5ca39-116">How to create agreements</span></span>

* [<span data-ttu-id="5ca39-117">Создание соглашения AS2</span><span class="sxs-lookup"><span data-stu-id="5ca39-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="5ca39-118">Создание соглашения X12</span><span class="sxs-lookup"><span data-stu-id="5ca39-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="5ca39-119">Создание соглашения EDIFACT</span><span class="sxs-lookup"><span data-stu-id="5ca39-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="5ca39-120">Как использовать соглашение</span><span class="sxs-lookup"><span data-stu-id="5ca39-120">How to use an agreement</span></span>

<span data-ttu-id="5ca39-121">Вы можете создавать [приложения логики](logic-apps-what-are-logic-apps.md "Дополнительные сведения о приложениях логики") с возможностями B2B, используя созданные вами соглашения.</span><span class="sxs-lookup"><span data-stu-id="5ca39-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="5ca39-122">Как изменить соглашение</span><span class="sxs-lookup"><span data-stu-id="5ca39-122">How to edit an agreement</span></span>

<span data-ttu-id="5ca39-123">Любое соглашение можно изменить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5ca39-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="5ca39-124">Выберите учетную запись интеграции, содержащую изменяемое соглашение.</span><span class="sxs-lookup"><span data-stu-id="5ca39-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="5ca39-125">Щелкните плитку **Соглашения**.</span><span class="sxs-lookup"><span data-stu-id="5ca39-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="5ca39-126">В колонке **Соглашения** выберите соглашение.</span><span class="sxs-lookup"><span data-stu-id="5ca39-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="5ca39-127">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="5ca39-127">Choose **Edit**.</span></span> <span data-ttu-id="5ca39-128">Внесите нужные изменения.</span><span class="sxs-lookup"><span data-stu-id="5ca39-128">Make your changes.</span></span>

5. <span data-ttu-id="5ca39-129">Нажмите кнопку **ОК**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="5ca39-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="5ca39-130">Как удалить учетную запись</span><span class="sxs-lookup"><span data-stu-id="5ca39-130">How to delete an agreement</span></span>

<span data-ttu-id="5ca39-131">Любое соглашение можно удалить. Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5ca39-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="5ca39-132">Выберите учетную запись интеграции, содержащую удаляемое соглашение.</span><span class="sxs-lookup"><span data-stu-id="5ca39-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="5ca39-133">Щелкните плитку **Соглашения**.</span><span class="sxs-lookup"><span data-stu-id="5ca39-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="5ca39-134">В колонке **Соглашения** выберите соглашение.</span><span class="sxs-lookup"><span data-stu-id="5ca39-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="5ca39-135">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="5ca39-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="5ca39-136">Подтвердите удаление соглашения.</span><span class="sxs-lookup"><span data-stu-id="5ca39-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="5ca39-137">В колонке соглашений удаленное соглашение больше не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="5ca39-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ca39-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ca39-138">Next steps</span></span>
* [<span data-ttu-id="5ca39-139">Создание соглашения AS2</span><span class="sxs-lookup"><span data-stu-id="5ca39-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
