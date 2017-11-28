---
title: "aaaExploring HockeyApp данные в Azure Application Insights | Документы Microsoft"
description: "Анализ использования и производительности приложения Azure с помощью Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="f324f-103">Просмотр данных HockeyApp в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f324f-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="f324f-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello рекомендуется использовать платформу для отслеживания динамической приложений для настольных компьютеров и мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="f324f-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="f324f-105">От HockeyApp можно отправлять пользовательские и трассировки телеметрии toomonitor использования и упростить диагностику (в данных аварийного toogetting сложения).</span><span class="sxs-lookup"><span data-stu-id="f324f-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="f324f-106">Этот поток телеметрии можно запросить, используя hello мощные [Analytics](app-insights-analytics.md) функция [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f324f-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f324f-107">Кроме того, вы можете [экспорт пользовательских hello и телеметрии трассировки](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="f324f-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="f324f-108">tooenable их с функциями, можно настроить мост, который ретранслирует tooApplication HockeyApp пользовательские данные аналитики.</span><span class="sxs-lookup"><span data-stu-id="f324f-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="f324f-109">приложение Hello моста HockeyApp</span><span class="sxs-lookup"><span data-stu-id="f324f-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="f324f-110">HockeyApp моста приложения Hello является основной функцией hello, благодаря которой вы tooaccess ваши пользовательские HockeyApp и трассировки телеметрии в Application Insights через hello аналитика и непрерывный Экспорт функций.</span><span class="sxs-lookup"><span data-stu-id="f324f-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="f324f-111">Пользовательские и трассировки событий, собранных HockeyApp после создания hello hello HockeyApp мост приложения будут доступны из этих функций.</span><span class="sxs-lookup"><span data-stu-id="f324f-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="f324f-112">Давайте посмотрим, как tooset один из этих приложений моста.</span><span class="sxs-lookup"><span data-stu-id="f324f-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="f324f-113">В HockeyApp откройте параметры учетной записи и щелкните [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Маркеры API).</span><span class="sxs-lookup"><span data-stu-id="f324f-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="f324f-114">Создайте новый маркер или воспользуйтесь существующим.</span><span class="sxs-lookup"><span data-stu-id="f324f-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="f324f-115">минимальные права Hello требуется являются «только для чтения».</span><span class="sxs-lookup"><span data-stu-id="f324f-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="f324f-116">Сделайте копию hello API маркеров.</span><span class="sxs-lookup"><span data-stu-id="f324f-116">Take a copy of hello API token.</span></span>

![Получение маркера API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="f324f-118">Привет открыть портал Microsoft Azure и [создать ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f324f-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="f324f-119">Задайте тип приложения слишком «Приложение моста HockeyApp»:</span><span class="sxs-lookup"><span data-stu-id="f324f-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Новый ресурс Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="f324f-121">Не нужно tooset имя — это будет автоматически на основе имени HockeyApp hello.</span><span class="sxs-lookup"><span data-stu-id="f324f-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="f324f-122">отображаются поля моста HockeyApp Hello.</span><span class="sxs-lookup"><span data-stu-id="f324f-122">hello HockeyApp bridge fields appear.</span></span> 

![Мост: заполнение полей](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="f324f-124">Введите токен HockeyApp hello записанные ранее.</span><span class="sxs-lookup"><span data-stu-id="f324f-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="f324f-125">Это действие вносит hello «HockeyApp приложение» раскрывающееся меню в приложениях HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="f324f-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="f324f-126">Выберите hello один toouse и завершения hello оставшуюся часть поля hello.</span><span class="sxs-lookup"><span data-stu-id="f324f-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="f324f-127">Откройте новый ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="f324f-127">Open hello new resource.</span></span> 

<span data-ttu-id="f324f-128">Обратите внимание, что hello данных занимает некоторое время toostart потока.</span><span class="sxs-lookup"><span data-stu-id="f324f-128">Note that hello data takes a while toostart flowing.</span></span>

![Ресурс Application Insights: ожидание данных](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="f324f-130">Это все!</span><span class="sxs-lookup"><span data-stu-id="f324f-130">That’s it!</span></span> <span data-ttu-id="f324f-131">Пользовательские и трассировки данных, собранных в HockeyApp инструментированного приложения с этого момента теперь также является доступной tooyou в hello аналитика и непрерывный Экспорт функций Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f324f-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="f324f-132">Кратко рассмотрим каждый из эти компоненты теперь доступно tooyou.</span><span class="sxs-lookup"><span data-stu-id="f324f-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="f324f-133">Аналитика</span><span class="sxs-lookup"><span data-stu-id="f324f-133">Analytics</span></span>
<span data-ttu-id="f324f-134">Аналитика является мощным средством для нерегламентированных запросов данных, позволяя toodiagnose анализа телеметрии и быстро Осваивайте шаблоны и основных причин.</span><span class="sxs-lookup"><span data-stu-id="f324f-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Аналитика](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="f324f-136">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f324f-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="f324f-137">непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="f324f-137">Continuous export</span></span>
<span data-ttu-id="f324f-138">Непрерывный Экспорт позволяет tooexport данных в контейнер хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f324f-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="f324f-139">Это очень полезно, если необходимо tookeep данных дольше, чем срок хранения hello в настоящее время предлагаемых Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f324f-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="f324f-140">Можно хранить данные hello в хранилище больших двоичных объектов, его обработки в базе данных SQL или предпочтительный решения хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="f324f-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="f324f-141">Экспорт данных телеметрии из Application Insights</span><span class="sxs-lookup"><span data-stu-id="f324f-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="f324f-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f324f-142">Next steps</span></span>
* [<span data-ttu-id="f324f-143">Применить данные tooyour аналитика</span><span class="sxs-lookup"><span data-stu-id="f324f-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

