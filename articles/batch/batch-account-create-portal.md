---
title: "aaaCreate учетной записи пакета в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate пакетной службы Azure учетной записи в Azure портала toorun hello крупномасштабных параллельных рабочих нагрузок в облако hello"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="e6673-103">Создать пакетную учетную запись с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e6673-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6673-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e6673-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="e6673-105">Библиотека .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="e6673-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="e6673-106">Узнайте, как учетной записи пакетной службы Azure toocreate в hello [портал Azure][azure_portal]и выберите свойства hello учетной записи, которые соответствуют вашему сценарию вычислений.</span><span class="sxs-lookup"><span data-stu-id="e6673-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="e6673-107">Узнайте, где toofind важные учетной записи свойства, такие как клавиши доступа и URL-адреса учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="e6673-108">Основные сведения о сценариях и массовых учетных записей см. в разделе hello [компонентов Обзор](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e6673-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="e6673-109">Создание учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-109">Create a Batch account</span></span>

<span data-ttu-id="e6673-110">Используйте портала toocreate hello пакетную учетную запись в одном из двух hello *режимы распределения пула*: **пакетной службы** режиме или в новой hello **подписки пользователя** режим, в котором требуется больше Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="e6673-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="e6673-111">Сведения об этих двух режимов см. в разделе hello [компонентов Обзор](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="e6673-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="e6673-112">Для функций hello режиме подписки пользователя, см. также: hello [блога](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="e6673-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="e6673-113">Режим пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-113">Batch service mode</span></span>



1. <span data-ttu-id="e6673-114">Войдите в toohello [портал Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e6673-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="e6673-115">Щелкните **Создать** > **Вычисление** > **Пакетная служба**.</span><span class="sxs-lookup"><span data-stu-id="e6673-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Пакет в hello Marketplace][marketplace_portal]
3. <span data-ttu-id="e6673-117">Hello **новую пакетную учетную запись** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="e6673-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e6673-118">См. описания hello ниже всех элементов колонку.</span><span class="sxs-lookup"><span data-stu-id="e6673-118">See hello descriptions below of each blade element.</span></span>

    ![Создание учетной записи Пакетной службы][account_portal]

    <span data-ttu-id="e6673-120">а.</span><span class="sxs-lookup"><span data-stu-id="e6673-120">a.</span></span> <span data-ttu-id="e6673-121">**Имя учетной записи**: hello выбрать имя пакетной учетной записи должно быть уникальным в hello регион Azure, где создается hello учетной записи (в разделе **расположение** ниже).</span><span class="sxs-lookup"><span data-stu-id="e6673-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="e6673-122">Имя учетной записи Hello может содержать только строчные буквы и цифры и должно быть 3 до 24 символов.</span><span class="sxs-lookup"><span data-stu-id="e6673-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e6673-123">b.</span><span class="sxs-lookup"><span data-stu-id="e6673-123">b.</span></span> <span data-ttu-id="e6673-124">**Подписки**: hello подписки в какие toocreate hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="e6673-125">Если у вас только одна подписка, она будет выбрана по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e6673-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="e6673-126">c.</span><span class="sxs-lookup"><span data-stu-id="e6673-126">c.</span></span> <span data-ttu-id="e6673-127">**Режим распределения пула**: выберите параметр **Пакетная служба**.</span><span class="sxs-lookup"><span data-stu-id="e6673-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="e6673-128">c.</span><span class="sxs-lookup"><span data-stu-id="e6673-128">c.</span></span> <span data-ttu-id="e6673-129">**Группа ресурсов** — существующая группа ресурсов для новой учетной записи пакетной службы (при необходимости можно создать другую группу).</span><span class="sxs-lookup"><span data-stu-id="e6673-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="e6673-130">d.</span><span class="sxs-lookup"><span data-stu-id="e6673-130">d.</span></span> <span data-ttu-id="e6673-131">**Расположение**: hello регион Azure, в какие toocreate hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="e6673-132">Только для областей hello поддерживается вашей подписки и группы ресурсов отображаются в виде параметров.</span><span class="sxs-lookup"><span data-stu-id="e6673-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="e6673-133">д.</span><span class="sxs-lookup"><span data-stu-id="e6673-133">e.</span></span> <span data-ttu-id="e6673-134">**Учетная запись хранения** (необязательно) — учетная запись хранения Azure общего назначения, которая будет связана с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e6673-135">Мы рекомендуем использовать ее для большинства учетных записей пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e6673-136">Дополнительные сведения см. в разделе [Связанная учетная запись хранения Azure](#linked-azure-storage-account) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e6673-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="e6673-137">Нажмите кнопку **создать** учетной записи toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e6673-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="e6673-138">портал Hello указывает, что развертывание выполняется в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e6673-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="e6673-139">По завершении в разделе **уведомлений** появляется уведомление об **успешном развертывании**.</span><span class="sxs-lookup"><span data-stu-id="e6673-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="e6673-140">Режим пользовательской подписки</span><span class="sxs-lookup"><span data-stu-id="e6673-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="e6673-141">Разрешить tooaccess пакетной службы Azure hello подписки (одноразовая операция)</span><span class="sxs-lookup"><span data-stu-id="e6673-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="e6673-142">При создании учетной записи первого пакета в пользовательском режиме подписки, выполните следующие шаги tooregister hello подписки с использованием пакета.</span><span class="sxs-lookup"><span data-stu-id="e6673-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="e6673-143">(Если вы ранее уже сделали это, пропустите следующий раздел toohello).</span><span class="sxs-lookup"><span data-stu-id="e6673-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="e6673-144">Войдите в toohello [портал Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e6673-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="e6673-145">Нажмите кнопку **более служб** > **подписки**и нажмите кнопку hello подписку toouse для hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="e6673-146">В hello **подписки** колонка, щелкните **(IAM) управления доступом к** > **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e6673-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Управление доступом к подписке][subscription_access]

4. <span data-ttu-id="e6673-148">На hello **добавить разрешения** колонки, выберите hello **участника** роли, поиск hello API пакета.</span><span class="sxs-lookup"><span data-stu-id="e6673-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="e6673-149">Поиск для каждого из этих строк, пока не найдете hello API:</span><span class="sxs-lookup"><span data-stu-id="e6673-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="e6673-150">**MicrosoftAzureBatch**;</span><span class="sxs-lookup"><span data-stu-id="e6673-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="e6673-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="e6673-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="e6673-152">Более новые клиенты Azure AD могут использовать это имя.</span><span class="sxs-lookup"><span data-stu-id="e6673-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="e6673-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** идентификатор hello hello API пакета.</span><span class="sxs-lookup"><span data-stu-id="e6673-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="e6673-154">Найдя hello API пакета, выберите его и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e6673-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Добавление разрешений для пакетной службы][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="e6673-156">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="e6673-156">Create a key vault</span></span>
<span data-ttu-id="e6673-157">В пользовательском режиме подписки, хранилище ключей Azure является обязательным, принадлежит toothe hello пакетной учетной записи toobe создан же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e6673-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="e6673-158">Убедитесь, что группа ресурсов hello в регионе, где пакет — [доступных](https://azure.microsoft.com/regions/services/) и поддерживающий вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="e6673-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="e6673-159">В hello [портал Azure][azure_portal], нажмите кнопку **New** > **безопасность + удостоверения** > **хранилища ключей** .</span><span class="sxs-lookup"><span data-stu-id="e6673-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="e6673-160">В hello **Создание хранилища ключей** колонки, введите имя для хранилища ключей hello и создайте группу ресурсов в регионе hello для вашей учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="e6673-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="e6673-161">Оставьте для оставшихся параметров значения по умолчанию hello, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="e6673-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="e6673-162">Создание учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-162">Create a Batch account</span></span>

1. <span data-ttu-id="e6673-163">В hello [портал Azure][azure_portal], нажмите кнопку **New** > **вычислений** > **пакетная служба**.</span><span class="sxs-lookup"><span data-stu-id="e6673-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Пакет в hello Marketplace][marketplace_portal]
3. <span data-ttu-id="e6673-165">Hello **новую пакетную учетную запись** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="e6673-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e6673-166">См. описания hello ниже всех элементов колонку.</span><span class="sxs-lookup"><span data-stu-id="e6673-166">See hello descriptions below of each blade element.</span></span>

    ![Создание учетной записи Пакетной службы][account_portal_byos]

    <span data-ttu-id="e6673-168">а.</span><span class="sxs-lookup"><span data-stu-id="e6673-168">a.</span></span> <span data-ttu-id="e6673-169">**Имя учетной записи**: hello выбрать имя пакетной учетной записи должно быть уникальным в hello регион Azure, где создается hello учетной записи (в разделе **расположение** ниже).</span><span class="sxs-lookup"><span data-stu-id="e6673-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="e6673-170">Имя учетной записи Hello может содержать только строчные буквы и цифры и должно быть 3 до 24 символов.</span><span class="sxs-lookup"><span data-stu-id="e6673-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e6673-171">b.</span><span class="sxs-lookup"><span data-stu-id="e6673-171">b.</span></span> <span data-ttu-id="e6673-172">**Подписки**: при наличии нескольких подписок выберите подписку hello, зарегистрированный для hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="e6673-173">c.</span><span class="sxs-lookup"><span data-stu-id="e6673-173">c.</span></span> <span data-ttu-id="e6673-174">**Режим распределения пула** — выберите **Пользовательская подписка** .</span><span class="sxs-lookup"><span data-stu-id="e6673-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="e6673-175">d.</span><span class="sxs-lookup"><span data-stu-id="e6673-175">d.</span></span> <span data-ttu-id="e6673-176">**Хранилище ключей**: hello выберите хранилище ключей был создан для вашей учетной записи пакета в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="e6673-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="e6673-177">Или создайте новое хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="e6673-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="e6673-178">После выбора hello хранилища, выберите hello флажок toogrant пакетной службы Azure access toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e6673-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="e6673-179">c.</span><span class="sxs-lookup"><span data-stu-id="e6673-179">c.</span></span> <span data-ttu-id="e6673-180">**Группа ресурсов**: hello выберите группы ресурсов, в котором был создан hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e6673-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="e6673-181">d.</span><span class="sxs-lookup"><span data-stu-id="e6673-181">d.</span></span> <span data-ttu-id="e6673-182">**Расположение**: hello регион Azure, в котором был создан hello хранилища ключей для учетной записи пакетной hello.</span><span class="sxs-lookup"><span data-stu-id="e6673-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="e6673-183">д.</span><span class="sxs-lookup"><span data-stu-id="e6673-183">e.</span></span> <span data-ttu-id="e6673-184">**Учетная запись хранения** (необязательно) — учетная запись хранения Azure общего назначения, которая будет связана с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e6673-185">Мы рекомендуем использовать ее для большинства учетных записей пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e6673-186">Дополнительные сведения см. в разделе [Связанная учетная запись хранения Azure](#linked-azure-storage-account) ниже.</span><span class="sxs-lookup"><span data-stu-id="e6673-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="e6673-187">Нажмите кнопку **создать** учетной записи toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e6673-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="e6673-188">портал Hello указывает, что развертывание выполняется в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e6673-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="e6673-189">По завершении в разделе **уведомлений** появляется уведомление об **успешном развертывании**.</span><span class="sxs-lookup"><span data-stu-id="e6673-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="e6673-190">Просмотр свойств учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-190">View Batch account properties</span></span>
<span data-ttu-id="e6673-191">После создания учетной записи hello можно открыть hello **колонке пакетной учетной записи** tooaccess его параметры и свойства.</span><span class="sxs-lookup"><span data-stu-id="e6673-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="e6673-192">С помощью меню слева hello hello пакетной учетной записи колонка доступны все параметры учетной записи и свойства.</span><span class="sxs-lookup"><span data-stu-id="e6673-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Колонка учетной записи пакетной службы на портале Azure][account_blade]

* <span data-ttu-id="e6673-194">**URL-адреса пакета**: при разработке приложения с hello [API-интерфейсы пакета](batch-apis-tools.md#azure-accounts-for-batch-development), вам потребуется tooaccess URL-адрес учетной записи ресурсов пакета.</span><span class="sxs-lookup"><span data-stu-id="e6673-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="e6673-195">URL-адрес пакета учетная запись имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="e6673-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL-адрес учетной записи пакетной службы на портале][account_url]

* <span data-ttu-id="e6673-197">**Ключи доступа** (режим пакета обновления): tooyour tooauthenticate доступа учетной записи пакетной службы из своего приложения, вам потребуется ключ доступа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="e6673-198">Этот параметр недоступен в режиме пользовательской подписки, в котором используется аутентификация Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e6673-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="e6673-199">tooview или повторное создание ключа доступа учетной записи пакета, введите `keys` в левом меню hello **поиска** колонке учетной записи пакетного hello, а затем выберите **ключей**.</span><span class="sxs-lookup"><span data-stu-id="e6673-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Ключи учетной записи пакетной службы на портале Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="e6673-201">Связанная учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e6673-201">Linked Azure Storage account</span></span>

<span data-ttu-id="e6673-202">При необходимости можно связать общего назначения tooyour учетной записи хранилища Azure пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="e6673-203">Hello [пакетов приложений](batch-application-packages.md) компонентов пакета использует хранилище больших двоичных объектов Azure, как hello [пакетного файла соглашения .NET](batch-task-output.md) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e6673-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="e6673-204">Эти дополнительные функции, чтобы помочь в развертывание приложения hello, которые выполняются задачи пакета и сохранения данных hello, которые они создают.</span><span class="sxs-lookup"><span data-stu-id="e6673-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="e6673-205">Рекомендуем создать учетную запись хранения, которая будет использоваться исключительно с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="e6673-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Создание учетной записи хранения общего назначения][storage_account]

> [!NOTE]
> <span data-ttu-id="e6673-207">Пакет Azure в настоящее время поддерживает только hello универсальный тип учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6673-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="e6673-208">Этот тип учетной записи описан на шаге 5 [Создайте учетную запись хранения] (../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6673-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="e6673-209">Будьте внимательны при повторном создании ключей доступа hello связанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6673-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="e6673-210">Повторно создать только один ключ учетной записи хранилища и нажмите кнопку **синхронизация ключей** на hello связаны колонке учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e6673-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="e6673-211">Подождите пять минут tooallow hello ключей toopropagate toohello вычислительных узлов в пулов, а затем повторно создать и синхронизировать hello другого ключа, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e6673-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="e6673-212">При повторном создании обоих ключей на hello же времени, вычислительных узлов не будет возможности toosynchronize или ключ и доступа к учетной записи хранилища toohello будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="e6673-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="e6673-213">![Повторное создание ключей учетной записи хранения][4]</span><span class="sxs-lookup"><span data-stu-id="e6673-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="e6673-214">Квоты и ограничения пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-214">Batch service quotas and limits</span></span>
<span data-ttu-id="e6673-215">Имейте в виду, что как подписки Azure и Azure других служб, некоторые [квоты и лимиты](batch-quota-limit.md) применить tooBatch учетные записи.</span><span class="sxs-lookup"><span data-stu-id="e6673-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="e6673-216">Текущие квоты для учетной записи пакетной отображаться на портале hello в учетной записи hello **свойства**.</span><span class="sxs-lookup"><span data-stu-id="e6673-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Квоты учетной записи пакетной службы на портале Azure][quotas]



<span data-ttu-id="e6673-218">Кроме того многие из эти квоты можно увеличить просто с помощью запроса поддержки продукта, поступающими в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e6673-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="e6673-219">В разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md) сведения о запросе увеличения квоты.</span><span class="sxs-lookup"><span data-stu-id="e6673-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="e6673-220">Другие параметры управления учетной записью пакетной службы</span><span class="sxs-lookup"><span data-stu-id="e6673-220">Other Batch account management options</span></span>
<span data-ttu-id="e6673-221">В дополнение к этому toousing Здравствуйте портал Azure, можно создать и управлять учетными записями пакетной hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e6673-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="e6673-222">командлеты PowerShell для пакетной службы;</span><span class="sxs-lookup"><span data-stu-id="e6673-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="e6673-223">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e6673-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="e6673-224">Библиотека .NET для управления пакетной службой</span><span class="sxs-lookup"><span data-stu-id="e6673-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="e6673-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6673-225">Next steps</span></span>
* <span data-ttu-id="e6673-226">В разделе hello [Обзор возможностей пакетной](batch-api-basics.md) toolearn Дополнительные сведения о пакете основные понятия службы и компоненты.</span><span class="sxs-lookup"><span data-stu-id="e6673-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="e6673-227">Hello статье обсуждаются hello основными ресурсами пакета пулов, вычислительные узлы, заданий и задач и общие сведения о hello функции службы, позволяющие выполнения крупномасштабных вычислительных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e6673-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="e6673-228">Основы hello разработки приложений с поддержкой пакета, используя hello [клиентская библиотека .NET пакета](batch-dotnet-get-started.md) или [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e6673-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="e6673-229">Эти Вводные статьи описывают рабочее приложение, которое использует hello пакетной службы tooexecute рабочей нагрузки на несколько вычислительных узлов и включает использование хранилища Azure для размещения файла рабочей нагрузки и извлечения.</span><span class="sxs-lookup"><span data-stu-id="e6673-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Повторное создание ключей учетной записи хранения"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
