---
title: "пропускная способность сети RemoteApp aaaAzure — Общие рекомендации | Документы Microsoft"
description: "Описание общих рекомендаций по пропускной способности сети для приложений и коллекций Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="13a26-103">Пропускная способность сети Azure RemoteApp — общие рекомендации (если невозможно провести свои тесты)</span><span class="sxs-lookup"><span data-stu-id="13a26-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="13a26-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="13a26-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="13a26-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="13a26-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="13a26-106">Если у вас hello hello времени или возможности toorun [тесты пропускной способности сети](remoteapp-bandwidthtests.md) для Azure RemoteApp, ниже приведены некоторые достаточно общий рекомендации, которые могут помочь оценить пропускной способности сети для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="13a26-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="13a26-107">Если имеется смесь этих сценариев, мы не рекомендуем ничего не превышала (в) 10 МБИТ/с, hello минимальную пропускную способность сети для современных приложений, подключенных к Интернету, в удаленной среде.</span><span class="sxs-lookup"><span data-stu-id="13a26-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="13a26-108">(Хотя, как уже было сказано, это обеспечивает взаимодействие с пользователем лишь на приемлемом уровне.)</span><span class="sxs-lookup"><span data-stu-id="13a26-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="13a26-109">Сложный PowerPoint, простой PowerPoint</span><span class="sxs-lookup"><span data-stu-id="13a26-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="13a26-110">Лучше всего Azure RemoteApp работает в локальной сети 100 МБ/с.</span><span class="sxs-lookup"><span data-stu-id="13a26-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="13a26-111">В hello 10 МБ/s сетевого профиля при флуктуации выше 120 ms более 5%, hello пользователя будет отображаться среднее взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="13a26-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="13a26-112">На 1 МБ в секунду hello другой glaring - например, слайд-шоу, hello пользователь может не видеть анимации вообще поскольку кадры пропускаются.</span><span class="sxs-lookup"><span data-stu-id="13a26-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="13a26-113">Internet Explorer, смешанный PDF, PDF, текст</span><span class="sxs-lookup"><span data-stu-id="13a26-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="13a26-114">Сетевой профиль 10 МБИТ/с — закрыть tooLAN по большей части.</span><span class="sxs-lookup"><span data-stu-id="13a26-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="13a26-115">1 МБ в секунду предоставит интерфейс ОК, несмотря на то, что возможны некоторые флуктуации когда пользователь выполняет прокрутку, пока имеются изображения на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="13a26-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="13a26-116">Видео в формате Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="13a26-116">Flash video (YouTube)</span></span>
<span data-ttu-id="13a26-117">100 МБИТ/с локальной сети обеспечивает максимальное удобство hello, допустимые (то есть вам справиться с частотой кадров hello, однако флуктуаций увеличивается) — 10 МБИТ/с.</span><span class="sxs-lookup"><span data-stu-id="13a26-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="13a26-118">При скорости 1 МБ/с дрожание достигает очень высокого уровня и становится заметным.</span><span class="sxs-lookup"><span data-stu-id="13a26-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="13a26-119">Ввод в Word (удаленный ввод в Word)</span><span class="sxs-lookup"><span data-stu-id="13a26-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="13a26-120">Это сценарий отличается низким использованием пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="13a26-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="13a26-121">При 256 КБ/с обеспечивается качество работы, сопоставимое с локальной сетью.</span><span class="sxs-lookup"><span data-stu-id="13a26-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="13a26-122">Подробнее</span><span class="sxs-lookup"><span data-stu-id="13a26-122">Learn more</span></span>
* [<span data-ttu-id="13a26-123">Оценка использования пропускной способности сети Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="13a26-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="13a26-124">Azure RemoteApp — как пропускная способность сети и качество взаимодействия связаны друг с другом?</span><span class="sxs-lookup"><span data-stu-id="13a26-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="13a26-125">Azure RemoteApp — тест использования пропускной способности сети в рамках распространенных сценариев</span><span class="sxs-lookup"><span data-stu-id="13a26-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

