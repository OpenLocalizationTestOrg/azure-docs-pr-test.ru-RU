---
title: "aaaWindows содержимое пакета SDK для универсальных приложений"
description: "Дополнительные сведения о hello содержимое пакета SDK универсальных приложений Windows hello для Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="e78a1-103">Содержимое пакета SDK для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="e78a1-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="e78a1-104">В этом документе перечислены и описаны hello содержимого, развернутого с hello SDK в приложении.</span><span class="sxs-lookup"><span data-stu-id="e78a1-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="e78a1-105">Hello `/Resources` папки</span><span class="sxs-lookup"><span data-stu-id="e78a1-105">hello `/Resources` folder</span></span>
<span data-ttu-id="e78a1-106">Эта папка содержит все hello ресурсы, необходимые для мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="e78a1-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="e78a1-107">Также можно настроить их toofit приложения.</span><span class="sxs-lookup"><span data-stu-id="e78a1-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="e78a1-108">`EngagementConfiguration.xml`: hello файла конфигурации мобильного охвата, это настройки параметров мобильного охвата (строка подключения мобильного охвата, сбой отчет...).</span><span class="sxs-lookup"><span data-stu-id="e78a1-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="e78a1-109">Папка /html</span><span class="sxs-lookup"><span data-stu-id="e78a1-109">/html folder</span></span>
* <span data-ttu-id="e78a1-110">`EngagementNotification.html`: hello `Notification` веб-представлении конструктора html для ленты в приложении.</span><span class="sxs-lookup"><span data-stu-id="e78a1-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="e78a1-111">`EngagementAnnouncement.html`: hello `Announcement` веб-представление конструктора html для представления interstitial в приложении.</span><span class="sxs-lookup"><span data-stu-id="e78a1-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="e78a1-112">Папка /images</span><span class="sxs-lookup"><span data-stu-id="e78a1-112">/images folder</span></span>
* <span data-ttu-id="e78a1-113">`EngagementIconNotification.png`: hello фирменной символики значка, отображаемого в hello слева уведомления — заменить этот значок вашей торговой марки.</span><span class="sxs-lookup"><span data-stu-id="e78a1-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="e78a1-114">`EngagementIconOk.png`: hello `Ok` значок hello reach содержимого страниц для кнопки действия или проверки hello.</span><span class="sxs-lookup"><span data-stu-id="e78a1-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="e78a1-115">`EngagementIconNOK.png`: hello `NOK` значок, используемый при отключении кнопка проверки hello hello reach содержимого страниц.</span><span class="sxs-lookup"><span data-stu-id="e78a1-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="e78a1-116">`EngagementIconClose.png`: hello `Close` значок hello достичь уведомления и содержимое для hello пропустить кнопки.</span><span class="sxs-lookup"><span data-stu-id="e78a1-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="e78a1-117">Папка /overlay</span><span class="sxs-lookup"><span data-stu-id="e78a1-117">/overlay folder</span></span>
* <span data-ttu-id="e78a1-118">`EngagementPageOverlay.cs`: hello наложения страницы должен добавлять hello Engagement reach дочерних tooits пользовательского интерфейса в приложении.</span><span class="sxs-lookup"><span data-stu-id="e78a1-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

