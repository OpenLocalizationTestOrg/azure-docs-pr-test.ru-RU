---
title: "Запись данных из концентраторов событий в Azure Data Lake Store | Документация Майкрософт"
description: "Запись данных из концентраторов событий с помощью Azure Data Lake Store."
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
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="7a4c9-103">Запись данных из концентраторов событий с помощью Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a4c9-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="7a4c9-104">В этой статье приведены сведения о записи данных, полученных концентратором событий Azure с помощью Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a4c9-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a4c9-105">Prerequisites</span></span>

* <span data-ttu-id="7a4c9-106">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-106">**An Azure subscription**.</span></span> <span data-ttu-id="7a4c9-107">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7a4c9-108">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="7a4c9-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="7a4c9-109">Инструкции по созданию учетной записи см. в статье, посвященной [началу работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="7a4c9-110">**Пространство имен концентраторов событий.**</span><span class="sxs-lookup"><span data-stu-id="7a4c9-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="7a4c9-111">Дополнительные сведения см. в разделе [Создание пространства имен концентраторов событий](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="7a4c9-112">Убедитесь, что учетная запись Data Lake Store и пространство имен концентраторов событий находятся в одной подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="7a4c9-113">Назначение разрешений концентраторам событий</span><span class="sxs-lookup"><span data-stu-id="7a4c9-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="7a4c9-114">В этом разделе вы создадите папку в учетной записи, в которой необходимо сохранить данные из концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="7a4c9-115">Вы также можете назначить разрешения концентраторам событий. Это позволит им записывать данные в учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="7a4c9-116">Откройте учетную запись Data Lake Store, в которой необходимо сохранить данные из концентраторов событий, и щелкните **Обозреватель данных**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="7a4c9-117">![Обозреватель данных Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="7a4c9-118">Выберите **Создать папку** и введите имя папки, в которую необходимо сохранять данные.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="7a4c9-119">![Создание папки в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="7a4c9-120">Назначьте разрешения в корневой папке Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="7a4c9-121">а.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-121">a.</span></span> <span data-ttu-id="7a4c9-122">Щелкните **Обозреватель данных**, выберите корневую папку учетной записи Data Lake Store, а затем — **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="7a4c9-123">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="7a4c9-124">b.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-124">b.</span></span> <span data-ttu-id="7a4c9-125">В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="7a4c9-126">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="7a4c9-127">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-127">Click **Select**.</span></span>

    <span data-ttu-id="7a4c9-128">c.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-128">c.</span></span> <span data-ttu-id="7a4c9-129">В разделе **Назначение разрешений** выберите **Выбор разрешений**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="7a4c9-130">Задайте для параметра **Разрешения** значение **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="7a4c9-131">Задайте для параметра **Добавить к** значение **К этой папке и всем вложенным элементам**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="7a4c9-132">Задайте для параметра **Add as** (Добавить как) значение **Запись разрешений доступа и запись разрешений по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="7a4c9-133">![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="7a4c9-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-134">Click **OK**.</span></span>

4. <span data-ttu-id="7a4c9-135">Назначьте разрешения папке в учетной записи Data Lake Store, в которой необходимо сохранить данные.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="7a4c9-136">а.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-136">a.</span></span> <span data-ttu-id="7a4c9-137">Щелкните **Обозреватель данных**, выберите папку в учетной записи Data Lake Store, а затем — **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="7a4c9-138">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="7a4c9-139">b.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-139">b.</span></span> <span data-ttu-id="7a4c9-140">В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="7a4c9-141">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="7a4c9-142">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-142">Click **Select**.</span></span>

    <span data-ttu-id="7a4c9-143">c.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-143">c.</span></span> <span data-ttu-id="7a4c9-144">В разделе **Назначение разрешений** выберите **Выбор разрешений**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="7a4c9-145">Для параметра **Разрешения** установите флажки **Чтение, Запись** и **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="7a4c9-146">Задайте для параметра **Добавить к** значение **К этой папке и всем вложенным элементам**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="7a4c9-147">Наконец, задайте для параметра **Add as** (Добавить как) значение **Запись разрешений доступа и запись разрешений по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="7a4c9-148">![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="7a4c9-149">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="7a4c9-150">Настройка концентраторов событий для записи данных в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a4c9-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="7a4c9-151">В этом разделе вы создаете концентратор событий в пространстве имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="7a4c9-152">Кроме того, вы также настроите концентратор событий для записи данных в учетную запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="7a4c9-153">В этом разделе предполагается, что вы уже создали пространство имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="7a4c9-154">В области **Обзор** пространства имен концентраторов событий выберите **Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="7a4c9-155">![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="7a4c9-156">Чтобы настроить концентратор событий для записи данных в Data Lake Store, укажите приведенные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="7a4c9-157">![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="7a4c9-158">а.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-158">a.</span></span> <span data-ttu-id="7a4c9-159">Укажите имя концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="7a4c9-160">b.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-160">b.</span></span> <span data-ttu-id="7a4c9-161">В этом руководстве задайте для параметров **Количество разделов** и **Хранение сообщений** значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="7a4c9-162">c.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-162">c.</span></span> <span data-ttu-id="7a4c9-163">Установите для параметра **Запись** значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="7a4c9-164">Задайте **окно времени** (частота выполнения записи) и **окно размера** (размер данных для записи).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="7a4c9-165">d.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-165">d.</span></span> <span data-ttu-id="7a4c9-166">Для параметра **Capture Provider** (Поставщик записи) задайте значение **Azure Data Lake Store** и выберите хранилище Data Lake Store, созданное ранее.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="7a4c9-167">В качестве значения параметра **Data Lake Path** (Путь к Data Lake) введите имя папки, созданной в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="7a4c9-168">Необходимо только указать относительный путь к папке.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="7a4c9-169">д.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-169">e.</span></span> <span data-ttu-id="7a4c9-170">Оставьте стандартное значение параметра **Воспользуйтесь поиском, чтобы отфильтровать репликации**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="7a4c9-171">Этот параметр определяет структуру папки, созданной в папке записи.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="7a4c9-172">f.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-172">f.</span></span> <span data-ttu-id="7a4c9-173">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="7a4c9-174">Тестирование настройки</span><span class="sxs-lookup"><span data-stu-id="7a4c9-174">Test the setup</span></span>

<span data-ttu-id="7a4c9-175">Теперь вы можете протестировать решение, отправив данные в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="7a4c9-176">Инструкции см. в статье [Отправка событий в концентраторы событий Azure с помощью платформы .NET Framework](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="7a4c9-177">Отправляемые данные отобразятся в Data Lake Store с использованием указанной структуры папки.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="7a4c9-178">Например, на снимке экрана ниже приведена структура папки, в которой отобразятся данные в Data Lake Store данные.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="7a4c9-179">![Пример данных концентратора событий в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7a4c9-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="7a4c9-180">Даже если в концентратор событий не поступают сообщения, он записывает пустые файлы лишь с заголовками в учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="7a4c9-181">Файлы записываются с интервалом времени, указанным при создании концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="7a4c9-182">Анализ данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="7a4c9-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="7a4c9-183">Когда данные появятся в Data Lake Store, вы можете выполнить задания аналитики, чтобы обработать их.</span><span class="sxs-lookup"><span data-stu-id="7a4c9-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="7a4c9-184">Сведения об использовании Azure Data Lake Analytics для выполнения этих действий см. в [примере USQL Avro](https://github.com/Azure/usql/tree/master/Examples/AvroExamples).</span><span class="sxs-lookup"><span data-stu-id="7a4c9-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="7a4c9-185">См. также</span><span class="sxs-lookup"><span data-stu-id="7a4c9-185">See also</span></span>
* [<span data-ttu-id="7a4c9-186">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="7a4c9-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7a4c9-187">Копирование данных из больших двоичных объектов службы хранилища Azure в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7a4c9-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
