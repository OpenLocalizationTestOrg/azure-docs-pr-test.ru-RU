---
title: "aaaCapture данные из концентраторов событий в хранилище Озера данных Azure | Документы Microsoft"
description: "Хранилище Озера данных Azure используйте toocapture данные из концентраторов событий"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="e33b1-103">Хранилище Озера данных Azure используйте toocapture данные из концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="e33b1-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="e33b1-104">Узнайте, как toouse данных toocapture хранилища Озера данных Azure полученных концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="e33b1-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e33b1-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e33b1-105">Prerequisites</span></span>

* <span data-ttu-id="e33b1-106">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-106">**An Azure subscription**.</span></span> <span data-ttu-id="e33b1-107">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e33b1-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e33b1-108">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="e33b1-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="e33b1-109">Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e33b1-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="e33b1-110">**Пространство имен концентраторов событий.**</span><span class="sxs-lookup"><span data-stu-id="e33b1-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="e33b1-111">Дополнительные сведения см. в разделе [Создание пространства имен концентраторов событий](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="e33b1-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="e33b1-112">Убедитесь, что учетная запись хранилища Озера данных hello и пространство имен hello концентраторов событий в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="e33b1-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="e33b1-113">Назначение разрешений tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="e33b1-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="e33b1-114">В этом разделе создайте папку в пределах учетной записи hello toocapture hello данные из концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="e33b1-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="e33b1-115">Можно также назначить разрешения tooEvent концентраторы, чтобы его можно записать данные в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e33b1-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="e33b1-116">Открыть учетную запись хранилища Озера данных hello где toocapture данные из концентраторов событий и выберите команду **обозреватель данных**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="e33b1-117">![Обозреватель данных Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span><span class="sxs-lookup"><span data-stu-id="e33b1-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="e33b1-118">Нажмите кнопку **новую папку** и введите имя папки, где требуется сохранить данные hello toocapture.</span><span class="sxs-lookup"><span data-stu-id="e33b1-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="e33b1-119">![Создание папки в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="e33b1-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="e33b1-120">Назначьте разрешения на корневой hello объекта hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e33b1-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="e33b1-121">а.</span><span class="sxs-lookup"><span data-stu-id="e33b1-121">a.</span></span> <span data-ttu-id="e33b1-122">Нажмите кнопку **обозреватель данных**выберите корень hello hello хранилища Озера данных и нажмите кнопку **доступа**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="e33b1-123">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="e33b1-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="e33b1-124">b.</span><span class="sxs-lookup"><span data-stu-id="e33b1-124">b.</span></span> <span data-ttu-id="e33b1-125">В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="e33b1-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="e33b1-126">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="e33b1-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="e33b1-127">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-127">Click **Select**.</span></span>

    <span data-ttu-id="e33b1-128">c.</span><span class="sxs-lookup"><span data-stu-id="e33b1-128">c.</span></span> <span data-ttu-id="e33b1-129">В разделе **Назначение разрешений** выберите **Выбор разрешений**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="e33b1-130">Задать **разрешений** слишком**Execute**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="e33b1-131">Задать **добавить** слишком**эту папку и все дочерние элементы**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="e33b1-132">Задать **добавить в качестве** слишком**запись разрешения доступа, а элемент разрешения по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="e33b1-133">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="e33b1-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="e33b1-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-134">Click **OK**.</span></span>

4. <span data-ttu-id="e33b1-135">Назначение разрешений для папки hello под учетной записью хранилища Озера данных место toocapture данных.</span><span class="sxs-lookup"><span data-stu-id="e33b1-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="e33b1-136">а.</span><span class="sxs-lookup"><span data-stu-id="e33b1-136">a.</span></span> <span data-ttu-id="e33b1-137">Нажмите кнопку **обозреватель данных**, выберите папку hello в hello хранилища Озера данных и нажмите кнопку **доступа**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="e33b1-138">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="e33b1-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="e33b1-139">b.</span><span class="sxs-lookup"><span data-stu-id="e33b1-139">b.</span></span> <span data-ttu-id="e33b1-140">В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="e33b1-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="e33b1-141">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="e33b1-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="e33b1-142">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-142">Click **Select**.</span></span>

    <span data-ttu-id="e33b1-143">c.</span><span class="sxs-lookup"><span data-stu-id="e33b1-143">c.</span></span> <span data-ttu-id="e33b1-144">В разделе **Назначение разрешений** выберите **Выбор разрешений**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="e33b1-145">Задать **разрешений** слишком**чтение, запись и** и **Execute**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="e33b1-146">Задать **добавить** слишком**эту папку и все дочерние элементы**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="e33b1-147">Задайте **добавить в качестве** слишком**запись разрешения доступа, а элемент разрешения по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="e33b1-148">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="e33b1-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="e33b1-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="e33b1-150">Настройка хранилища Озера tooData данных toocapture концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="e33b1-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="e33b1-151">В этом разделе вы создаете концентратор событий в пространстве имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="e33b1-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="e33b1-152">Можно также настроить hello концентратора событий toocapture данных tooan хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="e33b1-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="e33b1-153">В этом разделе предполагается, что вы уже создали пространство имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="e33b1-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="e33b1-154">Из hello **Обзор** области пространства имен hello концентраторов событий, выберите **+ концентратора событий**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="e33b1-155">![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="e33b1-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="e33b1-156">Предоставляют следующие hello значения хранилища Озера данных tooData tooconfigure концентраторов событий toocapture.</span><span class="sxs-lookup"><span data-stu-id="e33b1-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="e33b1-157">![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="e33b1-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="e33b1-158">а.</span><span class="sxs-lookup"><span data-stu-id="e33b1-158">a.</span></span> <span data-ttu-id="e33b1-159">Введите имя для hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="e33b1-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="e33b1-160">b.</span><span class="sxs-lookup"><span data-stu-id="e33b1-160">b.</span></span> <span data-ttu-id="e33b1-161">В этом учебнике значение **количество разделов** и **хранение сообщений** toohello значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e33b1-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="e33b1-162">c.</span><span class="sxs-lookup"><span data-stu-id="e33b1-162">c.</span></span> <span data-ttu-id="e33b1-163">Задать **захвата** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="e33b1-164">Набор hello **временное окно** (как часто toocapture) и **размер окна** (toocapture размер данных).</span><span class="sxs-lookup"><span data-stu-id="e33b1-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="e33b1-165">d.</span><span class="sxs-lookup"><span data-stu-id="e33b1-165">d.</span></span> <span data-ttu-id="e33b1-166">Для **записи поставщика**выберите **хранилища Озера данных Azure** и hello выберите hello хранилища Озера данных, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="e33b1-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="e33b1-167">Для **пути Озера данных**, введите имя hello hello папку, созданную в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e33b1-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="e33b1-168">Требуется только относительный путь toohello tooprovide hello папки.</span><span class="sxs-lookup"><span data-stu-id="e33b1-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="e33b1-169">д.</span><span class="sxs-lookup"><span data-stu-id="e33b1-169">e.</span></span> <span data-ttu-id="e33b1-170">Оставьте hello **имя образца отслеживания форматах** toohello значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e33b1-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="e33b1-171">Этот параметр определяет структуру папок hello, созданному в папку отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="e33b1-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="e33b1-172">f.</span><span class="sxs-lookup"><span data-stu-id="e33b1-172">f.</span></span> <span data-ttu-id="e33b1-173">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e33b1-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="e33b1-174">Программа установки hello теста</span><span class="sxs-lookup"><span data-stu-id="e33b1-174">Test hello setup</span></span>

<span data-ttu-id="e33b1-175">Теперь можно проверить hello решения путем отправки данных toohello концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="e33b1-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="e33b1-176">Следуйте инструкциям hello в [отправки событий концентраторов событий tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="e33b1-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="e33b1-177">После начала отправки данных hello появиться hello данные отражаются в хранилище Озера данных hello структуру папок, указанные с помощью.</span><span class="sxs-lookup"><span data-stu-id="e33b1-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="e33b1-178">Просмотреть структуру папок, например, как показано на следующий снимок экрана, находящихся в хранилище Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="e33b1-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="e33b1-179">![Пример данных концентратора событий в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="e33b1-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="e33b1-180">Даже если нет сообщений, поступающих в концентраторы событий, концентраторы событий записывает пустые файлы с только что hello заголовки в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e33b1-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="e33b1-181">Hello файлы записываются в hello же интервал времени, который был предоставлен при создании hello концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="e33b1-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="e33b1-182">Анализ данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="e33b1-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="e33b1-183">После загрузки данных hello в хранилище Озера данных, аналитических задания можно выполнять tooprocess и обработайте данные hello.</span><span class="sxs-lookup"><span data-stu-id="e33b1-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="e33b1-184">В разделе [USQL Avro пример](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) о том, как toodo этот с помощью аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="e33b1-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="e33b1-185">См. также</span><span class="sxs-lookup"><span data-stu-id="e33b1-185">See also</span></span>
* [<span data-ttu-id="e33b1-186">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="e33b1-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e33b1-187">Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e33b1-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
