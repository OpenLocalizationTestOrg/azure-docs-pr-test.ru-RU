---
title: "Включение записи концентраторов событий с помощью портала | Документация Microsoft"
description: "Включите функцию записи концентраторов событий с помощью портала Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="e6ce3-103">Включение записи концентраторов событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e6ce3-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="e6ce3-104">Запись можно настроить при создании концентратора событий с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6ce3-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e6ce3-105">Данные можно записывать в контейнер [хранилища BLOB-объектов Azure](https://azure.microsoft.com/services/storage/blobs/) или в учетную запись [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="e6ce3-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="e6ce3-106">Запись данных в учетную запись службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e6ce3-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="e6ce3-107">При создании концентратора событий можно включить сбор, щелкнув **на** кнопку в **создать концентратор событий** портала колонку.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="e6ce3-108">Затем укажите учетную запись хранения и контейнер, выбрав **Служба хранилища Azure** в поле **поставщика записи**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="e6ce3-109">Так как для функции записи концентраторов событий и хранилища используется проверка подлинности с взаимодействием между службами, указывать строку подключения к хранилищу не нужно.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="e6ce3-110">Средство выбора ресурсов автоматически выбирает универсальный код ресурса (URI) для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="e6ce3-111">При использовании Azure Resource Manager этот универсальный код ресурса необходимо явным образом указать как строку.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="e6ce3-112">Продолжительность времени окна по умолчанию составляет 5 минут.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="e6ce3-113">Минимальное значение равно 1, а максимальное — 15.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="e6ce3-114">Диапазон **окна размера** составляет 10–500 МБ.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="e6ce3-115">Запись данных в учетную запись Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e6ce3-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="e6ce3-116">Для записи данных в Azure Data Lake Store создайте учетную запись Data Lake Store и концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="e6ce3-117">Создание учетной записи и папок Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e6ce3-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="e6ce3-118">Создайте учетную запись Data Lake Store, следуя инструкциям в статье [Начало работы с Azure Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6ce3-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="e6ce3-119">Создайте папку в этой учетной записи, следуя инструкциям в разделе [Создание папок в учетной записи хранения озера данных Azure](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="e6ce3-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="e6ce3-120">В колонке учетной записи хранилища Озера данных щелкните **обозреватель данных**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="e6ce3-121">Щелкните **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-121">Click **Access**.</span></span>
5. <span data-ttu-id="e6ce3-122">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-122">Click **Add**.</span></span>
6. <span data-ttu-id="e6ce3-123">В поле **Поиск по имени или электронной почте** введите **Microsoft.EventHubs** и выберите этот вариант.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="e6ce3-124">Появится вкладка **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="e6ce3-125">Задайте разрешения, как показано на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="e6ce3-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="e6ce3-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-126">Click **OK**.</span></span>
9. <span data-ttu-id="e6ce3-127">Теперь создайте папку в корневой папке, выбрав целевую папку и щелкнув ее имя.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="e6ce3-128">Щелкните **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-128">Click **Access**.</span></span>
11. <span data-ttu-id="e6ce3-129">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-129">Click **Add**.</span></span>
12. <span data-ttu-id="e6ce3-130">В поле **Поиск по имени или электронной почте** введите **Microsoft.EventHubs** и выберите этот вариант.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="e6ce3-131">Снова появится вкладка **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="e6ce3-132">Задайте разрешения, как показано на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="e6ce3-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="e6ce3-133">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="e6ce3-133">Create an event hub</span></span>

1. <span data-ttu-id="e6ce3-134">Обратите внимание, что концентратор событий должен находиться в той же подписке Azure, что и только что созданная учетная запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="e6ce3-135">Создать концентратор событий, щелкнув **на** под заголовком **захвата** в **создать концентратор событий** портала колонку.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="e6ce3-136">В **создать концентратор событий** портала колонки, **хранилища Озера данных Azure** из **записи поставщика** поле.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="e6ce3-137">В поле **Выберите Data Lake Store** укажите учетную запись Data Lake Store, созданную ранее, а в поле **Data Lake Path** (Путь к Data Lake) введите путь к созданной папке данных.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="e6ce3-138">Добавление или настройка функции записи для существующего концентратора событий</span><span class="sxs-lookup"><span data-stu-id="e6ce3-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="e6ce3-139">Функцию записи можно настроить в существующих концентраторах событий, расположенных в соответствующих пространствах имен.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="e6ce3-140">Чтобы включить запись в существующем концентраторе событий или изменить параметры записи, щелкните пространство имен. Откроется колонка **Основные компоненты**. Затем щелкните концентратор событий, для которого необходимо включить запись или изменить ее параметры.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="e6ce3-141">Наконец, нажмите кнопку **свойства** раздел откройте колонку и настройте параметры захвата, как показано на следующих рисунках:</span><span class="sxs-lookup"><span data-stu-id="e6ce3-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="e6ce3-142">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="e6ce3-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="e6ce3-143">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="e6ce3-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="e6ce3-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6ce3-144">Next steps</span></span>

<span data-ttu-id="e6ce3-145">Запись концентраторов событий можно также настроить с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6ce3-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="e6ce3-146">См. дополнительные сведения [о включении записи с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="e6ce3-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
