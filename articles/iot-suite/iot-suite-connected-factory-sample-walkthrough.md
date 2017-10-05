---
title: "Пошаговое руководство по работе с решением подключенной фабрики Azure IoT Suite | Документация Майкрософт"
description: "Описание предварительно настроенного решения подключенной фабрики Azure IoT и его архитектура."
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
ms.openlocfilehash: 517e908a744734139ed0aeee314a4f3b9eda86cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="cdb34-103">Пошаговое руководство по работе с предварительно настроенным решением подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="cdb34-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="cdb34-104">[Предварительно настроенное решение][lnk-preconfigured-solutions] подключенной фабрики IoT Suite представляет собой законченную реализацию отраслевого решения, которое умеет выполнять следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="cdb34-104">The IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="cdb34-105">Подключается к виртуальным отраслевым устройствам под управлением серверов OPC UA на производственных линиях виртуальной фабрики и к физическим устройствам сервера OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="cdb34-106">Дополнительные сведения об OPC UA см. в статье [Часто задаваемые вопросы о предварительно настроенном решении для подключенной фабрики IoT Suite](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="cdb34-106">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="cdb34-107">Показывает оперативные ключевые показатели эффективности и общую эффективность оборудования этих устройств и производственных линий.</span><span class="sxs-lookup"><span data-stu-id="cdb34-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="cdb34-108">Демонстрирует, как можно использовать облачное приложение для взаимодействия с серверными системами OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="cdb34-109">Позволяет подключать собственные устройства под управлением сервера OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="cdb34-110">Позволяет просматривать и изменять данные сервера OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="cdb34-111">Интегрируется со службой Azure Time Series Insights (TSI) для предоставления пользовательских представлений данных с серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="cdb34-112">Его можно использовать в качестве отправной точки для собственной реализации и [настроить][lnk-customize] в соответствии с потребностями конкретной организации.</span><span class="sxs-lookup"><span data-stu-id="cdb34-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="cdb34-113">В этой статье рассматриваются некоторые основные компоненты решения подключенной фабрики, которые помогут вам представить, как оно работает.</span><span class="sxs-lookup"><span data-stu-id="cdb34-113">This article walks you through some of the key elements of the connected factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="cdb34-114">Эти знания помогут вам:</span><span class="sxs-lookup"><span data-stu-id="cdb34-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="cdb34-115">устранить проблемы, возникшие с решением;</span><span class="sxs-lookup"><span data-stu-id="cdb34-115">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="cdb34-116">спланировать настройку решения в соответствии с определенными требованиями;</span><span class="sxs-lookup"><span data-stu-id="cdb34-116">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="cdb34-117">спроектировать собственное решение IoT, использующее службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb34-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="cdb34-118">Дополнительные сведения см. в разделе с [часто задаваемыми вопросами о подключенной фабрике](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="cdb34-118">For more information, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="cdb34-119">Логическая архитектура</span><span class="sxs-lookup"><span data-stu-id="cdb34-119">Logical architecture</span></span>

<span data-ttu-id="cdb34-120">На следующей диаграмме показаны логические компоненты предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="cdb34-120">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Логическая архитектура подключенной фабрики][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="cdb34-122">Модели связи</span><span class="sxs-lookup"><span data-stu-id="cdb34-122">Communication patterns</span></span>

<span data-ttu-id="cdb34-123">Решение использует [спецификацию публикации и подписки OPC UA](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) для отправки данных телеметрии OPC UA в Центр Интернета вещей в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cdb34-123">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="cdb34-124">В решении для этого используется модуль IoT Edge [издателя OPC](https://github.com/Azure/iot-edge-opc-publisher).</span><span class="sxs-lookup"><span data-stu-id="cdb34-124">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="cdb34-125">Решение также содержит клиент OPC UA, интегрированный в веб-приложение, которое может устанавливать соединение с локальными серверами OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-125">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="cdb34-126">Клиент использует [обратный прокси-сервер](https://wikipedia.org/wiki/Reverse_proxy) и с помощью Центра Интернета вещей создает подключение без необходимости открывать порты в локальном брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="cdb34-126">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="cdb34-127">Эта модель связи называется [взаимодействием с поддержкой службы](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="cdb34-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="cdb34-128">В решении для этого используется модуль IoT Edge [прокси OPC](https://github.com/Azure/iot-edge-opc-proxy/).</span><span class="sxs-lookup"><span data-stu-id="cdb34-128">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="cdb34-129">Моделирование</span><span class="sxs-lookup"><span data-stu-id="cdb34-129">Simulation</span></span>

<span data-ttu-id="cdb34-130">Виртуальные станции и системы управления производственными процессами (MES) образуют производственную линию фабрики.</span><span class="sxs-lookup"><span data-stu-id="cdb34-130">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="cdb34-131">Виртуальные устройства и модуль издателя OPC основаны на [стандарте OPC UA .NET][lnk-OPC-UA-NET-Standard], опубликованном OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="cdb34-131">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="cdb34-132">Прокси-сервер и издатель OPC реализованы как модули на основе [Edge Интернета вещей Azure][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="cdb34-132">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="cdb34-133">К каждой виртуальной производственной линии подключен отдельный шлюз.</span><span class="sxs-lookup"><span data-stu-id="cdb34-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="cdb34-134">Все виртуальные компоненты работают в контейнерах Docker, размещенных на виртуальной машине Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="cdb34-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="cdb34-135">По умолчанию моделирование настроено для работы восьми виртуальных производственных линий.</span><span class="sxs-lookup"><span data-stu-id="cdb34-135">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="cdb34-136">Виртуальная производственная линия</span><span class="sxs-lookup"><span data-stu-id="cdb34-136">Simulated production line</span></span>

<span data-ttu-id="cdb34-137">Производственная линия изготавливает детали.</span><span class="sxs-lookup"><span data-stu-id="cdb34-137">A production line manufactures parts.</span></span> <span data-ttu-id="cdb34-138">Она состоит из различных станций: станция сборки, станция тестирования и станция упаковки.</span><span class="sxs-lookup"><span data-stu-id="cdb34-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="cdb34-139">Моделирование работает и обновляет данные, которые отображаются на узлах OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-139">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="cdb34-140">Работа всех станций виртуальной производственной линии координируется с помощью MES через OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-140">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="cdb34-141">Виртуальная система управления производственными процессами</span><span class="sxs-lookup"><span data-stu-id="cdb34-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="cdb34-142">Система MES отслеживает каждую станцию на производственной линии через OPC UA для обнаружения изменений в состоянии станции.</span><span class="sxs-lookup"><span data-stu-id="cdb34-142">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="cdb34-143">Она вызывает методы OPC UA для управления станциями и передает изделие с одной рабочей станции на другую, пока оно не будет готово.</span><span class="sxs-lookup"><span data-stu-id="cdb34-143">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="cdb34-144">Модуль издателя OPC шлюза</span><span class="sxs-lookup"><span data-stu-id="cdb34-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="cdb34-145">Модуль издателя OPC подключается к серверам OPC UA на станции и подписывается на узлы OPC, которые должны быть опубликованы.</span><span class="sxs-lookup"><span data-stu-id="cdb34-145">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="cdb34-146">Модуль преобразует данные узла в формат JSON, шифрует их и отправляет Центр Интернета вещей в виде сообщений публикации и подписки OPC UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-146">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="cdb34-147">Модулю издателя OPC требуется только исходящий порт HTTPS (443), и он может работать с существующей инфраструктурой предприятия.</span><span class="sxs-lookup"><span data-stu-id="cdb34-147">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="cdb34-148">Модуль прокси OPC шлюза</span><span class="sxs-lookup"><span data-stu-id="cdb34-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="cdb34-149">Модуль прокси OPC UA шлюза предоставляет доступ через туннели двоичным командам и управляющим сообщениям OPC UA. Для его работы требуется только исходящий порт HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="cdb34-149">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="cdb34-150">Он может работать с существующей инфраструктурой предприятия, в том числе с веб-прокси.</span><span class="sxs-lookup"><span data-stu-id="cdb34-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="cdb34-151">Этот модуль использует методы устройства Центра Интернета вещей для передачи пакетированных данных TCP/IP на уровне приложения. Таким образом с помощью SSL/TLS он обеспечивает доверие конечной точки, шифрование данных и их целостность.</span><span class="sxs-lookup"><span data-stu-id="cdb34-151">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="cdb34-152">Двоичный протокол OPC UA, который ретранслируется через сам прокси, использует проверку подлинности и шифрование UA.</span><span class="sxs-lookup"><span data-stu-id="cdb34-152">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="cdb34-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="cdb34-153">Azure Time Series Insights</span></span>

<span data-ttu-id="cdb34-154">Модуль издателя OPC шлюза подписывается на узлы сервера OPC UA для обнаружения изменений в значениях данных.</span><span class="sxs-lookup"><span data-stu-id="cdb34-154">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="cdb34-155">Если обнаруживается изменение данных на одном из узлов, этот модуль отправляет сообщения в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb34-155">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="cdb34-156">Центр Интернета вещей передает источник события в Azure TSI.</span><span class="sxs-lookup"><span data-stu-id="cdb34-156">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="cdb34-157">TSI хранит данные в течение 30 дней в зависимости от меток времени, вложенных в сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdb34-157">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="cdb34-158">Эти данные включают:</span><span class="sxs-lookup"><span data-stu-id="cdb34-158">This data includes:</span></span>

* <span data-ttu-id="cdb34-159">OPC UA ApplicationUri;</span><span class="sxs-lookup"><span data-stu-id="cdb34-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="cdb34-160">OPC UA NodeId;</span><span class="sxs-lookup"><span data-stu-id="cdb34-160">OPC UA NodeId</span></span>
* <span data-ttu-id="cdb34-161">значение узла;</span><span class="sxs-lookup"><span data-stu-id="cdb34-161">Value of the node</span></span>
* <span data-ttu-id="cdb34-162">метка времени источника;</span><span class="sxs-lookup"><span data-stu-id="cdb34-162">Source timestamp</span></span>
* <span data-ttu-id="cdb34-163">OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="cdb34-163">OPC UA DisplayName</span></span>

<span data-ttu-id="cdb34-164">Сейчас TSI не позволяет клиентам настраивать продолжительность хранения данных.</span><span class="sxs-lookup"><span data-stu-id="cdb34-164">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="cdb34-165">TSI отправляет запрос к данным узла с помощью SearchSpan (Time.From, Time.To) и выполняет вычисление на основе значений OPC UA ApplicationUri, OPC UA NodeId или OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="cdb34-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="cdb34-166">Чтобы получить данные для датчиков общей эффективности оборудования и ключевых показателей эффективности, а также диаграммы временных рядов, данные группируются по количеству событий (Sum — всего событий, Avg — среднее количество, Min — минимальное количество и Max — максимальное количество).</span><span class="sxs-lookup"><span data-stu-id="cdb34-166">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="cdb34-167">Временные ряды создаются с помощью другого процесса.</span><span class="sxs-lookup"><span data-stu-id="cdb34-167">The time series are built using a different process.</span></span> <span data-ttu-id="cdb34-168">Показатели общей эффективности оборудования и ключевые показатели эффективности вычисляются на основе базовых данных станции и отображаются для топологии (производственные линии, фабрики, предприятие) в приложении.</span><span class="sxs-lookup"><span data-stu-id="cdb34-168">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="cdb34-169">Кроме того, временные ряды для топологии общей эффективности оборудования и ключевых показателей эффективности вычисляются в приложении, когда готов отображаемый временной диапазон.</span><span class="sxs-lookup"><span data-stu-id="cdb34-169">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="cdb34-170">Например, представление за день обновляется каждый час.</span><span class="sxs-lookup"><span data-stu-id="cdb34-170">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="cdb34-171">Представление временного ряда данных узла извлекается напрямую из TSI с помощью вычисления временного диапазона.</span><span class="sxs-lookup"><span data-stu-id="cdb34-171">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="cdb34-172">Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cdb34-172">IoT Hub</span></span>
<span data-ttu-id="cdb34-173">[Центр Интернета вещей][lnk-IoT Hub] принимает данные, отправленные из модуля издателя OPC в облако, и предоставляет к ним доступ службе Azure TSI.</span><span class="sxs-lookup"><span data-stu-id="cdb34-173">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="cdb34-174">Центр Интернета вещей также выполняет в решении следующие функции.</span><span class="sxs-lookup"><span data-stu-id="cdb34-174">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="cdb34-175">Поддерживает реестр удостоверений, в котором хранятся идентификаторы всех модулей издателя OPC и модулей прокси OPC.</span><span class="sxs-lookup"><span data-stu-id="cdb34-175">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="cdb34-176">Используется в качестве канала транспортировки для двустороннего обмена данными модуля прокси OPC.</span><span class="sxs-lookup"><span data-stu-id="cdb34-176">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="cdb34-177">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="cdb34-177">Azure Storage</span></span>
<span data-ttu-id="cdb34-178">Решение использует хранилище BLOB-объектов Azure в качестве дискового хранилища виртуальной машины и в качестве хранилища данных развертывания.</span><span class="sxs-lookup"><span data-stu-id="cdb34-178">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="cdb34-179">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="cdb34-179">Web app</span></span>
<span data-ttu-id="cdb34-180">Веб-приложение, развернутое как часть предварительно настроенного решения, состоит из встроенного клиента OPC UA, механизма обработки оповещений и визуализации данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="cdb34-180">The web app deployed as part of the preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdb34-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cdb34-181">Next steps</span></span>

<span data-ttu-id="cdb34-182">Дополнительные сведения об IoT Suite см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="cdb34-182">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="cdb34-183">[Разрешения на сайте azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="cdb34-183">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* <span data-ttu-id="cdb34-184">[Развертывание шлюза в ОС Windows или Linux для предварительно настроенного решения подключенной фабрики](iot-suite-connected-factory-gateway-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="cdb34-184">[Deploy a gateway on Windows or Linux for the connected factory preconfigured solution](iot-suite-connected-factory-gateway-deployment.md)</span></span>

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
