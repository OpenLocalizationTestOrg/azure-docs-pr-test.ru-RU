---
title: "aaaAzure управляемого приложения в hello Marketplace | Документы Microsoft"
description: "Описывает Azure управляемых приложений, доступных через hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="b1b03-103">Azure управляемого приложения в hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="b1b03-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="b1b03-104">MSPs, независимые поставщики программного обеспечения и системным интеграторам (копий SIs) могут использовать Azure управляемых приложений toooffer своим клиентам решения tooall Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1b03-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="b1b03-105">Такие решения сократить обслуживания hello и необходимость обновления для клиентов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="b1b03-106">Издатели могут продавать инфраструктуры и программное обеспечение с помощью hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1b03-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="b1b03-107">Их можно присоединить службы и приложения toomanaged оперативного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1b03-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="b1b03-108">Дополнительные сведения см. в разделе [Обзор управляемых приложений Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="b1b03-109">В этой статье объясняется, как MSP, ISV или удостоверения службы можно опубликовать приложение toohello Marketplace и сделать его toocustomers широко доступны.</span><span class="sxs-lookup"><span data-stu-id="b1b03-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="b1b03-110">Предварительные требования для публикации управляемого приложения</span><span class="sxs-lookup"><span data-stu-id="b1b03-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="b1b03-111">Предварительные требования toolisting в hello Marketplace:</span><span class="sxs-lookup"><span data-stu-id="b1b03-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="b1b03-112">Технические требования</span><span class="sxs-lookup"><span data-stu-id="b1b03-112">Technical</span></span>

    *  <span data-ttu-id="b1b03-113">Сведения о hello базовая структура и синтаксис шаблонов диспетчера ресурсов Azure см. в разделе [шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="b1b03-114">tooview завершения и шаблонов, в разделе [шаблоны быстрый запуск Azure](https://azure.microsoft.com/en-us/documentation/templates/) или hello [шаблон репозитория краткое руководство](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="b1b03-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="b1b03-115">Сведения о том, как toocreate hello интерфейс пользователям для развертывания приложения через hello Marketplace см. в разделе [создать файл определения интерфейса пользователя](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="b1b03-116">Требования нетехнического характера (бизнес-требования)</span><span class="sxs-lookup"><span data-stu-id="b1b03-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="b1b03-117">Ваша компания или его дочерним подразделением должен быть расположен в стране, где продажи поддерживаются hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1b03-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="b1b03-118">Способом, совместимый с моделями выставления счетов, поддерживаемые hello Marketplace должны иметь лицензию на продукт.</span><span class="sxs-lookup"><span data-stu-id="b1b03-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="b1b03-119">Вы ответственным за обеспечение разумные образом доступных toocustomers технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="b1b03-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="b1b03-120">Поддержка Hello можно бесплатно, оплачен, или сообществе поддержки.</span><span class="sxs-lookup"><span data-stu-id="b1b03-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="b1b03-121">Вы несете ответственность за лицензирование программного обеспечения, а также любых зависимостей от стороннего программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="b1b03-122">Необходимо предоставить содержимое, которое не отвечает требованиям вашего предложения toobe, перечисленных в hello Marketplace и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b03-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="b1b03-123">Необходимо принять условия toohello hello Azure Marketplace участие политик и соглашение для издателей.</span><span class="sxs-lookup"><span data-stu-id="b1b03-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="b1b03-124">Toocomply hello условия использования, заявление о конфиденциальности и соглашение Microsoft Azure Certified программы должны быть согласованы.</span><span class="sxs-lookup"><span data-stu-id="b1b03-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="b1b03-125">Создание предложения приложения Azure</span><span class="sxs-lookup"><span data-stu-id="b1b03-125">Create a new Azure application offer</span></span>

<span data-ttu-id="b1b03-126">После требованиям hello вы будете готовы toocreate ваше предложение управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="b1b03-127">Давайте ознакомимся с кратким обзором предложения и SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="b1b03-128">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="b1b03-128">Offer</span></span>

<span data-ttu-id="b1b03-129">предложение Hello управляемого приложения соответствует класс tooa продукта предложения от издателя.</span><span class="sxs-lookup"><span data-stu-id="b1b03-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="b1b03-130">Если новый тип решения или приложения, которые должны toomake в hello Marketplace, можно настроить его как новое предложение.</span><span class="sxs-lookup"><span data-stu-id="b1b03-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="b1b03-131">Предложение — это коллекция SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="b1b03-132">Каждый предложение отображается как свой собственный сущности в hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1b03-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="b1b03-133">SKU</span><span class="sxs-lookup"><span data-stu-id="b1b03-133">SKU</span></span>

<span data-ttu-id="b1b03-134">SKU — hello наименьший предлагаемые для продажи Единица предложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="b1b03-135">Можно использовать SKU внутри hello же toodifferentiate продукта класс (предложение) между:</span><span class="sxs-lookup"><span data-stu-id="b1b03-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="b1b03-136">указывать различные функции, которые поддерживаются;</span><span class="sxs-lookup"><span data-stu-id="b1b03-136">Different features that are supported.</span></span>
* <span data-ttu-id="b1b03-137">Является ли предложение hello управляемым или неуправляемым.</span><span class="sxs-lookup"><span data-stu-id="b1b03-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="b1b03-138">указывать разные модели выставления счетов, которые поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b1b03-138">Billing models that are supported.</span></span>

<span data-ttu-id="b1b03-139">В рамках предложения родительского hello в hello Marketplace появляется SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="b1b03-140">Он отображается как свой собственный предлагаемые для продажи сущности в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b03-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="b1b03-141">Настройка предложения</span><span class="sxs-lookup"><span data-stu-id="b1b03-141">Set up an offer</span></span>

1. <span data-ttu-id="b1b03-142">Войдите в toohello [портал Cloud Partner](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b1b03-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="b1b03-143">В области навигации hello hello левой части окна выберите **+ новое предложение** > **приложений Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1b03-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Новое предложение](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="b1b03-145">Заполнение форм hello, отображаемые на оставшийся hello hello **редактор** представления.</span><span class="sxs-lookup"><span data-stu-id="b1b03-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="b1b03-146">Обязательные для заполнения поля отмечены красной звездочкой (*).</span><span class="sxs-lookup"><span data-stu-id="b1b03-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Параметры предложения](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="b1b03-148">Четыре основные формы являются используется toocreate управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="b1b03-149">а.</span><span class="sxs-lookup"><span data-stu-id="b1b03-149">a.</span></span> <span data-ttu-id="b1b03-150">Параметры предложения</span><span class="sxs-lookup"><span data-stu-id="b1b03-150">Offer Settings</span></span>

    <span data-ttu-id="b1b03-151">b.</span><span class="sxs-lookup"><span data-stu-id="b1b03-151">b.</span></span> <span data-ttu-id="b1b03-152">Номера SKU</span><span class="sxs-lookup"><span data-stu-id="b1b03-152">SKUs</span></span>

    <span data-ttu-id="b1b03-153">c.</span><span class="sxs-lookup"><span data-stu-id="b1b03-153">c.</span></span> <span data-ttu-id="b1b03-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="b1b03-154">Marketplace</span></span>

    <span data-ttu-id="b1b03-155">d.</span><span class="sxs-lookup"><span data-stu-id="b1b03-155">d.</span></span> <span data-ttu-id="b1b03-156">Поддержка</span><span class="sxs-lookup"><span data-stu-id="b1b03-156">Support</span></span>

<span data-ttu-id="b1b03-157">Эти формы описаны более подробно в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="b1b03-158">Форма параметров предложения</span><span class="sxs-lookup"><span data-stu-id="b1b03-158">Offer Settings form</span></span>
<span data-ttu-id="b1b03-159">С помощью этой базовой форме toospecify hello предложение параметров.</span><span class="sxs-lookup"><span data-stu-id="b1b03-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="b1b03-160">Заполните hello **предоставляют параметры** формы.</span><span class="sxs-lookup"><span data-stu-id="b1b03-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="b1b03-161">Hello различные поля являются:</span><span class="sxs-lookup"><span data-stu-id="b1b03-161">hello different fields are:</span></span>

    <span data-ttu-id="b1b03-162">а.</span><span class="sxs-lookup"><span data-stu-id="b1b03-162">a.</span></span> <span data-ttu-id="b1b03-163">**Код предложения**: предложение hello в профиле издателя идентифицирует этот уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b1b03-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="b1b03-164">Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="b1b03-165">Идентификатор может содержать только строчные буквы, цифры или дефисы (-).</span><span class="sxs-lookup"><span data-stu-id="b1b03-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="b1b03-166">Идентификатор Hello не может заканчиваться дефисом.</span><span class="sxs-lookup"><span data-stu-id="b1b03-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="b1b03-167">Это ограниченное tooa более 50 символов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="b1b03-168">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="b1b03-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="b1b03-169">b.</span><span class="sxs-lookup"><span data-stu-id="b1b03-169">b.</span></span> <span data-ttu-id="b1b03-170">**Идентификатор издателя**: использовать конфигурацию издателя раскрывающегося списка toochoose hello требуется toopublish это предложение в группе.</span><span class="sxs-lookup"><span data-stu-id="b1b03-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="b1b03-171">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="b1b03-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="b1b03-172">c.</span><span class="sxs-lookup"><span data-stu-id="b1b03-172">c.</span></span> <span data-ttu-id="b1b03-173">**Имя**: это отображаемое имя для вашего предложения отображается в hello Marketplace и hello портала.</span><span class="sxs-lookup"><span data-stu-id="b1b03-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="b1b03-174">Его длина не должна превышать 50 символов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="b1b03-175">Укажите для своего продукта узнаваемое название торговой марки.</span><span class="sxs-lookup"><span data-stu-id="b1b03-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="b1b03-176">Не включайте в него название своей организации, если только это не требуется для продвижения продукта.</span><span class="sxs-lookup"><span data-stu-id="b1b03-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="b1b03-177">Если маркетинг это предложение на собственных веб-сайте убедитесь, что это имя hello именно ее отображение на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="b1b03-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="b1b03-178">Выберите **Сохранить** toosave хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="b1b03-179">Форма номеров SKU</span><span class="sxs-lookup"><span data-stu-id="b1b03-179">SKUs form</span></span>
<span data-ttu-id="b1b03-180">Hello следующим шагом является tooadd SKU для вашего предложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="b1b03-181">Выберите **Номера SKU** > **Новый код SKU**.</span><span class="sxs-lookup"><span data-stu-id="b1b03-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Выбор нового номера SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="b1b03-183">Введите **идентификатор SKU**.</span><span class="sxs-lookup"><span data-stu-id="b1b03-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="b1b03-184">Идентификатор SKU — это уникальный идентификатор для hello SKU внутри предложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="b1b03-185">Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="b1b03-186">Идентификатор может содержать только строчные буквы, цифры или дефисы (-).</span><span class="sxs-lookup"><span data-stu-id="b1b03-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="b1b03-187">Идентификатор Hello не может заканчиваться дефисом и является ограниченной tooa более 50 символов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="b1b03-188">После активации предложения это поле блокируется.</span><span class="sxs-lookup"><span data-stu-id="b1b03-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="b1b03-189">В предложении можно использовать несколько SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="b1b03-190">Требуется SKU для каждого изображения планирование toopublish.</span><span class="sxs-lookup"><span data-stu-id="b1b03-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="b1b03-191">Заполните hello **подробности номера SKU** раздела, посвященного hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="b1b03-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Указание нового номера SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="b1b03-193">Заполните следующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="b1b03-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="b1b03-194">а.</span><span class="sxs-lookup"><span data-stu-id="b1b03-194">a.</span></span> <span data-ttu-id="b1b03-195">**Название**. Введите название для номера SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="b1b03-196">Этот заголовок отображается в галерее hello для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="b1b03-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="b1b03-197">b.</span><span class="sxs-lookup"><span data-stu-id="b1b03-197">b.</span></span> <span data-ttu-id="b1b03-198">**Сводка**. Введите краткое описание номера SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="b1b03-199">Этот текст отображается под заголовок hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="b1b03-200">c.</span><span class="sxs-lookup"><span data-stu-id="b1b03-200">c.</span></span> <span data-ttu-id="b1b03-201">**Описание**: Введите подробное описание hello SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="b1b03-202">d.</span><span class="sxs-lookup"><span data-stu-id="b1b03-202">d.</span></span> <span data-ttu-id="b1b03-203">**Тип SKU**: hello допустимые значения: **управляемые приложения** и **шаблоны решений**.</span><span class="sxs-lookup"><span data-stu-id="b1b03-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="b1b03-204">В этом случае выберите **Managed Application** (Управляемое приложение).</span><span class="sxs-lookup"><span data-stu-id="b1b03-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="b1b03-205">Заполните hello **сведения о пакете** раздела, посвященного hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="b1b03-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="b1b03-207">Заполните следующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="b1b03-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="b1b03-208">а.</span><span class="sxs-lookup"><span data-stu-id="b1b03-208">a.</span></span> <span data-ttu-id="b1b03-209">**Текущая версия**: введите версию для отправки пакета hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="b1b03-210">Он должен быть в формате hello `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="b1b03-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="b1b03-211">b.</span><span class="sxs-lookup"><span data-stu-id="b1b03-211">b.</span></span> <span data-ttu-id="b1b03-212">**Выберите файл пакета**: этот пакет содержит следующие файлы, которые сжимаются в ZIP-файл hello:</span><span class="sxs-lookup"><span data-stu-id="b1b03-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="b1b03-213">**applianceMainTemplate.json**: файл шаблона развертывания hello, применяющее toodeploy hello решения или приложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="b1b03-214">Сведения о том, как файлы шаблона toocreate развертывания, в разделе [создать свой первый диспетчера ресурсов Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="b1b03-215">**appliancecreateUIDefinition.json**: этот файл используется hello Azure портала toogenerate hello пользовательский интерфейс, который использовал tooprovision решений/приложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="b1b03-216">Дополнительные сведения см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="b1b03-217">**mainTemplate.json**: этот файл шаблона содержит только hello Microsoft.Solution/appliances ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="b1b03-218">файл mainTemplate Hello включает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b1b03-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="b1b03-219">**Тип**: использование **Marketplace** для управляемых приложений в hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1b03-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="b1b03-220">**ManagedResourceGroupId**: Эта группа ресурсов в подписке клиента hello — где развернуты все ресурсы hello, определенные в applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="b1b03-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="b1b03-221">**PublisherPackageId**: Эта строка, однозначно определяющее hello пакета.</span><span class="sxs-lookup"><span data-stu-id="b1b03-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="b1b03-222">Укажите значение hello в формат hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="b1b03-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="b1b03-223">Получить hello **предлагают идентификатор** и **идентификатор издателя** из hello публикации портала, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="b1b03-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Offer ID (Идентификатор предложения)](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="b1b03-225">Получить hello **SKU ID**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="b1b03-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![Идентификатор SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="b1b03-227">Получить пакет hello **версии**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="b1b03-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Версия пакета](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="b1b03-229">На основании hello в предыдущих примерах, hello значение **PublisherPackageId** — `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="b1b03-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="b1b03-230">Пример mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="b1b03-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
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

<span data-ttu-id="b1b03-231">Этот пакет должен содержать вложенные шаблоны или скрипты, необходимые toosuccessfully подготовки этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="b1b03-232">Hello mainTemplate.json, applianceMainTemplate.json и applianceCreateUIDefinition.json файла должны находиться в корневой папке hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="b1b03-233">**Параметры авторизации**: это свойство определяет, кто получает доступ и hello уровень доступа toohello ресурсы в подписках клиентов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="b1b03-234">Hello publisher можно использовать приложение hello toomanage от имени клиента hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="b1b03-235">**PrincipalId**: это свойство является hello Azure Active Directory (Azure AD) идентификатор пользователя, группы пользователей или приложение, которое предоставляет определенные разрешения на ресурсы hello в подписке клиента hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="b1b03-236">Hello определение роли описывает hello разрешения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="b1b03-237">**Определение роли**: это свойство является всех hello встроенных управление доступом на основе ролей (RBAC) роли, предоставляемые Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1b03-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="b1b03-238">Вы можете выбрать роли hello, наиболее подходящий toouse toomanage hello ресурсам от имени клиента hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="b1b03-239">Можно добавить несколько разрешений.</span><span class="sxs-lookup"><span data-stu-id="b1b03-239">You can add multiple authorizations.</span></span> <span data-ttu-id="b1b03-240">Рекомендуется создать группу пользователей AD и указать ее идентификатор в свойстве **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="b1b03-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="b1b03-241">Таким образом, можно добавить дополнительные группы пользователей toohello пользователей без hello необходимость tooupdate hello SKU.</span><span class="sxs-lookup"><span data-stu-id="b1b03-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="b1b03-242">Дополнительные сведения о ролевой Авторизации см. в разделе [Приступая к работе с RBAC в hello портал Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="b1b03-243">Форма Marketplace</span><span class="sxs-lookup"><span data-stu-id="b1b03-243">Marketplace form</span></span>

<span data-ttu-id="b1b03-244">запрашивает у Hello Marketplace формы поля, которые отображаются на hello [Azure Marketplace](https://azuremarketplace.microsoft.com) и на hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b1b03-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="b1b03-245">Идентификаторы подписок для предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="b1b03-245">Preview subscription IDs</span></span>

<span data-ttu-id="b1b03-246">Введите список подписки Azure идентификаторы, которые могут обращаться к предложению hello после его публикации.</span><span class="sxs-lookup"><span data-stu-id="b1b03-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="b1b03-247">Прежде чем сделать ее можно использовать эти предложения hello предварительного просмотра tootest белого списка подписок live.</span><span class="sxs-lookup"><span data-stu-id="b1b03-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="b1b03-248">Можно скомпилировать белый список too100 подписки на портале партнера hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="b1b03-249">Предлагаемые категории</span><span class="sxs-lookup"><span data-stu-id="b1b03-249">Suggested categories</span></span>

<span data-ttu-id="b1b03-250">Выберите категории toofive из списка hello, ваше предложение может быть лучше всего связан.</span><span class="sxs-lookup"><span data-stu-id="b1b03-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="b1b03-251">Эти категории являются вашего предложения toohello категории продуктов, доступных в hello используется toomap [Azure Marketplace](https://azuremarketplace.microsoft.com) и hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b1b03-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="b1b03-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b1b03-252">Azure Marketplace</span></span>

<span data-ttu-id="b1b03-253">Сводка Hello приложение отображает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="b1b03-253">hello summary of your managed application displays hello following fields:</span></span>

![Сводка Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="b1b03-255">Hello **Обзор** вкладке приложение отображает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="b1b03-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Обзор Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="b1b03-257">Hello **планы + цены** вкладке приложение отображает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="b1b03-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Планы Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="b1b03-259">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b1b03-259">Azure portal</span></span>

<span data-ttu-id="b1b03-260">Сводка Hello приложение отображает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="b1b03-260">hello summary of your managed application displays hello following fields:</span></span>

![Сводка на портале](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="b1b03-262">Общие сведения о Hello для управляемого приложения отображает hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="b1b03-262">hello overview for your managed application displays hello following fields:</span></span>

![Общие сведения на портале](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="b1b03-264">Рекомендации по логотипам</span><span class="sxs-lookup"><span data-stu-id="b1b03-264">Logo guidelines</span></span>

<span data-ttu-id="b1b03-265">Руководствуйтесь следующими рекомендациями для любого логотипа, загруженный на портале Cloud Partner hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="b1b03-266">Hello проектирования Azure имеет простой цветовой палитры.</span><span class="sxs-lookup"><span data-stu-id="b1b03-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="b1b03-267">Ограничение числа hello первичной и вторичными цветами на ваш логотип.</span><span class="sxs-lookup"><span data-stu-id="b1b03-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="b1b03-268">цвета темы Hello портала hello белого и черного.</span><span class="sxs-lookup"><span data-stu-id="b1b03-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="b1b03-269">Не используйте эти цвета как hello цвет фона вашей эмблемы.</span><span class="sxs-lookup"><span data-stu-id="b1b03-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="b1b03-270">Используйте цвет, который делает ваш логотип Показательным hello портала.</span><span class="sxs-lookup"><span data-stu-id="b1b03-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="b1b03-271">Мы рекомендуем простые основные цвета.</span><span class="sxs-lookup"><span data-stu-id="b1b03-271">We recommend simple primary colors.</span></span> <span data-ttu-id="b1b03-272">*При использовании прозрачности фона, убедитесь, что не белый, текстом и hello черный или синий.*</span><span class="sxs-lookup"><span data-stu-id="b1b03-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="b1b03-273">Не используйте градиента фона на эмблеме hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="b1b03-274">Не разместить текст hello логотип, даже вашей компании или собственное имя.</span><span class="sxs-lookup"><span data-stu-id="b1b03-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="b1b03-275">Hello внешний вид и поведение логотип должен быть плоским и избежать градиентов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="b1b03-276">Убедитесь, что не растягивается логотип hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="b1b03-277">Имиджевый логотип</span><span class="sxs-lookup"><span data-stu-id="b1b03-277">Hero logo</span></span>

<span data-ttu-id="b1b03-278">Эмблема героя Hello не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b1b03-278">hello hero logo is optional.</span></span> <span data-ttu-id="b1b03-279">Издатель Hello можно выбрать не tooupload героя эмблему.</span><span class="sxs-lookup"><span data-stu-id="b1b03-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="b1b03-280">После передачи значок героя hello, его нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="b1b03-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="b1b03-281">В этот момент hello партнера должно следовать правилам Marketplace hello героя значков.</span><span class="sxs-lookup"><span data-stu-id="b1b03-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="b1b03-282">Руководствуйтесь следующими рекомендациями для значка логотипа героя hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="b1b03-283">отображаемое имя издателя Hello, Название плана hello и предложение hello длинными сводными отображаются в белый.</span><span class="sxs-lookup"><span data-stu-id="b1b03-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="b1b03-284">Таким образом не используйте светлый цвет фона hello hello героя значка.</span><span class="sxs-lookup"><span data-stu-id="b1b03-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="b1b03-285">Фон имиджевого значка не может быть черным, белым или прозрачным.</span><span class="sxs-lookup"><span data-stu-id="b1b03-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="b1b03-286">После указано предложение hello, издателю hello отображаются имя, заголовок hello плана, предложение hello длинными сводными и hello **создать** кнопку внедренные программными средствами в логотип героя hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="b1b03-287">Следовательно не ввести текст в процессе разработки логотип героя hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="b1b03-288">Оставьте пустое место hello вправо так, как программным образом включается текст hello в этой области.</span><span class="sxs-lookup"><span data-stu-id="b1b03-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="b1b03-289">Hello пустое место для текста hello следует 415 x 100 пикселей на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="b1b03-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="b1b03-290">Смещением 370 пикселей от левого края hello.</span><span class="sxs-lookup"><span data-stu-id="b1b03-290">It's offset by 370 pixels from hello left.</span></span>

    ![Пример имиджевого логотипа](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="b1b03-292">Форма службы поддержки</span><span class="sxs-lookup"><span data-stu-id="b1b03-292">Support form</span></span>

<span data-ttu-id="b1b03-293">Заполните hello **поддерживает** формы с поддержкой контактов из вашей компании.</span><span class="sxs-lookup"><span data-stu-id="b1b03-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="b1b03-294">Это могут быть контактные данные технического отдела или службы поддержки клиентов.</span><span class="sxs-lookup"><span data-stu-id="b1b03-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="b1b03-295">Публикация предложения</span><span class="sxs-lookup"><span data-stu-id="b1b03-295">Publish an offer</span></span>

<span data-ttu-id="b1b03-296">После заполнения всех разделов hello выберите **публикации** toostart hello процесс, который делает доступными toocustomers вашего предложения.</span><span class="sxs-lookup"><span data-stu-id="b1b03-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b03-297">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1b03-297">Next steps</span></span>

* <span data-ttu-id="b1b03-298">Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b1b03-299">Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="b1b03-300">Сведения о публикации управляемых приложений в каталоге услуг см. в разделе [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="b1b03-301">Дополнительные сведения об использовании управляемых приложений из каталога услуг см. в разделе [Использование управляемого приложения Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="b1b03-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
