---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - службы"
description: "Руководства по устранению неполадок для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="7349e-103">Поиск и устранение неполадок в службе</span><span class="sxs-lookup"><span data-stu-id="7349e-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="7349e-104">Hello ниже приведены возможные проблемы, которые могут возникнуть с выполнением Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="7349e-105">Простои службы.</span><span class="sxs-lookup"><span data-stu-id="7349e-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="7349e-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="7349e-106">Issue</span></span>
* <span data-ttu-id="7349e-107">Проблемы, которые появляются toobe вызвано отключений служб Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="7349e-108">Причины</span><span class="sxs-lookup"><span data-stu-id="7349e-108">Causes</span></span>
* <span data-ttu-id="7349e-109">Проблемы, которые появляются toobe вызвано отключений служб Azure Mobile Engagement может быть вызвана несколько различных проблем:</span><span class="sxs-lookup"><span data-stu-id="7349e-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="7349e-110">Изолированной проблемы, которые первоначально отображаются системные tooall Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7349e-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="7349e-111">Известные проблемы, вызванные сбоем сервера (это не всегда отображается в состоянии сервера):</span><span class="sxs-lookup"><span data-stu-id="7349e-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="7349e-112">Планирование задержки, Targeting ошибки, проблемы с устранением эмблемы, Статистика остановить сбор принудительной перестанет работать, остановите работу API-интерфейса, новых приложений или пользователей, DNS ошибки и ошибки времени ожидания в невозможно hello пользовательского интерфейса, API или приложения на устройстве.</span><span class="sxs-lookup"><span data-stu-id="7349e-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="7349e-113">Простои, связанные с облаком [Состояние службы Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="7349e-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="7349e-114">Простои, связанные со службами push-уведомлений (PNS)</span><span class="sxs-lookup"><span data-stu-id="7349e-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="7349e-115">Перерывы в работе Магазина приложений</span><span class="sxs-lookup"><span data-stu-id="7349e-115">App Store Outages</span></span>

1) <span data-ttu-id="7349e-116">toosee tootest в случае системной проблемы hello можно протестировать hello же функции из другой</span><span class="sxs-lookup"><span data-stu-id="7349e-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="7349e-117">Встроенное приложение Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="7349e-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="7349e-118">Устройство для тестирования</span><span class="sxs-lookup"><span data-stu-id="7349e-118">Test device</span></span>
* <span data-ttu-id="7349e-119">Версия ОС устройства для тестирования</span><span class="sxs-lookup"><span data-stu-id="7349e-119">Test device OS version</span></span>
* <span data-ttu-id="7349e-120">Кампания</span><span class="sxs-lookup"><span data-stu-id="7349e-120">Campaign</span></span>
* <span data-ttu-id="7349e-121">Учетная запись администратора</span><span class="sxs-lookup"><span data-stu-id="7349e-121">Administrator user account</span></span>
* <span data-ttu-id="7349e-122">Браузер (IE, Firefox, Chrome и т. д.)</span><span class="sxs-lookup"><span data-stu-id="7349e-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="7349e-123">Компьютер</span><span class="sxs-lookup"><span data-stu-id="7349e-123">Computer</span></span>

2) <span data-ttu-id="7349e-124">tootest Если hello проблема касается только hello пользовательского интерфейса или hello API-Интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="7349e-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="7349e-125">Протестируйте hello hello Azure Mobile Engagement API и же функции из обоих hello пользовательского интерфейса Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="7349e-126">tootest hello проблемы в случае с сотовой сети:</span><span class="sxs-lookup"><span data-stu-id="7349e-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="7349e-127">Проверить при подключенных toohello в Интернет через Wi-Fi и при подключении через сеть 3G сотовых телефонов.</span><span class="sxs-lookup"><span data-stu-id="7349e-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="7349e-128">Убедитесь, что брандмауэр не блокирует любые hello Azure Mobile Engagement IP-адресов и портов.</span><span class="sxs-lookup"><span data-stu-id="7349e-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="7349e-129">tootest hello проблемы в случае с вашим устройством:</span><span class="sxs-lookup"><span data-stu-id="7349e-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="7349e-130">Проверьте, если устройство не может tooconnect tooAzure Mobile Engagement с другой Azure Mobile Engagement интегрированного приложения.</span><span class="sxs-lookup"><span data-stu-id="7349e-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="7349e-131">Проверьте, можно создать события, задания и сбои с телефона, можно увидеть в hello пользовательского интерфейса Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="7349e-132">Проверить при отправке push-уведомления из hello пользовательского интерфейса Azure Mobile Engagement tooyour устройство, основываясь на его идентификатор устройства.</span><span class="sxs-lookup"><span data-stu-id="7349e-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="7349e-133">tootest hello проблемы в случае с приложением:</span><span class="sxs-lookup"><span data-stu-id="7349e-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="7349e-134">Установите и протестируйте приложение, используя вместо физического устройства эмулятор:</span><span class="sxs-lookup"><span data-stu-id="7349e-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="7349e-135">tootest hello проблемы в случае с пользователем tooend обновления операционной системы устройства, которые требуют обновления tooresolve SDK:</span><span class="sxs-lookup"><span data-stu-id="7349e-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="7349e-136">Тестирование приложения на разных устройствах с различными версиями hello ОС.</span><span class="sxs-lookup"><span data-stu-id="7349e-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="7349e-137">Убедитесь, что вы используете самую последнюю версию пакета SDK для hello hello.</span><span class="sxs-lookup"><span data-stu-id="7349e-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="7349e-138">Проблемы, связанные с подключением и отображением неправильной информации.</span><span class="sxs-lookup"><span data-stu-id="7349e-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="7349e-139">Проблема</span><span class="sxs-lookup"><span data-stu-id="7349e-139">Issue</span></span>
* <span data-ttu-id="7349e-140">Проблемы при входе в hello пользовательского интерфейса Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="7349e-141">Ошибки соединения с hello Azure Mobile Engagement API элемента.</span><span class="sxs-lookup"><span data-stu-id="7349e-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="7349e-142">Проблемы с передачей через интерфейс API устройства hello теги сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="7349e-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="7349e-143">Проблемы со скачиванием журналов или экспортированных данных из Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="7349e-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="7349e-144">Неверные сведения, отображаемые в hello пользовательского интерфейса Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7349e-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="7349e-145">В журналах Служб мобильного взаимодействия Azure показана неправильная информация.</span><span class="sxs-lookup"><span data-stu-id="7349e-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="7349e-146">Причины</span><span class="sxs-lookup"><span data-stu-id="7349e-146">Causes</span></span>
* <span data-ttu-id="7349e-147">Убедитесь, что учетная запись имеет достаточные разрешения tooperform hello задачи.</span><span class="sxs-lookup"><span data-stu-id="7349e-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="7349e-148">Убедитесь, что этой проблеме hello не является изолированной tooone компьютера или в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="7349e-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="7349e-149">Убедитесь, что hello Azure Mobile Engagement службы имеет не отчет о простоях.</span><span class="sxs-lookup"><span data-stu-id="7349e-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="7349e-150">Убедитесь, что при создании файлов тегов информации о приложении соблюдены все следующие правила.</span><span class="sxs-lookup"><span data-stu-id="7349e-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="7349e-151">Используйте только hello кодировку UTF-8 (набора знаков ANSI hello не поддерживается).</span><span class="sxs-lookup"><span data-stu-id="7349e-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="7349e-152">Используйте запятую «,» как символ разделителя hello (служба запроса toorequest toochange hello .csv символ-разделитель можно открыть из запятая «,» tooanother символами, например точкой с запятой «;»).</span><span class="sxs-lookup"><span data-stu-id="7349e-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="7349e-153">Используйте только строчные буквы для логических значений true и false.</span><span class="sxs-lookup"><span data-stu-id="7349e-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="7349e-154">Используйте файл, меньше, чем hello максимальный размер файла 35 МБ.</span><span class="sxs-lookup"><span data-stu-id="7349e-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

