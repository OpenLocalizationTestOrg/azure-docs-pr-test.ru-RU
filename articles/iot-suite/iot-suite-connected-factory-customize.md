---
title: "aaaCustomize Azure IoT Suite подключен фабрики | Документы Microsoft"
description: "Описание как поведение hello toocustomize hello подключаться фабрики предварительно настроенных решений."
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
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="d9b7c-103">Настроить способ hello подключения фабрики решений отображает данные с серверов OPC UA</span><span class="sxs-lookup"><span data-stu-id="d9b7c-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="d9b7c-104">Введение</span><span class="sxs-lookup"><span data-stu-id="d9b7c-104">Introduction</span></span>

<span data-ttu-id="d9b7c-105">Hello решения подключенных фабрики собираются и отображаются данные из hello решения toohello подключенных серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="d9b7c-106">Можно просматривать и отправлять команды toohello OPC UA серверов в вашем решении.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="d9b7c-107">Дополнительные сведения о OPC UA см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d9b7c-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="d9b7c-108">Статистические данные в решении hello примеры hello общую эффективность работы оборудования (OEE) и ключевые показатели эффективности (KPI), которые можно просмотреть на панели мониторинга hello уровне фабрики hello, строки и станции.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="d9b7c-109">Hello следующем снимке экрана показаны hello OEE и ключевого показателя Эффективности значения для hello **сборки** станции на **рабочей строки 1**, в hello **Мюнхен** фабрики:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Пример значения OEE и ключевых показателей Эффективности в решении hello][img-oee-kpi]

<span data-ttu-id="d9b7c-111">Hello позволяет вам tooview подробные сведения из элементов данных из hello OPC UA серверы, называемые *станции*.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="d9b7c-112">Hello следующем снимке экрана показано точечное hello количество произведенных элементов с определенной рабочей станции:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Графики количества произведенных элементов][img-manufactured-items]

<span data-ttu-id="d9b7c-114">Если щелкнуть hello диаграмм позволяет исследовать данные hello дальше с помощью аналитики ряда времени (TSI):</span><span class="sxs-lookup"><span data-stu-id="d9b7c-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Просмотр данных с помощью Time Series Insights][img-tsi]

<span data-ttu-id="d9b7c-116">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="d9b7c-116">This article describes:</span></span>

- <span data-ttu-id="d9b7c-117">Как hello данных становится доступной toohello различные представления в решении hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="d9b7c-118">Настройка решения hello способом hello отображает hello данные.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="d9b7c-119">Источники данных</span><span class="sxs-lookup"><span data-stu-id="d9b7c-119">Data sources</span></span>

<span data-ttu-id="d9b7c-120">Hello подключенных фабрики решений отображает данные из hello решения toohello подключенных серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="d9b7c-121">Установка по умолчанию Hello включает несколько серверов OPC UA работе модели фабрики.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="d9b7c-122">Можно добавить собственные серверы OPC UA, [подключения через шлюз] [ lnk-connect-cf] tooyour решения.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="d9b7c-123">Можно просмотреть элементы данных hello отправку подключенного сервера OPC UA tooyour решение на панели мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="d9b7c-124">Перейдите toohello **выбрать сервер OPC UA** представления:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Перейдите toohello выберите представление OPC UA][img-select-server]

1. <span data-ttu-id="d9b7c-126">Выберите сервер и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="d9b7c-127">Нажмите кнопку **Продолжение** при отображении hello предупреждение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9b7c-128">Это предупреждение только отображается один раз для каждого сервера и устанавливает отношение доверия между hello решений мониторинга и сервером hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="d9b7c-129">Теперь можно обзора hello элементов данных hello server можно отправить toohello решения.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="d9b7c-130">Элементы, которые отправляются toohello решения имеют Зеленый флажок:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Опубликованные элементы][img-published]

1. <span data-ttu-id="d9b7c-132">При наличии *администратора* hello решения, вы можете toopublish toomake элемента данных доступно в hello подключен фабрики решения.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="d9b7c-133">Как администратор можно изменить значение hello элементов данных и вызывать методы в hello server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="d9b7c-134">Данные карты hello</span><span class="sxs-lookup"><span data-stu-id="d9b7c-134">Map hello data</span></span>

<span data-ttu-id="d9b7c-135">Hello подключен maps решения фабрики и статистические функции hello элементов опубликованных данных из hello toohello server OPC UA различных представлений в решении hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="d9b7c-136">Hello подключенных фабрики решение развертывается tooyour учетная запись Azure при подготовке hello решения.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="d9b7c-137">JSON-файла в hello решения фабрики подключить Visual Studio сохраняет сведения о сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="d9b7c-138">Можно просматривать и изменять этот файл конфигурации JSON в фабрике подключенных hello решения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="d9b7c-139">Можно повторно развернуть решение hello, после внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="d9b7c-140">Можно использовать файл конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="d9b7c-141">Измените существующий имитацию фабрик hello, производственных линиях и станции.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="d9b7c-142">Сопоставление данных из существующих серверов OPC UA подключении toohello решения.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="d9b7c-143">tooclone копию hello подключения решения Visual Studio фабрики, hello используйте следующую команду git.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="d9b7c-144">файл Hello **ContosoTopologyDescription.json** определяет сопоставление из hello OPC UA сервера данных представления toohello элементы на панели мониторинга решения подключенных фабрики hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="d9b7c-145">Этот файл конфигурации можно найти в hello **Contoso\Topology** папки в hello **веб-приложение** проект в решение Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="d9b7c-146">содержимое JSON-файла hello Hello, организованные в виде иерархии фабрики, строка производства и узлы станции.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="d9b7c-147">Эта иерархия определяет иерархии навигации hello в панель мониторинга подключенных фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="d9b7c-148">Значения в каждом узле иерархии hello определяют hello сведений, отображаемых на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="d9b7c-149">Например hello JSON-файл содержит следующие значения для hello фабрики Мюнхен hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

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

<span data-ttu-id="d9b7c-150">Hello имя, описание и расположение отображаются в представлении, в панели мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Данные Мюнхен hello панели управления][img-munich]

<span data-ttu-id="d9b7c-152">Каждая фабрика, производственная линия и станция имеют свойство изображений.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="d9b7c-153">JPEG-файлы можно найти в hello **Content\img** папки в hello **веб-приложение** проекта.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="d9b7c-154">Эти изображения файлы отображаются в панели мониторинга подключенных фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="d9b7c-155">Каждая станция включает несколько подробные свойства, определяющие hello сопоставления из hello OPC UA элементов данных.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="d9b7c-156">Эти свойства описаны в следующих разделах hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="d9b7c-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="d9b7c-157">OpcUri</span></span>

<span data-ttu-id="d9b7c-158">Hello **OpcUri** значение — hello OPC UA приложения URI, однозначно определяющий hello server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="d9b7c-159">Например, hello **OpcUri** станции сборки hello в строке производственного 1 в Мюнхен выглядит hello следующее значение: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="d9b7c-160">Hello идентификаторы URI hello подключенных серверов OPC UA можно просмотреть в панели мониторинга hello решения:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Представление идентификаторов URI сервера OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="d9b7c-162">Моделирование</span><span class="sxs-lookup"><span data-stu-id="d9b7c-162">Simulation</span></span>

<span data-ttu-id="d9b7c-163">Здравствуйте, сведения в hello **моделирование** узел является конкретных toohello моделирование OPC UA, которое выполняется в hello OPC UA серверов, предоставляемых по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="d9b7c-164">Он не используется для физических серверов OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="d9b7c-165">Kpi1 и Kpi2</span><span class="sxs-lookup"><span data-stu-id="d9b7c-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="d9b7c-166">Эти узлы описывают, как данные из станции hello влияют toohello два значения ключевого показателя Эффективности в панель мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="d9b7c-167">В развертывании по умолчанию эти значения KPI являются единицами в час и расходом энергии в кВт в час.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="d9b7c-168">решение Hello вычисляет значения ключевого показателя Эффективности на уровне hello станции и объединяет их на уровнях фабрики и строка hello производства.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="d9b7c-169">Каждый показатель KPI имеет минимальное, максимальное и целевое значение.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="d9b7c-170">Каждое значение ключевого показателя Эффективности можно также определить предупреждения действия для решения tooperform hello подключен фабрики.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="d9b7c-171">Hello следующий фрагмент кода показывает hello определений KPI для hello сборки станции производственного строке 1 в Мюнхен:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="d9b7c-172">Hello следующем снимке экрана показано hello данных ключевого показателя Эффективности в панель мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Сведения о ключевых показателей Эффективности в hello панели мониторинга][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="d9b7c-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="d9b7c-174">OpcNodes</span></span>

<span data-ttu-id="d9b7c-175">Hello **OpcNodes** идентификации узлов hello элементов опубликованных данных из сервера OPC UA hello и указать способ tooprocess этих данных.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="d9b7c-176">Hello **NodeId** значение идентифицирует hello конкретных NodeID UA OPC из hello server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="d9b7c-177">первый узел Hello в hello станции сборки для производства 1 в Мюнхен имеет значение **ns = 2; i = 385**.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="d9b7c-178">Объект **NodeId** указывает hello tooread элемента данных из сервера OPC UA hello и hello **символическое** предоставляет toouse понятное имя в панели мониторинга hello для этих данных.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="d9b7c-179">Другие значения, связанные с каждым узлом, приведены в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="d9b7c-180">Значение</span><span class="sxs-lookup"><span data-stu-id="d9b7c-180">Value</span></span> | <span data-ttu-id="d9b7c-181">Описание</span><span class="sxs-lookup"><span data-stu-id="d9b7c-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="d9b7c-182">релевантности</span><span class="sxs-lookup"><span data-stu-id="d9b7c-182">Relevance</span></span>  | <span data-ttu-id="d9b7c-183">значения ключевого показателя Эффективности и OEE Hello позволяет согласовывать данные.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="d9b7c-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="d9b7c-184">OpCode</span></span>     | <span data-ttu-id="d9b7c-185">Агрегирование данных hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="d9b7c-186">Units</span><span class="sxs-lookup"><span data-stu-id="d9b7c-186">Units</span></span>      | <span data-ttu-id="d9b7c-187">toouse единицы Hello в панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="d9b7c-188">Visible</span><span class="sxs-lookup"><span data-stu-id="d9b7c-188">Visible</span></span>    | <span data-ttu-id="d9b7c-189">Ли toodisplay, это значение в панель мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="d9b7c-190">Некоторые значения используются в вычислениях, но не отображаются.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="d9b7c-191">Максимальная</span><span class="sxs-lookup"><span data-stu-id="d9b7c-191">Maximum</span></span>    | <span data-ttu-id="d9b7c-192">Hello максимальное значение, которое создает предупреждение в панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="d9b7c-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="d9b7c-193">MaximumAlertActions</span></span> | <span data-ttu-id="d9b7c-194">Tootake действие в предупреждении tooan ответа.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="d9b7c-195">Например отправьте команды tooa станции.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="d9b7c-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="d9b7c-196">ConstValue</span></span> | <span data-ttu-id="d9b7c-197">Значение константы, используемое в вычислениях.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="d9b7c-198">Развертывание изменений hello</span><span class="sxs-lookup"><span data-stu-id="d9b7c-198">Deploy hello changes</span></span>

<span data-ttu-id="d9b7c-199">После завершения внесения изменений toohello **ContosoTopologyDescription.json** файл, необходимо повторно развернуть hello подключен tooyour решения фабрики учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="d9b7c-200">Hello **-iot подключен фабрики azure** репозиторий включает **build.ps1** сценарий PowerShell, можно использовать toorebuild и развернуть решение hello.</span><span class="sxs-lookup"><span data-stu-id="d9b7c-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9b7c-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9b7c-201">Next Steps</span></span>

<span data-ttu-id="d9b7c-202">Дополнительные сведения об hello подключен фабрики предварительно настроенное решение hello чтение, следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="d9b7c-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="d9b7c-203">[Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="d9b7c-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="d9b7c-204">[Развертывание шлюза для подключенной фабрики][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="d9b7c-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="d9b7c-205">[Разрешения на сайт azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d9b7c-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="d9b7c-206">Подключенная фабрика: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="d9b7c-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="d9b7c-207">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="d9b7c-207">[FAQ][lnk-faq]</span></span>


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