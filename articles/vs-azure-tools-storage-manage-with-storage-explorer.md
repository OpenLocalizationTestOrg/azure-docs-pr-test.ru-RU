---
title: "aaaGet работы с обозреватель хранилищ (Предварительная версия) | Документы Microsoft"
description: "Управление ресурсами хранилища Azure с помощью обозревателя хранилищ (предварительная версия)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="f19b1-103">Приступая к работе с обозревателем службы хранилища (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f19b1-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="f19b1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f19b1-104">Overview</span></span>
<span data-ttu-id="f19b1-105">Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="f19b1-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="f19b1-106">В этой статье вы узнаете hello различные способы соединения tooand управление учетных записей хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Обозреватель службы хранилища Microsoft Azure (предварительная версия)][15]

## <a name="prerequisites"></a><span data-ttu-id="f19b1-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f19b1-108">Prerequisites</span></span>
* [<span data-ttu-id="f19b1-109">Скачайте и установите обозреватель службы хранилища (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="f19b1-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="f19b1-110">Подключите tooa учетной записи хранилища или службы</span><span class="sxs-lookup"><span data-stu-id="f19b1-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="f19b1-111">Обозреватель хранилищ (Предварительная версия) предоставляет несколько способов tooconnect toostorage счетов.</span><span class="sxs-lookup"><span data-stu-id="f19b1-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="f19b1-112">Вот что вы можете, к примеру, делать:</span><span class="sxs-lookup"><span data-stu-id="f19b1-112">For example, you can:</span></span>
* <span data-ttu-id="f19b1-113">Подключите toostorage учетные записи, связанные с подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="f19b1-114">Подключение toostorage учетных записей и служб, которые являются общими из подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="f19b1-115">Подключение tooand управление локальным хранилищем с помощью hello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="f19b1-116">Можно также работать с учетными записями хранения в глобальной и национальной среде Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="f19b1-117">[Подключение tooan подписки Azure](#connect-to-an-azure-subscription): управлять ресурсами, которые принадлежат tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="f19b1-118">[Работать с локальной разработки хранилища](#work-with-local-development-storage): управление локальным хранилищем с помощью hello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="f19b1-119">[Подключить хранилище tooexternal](#attach-or-detach-an-external-storage-account): управлять ресурсами, которые принадлежат tooanother подписки Azure или, находящиеся в национальной облаков Azure, используя имя учетной записи хранилища hello, ключ и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f19b1-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="f19b1-120">[Добавить учетную запись хранилища с помощью SAS](#attach-storage-account-using-sas): управление ресурсами хранилища, которые принадлежат tooanother подписки Azure с помощью подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="f19b1-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="f19b1-121">[Присоединение службы с помощью SAS](#attach-service-using-sas): управление службой носителей (контейнер больших двоичных объектов, очереди или таблицы), к которому относится tooanother подписки Azure с помощью SAS.</span><span class="sxs-lookup"><span data-stu-id="f19b1-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="f19b1-122">Подключение tooan подписки Azure</span><span class="sxs-lookup"><span data-stu-id="f19b1-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="f19b1-123">Если у вас нет учетной записи Azure, [зарегистрируйтесь для работы с бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f19b1-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="f19b1-124">В обозревателе хранилищ (предварительная версия) выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Параметры учетной записи Azure][0]

2. <span data-ttu-id="f19b1-126">Hello левая панель содержит все учетные записи Microsoft hello, вы вошли.</span><span class="sxs-lookup"><span data-stu-id="f19b1-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="f19b1-127">tooconnect tooanother учетной записи выберите **добавить учетную запись**, а затем следуйте hello toosign инструкции с учетной записью Майкрософт, которая связана с по крайней мере одну подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f19b1-128">Подключение toonational Azure (например, Германии Azure, Azure для государственных и Azure China через вход) в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f19b1-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="f19b1-129">Hello. в разделе «присоединение или отключение учетной записи внешнего хранилища» как в разделе учетных записей хранилища Azure toonational tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f19b1-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="f19b1-130">После успешной регистрации учетную запись Майкрософт, hello слева, панель заполняется hello Azure подписок, связанных с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f19b1-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="f19b1-131">Здравствуйте, выберите подписки Azure, которые вы хотите toowork с, а затем выберите **применить**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="f19b1-132">(При выборе **все подписки** переключатели, выбрав все или никакие из hello в списке подписок Azure.)</span><span class="sxs-lookup"><span data-stu-id="f19b1-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Выбор подписок Azure][3]  
    <span data-ttu-id="f19b1-134">Hello левая панель отображает связанные с подписками Azure hello выбранные учетные записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Выбранные подписки Azure][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="f19b1-136">Подключение подписки tooan стек Azure</span><span class="sxs-lookup"><span data-stu-id="f19b1-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="f19b1-137">Сведения о подключении подписки tooan стека Azure см. в разделе [tooan подключить обозреватель хранилища Azure стека подписки](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="f19b1-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="f19b1-138">Работа с локальным хранилищем разработки</span><span class="sxs-lookup"><span data-stu-id="f19b1-138">Work with local development storage</span></span>
<span data-ttu-id="f19b1-139">Обозреватель хранилищ (Предварительная версия) позволяет работать для локального хранилища с помощью hello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="f19b1-140">Такой подход позволяет писать код на соответствие и хранения данных тестирования не имея учетной записи хранилища, развернутое в Azure, так как учетная запись хранения hello эмулируется по hello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="f19b1-141">Hello эмулятор хранилища Azure в настоящее время поддерживается только для Windows.</span><span class="sxs-lookup"><span data-stu-id="f19b1-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="f19b1-142">Hello левой панели проводника хранилищ (Предварительная версия), разверните hello **(локальное и присоединенные)** > **учетные записи хранения** > **(разработка)** узла.</span><span class="sxs-lookup"><span data-stu-id="f19b1-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Узел локальной разработки][21]

2. <span data-ttu-id="f19b1-144">Hello эмулятор хранилища Azure еще не установлен, имеется ли запрос toodo так через информационной панели.</span><span class="sxs-lookup"><span data-stu-id="f19b1-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="f19b1-145">Если hello информационная панель отображается, выберите **Загрузка последней версии hello**и затем установить эмулятор hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Строка эмулятора хранения Azure с предложением скачать последнюю версию][22]

3. <span data-ttu-id="f19b1-147">После установки эмулятора hello, можно создать и работать с локальной больших двоичных объектов, очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="f19b1-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="f19b1-148">toolearn как тип toowork с каждой учетной записи хранилища, см. в одном hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f19b1-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="f19b1-149">Управление ресурсами хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="f19b1-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="f19b1-150">Управление ресурсами хранилища файловых ресурсов Azure — *ожидается в ближайшее время*.</span><span class="sxs-lookup"><span data-stu-id="f19b1-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="f19b1-151">Управление ресурсами хранилища очередей Azure — *ожидается в ближайшее время*.</span><span class="sxs-lookup"><span data-stu-id="f19b1-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="f19b1-152">Управление ресурсами хранилища таблиц Azure — *ожидается в ближайшее время*.</span><span class="sxs-lookup"><span data-stu-id="f19b1-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="f19b1-153">Присоединение и отсоединение учетной записи внешнего хранилища</span><span class="sxs-lookup"><span data-stu-id="f19b1-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="f19b1-154">С помощью обозревателя хранилища (Предварительная версия) можно присоединить tooexternal учетных записей хранилища, чтобы учетные записи хранения можно было легко совместно.</span><span class="sxs-lookup"><span data-stu-id="f19b1-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="f19b1-155">В этом разделе объясняется, как tooattach too(and detach from) учетные записи внешнего хранилища.</span><span class="sxs-lookup"><span data-stu-id="f19b1-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="f19b1-156">Получить учетные данные хранилища hello</span><span class="sxs-lookup"><span data-stu-id="f19b1-156">Get hello storage account credentials</span></span>
<span data-ttu-id="f19b1-157">tooshare учетной записи внешнего хранилища hello владельца этой учетной записи необходимо сначала получить hello учетные данные (имя учетной записи и ключ) для учетной записи hello и затем предоставить эти сведения hello, кто хочет учетной записи tooattach toothat (внешнего).</span><span class="sxs-lookup"><span data-stu-id="f19b1-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="f19b1-158">Учетные данные хранилища hello через портал Azure hello можно получить, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="f19b1-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="f19b1-159">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f19b1-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f19b1-160">Щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-160">Select **Browse**.</span></span>

3. <span data-ttu-id="f19b1-161">Выберите **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="f19b1-162">На hello **учетные записи хранения** колонки, выберите hello требуемой учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f19b1-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="f19b1-163">На hello **параметры** колонке hello выбранную учетную запись хранилища, выберите **ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Варианты ключей доступа][5]

6. <span data-ttu-id="f19b1-165">На hello **ключи доступа** колонки, hello копирования **имя учетной записи хранения** и **key1** значения для использования при присоединении toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f19b1-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Ключи доступа][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="f19b1-167">Присоединение tooan учетной записи внешнего хранилища</span><span class="sxs-lookup"><span data-stu-id="f19b1-167">Attach tooan external storage account</span></span>
<span data-ttu-id="f19b1-168">учетной записи внешнего хранилища tooan tooattach, необходимо имя и ключ учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="f19b1-169">раздел «Get hello учетные данные хранилища» Hello объясняется, как эти значения из tooobtain hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="f19b1-170">Однако портал hello hello ключ учетной записи называется **key1**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="f19b1-171">Поэтому там, где обозреватель хранилищ (Предварительная версия) запрашивает ключ учетной записи, введите hello **key1** значение.</span><span class="sxs-lookup"><span data-stu-id="f19b1-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="f19b1-172">В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Параметр хранения tooAzure подключения][23]

2. <span data-ttu-id="f19b1-174">В hello **подключения tooAzure хранилища** диалоговом окне укажите ключ учетной записи hello (hello **key1** значение из hello портал Azure) и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f19b1-175">Можно вводить строки подключения к хранилищу hello из учетной записи хранения в национальной Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="f19b1-176">Например учетные записи хранения Германия tooAzure tooconnect, введите соединения строки аналогичные toohello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f19b1-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="f19b1-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="f19b1-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="f19b1-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="f19b1-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="f19b1-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="f19b1-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="f19b1-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="f19b1-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="f19b1-181">Можно получить строки подключения hello hello Azure портала в hello таким же, как описано в hello раздел «Получить учетные данные хранилища hello».</span><span class="sxs-lookup"><span data-stu-id="f19b1-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. <span data-ttu-id="f19b1-183">В hello **присоединить внешнее хранилище** диалогового окна hello **имя учетной записи** введите имя учетной записи хранения hello, укажите нужные параметры и затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Диалоговое окно присоединения внешнего хранилища][8]

4. <span data-ttu-id="f19b1-185">В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="f19b1-186">Toochange всего, установите **обратно** и снова введите параметры требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="f19b1-187">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-187">Select **Connect**.</span></span>

6. <span data-ttu-id="f19b1-188">После успешного подключения учетной записи внешнего хранилища hello отображается с **(внешнего)** добавляется toohello имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f19b1-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Результат подключения учетной записи внешнего хранилища tooan][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="f19b1-190">Отсоединение учетной записи внешнего хранилища</span><span class="sxs-lookup"><span data-stu-id="f19b1-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="f19b1-191">Щелкните правой кнопкой мыши hello учетной записи внешнего хранилища требуется toodetach, а затем выберите **отсоединения**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Вариант отсоединения от хранилища][10]

2. <span data-ttu-id="f19b1-193">Сообщения о подтверждении hello выберите **Да** tooconfirm hello отсоединение от учетной записи внешнего хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="f19b1-194">Присоединение учетной записи хранения с помощью SAS</span><span class="sxs-lookup"><span data-stu-id="f19b1-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="f19b1-195">[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) позволяет Здравствуйте, администратор подписки Azure предоставьте учетной записи хранилища tooa временный доступ без необходимости учетные данные tooprovide подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f19b1-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="f19b1-196">tooillustrate этот сценарий, давайте предположим, пользователь UserA является администратором, подписка Azure, и UserA хочет tooaccess UserB tooallow учетную запись хранилища в течение ограниченного времени с определенными разрешениями:</span><span class="sxs-lookup"><span data-stu-id="f19b1-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="f19b1-197">Пользователь UserA приводит к возникновению ошибки SAS (состоящие из hello строку подключения для учетной записи хранения hello) на определенное время период и с hello требуемого разрешения.</span><span class="sxs-lookup"><span data-stu-id="f19b1-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="f19b1-198">Общие папки пользователя UserA hello SAS с hello пользователь (в нашем примере UserB), который должен учетной записи хранилища toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="f19b1-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="f19b1-199">Пользователь б использует обозреватель хранилищ (Предварительная версия) tooattach toohello счет принадлежит tooUserA с помощью hello указан SAS.</span><span class="sxs-lookup"><span data-stu-id="f19b1-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="f19b1-200">Получить SAS для hello имени учетной записи которого tooshare</span><span class="sxs-lookup"><span data-stu-id="f19b1-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="f19b1-201">В обозревателе хранилищ (Предварительная версия), щелкните правой кнопкой мыши учетную запись хранения hello, нужно совместно использовать, а затем выберите **получить подпись общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Вариант получения SAS в контекстном меню][13]

2. <span data-ttu-id="f19b1-203">В hello **подписи общего доступа** диалоговом окне укажите hello промежуток времени, а также разрешения для учетной записи hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="f19b1-204">![Диалоговое окно получения SAS][14]</span><span class="sxs-lookup"><span data-stu-id="f19b1-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="f19b1-205">Hello **подписи общего доступа** диалоговое окно открывается и отображает hello SAS.</span><span class="sxs-lookup"><span data-stu-id="f19b1-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="f19b1-206">Далее toohello **строка подключения**выберите **копирования** toocopy его toohello буфер обмена и выберите **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="f19b1-207">Присоединение toohello общей учетной записи с помощью hello SAS</span><span class="sxs-lookup"><span data-stu-id="f19b1-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="f19b1-208">В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Параметр хранения tooAzure подключения][23]

2. <span data-ttu-id="f19b1-210">В hello **подключения tooAzure хранения** диалоговое окно, укажите строку подключения hello, а затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. <span data-ttu-id="f19b1-212">В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="f19b1-213">Выберите изменения toomake **обратно**и введите параметры hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="f19b1-214">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-214">Select **Connect**.</span></span>

5. <span data-ttu-id="f19b1-215">После присоединения, hello учетной записи хранилища отображается с **(SAS)** добавляется предоставленное имя учетной записи toohello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Результат вложенного tooan учетной записи с помощью SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="f19b1-217">Присоединение службы с помощью SAS</span><span class="sxs-lookup"><span data-stu-id="f19b1-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="f19b1-218">раздел «Присоединения» учетной записи хранилища с помощью SAS Hello поясняет, как администратор подписки Azure можно предоставить учетной записи хранилища tooa временный доступ путем создания и совместного использования SAS для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="f19b1-219">Аналогичным образом SAS можно создать для конкретной службы (контейнера больших двоичных объектов, очереди или таблицы) в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f19b1-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="f19b1-220">Создать SAS для hello службы, которые должны tooshare</span><span class="sxs-lookup"><span data-stu-id="f19b1-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="f19b1-221">В этом контексте служба может быть контейнером больших двоичных объектов, очередью или таблицей.</span><span class="sxs-lookup"><span data-stu-id="f19b1-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="f19b1-222">hello toogenerate SAS для перечисленных службы, см.:</span><span class="sxs-lookup"><span data-stu-id="f19b1-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="f19b1-223">Получить hello SAS для контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="f19b1-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="f19b1-224">Получить hello SAS для общей папки: *ожидается в ближайшее время*</span><span class="sxs-lookup"><span data-stu-id="f19b1-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="f19b1-225">Получить hello SAS для очереди: *ожидается в ближайшее время*</span><span class="sxs-lookup"><span data-stu-id="f19b1-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="f19b1-226">Получить hello SAS для таблицы: *ожидается в ближайшее время*</span><span class="sxs-lookup"><span data-stu-id="f19b1-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="f19b1-227">Подключите общие toohello учетную запись службы с помощью hello SAS</span><span class="sxs-lookup"><span data-stu-id="f19b1-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="f19b1-228">В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Параметр хранения tooAzure подключения][23]

2. <span data-ttu-id="f19b1-230">В hello **подключения tooAzure хранения** диалоговое окно, укажите hello универсальный код Ресурса SAS, а затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. <span data-ttu-id="f19b1-232">В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="f19b1-233">Выберите изменения toomake **обратно**и введите параметры hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="f19b1-234">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="f19b1-234">Select **Connect**.</span></span>

5. <span data-ttu-id="f19b1-235">После присоединения, hello присоединенную службы отображается под hello **(служба SAS)** узла.</span><span class="sxs-lookup"><span data-stu-id="f19b1-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Результат присоединение tooa общие службы с помощью SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="f19b1-237">Поиск учетных записей хранилищ</span><span class="sxs-lookup"><span data-stu-id="f19b1-237">Search for storage accounts</span></span>
<span data-ttu-id="f19b1-238">При наличии длинный список учетных записей хранения toolocate быстрый способ записи — поле поиска hello toouse hello верхней части левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="f19b1-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="f19b1-239">При вводе в поле поиска hello hello левой области учетных записей хранилища отображает hello, соответствует значению hello поиска введенные вами toothat точку.</span><span class="sxs-lookup"><span data-stu-id="f19b1-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="f19b1-240">Например, для поиска для хранения всех учетных записей, имя которого содержит **tarcher** показан на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="f19b1-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Поиск учетной записи хранения][11]

## <a name="next-steps"></a><span data-ttu-id="f19b1-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f19b1-242">Next steps</span></span>
* [<span data-ttu-id="f19b1-243">Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f19b1-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
