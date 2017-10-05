---
title: "Настройка подключенной фабрики Azure IoT Suite | Документация Майкрософт"
description: "Описание настройки поведения предварительно настроенного решения подключенной фабрики."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="12c23-103">Настройка отображения данных серверов на основе унифицированной архитектуры OPC решением подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="12c23-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="12c23-104">Введение</span><span class="sxs-lookup"><span data-stu-id="12c23-104">Introduction</span></span>

<span data-ttu-id="12c23-105">Решение подключенной фабрики агрегирует и отображает данные с серверов OPC UA, подключенных к решению.</span><span class="sxs-lookup"><span data-stu-id="12c23-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="12c23-106">В решении можно просматривать и отправлять команды на серверы OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="12c23-107">Дополнительные сведения об OPC UA см. в статье [Часто задаваемые вопросы о предварительно настроенном решении для подключенной фабрики IoT Suite](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="12c23-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="12c23-108">Примеры агрегированных данных в решении включают общую эффективность оборудования (OEE) и ключевые показатели эффективности (KPI), которые можно просмотреть на панели мониторинга на уровне станции, линии и фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="12c23-109">На следующем рисунке показаны значения OEE и KPI для станции **сборки** на **производственной линии 1** фабрики в **Мюнхене**:</span><span class="sxs-lookup"><span data-stu-id="12c23-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Пример значений OEE и KPI в решении][img-oee-kpi]

<span data-ttu-id="12c23-111">Решение позволяет просматривать подробные сведения об определенных элементах данных с серверов OPC UA, называемых *станциями*.</span><span class="sxs-lookup"><span data-stu-id="12c23-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="12c23-112">На следующем рисунке показаны графики количества произведенных элементов на конкретной станции:</span><span class="sxs-lookup"><span data-stu-id="12c23-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Графики количества произведенных элементов][img-manufactured-items]

<span data-ttu-id="12c23-114">Если выбрать один из графиков, можно просмотреть более подробные данные с помощью Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="12c23-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Просмотр данных с помощью Time Series Insights][img-tsi]

<span data-ttu-id="12c23-116">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="12c23-116">This article describes:</span></span>

- <span data-ttu-id="12c23-117">Доступность данных для различных представлений в решении.</span><span class="sxs-lookup"><span data-stu-id="12c23-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="12c23-118">Настройка способа отображения данных в решении.</span><span class="sxs-lookup"><span data-stu-id="12c23-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="12c23-119">Источники данных</span><span class="sxs-lookup"><span data-stu-id="12c23-119">Data sources</span></span>

<span data-ttu-id="12c23-120">Решение подключенной фабрики отображает данные с серверов OPC UA, подключенных к решению.</span><span class="sxs-lookup"><span data-stu-id="12c23-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="12c23-121">Установка по умолчанию содержит несколько серверов OPC UA, на которых запущено моделирование фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="12c23-122">В решение можно добавить собственные серверы OPC UA, [подключенные через шлюз][lnk-connect-cf].</span><span class="sxs-lookup"><span data-stu-id="12c23-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="12c23-123">На панели мониторинга можно просмотреть элементы данных, передаваемых подключенным сервером OPC UA в решение:</span><span class="sxs-lookup"><span data-stu-id="12c23-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="12c23-124">Перейдите к представлению **выбора сервера OPC UA**:</span><span class="sxs-lookup"><span data-stu-id="12c23-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Переход к представлению выбора сервера OPC UA][img-select-server]

1. <span data-ttu-id="12c23-126">Выберите сервер и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="12c23-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="12c23-127">Щелкните **Продолжить** при появлении предупреждения системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="12c23-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12c23-128">Это предупреждение отображается только один раз для каждого сервера и устанавливает отношение доверия между панелью мониторинга решения и сервером.</span><span class="sxs-lookup"><span data-stu-id="12c23-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="12c23-129">Теперь можно просмотреть элементы данных, которые сервер может отправлять в решение.</span><span class="sxs-lookup"><span data-stu-id="12c23-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="12c23-130">Элементы, которые отправляются в решение, имеют зеленый флажок:</span><span class="sxs-lookup"><span data-stu-id="12c23-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Опубликованные элементы][img-published]

1. <span data-ttu-id="12c23-132">Если вы являетесь *администратором* решения, вы можете опубликовать элемент данных, чтобы сделать его доступным в решении подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="12c23-133">Имея права администратора, можно также изменять значение элементов данных и вызывать методы на сервере OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="12c23-134">Сопоставление данных</span><span class="sxs-lookup"><span data-stu-id="12c23-134">Map the data</span></span>

<span data-ttu-id="12c23-135">Решение подключенной фабрики сопоставляет и объединяет опубликованные элементы данных с сервера OPC UA для различных представлений в решении.</span><span class="sxs-lookup"><span data-stu-id="12c23-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="12c23-136">Подключенная фабрика развертывается в учетную запись Azure при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="12c23-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="12c23-137">В решении подключенной фабрики Visual Studio сведения о сопоставлении хранятся в JSON-файле.</span><span class="sxs-lookup"><span data-stu-id="12c23-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="12c23-138">Вы можете просматривать и изменять этот файл конфигурации JSON в решении подключенной фабрики Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12c23-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="12c23-139">После внесения изменений можно повторно развернуть решение.</span><span class="sxs-lookup"><span data-stu-id="12c23-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="12c23-140">Файл конфигурации можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="12c23-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="12c23-141">изменения существующих имитаций фабрик, производственных линий и станций;</span><span class="sxs-lookup"><span data-stu-id="12c23-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="12c23-142">сопоставления данных физических серверов OPC UA, подключаемых к решению.</span><span class="sxs-lookup"><span data-stu-id="12c23-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="12c23-143">Чтобы клонировать копию решения подключенной фабрики Visual Studio, используйте следующую команду git:</span><span class="sxs-lookup"><span data-stu-id="12c23-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="12c23-144">Файл **ContosoTopologyDescription.json** определяет сопоставление элементов данных сервера OPC UA с представлениями на панели мониторинга решения подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="12c23-145">Этот файл конфигурации находится в папке **Contoso\Topology** в проекте **WebApp** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12c23-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="12c23-146">Содержимое JSON-файла упорядочено в виде иерархии узлов фабрики, производственной линии и станции.</span><span class="sxs-lookup"><span data-stu-id="12c23-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="12c23-147">Эта иерархия определяет иерархию навигации на панели мониторинга решения подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="12c23-148">Значения в каждом узле иерархии определяют сведения, отображаемые на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="12c23-149">Например, JSON-файл содержит следующие значения для фабрики в Мюнхене:</span><span class="sxs-lookup"><span data-stu-id="12c23-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="12c23-150">В этом представлении на панели мониторинга отображаются имя, описание и расположение:</span><span class="sxs-lookup"><span data-stu-id="12c23-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Данные Мюнхена на панели мониторинга][img-munich]

<span data-ttu-id="12c23-152">Каждая фабрика, производственная линия и станция имеют свойство изображений.</span><span class="sxs-lookup"><span data-stu-id="12c23-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="12c23-153">Эти файлы JPEG находятся в папке **Content\img** в проекте **WebApp**.</span><span class="sxs-lookup"><span data-stu-id="12c23-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="12c23-154">Они отображаются на панели мониторинга подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="12c23-155">Каждая станция содержит несколько подробных свойств, определяющих сопоставления на основе элементов данных OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="12c23-156">Эти свойства описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="12c23-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="12c23-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="12c23-157">OpcUri</span></span>

<span data-ttu-id="12c23-158">Значение **OpcUri** представляет собой URI приложения OPC UA, однозначно определяющий сервер OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="12c23-159">Например, значение **OpcUri** станции сборки на производственной линии 1 в Мюнхене выглядит так: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="12c23-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="12c23-160">Идентификаторы URI подключенных серверов OPC UA можно просмотреть на панели мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="12c23-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Представление идентификаторов URI сервера OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="12c23-162">Моделирование</span><span class="sxs-lookup"><span data-stu-id="12c23-162">Simulation</span></span>

<span data-ttu-id="12c23-163">Сведения в **моделируемом** узле относятся к имитации OPC UA, выполняемой на серверах OPC UA, подготавливаемых по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="12c23-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="12c23-164">Он не используется для физических серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="12c23-165">Kpi1 и Kpi2</span><span class="sxs-lookup"><span data-stu-id="12c23-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="12c23-166">Эти узлы описывают, как данные, полученные от станции, добавляются к двум значениям KPI на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="12c23-167">В развертывании по умолчанию эти значения KPI являются единицами в час и расходом энергии в кВт в час.</span><span class="sxs-lookup"><span data-stu-id="12c23-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="12c23-168">Решение вычисляет значения KPI на уровне станции и агрегирует их на уровнях фабрики и производственной линии.</span><span class="sxs-lookup"><span data-stu-id="12c23-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="12c23-169">Каждый показатель KPI имеет минимальное, максимальное и целевое значение.</span><span class="sxs-lookup"><span data-stu-id="12c23-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="12c23-170">Каждое значение KPI может также определить действия оповещений для выполнения в решении подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="12c23-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="12c23-171">В следующем фрагменте показаны определения KPI для станции сборки на производственной линии 1 в Мюнхене.</span><span class="sxs-lookup"><span data-stu-id="12c23-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="12c23-172">На следующем снимке экрана показаны данные KPI на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![Данные KPI на панели мониторинга][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="12c23-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="12c23-174">OpcNodes</span></span>

<span data-ttu-id="12c23-175">Узлы **OpcNodes** определяют опубликованные элементы данных с сервера OPC UA и указывают способ обработки данных.</span><span class="sxs-lookup"><span data-stu-id="12c23-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="12c23-176">Значение **NodeId** определяет конкретный NodeID унифицированной архитектуры OPC сервера OPC UA.</span><span class="sxs-lookup"><span data-stu-id="12c23-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="12c23-177">Первый узел на станции сборки производственной линии 1 в Мюнхене имеет значение **ns=2;i=385**.</span><span class="sxs-lookup"><span data-stu-id="12c23-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="12c23-178">Значение **NodeId** указывает элемент данных, который нужно считать с сервера OPC UA, а **SymbolicName** представляет понятное имя для этих данных, отображаемое на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="12c23-179">В следующей таблице приведены другие значения, связанные с каждым узлом:</span><span class="sxs-lookup"><span data-stu-id="12c23-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="12c23-180">Значение</span><span class="sxs-lookup"><span data-stu-id="12c23-180">Value</span></span> | <span data-ttu-id="12c23-181">Описание</span><span class="sxs-lookup"><span data-stu-id="12c23-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="12c23-182">релевантности</span><span class="sxs-lookup"><span data-stu-id="12c23-182">Relevance</span></span>  | <span data-ttu-id="12c23-183">Значения KPI и OEE, на которые влияют эти данные.</span><span class="sxs-lookup"><span data-stu-id="12c23-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="12c23-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="12c23-184">OpCode</span></span>     | <span data-ttu-id="12c23-185">Способ агрегирования данных.</span><span class="sxs-lookup"><span data-stu-id="12c23-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="12c23-186">Units</span><span class="sxs-lookup"><span data-stu-id="12c23-186">Units</span></span>      | <span data-ttu-id="12c23-187">Единицы измерения, используемые на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="12c23-188">Visible</span><span class="sxs-lookup"><span data-stu-id="12c23-188">Visible</span></span>    | <span data-ttu-id="12c23-189">Следует ли отображать это значение на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="12c23-190">Некоторые значения используются в вычислениях, но не отображаются.</span><span class="sxs-lookup"><span data-stu-id="12c23-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="12c23-191">Максимальная</span><span class="sxs-lookup"><span data-stu-id="12c23-191">Maximum</span></span>    | <span data-ttu-id="12c23-192">Максимальное значение, которое инициирует оповещение на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="12c23-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="12c23-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="12c23-193">MaximumAlertActions</span></span> | <span data-ttu-id="12c23-194">Действия, предпринимаемые в ответ на оповещение.</span><span class="sxs-lookup"><span data-stu-id="12c23-194">An action to take in response to an alert.</span></span> <span data-ttu-id="12c23-195">Например, отправка команды на станцию.</span><span class="sxs-lookup"><span data-stu-id="12c23-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="12c23-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="12c23-196">ConstValue</span></span> | <span data-ttu-id="12c23-197">Значение константы, используемое в вычислениях.</span><span class="sxs-lookup"><span data-stu-id="12c23-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="12c23-198">Развертывание изменений</span><span class="sxs-lookup"><span data-stu-id="12c23-198">Deploy the changes</span></span>

<span data-ttu-id="12c23-199">После внесения изменений в файл **ContosoTopologyDescription.json** необходимо повторно развернуть решение подключенной фабрики в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="12c23-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="12c23-200">Репозиторий **azure-iot-connected-factory** содержит скрипт PowerShell **build.ps1**, который можно использовать, чтобы повторно создать и развернуть решение.</span><span class="sxs-lookup"><span data-stu-id="12c23-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c23-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12c23-201">Next Steps</span></span>

<span data-ttu-id="12c23-202">Дополнительные сведения о предварительно настроенном решении подключенной фабрики см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="12c23-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="12c23-203">[Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="12c23-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="12c23-204">[Развертывание шлюза для подключенной фабрики][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="12c23-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="12c23-205">[Разрешения на сайте azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="12c23-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="12c23-206">Подключенная фабрика: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="12c23-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="12c23-207">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="12c23-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md