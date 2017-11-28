---
title: "Отправка файлов в учетную запись служб мультимедиа Azure из Azure StorSimple | Документация Майкрософт"
description: "В этой статье рассматривается использование диспетчера данных Azure StorSimple. Она также содержит ссылки на руководства, в которых описывается, как извлечь данные из StorSimple и передать их в качестве ресурсов в учетную запись служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 636d55c15aa383208ffb39d5224123831af962c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="a2d1a-104">Отправка файлов в учетную запись служб мультимедиа Azure из Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="a2d1a-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="a2d1a-105">В этой статье рассматривается использование диспетчера данных Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="a2d1a-106">Она также содержит ссылки на руководства, в которых описывается, как извлечь данные из StorSimple и передать их в качестве ресурсов в учетную запись служб мультимедиа Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="a2d1a-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="a2d1a-107">В настоящее время диспетчер данных Azure StorSimple доступен в качестве закрытой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="a2d1a-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="a2d1a-108">Overview</span></span>

<span data-ttu-id="a2d1a-109">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a2d1a-110">Ресурс может содержать видео, аудио, изображения, коллекции эскизов, текстовые каналы и файлы скрытых субтитров (и метаданные этих файлов). После отправки этих файлов содержимое сохраняется в безопасном расположении в облаке для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="a2d1a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) использует облачное хранилище в качестве расширения локального решения и автоматически связывает данные локального хранилища с данными облачного хранилища.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="a2d1a-112">Перед отправкой данных в облако устройство StorSimple дублирует и сжимает их. Таким образом, в облако можно эффективно отправлять большие файлы.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="a2d1a-113">Служба [диспетчера данных StorSimple](../storsimple/storsimple-data-manager-overview.md) предоставляет интерфейсы API, позволяющие извлекать данные из StorSimple и представлять их в качестве ресурсов AMS.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="a2d1a-114">Начало работы</span><span class="sxs-lookup"><span data-stu-id="a2d1a-114">Get started</span></span>

1. <span data-ttu-id="a2d1a-115">[Создайте учетную запись служб мультимедиа](media-services-portal-create-account.md), в которую вы хотите перенести ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="a2d1a-116">Зарегистрируйтесь для получения предварительной версии диспетчера данных, как описано в статье [Общие сведения о диспетчере данных StorSimple (закрытая предварительная версия)](../storsimple/storsimple-data-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2d1a-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="a2d1a-117">Создайте учетную запись диспетчера данных StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="a2d1a-118">Создайте задание для преобразования данных, которое извлекает данные из устройства StorSimple, а затем переносит их в учетную запись AMS в качестве ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="a2d1a-119">При запуске задания создается очередь хранилища.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="a2d1a-120">Эта очередь по мере готовности заполняется сообщениями о преобразованных больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="a2d1a-121">Имя этой очереди совпадает с именем определения задания.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="a2d1a-122">Вы можете использовать эту очередь для определения готовности ресурсов, а затем вызвать необходимую операцию служб мультимедиа для этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="a2d1a-123">Например, вы можете использовать эту очередь, чтобы активировать функции Azure, в которых содержится нужный код служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="a2d1a-124">См. также</span><span class="sxs-lookup"><span data-stu-id="a2d1a-124">See also</span></span>

[<span data-ttu-id="a2d1a-125">Запуск преобразования данных с помощью пакета SDK для .NET (закрытая предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="a2d1a-125">Use the .Net SDK to trigger jobs in the Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="a2d1a-126">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a2d1a-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2d1a-127">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a2d1a-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a2d1a-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2d1a-128">Next steps</span></span>

<span data-ttu-id="a2d1a-129">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a2d1a-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a2d1a-130">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="a2d1a-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
