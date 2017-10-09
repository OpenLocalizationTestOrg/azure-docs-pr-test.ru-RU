---
title: "руководство по aaaTroubleshooting для динамической потоковой передачи | Документы Microsoft"
description: "В этом разделе приводятся рекомендации, в том, как tootroubleshoot live проблемы потоковой передачи."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="b21fd-103">Руководство по устранению неполадок потоковой передачи в реальном времени</span><span class="sxs-lookup"><span data-stu-id="b21fd-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="b21fd-104">В этом разделе приводятся рекомендации о том, как tootroubleshoot некоторые динамической потоковой передачи проблем.</span><span class="sxs-lookup"><span data-stu-id="b21fd-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="b21fd-105">Проблемы, связанные с локальной tooon кодировщики</span><span class="sxs-lookup"><span data-stu-id="b21fd-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="b21fd-106">В этом разделе рассматриваются рекомендации по настройке toosend tootroubleshoot проблем связанных tooon локальных кодировщиков, которые являются каналы tooAMS односкоростной поток, которые включены для динамического кодирования.</span><span class="sxs-lookup"><span data-stu-id="b21fd-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="b21fd-107">Проблема: Хотел toosee журналы</span><span class="sxs-lookup"><span data-stu-id="b21fd-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="b21fd-108">**Потенциальная проблема**. Не удается найти журналы кодировщика, которые могут помочь в отладке.</span><span class="sxs-lookup"><span data-stu-id="b21fd-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="b21fd-109">**Telestream Wirecast**. Обычно журналы можно найти в папке C:\Users\{имя_пользователя}\AppData\Roaming\Wirecast\.</span><span class="sxs-lookup"><span data-stu-id="b21fd-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="b21fd-110">**Элементарных Live**: можно найти, содержит toologs ссылки на портал управления hello.</span><span class="sxs-lookup"><span data-stu-id="b21fd-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="b21fd-111">Щелкните **Статистика**, а затем **Журналы**.</span><span class="sxs-lookup"><span data-stu-id="b21fd-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="b21fd-112">На hello **файлы журналов** страницы, вы увидите список журналов для всех hello LiveEvent элементы, выбрать hello подходящих текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="b21fd-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="b21fd-113">**Flash Media Live Encoder**: можно найти hello **каталог журналов...**  , перейдя по toohello **кодирование журнала** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b21fd-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="b21fd-114">Проблема. Невозможно вывести поток с прогрессивной разверткой</span><span class="sxs-lookup"><span data-stu-id="b21fd-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="b21fd-115">**Потенциальная проблема**: используется кодировщик hello не объединения полей автоматически.</span><span class="sxs-lookup"><span data-stu-id="b21fd-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="b21fd-116">**Действия по устранению неполадок**: поиск чередование параметра в интерфейсе кодировщика hello.</span><span class="sxs-lookup"><span data-stu-id="b21fd-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="b21fd-117">После включения устранения чересстрочной развертки еще раз проверьте настройки вывода потока с прогрессивной разверткой.</span><span class="sxs-lookup"><span data-stu-id="b21fd-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="b21fd-118">Проблема: Попытка несколько выходные параметры кодировщика и по-прежнему не удается tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b21fd-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="b21fd-119">**Потенциальная причина**. Канал службы кодирования Azure не был сброшен должным образом.</span><span class="sxs-lookup"><span data-stu-id="b21fd-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="b21fd-120">**Действия по устранению неполадок**: Убедитесь, что кодировщик hello больше не внедряет tooAMS, остановите и сброс hello канала.</span><span class="sxs-lookup"><span data-stu-id="b21fd-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="b21fd-121">После повторного запуска попытайтесь подключиться к нему кодировщик hello новыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="b21fd-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="b21fd-122">Если это по-прежнему не устраняет проблему hello, попробуйте создать полностью новый канал, иногда каналов может быть поврежден, после нескольких неудачных попыток.</span><span class="sxs-lookup"><span data-stu-id="b21fd-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="b21fd-123">**Потенциальная проблема**: hello GOP размер или параметры кадра не являются оптимальными.</span><span class="sxs-lookup"><span data-stu-id="b21fd-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="b21fd-124">**Шаги по устранению неполадок**. Рекомендуемое значение размера GOP или интервала опорного кадра — 2 секунды.</span><span class="sxs-lookup"><span data-stu-id="b21fd-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="b21fd-125">В некоторых кодировщиках этот параметр задается в количестве кадров, в других — в количестве секунд.</span><span class="sxs-lookup"><span data-stu-id="b21fd-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="b21fd-126">Например: при выводе 30 кадров/с, hello размер GOP бы 60 кадров это эквивалент too2 секунд.</span><span class="sxs-lookup"><span data-stu-id="b21fd-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="b21fd-127">**Потенциальная проблема**: закрытый порты блокируют поток hello.</span><span class="sxs-lookup"><span data-stu-id="b21fd-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="b21fd-128">**Действия по устранению неполадок**: во время потоковой передачи через RTMP, проверьте брандмауэр и/или tooconfirm параметры прокси-сервера, что 1935 и 1936 исходящие порты открыты.</span><span class="sxs-lookup"><span data-stu-id="b21fd-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="b21fd-129">При потоковой передаче через RTP убедитесь, что открыт исходящий порт 2010.</span><span class="sxs-lookup"><span data-stu-id="b21fd-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="b21fd-130">Проблема: При настройке toostream кодировщика hello с hello протокола RTP, нет места нет tooenter имя узла.</span><span class="sxs-lookup"><span data-stu-id="b21fd-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="b21fd-131">**Потенциальная проблема**: многие RTP кодировщиков не допускают имена узлов и IP-адрес, потребуется получить toobe.</span><span class="sxs-lookup"><span data-stu-id="b21fd-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="b21fd-132">**Действия по устранению неполадок**: toofind Здравствуйте IP-адрес, откройте командную строку на любом компьютере.</span><span class="sxs-lookup"><span data-stu-id="b21fd-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="b21fd-133">toodo это в Windows, откройте hello запуска выполнения (WIN + R) и введите «cmd» tooopen.</span><span class="sxs-lookup"><span data-stu-id="b21fd-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="b21fd-134">После открытия hello командной строке введите «Ping [имя ведущего AMS]».</span><span class="sxs-lookup"><span data-stu-id="b21fd-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="b21fd-135">Имя узла Hello могут быть производными, не указывайте номер порта hello hello Azure URL-адрес приема, как видно из hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b21fd-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="b21fd-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="b21fd-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="b21fd-138">Если после выполнения действия по устранению неполадок hello, вы по-прежнему не удается направить поток успешно, отправьте запрос на поддержку с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b21fd-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="b21fd-139">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b21fd-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b21fd-140">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b21fd-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

