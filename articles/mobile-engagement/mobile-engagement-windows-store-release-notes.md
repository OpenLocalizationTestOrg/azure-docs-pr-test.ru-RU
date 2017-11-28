---
title: "aaaAzure Mobile Engagement универсальных приложений SDK заметки о выпуске Windows | Документы Microsoft"
description: "Заметки о выпуске SDK для универсальных приложений Windows для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: de938ce5-93d5-4218-9e33-10eef102bd61
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 280bd064888f69a77d6fe0c31eafd98a0bbf724e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-release-notes"></a><span data-ttu-id="aff11-103">Заметки о выпуске пакета SDK для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="aff11-103">Windows Universal Apps SDK Release Notes</span></span>
## <a name="341-11032016"></a><span data-ttu-id="aff11-104">3.4.1 (03.11.2016)</span><span class="sxs-lookup"><span data-stu-id="aff11-104">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="aff11-105">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="aff11-105">Stability improvements.</span></span>

## <a name="340-04192016"></a><span data-ttu-id="aff11-106">3.4.0 (19.04.2016)</span><span class="sxs-lookup"><span data-stu-id="aff11-106">3.4.0 (04/19/2016)</span></span>
* <span data-ttu-id="aff11-107">Улучшения наложения Reach.</span><span class="sxs-lookup"><span data-stu-id="aff11-107">Reach overlay improvements.</span></span>
* <span data-ttu-id="aff11-108">Добавлены журналы консоли tooenable/disable фильтр «TestLogLevel» API, генерируемой hello SDK.</span><span class="sxs-lookup"><span data-stu-id="aff11-108">Added "TestLogLevel" API tooenable/disable/filter console logs emitted by hello SDK.</span></span>
* <span data-ttu-id="aff11-109">Запустите основных действия в уведомления, предназначенных для hello первое действие, не отображается в приложении.</span><span class="sxs-lookup"><span data-stu-id="aff11-109">Fixed in-activity notifications targeting hello first activity not displayed on App start.</span></span>

## <a name="331-02182016"></a><span data-ttu-id="aff11-110">3.3.1 (18.02.2016)</span><span class="sxs-lookup"><span data-stu-id="aff11-110">3.3.1 (02/18/2016)</span></span>
* <span data-ttu-id="aff11-111">Устранены конфликты между HTML-содержимым веб-объявления и HTML-страницей пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="aff11-111">Fixed conflicts between web announcement's HTML content and SDK's HTML page.</span></span>
* <span data-ttu-id="aff11-112">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="aff11-112">Stability improvements.</span></span>

## <a name="330-01222016"></a><span data-ttu-id="aff11-113">3.3.0 (22.01.2016 г.)</span><span class="sxs-lookup"><span data-stu-id="aff11-113">3.3.0 (01/22/2016)</span></span>
* <span data-ttu-id="aff11-114">Устранены сбои форматирования в приложениях UWP, работающих в режиме выпуска.</span><span class="sxs-lookup"><span data-stu-id="aff11-114">Fixed crash formatting on UWP apps running in release mode.</span></span>
* <span data-ttu-id="aff11-115">Исправлены однопиксельные поля в уведомлениях для приложений UWP 8.1.</span><span class="sxs-lookup"><span data-stu-id="aff11-115">Fixed 1px margin on notifications for Universal 8.1 apps.</span></span>
* <span data-ttu-id="aff11-116">По URL-адресам действия доступны ms-appx и ms-appdata.</span><span class="sxs-lookup"><span data-stu-id="aff11-116">ms-appx and ms-appdata schemes available on action urls.</span></span>
* <span data-ttu-id="aff11-117">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="aff11-117">Stability improvements.</span></span>

## <a name="320-11202015"></a><span data-ttu-id="aff11-118">3.2.0 (11/20/2015)</span><span class="sxs-lookup"><span data-stu-id="aff11-118">3.2.0 (11/20/2015)</span></span>
* <span data-ttu-id="aff11-119">Добавлена поддержка универсальных приложений для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="aff11-119">Added support for Windows 10 Universal Windows Platform applications.</span></span>
* <span data-ttu-id="aff11-120">Канал добавленных извещающих функция toofix канала конфликтов (теперь совместимы с концентраторами уведомлений Azure) для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="aff11-120">Added push channel sharing feature toofix channel conflicts (now compatible with Azure Notification Hubs).</span></span>
* <span data-ttu-id="aff11-121">Фиксированный сбоя при запросе hello идентификатор устройства сразу после инициализации hello.</span><span class="sxs-lookup"><span data-stu-id="aff11-121">Fixed crash while requesting hello device id just after hello initialization.</span></span>
* <span data-ttu-id="aff11-122">Улучшены журналы консоли.</span><span class="sxs-lookup"><span data-stu-id="aff11-122">Console logs improvements.</span></span>
* <span data-ttu-id="aff11-123">Исправлена проблема сбоев при анализе некоторых необработанных исключений.</span><span class="sxs-lookup"><span data-stu-id="aff11-123">Fixed crash while parsing some unhandled exceptions.</span></span>

## <a name="310-05212015"></a><span data-ttu-id="aff11-124">3.1.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="aff11-124">3.1.0 (05/21/2015)</span></span>
* <span data-ttu-id="aff11-125">ИД устройства Mobile Engagement Hello теперь основан на GUID, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="aff11-125">hello Mobile Engagement device id is now based on a GUID generated at installation time.</span></span>

## <a name="301-04292015"></a><span data-ttu-id="aff11-126">3.0.1 (29.04.2015)</span><span class="sxs-lookup"><span data-stu-id="aff11-126">3.0.1 (04/29/2015)</span></span>
* <span data-ttu-id="aff11-127">Исправлена ошибка влияния на инициализации SDK hello в некоторых приложениях Windows Phone WinRT.</span><span class="sxs-lookup"><span data-stu-id="aff11-127">Fixed a bug affecting hello SDK initialization on some Windows Phone WinRT apps.</span></span>

## <a name="300-04032015"></a><span data-ttu-id="aff11-128">3.0.0 (03.04.2015)</span><span class="sxs-lookup"><span data-stu-id="aff11-128">3.0.0 (04/03/2015)</span></span>
* <span data-ttu-id="aff11-129">Общие сведения о hello пакет SDK Mobile Engagement для универсального приложения (Windows и Windows Phone WinRT).</span><span class="sxs-lookup"><span data-stu-id="aff11-129">Introducing hello Mobile Engagement SDK for Universal App (Windows and Windows Phone WinRT).</span></span>
* <span data-ttu-id="aff11-130">Обновлен стандартный значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="aff11-130">Default notification icon updated.</span></span>
* <span data-ttu-id="aff11-131">При щелчке уведомления отправляется отклик на действие с системным уведомлением.</span><span class="sxs-lookup"><span data-stu-id="aff11-131">Send back system notification action feedback when a notification is clicked.</span></span>
* <span data-ttu-id="aff11-132">Исправлено системное уведомление, которое иногда воспроизводилось в приложении после щелчка.</span><span class="sxs-lookup"><span data-stu-id="aff11-132">Fixed system notification which is sometimes replayed in-app after being clicked.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="aff11-133">Версия 2.0.0 (17.02.2015)</span><span class="sxs-lookup"><span data-stu-id="aff11-133">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="aff11-134">Первый выпуск Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="aff11-134">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="aff11-135">Конфигурация appId/sdkKey заменена конфигурацией строки подключения.</span><span class="sxs-lookup"><span data-stu-id="aff11-135">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="aff11-136">Улучшения безопасности.</span><span class="sxs-lookup"><span data-stu-id="aff11-136">Security improvements.</span></span>

