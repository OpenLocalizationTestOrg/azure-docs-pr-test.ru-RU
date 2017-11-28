---
title: "Пропускная способность сети Azure RemoteApp — общие рекомендации | Документация Майкрософт"
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="34035-103">Пропускная способность сети Azure RemoteApp — общие рекомендации (если невозможно провести свои тесты)</span><span class="sxs-lookup"><span data-stu-id="34035-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34035-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="34035-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="34035-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="34035-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="34035-106">Если у вас нет времени или возможностей для выполнения [тестов пропускной способности сети](remoteapp-bandwidthtests.md) Azure RemoteApp, ниже приведено несколько общих рекомендаций, которые помогут оценить пропускную способность сети на пользователя.</span><span class="sxs-lookup"><span data-stu-id="34035-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="34035-107">Если имеется смесь таких сценариев, мы рекомендуем использовать для современных подключенных к Интернету приложений в удаленной среде пропускную способность НЕ МЕНЕЕ 10 МБ/с.</span><span class="sxs-lookup"><span data-stu-id="34035-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="34035-108">(Хотя, как уже было сказано, это обеспечивает взаимодействие с пользователем лишь на приемлемом уровне.)</span><span class="sxs-lookup"><span data-stu-id="34035-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="34035-109">Сложный PowerPoint, простой PowerPoint</span><span class="sxs-lookup"><span data-stu-id="34035-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="34035-110">Лучше всего Azure RemoteApp работает в локальной сети 100 МБ/с.</span><span class="sxs-lookup"><span data-stu-id="34035-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="34035-111">При сетевом профиле 10 МБ/с, когда дрожание свыше 120 мс составляет более 5 %, взаимодействие с пользователем осуществляется на среднем уровне.</span><span class="sxs-lookup"><span data-stu-id="34035-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="34035-112">На скорости 1 МБ/с возникает бликование, например во время показа слайдов, и пользователь может вообще не замечать анимированные переходы из-за пропуска кадров.</span><span class="sxs-lookup"><span data-stu-id="34035-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="34035-113">Internet Explorer, смешанный PDF, PDF, текст</span><span class="sxs-lookup"><span data-stu-id="34035-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="34035-114">По большинству показателей сетевой профиль 10 МБ/с близок к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="34035-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="34035-115">Скорость 1 МБ/с обеспечивает нормальную работу, однако при прокрутке экрана с изображениями может возникать дрожание.</span><span class="sxs-lookup"><span data-stu-id="34035-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="34035-116">Видео в формате Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="34035-116">Flash video (YouTube)</span></span>
<span data-ttu-id="34035-117">Локальная сеть 100 МБ/с обеспечивает наилучшее, а 10 МБ/с — приемлемое качество работы (то есть частота кадров остается допустимой, но увеличивается дрожание).</span><span class="sxs-lookup"><span data-stu-id="34035-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="34035-118">При скорости 1 МБ/с дрожание достигает очень высокого уровня и становится заметным.</span><span class="sxs-lookup"><span data-stu-id="34035-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="34035-119">Ввод в Word (удаленный ввод в Word)</span><span class="sxs-lookup"><span data-stu-id="34035-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="34035-120">Это сценарий отличается низким использованием пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="34035-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="34035-121">При 256 КБ/с обеспечивается качество работы, сопоставимое с локальной сетью.</span><span class="sxs-lookup"><span data-stu-id="34035-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="34035-122">Подробнее</span><span class="sxs-lookup"><span data-stu-id="34035-122">Learn more</span></span>
* [<span data-ttu-id="34035-123">Оценка использования пропускной способности сети Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="34035-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="34035-124">Azure RemoteApp — как пропускная способность сети и качество взаимодействия связаны друг с другом?</span><span class="sxs-lookup"><span data-stu-id="34035-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="34035-125">Azure RemoteApp — тест использования пропускной способности сети в рамках распространенных сценариев</span><span class="sxs-lookup"><span data-stu-id="34035-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

