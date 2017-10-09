---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - аналитика"
description: "Поиск и устранение неисправностей функций аналитики, мониторинга, сегментации и панели мониторинга в Службах мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="d8310-103">Поиск и устранение неисправностей функций аналитики, мониторинга, сегментации и панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="d8310-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="d8310-104">Hello ниже приведены возможные причины неполадок можно столкнуться с каким образом Azure Mobile Engagement собирает сведения о приложениях, устройствами и пользователями.</span><span class="sxs-lookup"><span data-stu-id="d8310-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="d8310-105">Отсутствие или задержка информации</span><span class="sxs-lookup"><span data-stu-id="d8310-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="d8310-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="d8310-106">Issue</span></span>
* <span data-ttu-id="d8310-107">Информация в разделе аналитики, сегментации или панели мониторинга отображается с задержкой.</span><span class="sxs-lookup"><span data-stu-id="d8310-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="d8310-108">Отсутствует информация в разделе мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="d8310-109">Отсутствует информация в разделе аналитики, сегментации или панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="d8310-110">Достигнут предел сегментации.</span><span class="sxs-lookup"><span data-stu-id="d8310-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="d8310-111">Причины</span><span class="sxs-lookup"><span data-stu-id="d8310-111">Causes</span></span>
* <span data-ttu-id="d8310-112">Можно использовать hello API аналитики API монитора и toosee API сегментов, если все данные вы отсутствуют hello пользовательского интерфейса доступны через hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="d8310-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="d8310-113">Если hello Azure Mobile Engagement SDK правильно не интегрирована в приложения, не будет возможности toosee сведения в hello аналитика, сегментация, мониторинга или панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="d8310-114">После создания сегменты нельзя изменить. Их можно только "клонировать" (скопировать) или "уничтожить" (удалить).</span><span class="sxs-lookup"><span data-stu-id="d8310-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="d8310-115">Сегменты могут содержать только 10 критериев.</span><span class="sxs-lookup"><span data-stu-id="d8310-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="d8310-116">Лучшим способом tootest Hello отсутствуют сведения из наблюдения toosetup тестовое устройство, удалите и/или переустановите приложение hello на hello тестовое устройство.</span><span class="sxs-lookup"><span data-stu-id="d8310-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="d8310-117">В разделах аналитики, сегментации и панели мониторинга информация обновляется каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="d8310-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="d8310-118">Сведения в новые сегменты могут не отображаться до 24 часов после они создаются, даже если сегмент hello основан на предыдущих данных.</span><span class="sxs-lookup"><span data-stu-id="d8310-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="d8310-119">Фильтрация данных аналитики в hello пользовательского интерфейса будет Показать все примеры этого типа, независимо от версии приложения hello (например) если "Сбои" отфильтровать по имени, отобразятся примеры версии 1 и 2 вашего приложения).</span><span class="sxs-lookup"><span data-stu-id="d8310-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="d8310-120">Hello период времени для анализа основан на hello дат из параметров устройства, пользователи hello, поэтому пользователь, которого на телефоне задан неправильно задана дата hello может отображаться в hello неправильный период времени.</span><span class="sxs-lookup"><span data-stu-id="d8310-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="d8310-121">Ни одна сторона сервера данных регистрируется при использовании кнопки hello слишком «test» помещает, регистрируются только данные для реальных push-кампаний.</span><span class="sxs-lookup"><span data-stu-id="d8310-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="d8310-122">Не удается найти элементы в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d8310-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="d8310-123">Проблема</span><span class="sxs-lookup"><span data-stu-id="d8310-123">Issue</span></span>
* <span data-ttu-id="d8310-124">Не удается создать сегменты на основе определенных критериев тега информации о встроенном или настраиваемом приложении.</span><span class="sxs-lookup"><span data-stu-id="d8310-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="d8310-125">Не удается найти определенные условия тега информации о встроенном или настраиваемом приложении в разделах аналитики, мониторинга или панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="d8310-126">Не удается интерпретировать данные hello в аналитика, мониторинг, сегментация или панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="d8310-127">Причины</span><span class="sxs-lookup"><span data-stu-id="d8310-127">Causes</span></span>
* <span data-ttu-id="d8310-128">Некоторые встроенные элементы и информация приложения доступны только в качестве условия для принудительной теги, но могут быть добавлены tooa сегмента или видимым из Analytics, мониторинга или панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d8310-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="d8310-129">Для встроенных элементов и приложение сведения о том, что теги, которые не могут быть добавлены tooa сегмента, вам потребуется toosetup список целевых условия в каждой hello tooperform кампании, функция аналогична нацеливания на основе сегмента.</span><span class="sxs-lookup"><span data-stu-id="d8310-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="d8310-130">Контекстные меню hello в hello аналитика, мониторинг, сегментации и панелей мониторинга разделах hello пользовательского интерфейса Azure Mobile Engagement для получения дополнительных сведений см. и как tooinformation.</span><span class="sxs-lookup"><span data-stu-id="d8310-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="d8310-131">Устранение неполадок при сбое</span><span class="sxs-lookup"><span data-stu-id="d8310-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="d8310-132">Проблема</span><span class="sxs-lookup"><span data-stu-id="d8310-132">Issue</span></span>
* <span data-ttu-id="d8310-133">В разделах аналитики, мониторинга и панели мониторинга отображаются данные о сбоях приложений.</span><span class="sxs-lookup"><span data-stu-id="d8310-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="d8310-134">Причины</span><span class="sxs-lookup"><span data-stu-id="d8310-134">Causes</span></span>
* <span data-ttu-id="d8310-135">tootroubleshoot приложение аварийно завершает работу в Analytics, мониторинга или панели мониторинга убедитесь, что toocheck hello заметки о выпуске известные проблемы с предыдущими версиями пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="d8310-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="d8310-136">toofurther устранения приложения происходит сбой выполнения события из тестовое устройство с установки приложения и поиск ИД устройства в разделе "hello «монитор событий —»" hello пользовательского интерфейса Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8310-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="d8310-137">Затем выполните hello событие, которое является причиной toocrash вашего приложения и найти дополнительные сведения в раздел «Монитор — приводит к сбою» hello пользовательского интерфейса Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="d8310-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

