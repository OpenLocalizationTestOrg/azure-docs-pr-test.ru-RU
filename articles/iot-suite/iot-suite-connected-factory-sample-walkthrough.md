---
title: "Пошаговое руководство по решениям Azure IoT Suite фабрики aaaConnected | Документы Microsoft"
description: "Описание hello Azure IoT предварительно настроенное решение подключен фабрики и его архитектуры."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="3ab95-103">Пошаговое руководство по работе с предварительно настроенным решением подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="3ab95-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="3ab95-104">Hello IoT Suite подключен фабрики [предварительно настроенное решение] [ lnk-preconfigured-solutions] представляет собой реализацию решения промышленным начала до конца:</span><span class="sxs-lookup"><span data-stu-id="3ab95-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="3ab95-105">Подключается tooboth имитируемые промышленных устройств работает OPC UA серверов в производственных линиях имитацию фабрики и реального устройства server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="3ab95-106">Дополнительные сведения о OPC UA см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3ab95-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="3ab95-107">Показывает оперативные ключевые показатели эффективности и общую эффективность оборудования этих устройств и производственных линий.</span><span class="sxs-lookup"><span data-stu-id="3ab95-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="3ab95-108">Демонстрирует, как приложение на основе облака может быть используется toointeract с OPC UA серверных систем.</span><span class="sxs-lookup"><span data-stu-id="3ab95-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="3ab95-109">Позволяет вам tooconnect устройства server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="3ab95-110">Позволяет toobrowse и изменения hello OPC UA данные сервера.</span><span class="sxs-lookup"><span data-stu-id="3ab95-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="3ab95-111">Интегрируется с hello tooprovide службы аналитики ряда времени Azure (TSI) пользовательских представлений данных hello серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="3ab95-112">Hello решения можно использовать в качестве отправной точки для свою собственную реализацию и [настроить] [ lnk-customize] его toomeet требованиями бизнеса.</span><span class="sxs-lookup"><span data-stu-id="3ab95-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="3ab95-113">В этой статье поможет выполнить некоторые ключевые элементы hello hello подключен фабрики решения tooenable toounderstand ее работы.</span><span class="sxs-lookup"><span data-stu-id="3ab95-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="3ab95-114">Эти знания помогут вам:</span><span class="sxs-lookup"><span data-stu-id="3ab95-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="3ab95-115">Устранение неполадок в решении hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="3ab95-116">Планирование как toocustomize toohello решения toomeet конкретным требованиям.</span><span class="sxs-lookup"><span data-stu-id="3ab95-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="3ab95-117">спроектировать собственное решение IoT, использующее службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3ab95-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="3ab95-118">Дополнительные сведения см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3ab95-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="3ab95-119">Логическая архитектура</span><span class="sxs-lookup"><span data-stu-id="3ab95-119">Logical architecture</span></span>

<span data-ttu-id="3ab95-120">Следующая схема Hello представлен краткий обзор hello логические компоненты hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="3ab95-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Логическая архитектура подключенной фабрики][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="3ab95-122">Модели связи</span><span class="sxs-lookup"><span data-stu-id="3ab95-122">Communication patterns</span></span>

<span data-ttu-id="3ab95-123">Hello решение использует hello [спецификации OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT данные телеметрии OPC UA концентратора в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="3ab95-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="3ab95-124">Hello решение использует hello [издатель OPC](https://github.com/Azure/iot-edge-opc-publisher) модуль IoT Edge для этой цели.</span><span class="sxs-lookup"><span data-stu-id="3ab95-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="3ab95-125">Hello решение также включает клиент OPC UA интегрированы в веб-приложении, смогут устанавливать соединения с локальными серверами OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="3ab95-126">Hello клиент использует [обратного прокси-сервера](https://wikipedia.org/wiki/Reverse_proxy) и получает справки из центра IoT toomake hello соединения без необходимости открыть порты в брандмауэре hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="3ab95-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="3ab95-127">Эта модель связи называется [взаимодействием с поддержкой службы](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="3ab95-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="3ab95-128">Hello решение использует hello [прокси OPC](https://github.com/Azure/iot-edge-opc-proxy/) модуль IoT Edge для этой цели.</span><span class="sxs-lookup"><span data-stu-id="3ab95-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="3ab95-129">Моделирование</span><span class="sxs-lookup"><span data-stu-id="3ab95-129">Simulation</span></span>

<span data-ttu-id="3ab95-130">Hello имитировать станции и имитировать hello производством, систем (MES) составляют производственной линии.</span><span class="sxs-lookup"><span data-stu-id="3ab95-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="3ab95-131">Hello имитации устройства и hello OPC издателя модуль на основе hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] опубликованное hello OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="3ab95-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="3ab95-132">Hello OPC прокси-сервер и издатель OPC реализованы в виде модулей на основе [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="3ab95-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="3ab95-133">К каждой виртуальной производственной линии подключен отдельный шлюз.</span><span class="sxs-lookup"><span data-stu-id="3ab95-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="3ab95-134">Все виртуальные компоненты работают в контейнерах Docker, размещенных на виртуальной машине Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="3ab95-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="3ab95-135">Моделирование Hello является настроенным toorun восемь имитации рабочей строки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ab95-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="3ab95-136">Виртуальная производственная линия</span><span class="sxs-lookup"><span data-stu-id="3ab95-136">Simulated production line</span></span>

<span data-ttu-id="3ab95-137">Производственная линия изготавливает детали.</span><span class="sxs-lookup"><span data-stu-id="3ab95-137">A production line manufactures parts.</span></span> <span data-ttu-id="3ab95-138">Она состоит из различных станций: станция сборки, станция тестирования и станция упаковки.</span><span class="sxs-lookup"><span data-stu-id="3ab95-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="3ab95-139">Моделирование Hello запускается и обновляет данные hello, доступных через узлы OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="3ab95-140">Все строки имитации рабочей станции оркестрация hello MES через OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="3ab95-141">Виртуальная система управления производственными процессами</span><span class="sxs-lookup"><span data-stu-id="3ab95-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="3ab95-142">Hello MES отслеживает каждой станции в hello рабочей строки до изменения состояния станции toodetect OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3ab95-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="3ab95-143">Он вызывает методы toocontrol hello станции OPC UA и передает продукта из одной станции toohello далее вплоть до его завершения.</span><span class="sxs-lookup"><span data-stu-id="3ab95-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="3ab95-144">Модуль издателя OPC шлюза</span><span class="sxs-lookup"><span data-stu-id="3ab95-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="3ab95-145">Модуль издателя OPC подключается toohello станции OPC UA серверов и подписывается toohello OPC узлы toobe публикации.</span><span class="sxs-lookup"><span data-stu-id="3ab95-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="3ab95-146">модуль Hello hello узел данные преобразуются в формат JSON, шифрует его и отправляет tooIoT концентратора как сообщения OPC UA Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="3ab95-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="3ab95-147">модуль издателя OPC Hello только требует исходящих https-порт (443) и может работать с существующие инфраструктуры предприятия.</span><span class="sxs-lookup"><span data-stu-id="3ab95-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="3ab95-148">Модуль прокси OPC шлюза</span><span class="sxs-lookup"><span data-stu-id="3ab95-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="3ab95-149">Hello модуль прокси-сервера шлюза OPC UA туннели двоичные сообщения управления OPC UA и требуется только порт исходящей https (443).</span><span class="sxs-lookup"><span data-stu-id="3ab95-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="3ab95-150">Он может работать с существующей инфраструктурой предприятия, в том числе с веб-прокси.</span><span class="sxs-lookup"><span data-stu-id="3ab95-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="3ab95-151">Он использует устройства IoT Hub методы tootransfer пакетный TCP/IP данные на уровне приложения hello и таким образом гарантирует доверия конечной точки, шифрование данных и целостности с помощью SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3ab95-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="3ab95-152">Hello OPC UA двоичный протокол с ретрансляцией через прокси-сервер hello сам использует агент пользователя проверку подлинности и шифрование.</span><span class="sxs-lookup"><span data-stu-id="3ab95-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="3ab95-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="3ab95-153">Azure Time Series Insights</span></span>

<span data-ttu-id="3ab95-154">Hello шлюза OPC издателя модуль подписывается tooOPC UA сервера узлов toodetect изменения в значениях данных hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="3ab95-155">Если обнаружено изменение данных в одном из узлов hello, этот модуль отправляет сообщения tooAzure центр IoT.</span><span class="sxs-lookup"><span data-stu-id="3ab95-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="3ab95-156">Центр IoT предоставляет tooAzure источника событий TSI.</span><span class="sxs-lookup"><span data-stu-id="3ab95-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="3ab95-157">TSI хранит данные в течение 30 дней, в зависимости от отметки времени присоединенного toohello сообщений.</span><span class="sxs-lookup"><span data-stu-id="3ab95-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="3ab95-158">Эти данные включают:</span><span class="sxs-lookup"><span data-stu-id="3ab95-158">This data includes:</span></span>

* <span data-ttu-id="3ab95-159">OPC UA ApplicationUri;</span><span class="sxs-lookup"><span data-stu-id="3ab95-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="3ab95-160">OPC UA NodeId;</span><span class="sxs-lookup"><span data-stu-id="3ab95-160">OPC UA NodeId</span></span>
* <span data-ttu-id="3ab95-161">Значение узла hello</span><span class="sxs-lookup"><span data-stu-id="3ab95-161">Value of hello node</span></span>
* <span data-ttu-id="3ab95-162">метка времени источника;</span><span class="sxs-lookup"><span data-stu-id="3ab95-162">Source timestamp</span></span>
* <span data-ttu-id="3ab95-163">OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="3ab95-163">OPC UA DisplayName</span></span>

<span data-ttu-id="3ab95-164">В настоящее время TSI не позволяет клиентам toocustomize продолжительность ими данные hello tookeep для.</span><span class="sxs-lookup"><span data-stu-id="3ab95-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="3ab95-165">TSI отправляет запрос к данным узла с помощью SearchSpan (Time.From, Time.To) и выполняет вычисление на основе значений OPC UA ApplicationUri, OPC UA NodeId или OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="3ab95-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="3ab95-166">данные hello tooretrieve для hello OEE и ключевого показателя Эффективности датчики и диаграммы ряда времени hello, данные агрегируются по число событий, Sum, Avg, Min и Max.</span><span class="sxs-lookup"><span data-stu-id="3ab95-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="3ab95-167">Hello временных рядов создаются с помощью другого процесса.</span><span class="sxs-lookup"><span data-stu-id="3ab95-167">hello time series are built using a different process.</span></span> <span data-ttu-id="3ab95-168">OEE и ключевые показатели эффективности, вычисленный на основе базовых данных станции и подниматься для топологии hello (производственных линиях, фабрики, enterprise) в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="3ab95-169">Кроме того каждый раз, когда отображается timespan готов временных рядов для топологии OEE и ключевого показателя Эффективности вычисляется в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="3ab95-170">Например представление дня hello обновляется каждый полный час.</span><span class="sxs-lookup"><span data-stu-id="3ab95-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="3ab95-171">данные узла представления ряда времени Hello поступающие непосредственно из TSI, с помощью агрегата для timespan.</span><span class="sxs-lookup"><span data-stu-id="3ab95-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="3ab95-172">Центр IoT</span><span class="sxs-lookup"><span data-stu-id="3ab95-172">IoT Hub</span></span>
<span data-ttu-id="3ab95-173">Hello [центр IoT] [ lnk-IoT Hub] получает данные, отправляемые hello OPC издателя модуля в облаке hello и делает ее доступной toohello Azure TSI службы.</span><span class="sxs-lookup"><span data-stu-id="3ab95-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="3ab95-174">Hello центр IoT в решении hello также:</span><span class="sxs-lookup"><span data-stu-id="3ab95-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="3ab95-175">Хранит в реестре удостоверений, сохраняет hello идентификаторы для всех модуля OPC издателя и всех модулей OPC прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3ab95-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="3ab95-176">Используется как канал транспорта для двусторонней связи из hello OPC модуль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3ab95-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="3ab95-177">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="3ab95-177">Azure Storage</span></span>
<span data-ttu-id="3ab95-178">Hello решение использует хранилище больших двоичных объектов как дискового хранилища для данных развертывания виртуальной Машины и toostore hello.</span><span class="sxs-lookup"><span data-stu-id="3ab95-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="3ab95-179">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="3ab95-179">Web app</span></span>
<span data-ttu-id="3ab95-180">веб-приложение Hello развернут как часть hello предварительно настроенное решение состоит из встроенный клиент OPC UA, обработки оповещений и визуализации данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3ab95-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ab95-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ab95-181">Next steps</span></span>

<span data-ttu-id="3ab95-182">Вы можете продолжить, Приступая к работе с IoT Suite, считывая hello следующих статей.</span><span class="sxs-lookup"><span data-stu-id="3ab95-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="3ab95-183">[Разрешения на сайт azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="3ab95-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="3ab95-184">Развертывание шлюза в Windows или Linux для hello подключен фабрики предварительно настроенных решений</span><span class="sxs-lookup"><span data-stu-id="3ab95-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
