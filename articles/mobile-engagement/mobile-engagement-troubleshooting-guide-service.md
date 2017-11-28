---
title: "Руководство по устранению неполадок в Службах мобильного взаимодействия Azure — Служба"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="58eac-103">Поиск и устранение неполадок в службе</span><span class="sxs-lookup"><span data-stu-id="58eac-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="58eac-104">Ниже представлены возможные проблемы в работе Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="58eac-105">Простои службы.</span><span class="sxs-lookup"><span data-stu-id="58eac-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="58eac-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="58eac-106">Issue</span></span>
* <span data-ttu-id="58eac-107">Проблемы, которые предположительно связаны с простоями Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="58eac-108">Причины</span><span class="sxs-lookup"><span data-stu-id="58eac-108">Causes</span></span>
* <span data-ttu-id="58eac-109">Проблемы, которые предположительно связаны с простоями Служб мобильного взаимодействия Azure, могут возникать по таким причинам:</span><span class="sxs-lookup"><span data-stu-id="58eac-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="58eac-110">Изолированные проблемы, которые изначально носят системный характер для всех компонентов Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="58eac-111">Известные проблемы, вызванные сбоем сервера (это не всегда отображается в состоянии сервера):</span><span class="sxs-lookup"><span data-stu-id="58eac-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="58eac-112">Задержки планирования, ошибки определения цели, проблемы обновления индикаторов событий, прекращение сбора статистических данных, прекращение отправки push-уведомлений, прекращение работы API, невозможность создать новые приложения или новых пользователей, ошибки DNS и ошибки времени ожидания в пользовательском интерфейсе, API или приложениях на устройстве.</span><span class="sxs-lookup"><span data-stu-id="58eac-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="58eac-113">Простои, связанные с облаком [Состояние службы Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="58eac-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="58eac-114">Простои, связанные со службами push-уведомлений (PNS)</span><span class="sxs-lookup"><span data-stu-id="58eac-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="58eac-115">Перерывы в работе Магазина приложений</span><span class="sxs-lookup"><span data-stu-id="58eac-115">App Store Outages</span></span>

1) <span data-ttu-id="58eac-116">Чтобы проверить и узнать, является ли проблема системной, вы можете протестировать одну и ту же функцию с помощью разных объектов:</span><span class="sxs-lookup"><span data-stu-id="58eac-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="58eac-117">Встроенное приложение Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="58eac-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="58eac-118">Устройство для тестирования</span><span class="sxs-lookup"><span data-stu-id="58eac-118">Test device</span></span>
* <span data-ttu-id="58eac-119">Версия ОС устройства для тестирования</span><span class="sxs-lookup"><span data-stu-id="58eac-119">Test device OS version</span></span>
* <span data-ttu-id="58eac-120">Кампания</span><span class="sxs-lookup"><span data-stu-id="58eac-120">Campaign</span></span>
* <span data-ttu-id="58eac-121">Учетная запись администратора</span><span class="sxs-lookup"><span data-stu-id="58eac-121">Administrator user account</span></span>
* <span data-ttu-id="58eac-122">Браузер (IE, Firefox, Chrome и т. д.)</span><span class="sxs-lookup"><span data-stu-id="58eac-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="58eac-123">Компьютер</span><span class="sxs-lookup"><span data-stu-id="58eac-123">Computer</span></span>

2) <span data-ttu-id="58eac-124">Чтобы проверить, влияет ли проблема только на пользовательский интерфейс или API:</span><span class="sxs-lookup"><span data-stu-id="58eac-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="58eac-125">протестируйте ту же функцию из пользовательского интерфейса Служб мобильного взаимодействия Azure и API Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="58eac-126">Чтобы проверить, заключается ли проблема в сети мобильного телефона:</span><span class="sxs-lookup"><span data-stu-id="58eac-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="58eac-127">Протестируйте во время подключения к Интернету через Wi-Fi и во время подключения по сети 3G для мобильного телефона.</span><span class="sxs-lookup"><span data-stu-id="58eac-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="58eac-128">Убедитесь, что брандмауэр не блокирует ни один из IP-адресов и портов Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="58eac-129">Чтобы проверить, заключается ли проблема в устройстве:</span><span class="sxs-lookup"><span data-stu-id="58eac-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="58eac-130">Проверьте возможность подключения к Службам мобильного взаимодействия Azure с помощью другого встроенного приложения Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="58eac-131">Проверьте, чтобы в пользовательском интерфейсе Служб мобильного взаимодействия Azure отображались созданные события, задания и сбои телефона.</span><span class="sxs-lookup"><span data-stu-id="58eac-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="58eac-132">Проверьте, можете ли вы на основании идентификатора устройства отправлять извещающие уведомления из пользовательского интерфейса Служб мобильного взаимодействия Azure на свое устройство.</span><span class="sxs-lookup"><span data-stu-id="58eac-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="58eac-133">Чтобы проверить, заключается ли проблема в приложении:</span><span class="sxs-lookup"><span data-stu-id="58eac-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="58eac-134">Установите и протестируйте приложение, используя вместо физического устройства эмулятор:</span><span class="sxs-lookup"><span data-stu-id="58eac-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="58eac-135">Чтобы проверить, касается ли проблема обновления операционных систем на устройствах конечных пользователей, в случае чего требуется обновить пакет SDK для устранения проблемы:</span><span class="sxs-lookup"><span data-stu-id="58eac-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="58eac-136">Протестируйте приложение на разных устройствах с различными версиями операционной системы.</span><span class="sxs-lookup"><span data-stu-id="58eac-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="58eac-137">Убедитесь, что вы используете самую последнюю версию пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="58eac-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="58eac-138">Проблемы, связанные с подключением и отображением неправильной информации.</span><span class="sxs-lookup"><span data-stu-id="58eac-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="58eac-139">Проблема</span><span class="sxs-lookup"><span data-stu-id="58eac-139">Issue</span></span>
* <span data-ttu-id="58eac-140">Проблемы со входом в пользовательский интерфейс Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="58eac-141">Ошибки подключения к API Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="58eac-142">Проблемы загрузки тегов информации о приложении через API устройства.</span><span class="sxs-lookup"><span data-stu-id="58eac-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="58eac-143">Проблемы со скачиванием журналов или экспортированных данных из Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="58eac-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="58eac-144">В пользовательском интерфейсе Служб мобильного взаимодействия Azure показана неправильная информация.</span><span class="sxs-lookup"><span data-stu-id="58eac-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="58eac-145">В журналах Служб мобильного взаимодействия Azure показана неправильная информация.</span><span class="sxs-lookup"><span data-stu-id="58eac-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="58eac-146">Причины</span><span class="sxs-lookup"><span data-stu-id="58eac-146">Causes</span></span>
* <span data-ttu-id="58eac-147">Убедитесь, что у учетной записи достаточно разрешений для выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="58eac-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="58eac-148">Убедитесь, что проблема не изолирована на одном компьютере или в вашей локальной сети.</span><span class="sxs-lookup"><span data-stu-id="58eac-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="58eac-149">Убедитесь, что Службы мобильного взаимодействия Azure не сообщали о простоях.</span><span class="sxs-lookup"><span data-stu-id="58eac-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="58eac-150">Убедитесь, что при создании файлов тегов информации о приложении соблюдены все следующие правила.</span><span class="sxs-lookup"><span data-stu-id="58eac-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="58eac-151">Используйте только кодировку UTF8 (кодировка ANSI не поддерживается).</span><span class="sxs-lookup"><span data-stu-id="58eac-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="58eac-152">Используйте запятую «,» как знак разделения (можно отправить запрос на обслуживание, чтобы запросить изменение знака разделения запятой «,» в CSV-файле на другой символ, например на точку с запятой «;»).</span><span class="sxs-lookup"><span data-stu-id="58eac-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="58eac-153">Используйте только строчные буквы для логических значений true и false.</span><span class="sxs-lookup"><span data-stu-id="58eac-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="58eac-154">Используйте файл, размер которого меньше, чем максимальный размер файла — 35 МБ.</span><span class="sxs-lookup"><span data-stu-id="58eac-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

