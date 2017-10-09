---
title: "Общие сведения о Azure IoT Suite aaaMicrosoft | Документы Microsoft"
description: "Общие сведения о том, как Azure IoT Suite доставляет Интернет вещей toocollect предварительно настроенных решений, анализ и хранения данных, предоставляют визуализацию и интеграцию с другими системами."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="1fb3f-103">Общие сведения о наборе Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="1fb3f-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="1fb3f-104">Hello Azure Интернета вещей (IoT) служб предоставляют широкий спектр возможностей.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="1fb3f-105">Это службы корпоративного уровня, которые обеспечивают:</span><span class="sxs-lookup"><span data-stu-id="1fb3f-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="1fb3f-106">сбор данных с устройств;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-106">Collect data from devices</span></span>
* <span data-ttu-id="1fb3f-107">анализ движения потоков данных;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="1fb3f-108">хранение больших наборов данных и создание запросов к ним;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-108">Store and query large data sets</span></span>
* <span data-ttu-id="1fb3f-109">визуализацию данных, получаемых в реальном времени, и архивных данных;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="1fb3f-110">интеграцию с системами операционных отделов организации.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="1fb3f-111">управление устройствами.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-111">Manage your devices</span></span>

<span data-ttu-id="1fb3f-112">toodeliver эти возможности Azure IoT Suite вместе пакеты несколько служб Azure с пользовательскими расширениями как *предварительно настроенных решений*.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="1fb3f-113">Эти заранее настроенных решений являются базовой реализацией распространенные шаблоны решения IoT, сократить время hello tooreduce принимать toodeliver вашего решения IoT.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="1fb3f-114">С помощью hello [пакеты средств разработки программного обеспечения IoT][lnk-sdks], можно настроить и расширить эти решения toomeet требованиями.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="1fb3f-115">Эти решения также можно использовать как примеры и шаблоны при разработке новых решений IoT.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="1fb3f-116">Hello следующие видеоматериалы содержат введение tooAzure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="1fb3f-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="1fb3f-117">Службы Azure IoT в наборе Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="1fb3f-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="1fb3f-118">Hello предварительно настроенных решений обычно используют hello следующие службы:</span><span class="sxs-lookup"><span data-stu-id="1fb3f-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="1fb3f-119">Основные tooAzure IoT Suite — hello [центр IoT Azure] [ lnk-iot-hub] службы.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="1fb3f-120">Эта служба предоставляет hello устройства в облако и возможности обмена сообщениями облака на устройство и действует как шлюз toohello hello облака и других ключевых служб IoT Suite hello.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="1fb3f-121">Hello службы позволяет tooreceive сообщений из устройства в масштабе, а также отправки команд tooyour устройств.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="1fb3f-122">Hello служба также позволяет слишком[управления устройствами][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="1fb3f-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="1fb3f-123">Например можно настроить, перезагрузить или восстановить заводские на один или несколько концентратора toohello подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="1fb3f-124">[Azure Stream Analytics][lnk-asa] обеспечивает оперативный анализ данных.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="1fb3f-125">IoT Suite использует службы tooprocess входящие данные телеметрии, выполнить агрегирование и обнаружения событий.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="1fb3f-126">Hello предварительно настроенных решений также использовать поток analytics tooprocess информационные сообщения, содержащие данные, например ответы метаданных или команды с устройств.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="1fb3f-127">Hello решения используют сообщения hello tooprocess Stream Analytics с устройств и доставка этих сообщений tooother служб.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="1fb3f-128">[Хранилище Azure] [ lnk-azure-storage] и [Azure Cosmos DB] [ lnk-document-db] предоставляют возможности хранения данных hello.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="1fb3f-129">Hello предварительно настроенного решения используют телеметрии toostore хранилища больших двоичных объектов и toomake его доступным для анализа.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="1fb3f-130">Hello решения с помощью Cosmos DB toostore устройства метаданных и предоставляют возможности управления устройствами hello hello решений.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="1fb3f-131">[Azure веб-приложений] [ lnk-web-apps] и [Microsoft Power BI] [ lnk-power-bi] предоставляют возможности визуализации данных hello.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="1fb3f-132">гибкость Hello Power BI позволяет tooquickly построения интерактивных панелей мониторинга, использующие данные IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="1fb3f-133">Обзор архитектуры hello стандартного решения IoT см. в разделе [Microsoft Azure и hello Интернета вещей (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="1fb3f-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="1fb3f-134">предварительно настроенные решения</span><span class="sxs-lookup"><span data-stu-id="1fb3f-134">Preconfigured solutions</span></span>

<span data-ttu-id="1fb3f-135">IoT Suite включает в себя предварительно настроенных решений, включите tooquickly вам начать работу с и tooexplore hello стандартных IoT сценариев, таких как:</span><span class="sxs-lookup"><span data-stu-id="1fb3f-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="1fb3f-136">удаленный мониторинг;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-136">Remote monitoring</span></span>
* <span data-ttu-id="1fb3f-137">диагностическое обслуживание;</span><span class="sxs-lookup"><span data-stu-id="1fb3f-137">Predictive maintenance</span></span>
* <span data-ttu-id="1fb3f-138">подключенная фабрика.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-138">Connected factory</span></span>

<span data-ttu-id="1fb3f-139">Можно развернуть эти решения tooyour подписки Azure и затем запустите сценарий IoT завершения, начала до конца.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fb3f-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1fb3f-140">Next steps</span></span>

<span data-ttu-id="1fb3f-141">Теперь, когда у вас есть общие сведения о возможностях IoT Suite и каковы ее основные компоненты, Дополнительные сведения о решениях hello предварительно настроен в IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="1fb3f-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="1fb3f-142">Дополнительные сведения см. в разделе [Каковы hello Azure IoT предварительно настроенных решений?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="1fb3f-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
