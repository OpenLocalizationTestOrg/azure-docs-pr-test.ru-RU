---
title: "aaaUpload файлы в учетную запись служб мультимедиа Azure из Azure StorSimple | Документы Microsoft"
description: "В этой статье рассматривается использование диспетчера данных Azure StorSimple. статья Hello также связывает tootutorials, показывается, как данные tooextract из StorSimple и передать его как активы tooan учетная запись служб мультимедиа Azure."
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
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="0be8c-104">Отправка файлов в учетную запись служб мультимедиа Azure из Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="0be8c-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="0be8c-105">В этой статье рассматривается использование диспетчера данных Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0be8c-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="0be8c-106">статья Hello также связывает tootutorials, показывается, как данные tooextract из StorSimple и передать эти данные как активы tooan учетной записи служб мультимедиа Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="0be8c-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="0be8c-107">В настоящее время диспетчер данных Azure StorSimple доступен в качестве закрытой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="0be8c-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="0be8c-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="0be8c-108">Overview</span></span>

<span data-ttu-id="0be8c-109">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="0be8c-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="0be8c-110">Hello актива может содержать видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.) После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0be8c-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="0be8c-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) использует Облачное хранилище, а расширение hello локальное решение автоматически уровнями данных через hello локальное хранилище и Облачное хранилище.</span><span class="sxs-lookup"><span data-stu-id="0be8c-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="0be8c-112">устройство StorSimple Hello dedupes и сжимает данные перед отправкой toohello облака, сделав его очень эффективен для отправки больших файлов toohello облака.</span><span class="sxs-lookup"><span data-stu-id="0be8c-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="0be8c-113">Hello [данных StorSimple Manager](../storsimple/storsimple-data-manager-overview.md) служба предоставляет интерфейсы API, которые позволяют вам tooextract данные из StorSimple и представлять их как AMS активы.</span><span class="sxs-lookup"><span data-stu-id="0be8c-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="0be8c-114">Начало работы</span><span class="sxs-lookup"><span data-stu-id="0be8c-114">Get started</span></span>

1. <span data-ttu-id="0be8c-115">[Создание учетной записи службы мультимедиа](media-services-portal-create-account.md) в которую будут tootransfer hello активы.</span><span class="sxs-lookup"><span data-stu-id="0be8c-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="0be8c-116">Зарегистрируйтесь диспетчер данных, как описано в hello [данных StorSimple Manager](../storsimple/storsimple-data-manager-overview.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0be8c-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="0be8c-117">Создайте учетную запись диспетчера данных StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0be8c-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="0be8c-118">Создайте задание для преобразования данных, которое извлекает данные из устройства StorSimple, а затем переносит их в учетную запись AMS в качестве ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0be8c-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="0be8c-119">В начале выполнения задания hello создается очередь хранилища.</span><span class="sxs-lookup"><span data-stu-id="0be8c-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="0be8c-120">Эта очередь по мере готовности заполняется сообщениями о преобразованных больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="0be8c-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="0be8c-121">имя этой очереди Hello hello совпадает с именем hello hello определения задания.</span><span class="sxs-lookup"><span data-stu-id="0be8c-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="0be8c-122">Можно использовать этот toodetermine очереди при как ресурс — готовых и вызова к требуемой toorun операции служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0be8c-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="0be8c-123">Например можно использовать этот очереди tootrigger функцию Azure, которая содержит в себе hello необходимый код для служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0be8c-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="0be8c-124">См. также</span><span class="sxs-lookup"><span data-stu-id="0be8c-124">See also</span></span>

[<span data-ttu-id="0be8c-125">Используйте hello .net SDK tootrigger заданий в диспетчер данных hello</span><span class="sxs-lookup"><span data-stu-id="0be8c-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="0be8c-126">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0be8c-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0be8c-127">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0be8c-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0be8c-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0be8c-128">Next steps</span></span>

<span data-ttu-id="0be8c-129">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0be8c-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="0be8c-130">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="0be8c-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
