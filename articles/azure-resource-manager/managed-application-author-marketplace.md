---
title: "Управляемые приложения Azure в Marketplace | Документация Майкрософт"
description: "Описываются управляемые приложения Azure, доступные в Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="023c4-103">Управляемые приложения Azure в Marketplace</span><span class="sxs-lookup"><span data-stu-id="023c4-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="023c4-104">Поставщики управляемых служб, независимые поставщики программного обеспечения и системные интеграторы могут использовать управляемые приложения Azure, чтобы предлагать свои решения всем клиентам Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="023c4-105">Такие решения уменьшают затраты на обслуживание и управление для клиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="023c4-106">Издатели могут продавать инфраструктуру и программное обеспечение через Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="023c4-107">Они могут подключать услуги и эксплуатационную поддержку к управляемым приложениям.</span><span class="sxs-lookup"><span data-stu-id="023c4-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="023c4-108">Дополнительные сведения см. в разделе [Обзор управляемых приложений Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="023c4-109">В этой статье описывается, как поставщики управляемых служб, независимые поставщики программного обеспечения и системные интеграторы могут опубликовать приложения в Marketplace и сделать их широкодоступными для клиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="023c4-110">Предварительные требования для публикации управляемого приложения</span><span class="sxs-lookup"><span data-stu-id="023c4-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="023c4-111">Предварительные требования для добавления приложения в Marketplace</span><span class="sxs-lookup"><span data-stu-id="023c4-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="023c4-112">Технические требования</span><span class="sxs-lookup"><span data-stu-id="023c4-112">Technical</span></span>

    *  <span data-ttu-id="023c4-113">Дополнительные сведения о базовой инфраструктуре и синтаксисе шаблонов Azure Resource Manager см. в статье [Описание структуры и синтаксиса шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="023c4-114">Готовые шаблоны можно найти в статье [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/en-us/documentation/templates/) или [репозитории шаблонов быстрого запуска](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="023c4-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="023c4-115">Дополнительные сведения о создании интерфейса для пользователей, развертывающих ваше приложение через Marketplace, см. в разделе [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="023c4-116">Требования нетехнического характера (бизнес-требования)</span><span class="sxs-lookup"><span data-stu-id="023c4-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="023c4-117">Ваша компания (или ее филиал) должна находиться в стране, на территории которой могут осуществляться продажи в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="023c4-118">Продукт должен иметь лицензию, совместимую с моделями выставления счетов, которые поддерживает Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="023c4-119">Вы должны предоставить клиентам техническую поддержку экономически обоснованным образом.</span><span class="sxs-lookup"><span data-stu-id="023c4-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="023c4-120">Поддержка может быть платной, бесплатной или обеспечиваться посредством поддержки от сообщества.</span><span class="sxs-lookup"><span data-stu-id="023c4-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="023c4-121">Вы несете ответственность за лицензирование программного обеспечения, а также любых зависимостей от стороннего программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="023c4-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="023c4-122">Предоставьте маркетинговые материалы, отвечающие критериям для вашего предложения, соблюдение которых требуется для добавления приложения в Marketplace и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="023c4-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="023c4-123">Вам нужно принять условия политик участия и соглашения для издателей Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="023c4-124">Вам нужно принять условия использования, заявление о конфиденциальности Майкрософт и соглашение по программе сертификации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="023c4-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="023c4-125">Создание предложения приложения Azure</span><span class="sxs-lookup"><span data-stu-id="023c4-125">Create a new Azure application offer</span></span>

<span data-ttu-id="023c4-126">После выполнения необходимых условий можно создать предложение управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="023c4-127">Давайте ознакомимся с кратким обзором предложения и SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="023c4-128">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="023c4-128">Offer</span></span>

<span data-ttu-id="023c4-129">Предложение управляемого приложения соответствует классу предложения продукта от издателя.</span><span class="sxs-lookup"><span data-stu-id="023c4-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="023c4-130">Если у вас есть новый тип решения или приложения, которое вы хотели бы добавить в Marketplace, можно разместить его в качестве нового предложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="023c4-131">Предложение — это коллекция SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="023c4-132">Каждое предложение отображается в виде отдельной сущности в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="023c4-133">SKU</span><span class="sxs-lookup"><span data-stu-id="023c4-133">SKU</span></span>

<span data-ttu-id="023c4-134">SKU — это наименьшая единица предложения, доступная для приобретения.</span><span class="sxs-lookup"><span data-stu-id="023c4-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="023c4-135">Номер SKU в том же классе продуктов (предложении) можно использовать, чтобы:</span><span class="sxs-lookup"><span data-stu-id="023c4-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="023c4-136">указывать различные функции, которые поддерживаются;</span><span class="sxs-lookup"><span data-stu-id="023c4-136">Different features that are supported.</span></span>
* <span data-ttu-id="023c4-137">указывать, является ли предложение управляемым или неуправляемым;</span><span class="sxs-lookup"><span data-stu-id="023c4-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="023c4-138">указывать разные модели выставления счетов, которые поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="023c4-138">Billing models that are supported.</span></span>

<span data-ttu-id="023c4-139">В Marketplace номер SKU отображается внутри родительского предложения,</span><span class="sxs-lookup"><span data-stu-id="023c4-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="023c4-140">а на портале Azure — в качестве отдельной сущности, доступной для приобретения.</span><span class="sxs-lookup"><span data-stu-id="023c4-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="023c4-141">Настройка предложения</span><span class="sxs-lookup"><span data-stu-id="023c4-141">Set up an offer</span></span>

1. <span data-ttu-id="023c4-142">Войдите на [портал Cloud Partner](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="023c4-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="023c4-143">В области навигации слева выберите **+ Новое предложение** > **Приложения Azure**.</span><span class="sxs-lookup"><span data-stu-id="023c4-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Новое предложение](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="023c4-145">Заполните формы в левой части представления **Редактор**.</span><span class="sxs-lookup"><span data-stu-id="023c4-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="023c4-146">Обязательные для заполнения поля отмечены красной звездочкой (*).</span><span class="sxs-lookup"><span data-stu-id="023c4-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Параметры предложения](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="023c4-148">Для создания управляемого приложения используются четыре основные формы.</span><span class="sxs-lookup"><span data-stu-id="023c4-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="023c4-149">а.</span><span class="sxs-lookup"><span data-stu-id="023c4-149">a.</span></span> <span data-ttu-id="023c4-150">Параметры предложения</span><span class="sxs-lookup"><span data-stu-id="023c4-150">Offer Settings</span></span>

    <span data-ttu-id="023c4-151">b.</span><span class="sxs-lookup"><span data-stu-id="023c4-151">b.</span></span> <span data-ttu-id="023c4-152">Номера SKU</span><span class="sxs-lookup"><span data-stu-id="023c4-152">SKUs</span></span>

    <span data-ttu-id="023c4-153">c.</span><span class="sxs-lookup"><span data-stu-id="023c4-153">c.</span></span> <span data-ttu-id="023c4-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="023c4-154">Marketplace</span></span>

    <span data-ttu-id="023c4-155">d.</span><span class="sxs-lookup"><span data-stu-id="023c4-155">d.</span></span> <span data-ttu-id="023c4-156">Поддержка</span><span class="sxs-lookup"><span data-stu-id="023c4-156">Support</span></span>

<span data-ttu-id="023c4-157">Эти формы описаны более подробно в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="023c4-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="023c4-158">Форма параметров предложения</span><span class="sxs-lookup"><span data-stu-id="023c4-158">Offer Settings form</span></span>
<span data-ttu-id="023c4-159">Укажите параметры предложения в этой базовой форме.</span><span class="sxs-lookup"><span data-stu-id="023c4-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="023c4-160">Заполните форму **Параметры предложения**.</span><span class="sxs-lookup"><span data-stu-id="023c4-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="023c4-161">Ниже описаны ее поля:</span><span class="sxs-lookup"><span data-stu-id="023c4-161">The different fields are:</span></span>

    <span data-ttu-id="023c4-162">а.</span><span class="sxs-lookup"><span data-stu-id="023c4-162">a.</span></span> <span data-ttu-id="023c4-163">**Идентификатор предложения**. Уникальный идентификатор предложения в профиле издателя.</span><span class="sxs-lookup"><span data-stu-id="023c4-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="023c4-164">Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="023c4-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="023c4-165">Идентификатор может содержать только строчные буквы, цифры или дефисы (-).</span><span class="sxs-lookup"><span data-stu-id="023c4-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="023c4-166">Идентификатор не может заканчиваться дефисом.</span><span class="sxs-lookup"><span data-stu-id="023c4-166">The ID can't end in a dash.</span></span> <span data-ttu-id="023c4-167">Его длина не должна превышать 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="023c4-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="023c4-168">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="023c4-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="023c4-169">b.</span><span class="sxs-lookup"><span data-stu-id="023c4-169">b.</span></span> <span data-ttu-id="023c4-170">**Идентификатор издателя**. Из этого раскрывающегося списка можно выбрать профиль издателя, используемый для публикации этого предложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="023c4-171">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="023c4-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="023c4-172">c.</span><span class="sxs-lookup"><span data-stu-id="023c4-172">c.</span></span> <span data-ttu-id="023c4-173">**Имя**. Отображаемое имя вашего предложения в Marketplace и на портале.</span><span class="sxs-lookup"><span data-stu-id="023c4-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="023c4-174">Его длина не должна превышать 50 символов.</span><span class="sxs-lookup"><span data-stu-id="023c4-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="023c4-175">Укажите для своего продукта узнаваемое название торговой марки.</span><span class="sxs-lookup"><span data-stu-id="023c4-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="023c4-176">Не включайте в него название своей организации, если только это не требуется для продвижения продукта.</span><span class="sxs-lookup"><span data-stu-id="023c4-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="023c4-177">Если вы продвигаете это предложение через свой веб-сайт, убедитесь, что данное имя полностью совпадает с используемым на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="023c4-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="023c4-178">Щелкните **Сохранить**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="023c4-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="023c4-179">Форма номеров SKU</span><span class="sxs-lookup"><span data-stu-id="023c4-179">SKUs form</span></span>
<span data-ttu-id="023c4-180">Следующим шагом является добавление номеров SKU для вашего предложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="023c4-181">Выберите **Номера SKU** > **Новый код SKU**.</span><span class="sxs-lookup"><span data-stu-id="023c4-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Выбор нового номера SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="023c4-183">Введите **идентификатор SKU**.</span><span class="sxs-lookup"><span data-stu-id="023c4-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="023c4-184">Идентификатор SKU — это уникальный идентификатор номера SKU в рамках предложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="023c4-185">Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="023c4-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="023c4-186">Идентификатор может содержать только строчные буквы, цифры или дефисы (-).</span><span class="sxs-lookup"><span data-stu-id="023c4-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="023c4-187">Он не может заканчиваться дефисом, а его длина не должна превышать 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="023c4-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="023c4-188">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="023c4-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="023c4-189">В предложении можно использовать несколько SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="023c4-190">Номер SKU нужен для каждого публикуемого образа.</span><span class="sxs-lookup"><span data-stu-id="023c4-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="023c4-191">Заполните раздел **SKU Details** (Сведения о номере SKU) в приведенной ниже форме.</span><span class="sxs-lookup"><span data-stu-id="023c4-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![Указание нового номера SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="023c4-193">Заполните приведенные ниже поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="023c4-194">а.</span><span class="sxs-lookup"><span data-stu-id="023c4-194">a.</span></span> <span data-ttu-id="023c4-195">**Название**. Введите название для номера SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="023c4-196">Данное название элемента отображается в коллекции.</span><span class="sxs-lookup"><span data-stu-id="023c4-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="023c4-197">b.</span><span class="sxs-lookup"><span data-stu-id="023c4-197">b.</span></span> <span data-ttu-id="023c4-198">**Сводка**. Введите краткое описание номера SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="023c4-199">Этот текст отображается под названием.</span><span class="sxs-lookup"><span data-stu-id="023c4-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="023c4-200">c.</span><span class="sxs-lookup"><span data-stu-id="023c4-200">c.</span></span> <span data-ttu-id="023c4-201">**Описание**. Введите подробное описание номера SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="023c4-202">d.</span><span class="sxs-lookup"><span data-stu-id="023c4-202">d.</span></span> <span data-ttu-id="023c4-203">**Тип SKU**. Допустимыми значениями являются **Управляемое приложение** и **Шаблоны решений**.</span><span class="sxs-lookup"><span data-stu-id="023c4-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="023c4-204">В этом случае выберите **Managed Application** (Управляемое приложение).</span><span class="sxs-lookup"><span data-stu-id="023c4-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="023c4-205">Заполните раздел **Сведения о пакете** в приведенной ниже форме.</span><span class="sxs-lookup"><span data-stu-id="023c4-205">Fill out the **Package Details** section on the following form:</span></span>

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="023c4-207">Заполните приведенные ниже поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-207">Fill out the following fields:</span></span>

    <span data-ttu-id="023c4-208">а.</span><span class="sxs-lookup"><span data-stu-id="023c4-208">a.</span></span> <span data-ttu-id="023c4-209">**Текущая версия**. Введите версию передаваемого пакета.</span><span class="sxs-lookup"><span data-stu-id="023c4-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="023c4-210">Ее необходимо указать в формате `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="023c4-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="023c4-211">b.</span><span class="sxs-lookup"><span data-stu-id="023c4-211">b.</span></span> <span data-ttu-id="023c4-212">**Выбор файла пакета**. Этот пакет содержит следующие файлы, которые будут сжаты в ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="023c4-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="023c4-213">**applianceMainTemplate.json**. Это файл шаблона развертывания, который используется для развертывания решения или приложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="023c4-214">Дополнительные сведения о создании файлов шаблонов развертывания см. в статье [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="023c4-215">**appliancecreateUIDefinition.json**. Этот файл используется порталом Azure, чтобы создать пользовательский интерфейс для подготовки этого решения или приложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="023c4-216">Дополнительные сведения см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="023c4-217">**mainTemplate.json**. Это файл шаблона, который содержит только ресурс Microsoft.Solution/appliances.</span><span class="sxs-lookup"><span data-stu-id="023c4-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="023c4-218">mainTemplate содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="023c4-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="023c4-219">**kind**. Используйте **Marketplace** для управляемых приложений в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="023c4-220">**managedResourceGroupId**. Это группа ресурсов в подписке клиента, в которой развертываются все ресурсы, определенные в файле applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="023c4-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="023c4-221">**PublisherPackageId**. Это строка, которая уникальным образом идентифицирует пакет.</span><span class="sxs-lookup"><span data-stu-id="023c4-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="023c4-222">Укажите значение в формате `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="023c4-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="023c4-223">Получите **идентификатор предложения** и **идентификатор издателя** на портале публикации, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="023c4-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![Offer ID (Идентификатор предложения)](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="023c4-225">Получите **идентификатор SKU**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="023c4-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![Идентификатор SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="023c4-227">Получите **версию** пакета, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="023c4-227">Obtain the package **Version**, as shown in the following image:</span></span>

![Версия пакета](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="023c4-229">Исходя из предыдущих примеров, значение **PublisherPackageId** — `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="023c4-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="023c4-230">Пример mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="023c4-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="023c4-231">Этот пакет должен содержать все другие вложенные шаблоны или скрипты, необходимые для успешной подготовки этого приложения.</span><span class="sxs-lookup"><span data-stu-id="023c4-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="023c4-232">Файлы mainTemplate.json, applianceMainTemplate.json и applianceCreateUIDefinition.json должны находиться в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="023c4-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="023c4-233">**Authorizations**. Это свойство определяет, кто и на каком уровне получает доступ к ресурсам в подписках клиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="023c4-234">Оно позволяет издателю управлять приложением от имени клиента.</span><span class="sxs-lookup"><span data-stu-id="023c4-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="023c4-235">**PrincipalId**. Это свойство является идентификатором Azure Active Directory (Azure AD) пользователя, группы пользователей или приложения, которому предоставляются определенные разрешения для ресурсов в подписке клиента.</span><span class="sxs-lookup"><span data-stu-id="023c4-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="023c4-236">Эти разрешения описывает свойство Role Definition.</span><span class="sxs-lookup"><span data-stu-id="023c4-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="023c4-237">**Role Definition**. Это свойство является списком всех встроенных ролей RBAC (управление доступом на основе ролей), предоставляемых Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023c4-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="023c4-238">Можно выбрать наиболее подходящую роль, чтобы управлять ресурсами от имени клиента.</span><span class="sxs-lookup"><span data-stu-id="023c4-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="023c4-239">Можно добавить несколько разрешений.</span><span class="sxs-lookup"><span data-stu-id="023c4-239">You can add multiple authorizations.</span></span> <span data-ttu-id="023c4-240">Рекомендуется создать группу пользователей AD и указать ее идентификатор в свойстве **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="023c4-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="023c4-241">Таким образом можно будет добавлять пользователей в эту группу без необходимости обновлять номер SKU.</span><span class="sxs-lookup"><span data-stu-id="023c4-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="023c4-242">Дополнительные сведения об управлении доступом на основе ролей см. в статье [Начало работы с управлением доступом на основе ролей на портале Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="023c4-243">Форма Marketplace</span><span class="sxs-lookup"><span data-stu-id="023c4-243">Marketplace form</span></span>

<span data-ttu-id="023c4-244">Форма Marketplace запрашивает поля, отображаемые в [Azure Marketplace](https://azuremarketplace.microsoft.com) и на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="023c4-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="023c4-245">Идентификаторы подписок для предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="023c4-245">Preview subscription IDs</span></span>

<span data-ttu-id="023c4-246">Введите список идентификаторов подписок Azure, у которых будет доступ к предложению после его публикации.</span><span class="sxs-lookup"><span data-stu-id="023c4-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="023c4-247">Эти разрешенные подписки можно использовать, чтобы протестировать предварительную версию предложения перед его активацией.</span><span class="sxs-lookup"><span data-stu-id="023c4-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="023c4-248">На портале для партнеров можно добавить в список разрешений до 100 подписок.</span><span class="sxs-lookup"><span data-stu-id="023c4-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="023c4-249">Предлагаемые категории</span><span class="sxs-lookup"><span data-stu-id="023c4-249">Suggested categories</span></span>

<span data-ttu-id="023c4-250">Выберите из списка до пяти категорий, которые точнее всего описывают ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="023c4-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="023c4-251">Эти категории используются для сопоставления вашего предложения с категориями продуктов, доступными в [Azure Marketplace](https://azuremarketplace.microsoft.com) и на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="023c4-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="023c4-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="023c4-252">Azure Marketplace</span></span>

<span data-ttu-id="023c4-253">В разделе сводки управляемого приложения отображаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-253">The summary of your managed application displays the following fields:</span></span>

![Сводка Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="023c4-255">На вкладке **Обзор** управляемого приложения отображаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![Обзор Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="023c4-257">На вкладке **Планы + цены** управляемого приложения отображаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Планы Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="023c4-259">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="023c4-259">Azure portal</span></span>

<span data-ttu-id="023c4-260">В разделе сводки управляемого приложения отображаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-260">The summary of your managed application displays the following fields:</span></span>

![Сводка на портале](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="023c4-262">В обзоре управляемого приложения отображаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="023c4-262">The overview for your managed application displays the following fields:</span></span>

![Общие сведения на портале](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="023c4-264">Рекомендации по логотипам</span><span class="sxs-lookup"><span data-stu-id="023c4-264">Logo guidelines</span></span>

<span data-ttu-id="023c4-265">Следуйте приведенным ниже указаниям для любого логотипа, передаваемого на портал Cloud Partner.</span><span class="sxs-lookup"><span data-stu-id="023c4-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="023c4-266">Дизайн Azure отличается простой цветовой палитрой.</span><span class="sxs-lookup"><span data-stu-id="023c4-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="023c4-267">Используйте в логотипах ограниченное число основных и дополнительных цветов.</span><span class="sxs-lookup"><span data-stu-id="023c4-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="023c4-268">Цвета темы портала — белый и черный.</span><span class="sxs-lookup"><span data-stu-id="023c4-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="023c4-269">Постарайтесь не использовать эти цвета для фона своего логотипа.</span><span class="sxs-lookup"><span data-stu-id="023c4-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="023c4-270">Используйте цвет, который выделяет ваш логотип на портале.</span><span class="sxs-lookup"><span data-stu-id="023c4-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="023c4-271">Мы рекомендуем простые основные цвета.</span><span class="sxs-lookup"><span data-stu-id="023c4-271">We recommend simple primary colors.</span></span> <span data-ttu-id="023c4-272">*При использовании прозрачного фона убедитесь, что для логотипа и текста не используется белый, черный или синий цвет.*</span><span class="sxs-lookup"><span data-stu-id="023c4-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="023c4-273">Не используйте в логотипе градиентный фон.</span><span class="sxs-lookup"><span data-stu-id="023c4-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="023c4-274">Не размещайте в логотипе текст, даже название своей компании или торговой марки.</span><span class="sxs-lookup"><span data-stu-id="023c4-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="023c4-275">Логотип должен быть сплошным, избегайте градиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="023c4-276">Логотип не должен быть растянут.</span><span class="sxs-lookup"><span data-stu-id="023c4-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="023c4-277">Имиджевый логотип</span><span class="sxs-lookup"><span data-stu-id="023c4-277">Hero logo</span></span>

<span data-ttu-id="023c4-278">Имиджевый логотип использовать необязательно.</span><span class="sxs-lookup"><span data-stu-id="023c4-278">The hero logo is optional.</span></span> <span data-ttu-id="023c4-279">Издатель может не передавать такой логотип.</span><span class="sxs-lookup"><span data-stu-id="023c4-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="023c4-280">После передачи имиджевого значка его нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="023c4-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="023c4-281">Партнер также должен следовать рекомендациям для имиджевых значков Marketplace.</span><span class="sxs-lookup"><span data-stu-id="023c4-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="023c4-282">Следуйте приведенным ниже рекомендациям для значка имиджевого логотипа.</span><span class="sxs-lookup"><span data-stu-id="023c4-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="023c4-283">Отображаемое имя издателя, название плана и развернутая сводка предложения отображаются белым цветом.</span><span class="sxs-lookup"><span data-stu-id="023c4-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="023c4-284">Поэтому не используйте светлый цвет для фона имиджевого значка.</span><span class="sxs-lookup"><span data-stu-id="023c4-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="023c4-285">Фон имиджевого значка не может быть черным, белым или прозрачным.</span><span class="sxs-lookup"><span data-stu-id="023c4-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="023c4-286">Как только предложение вносится в список, в имиджевый логотип программно вставляется отображаемое имя издателя, название плана, развернутая сводка предложения и кнопка **Создать**.</span><span class="sxs-lookup"><span data-stu-id="023c4-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="023c4-287">Следовательно, не нужно добавлять какой-либо текст в процессе разработки имиджевого логотипа.</span><span class="sxs-lookup"><span data-stu-id="023c4-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="023c4-288">Оставьте пустое место справа, так как туда будет программно добавлен текст.</span><span class="sxs-lookup"><span data-stu-id="023c4-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="023c4-289">Для текста следует оставить справа пустое место 415 на 100 пикселей.</span><span class="sxs-lookup"><span data-stu-id="023c4-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="023c4-290">Смещение от левого края должно составлять 370 пикселей.</span><span class="sxs-lookup"><span data-stu-id="023c4-290">It's offset by 370 pixels from the left.</span></span>

    ![Пример имиджевого логотипа](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="023c4-292">Форма службы поддержки</span><span class="sxs-lookup"><span data-stu-id="023c4-292">Support form</span></span>

<span data-ttu-id="023c4-293">Заполните форму **Поддержка** контактными данными службы поддержки своей компании.</span><span class="sxs-lookup"><span data-stu-id="023c4-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="023c4-294">Это могут быть контактные данные технического отдела или службы поддержки клиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="023c4-295">Публикация предложения</span><span class="sxs-lookup"><span data-stu-id="023c4-295">Publish an offer</span></span>

<span data-ttu-id="023c4-296">Заполнив все разделы, щелкните **Опубликовать**, чтобы начать процесс размещения вашего приложения для клиентов.</span><span class="sxs-lookup"><span data-stu-id="023c4-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="023c4-297">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="023c4-297">Next steps</span></span>

* <span data-ttu-id="023c4-298">Общие сведения об управляемых приложениях Azure см. в разделе [Обзор управляемых приложений Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="023c4-299">Сведения об использовании управляемого приложения из Marketplace см. в статье [Использование управляемых приложений Azure в Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="023c4-300">Сведения о публикации управляемых приложений в каталоге услуг см. в разделе [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="023c4-301">Дополнительные сведения об использовании управляемых приложений из каталога услуг см. в разделе [Использование управляемого приложения Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="023c4-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
