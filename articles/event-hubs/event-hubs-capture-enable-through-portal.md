---
title: "Включение захвата концентраторов событий aaaAzure через портал | Документы Microsoft"
description: "Включите функцию захвата концентраторов событий hello, с помощью портала Azure hello."
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
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="dff9d-103">Разрешить отслеживание концентраторов событий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="dff9d-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="dff9d-104">Можно настроить записи время hello события концентратора создания с помощью hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dff9d-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dff9d-105">Вы можете либо tooan данных отслеживания hello Azure [хранилище больших двоичных объектов](https://azure.microsoft.com/services/storage/blobs/) контейнера или tooan [хранилища Озера данных Azure](https://azure.microsoft.com/services/data-lake-store/) учетной записи.</span><span class="sxs-lookup"><span data-stu-id="dff9d-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="dff9d-106">Учетная запись для записи данных tooan хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="dff9d-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="dff9d-107">При создании концентратора событий можно включить сбор, щелкнув hello **на** кнопку в hello **создать концентратор событий** портала колонку.</span><span class="sxs-lookup"><span data-stu-id="dff9d-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="dff9d-108">Затем укажите учетную запись хранилища и контейнера, нажав кнопку **хранилища Azure** в hello **записи поставщика** поле.</span><span class="sxs-lookup"><span data-stu-id="dff9d-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="dff9d-109">Поскольку записи концентраторов событий использует проверку подлинности для службы с хранилищем, toospecify строки подключения хранилища не обязательно.</span><span class="sxs-lookup"><span data-stu-id="dff9d-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="dff9d-110">Средство выбора ресурсов Hello автоматически выбирает hello ресурса (URI) для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="dff9d-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="dff9d-111">При использовании Azure Resource Manager этот универсальный код ресурса необходимо явным образом указать как строку.</span><span class="sxs-lookup"><span data-stu-id="dff9d-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="dff9d-112">временное окно Hello по умолчанию равно 5 минутам.</span><span class="sxs-lookup"><span data-stu-id="dff9d-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="dff9d-113">Hello минимальное значение равно 1, максимальное 15 hello.</span><span class="sxs-lookup"><span data-stu-id="dff9d-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="dff9d-114">Hello **размер** окно имеет диапазон от 10 – 500 МБ.</span><span class="sxs-lookup"><span data-stu-id="dff9d-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="dff9d-115">Учетная запись для записи данных tooan хранилища Озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="dff9d-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="dff9d-116">tooAzure данных toocapture хранилища Озера данных, создать учетную запись хранилища Озера данных и концентратор событий:</span><span class="sxs-lookup"><span data-stu-id="dff9d-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="dff9d-117">Создание учетной записи и папок Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dff9d-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="dff9d-118">Создать учетную запись хранилища Озера данных, следуя инструкциям hello [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dff9d-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="dff9d-119">Создать папку в этой учетной записи, следуйте инструкциям hello в hello [создавать папки в учетной записи хранилища Озера данных Azure](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) раздела.</span><span class="sxs-lookup"><span data-stu-id="dff9d-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="dff9d-120">В колонке учетной записи хранилища Озера данных hello щелкните **обозреватель данных**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="dff9d-121">Щелкните **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-121">Click **Access**.</span></span>
5. <span data-ttu-id="dff9d-122">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-122">Click **Add**.</span></span>
6. <span data-ttu-id="dff9d-123">В hello **поиска по имени или по электронной почте** введите **Microsoft.EventHubs** и выберите этот параметр.</span><span class="sxs-lookup"><span data-stu-id="dff9d-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="dff9d-124">Hello **разрешений** появляется вкладка.</span><span class="sxs-lookup"><span data-stu-id="dff9d-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="dff9d-125">Задайте разрешения hello, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="dff9d-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="dff9d-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-126">Click **OK**.</span></span>
9. <span data-ttu-id="dff9d-127">Теперь создайте папку в корневой папке hello путем просмотра toohello целевую папку и щелкните имя папки hello.</span><span class="sxs-lookup"><span data-stu-id="dff9d-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="dff9d-128">Щелкните **Доступ**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-128">Click **Access**.</span></span>
11. <span data-ttu-id="dff9d-129">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dff9d-129">Click **Add**.</span></span>
12. <span data-ttu-id="dff9d-130">В hello **поиска по имени или по электронной почте** введите **Microsoft.EventHubs** и выберите этот параметр.</span><span class="sxs-lookup"><span data-stu-id="dff9d-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="dff9d-131">Hello **разрешений** появляется вкладка.</span><span class="sxs-lookup"><span data-stu-id="dff9d-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="dff9d-132">Задайте разрешения hello, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="dff9d-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="dff9d-133">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="dff9d-133">Create an event hub</span></span>

1. <span data-ttu-id="dff9d-134">Обратите внимание должен быть этот концентратор событий hello в hello ту же подписку Azure hello хранилища Озера данных Azure, вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="dff9d-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="dff9d-135">Концентратор событий hello создать, щелкнув hello **на** под заголовком **захвата** в hello **создать концентратор событий** портала колонку.</span><span class="sxs-lookup"><span data-stu-id="dff9d-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="dff9d-136">В hello **создать концентратор событий** портала колонки, **хранилища Озера данных Azure** из hello **записи поставщика** поле.</span><span class="sxs-lookup"><span data-stu-id="dff9d-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="dff9d-137">В **Выбор хранилища Озера данных**, укажите hello учетной записи хранилища Озера данных, созданную ранее, а hello **пути Озера данных** введите данные hello путь toohello папку, созданную.</span><span class="sxs-lookup"><span data-stu-id="dff9d-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="dff9d-138">Добавление или настройка функции записи для существующего концентратора событий</span><span class="sxs-lookup"><span data-stu-id="dff9d-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="dff9d-139">Функцию записи можно настроить в существующих концентраторах событий, расположенных в соответствующих пространствах имен.</span><span class="sxs-lookup"><span data-stu-id="dff9d-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="dff9d-140">tooenable записи на существующий концентратор событий, или toochange параметры отслеживания, щелкните приветствия имен tooload hello **Essentials** колонке нажмите кнопку hello концентратора событий, для которого вы хотите tooenable или изменить приветствия системы отслеживания.</span><span class="sxs-lookup"><span data-stu-id="dff9d-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="dff9d-141">Наконец, нажмите кнопку hello **свойства** раздел Привет открыть колонку и затем измените параметры захвата hello, как показано на следующих иллюстрациях hello:</span><span class="sxs-lookup"><span data-stu-id="dff9d-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="dff9d-142">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="dff9d-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="dff9d-143">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="dff9d-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="dff9d-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dff9d-144">Next steps</span></span>

<span data-ttu-id="dff9d-145">Запись концентраторов событий можно также настроить с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dff9d-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="dff9d-146">См. дополнительные сведения [о включении записи с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="dff9d-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
