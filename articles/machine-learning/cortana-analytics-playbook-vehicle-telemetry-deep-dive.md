---
title: "Углубленное aaaDeep прогнозирования vehicle работоспособности и управление им привычки - Azure | Документы Microsoft"
description: "Использовать возможности hello toogain Cortana аналитики в реальном времени и прогнозной аналитики на автомобиль работоспособности и пешком привычки."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="f96c2-103">Аналитика решения транспортных средств телеметрии репертуара: глубокое погружение в решение hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="f96c2-104">Это **меню** связывает этот репертуара toohello разделы:</span><span class="sxs-lookup"><span data-stu-id="f96c2-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="f96c2-105">Этот раздел детализируется углублением каждого из этапов hello, используемые в hello архитектура решения инструкции и указания для настройки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="f96c2-106">Источники данных</span><span class="sxs-lookup"><span data-stu-id="f96c2-106">Data Sources</span></span>
<span data-ttu-id="f96c2-107">Hello решение использует два различных источников данных:</span><span class="sxs-lookup"><span data-stu-id="f96c2-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="f96c2-108">**имитированные сигналы автомобиля и набор диагностических данных** ;</span><span class="sxs-lookup"><span data-stu-id="f96c2-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="f96c2-109">**каталог автомобилей.**</span><span class="sxs-lookup"><span data-stu-id="f96c2-109">**vehicle catalog**</span></span>

<span data-ttu-id="f96c2-110">В это решение входит симулятор телематики автомобиля.</span><span class="sxs-lookup"><span data-stu-id="f96c2-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="f96c2-111">Он выдает диагностических сведений и уведомляет соответствующее состояние toohello hello vehicle и toohello пешком шаблон в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="f96c2-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="f96c2-112">Нажмите кнопку [симулятор Vehicle Telematics](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **решение Visual Studio Vehicle Telematics симулятор** для настройки в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="f96c2-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="f96c2-113">каталог vehicle Hello содержит сопоставление toomodel VIN эталонного набора данных.</span><span class="sxs-lookup"><span data-stu-id="f96c2-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Симулятор телематики автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="f96c2-115">*Рис. 1. Симулятор телематики автомобиля*</span><span class="sxs-lookup"><span data-stu-id="f96c2-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="f96c2-116">Это формата JSON набора данных, содержащий hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="f96c2-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="f96c2-117">столбец</span><span class="sxs-lookup"><span data-stu-id="f96c2-117">Column</span></span> | <span data-ttu-id="f96c2-118">Описание</span><span class="sxs-lookup"><span data-stu-id="f96c2-118">Description</span></span> | <span data-ttu-id="f96c2-119">Значения</span><span class="sxs-lookup"><span data-stu-id="f96c2-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f96c2-120">VIN</span><span class="sxs-lookup"><span data-stu-id="f96c2-120">VIN</span></span> |<span data-ttu-id="f96c2-121">Случайно сгенерированный идентификационный номер автомобиля</span><span class="sxs-lookup"><span data-stu-id="f96c2-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="f96c2-122">Его можно получить из главного списка 10 000 случайно сгенерированных идентификационных номеров автомобилей</span><span class="sxs-lookup"><span data-stu-id="f96c2-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="f96c2-123">outsideTemperature</span><span class="sxs-lookup"><span data-stu-id="f96c2-123">Outside temperature</span></span> |<span data-ttu-id="f96c2-124">Hello за пределами температуры, где пешком hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="f96c2-125">Случайно сгенерированное число от 0 до 100</span><span class="sxs-lookup"><span data-stu-id="f96c2-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="f96c2-126">engineTemperature</span><span class="sxs-lookup"><span data-stu-id="f96c2-126">Engine temperature</span></span> |<span data-ttu-id="f96c2-127">Hello температуру ядра hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="f96c2-128">Случайно сгенерированное число от 0 до 500</span><span class="sxs-lookup"><span data-stu-id="f96c2-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="f96c2-129">Speed</span><span class="sxs-lookup"><span data-stu-id="f96c2-129">Speed</span></span> |<span data-ttu-id="f96c2-130">скорость Hello, влияющие на какие hello транспортного средства</span><span class="sxs-lookup"><span data-stu-id="f96c2-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="f96c2-131">Случайно сгенерированное число от 0 до 100</span><span class="sxs-lookup"><span data-stu-id="f96c2-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="f96c2-132">fuel</span><span class="sxs-lookup"><span data-stu-id="f96c2-132">Fuel</span></span> |<span data-ttu-id="f96c2-133">уровень топлива Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="f96c2-134">Случайно сгенерированное число от 0 до 100 (указывает уровень топлива в процентах)</span><span class="sxs-lookup"><span data-stu-id="f96c2-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="f96c2-135">engineoil</span><span class="sxs-lookup"><span data-stu-id="f96c2-135">EngineOil</span></span> |<span data-ttu-id="f96c2-136">уровень нефти engine Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="f96c2-137">Случайно сгенерированное число от 0 до 100 (указывает уровень моторного масла в процентах)</span><span class="sxs-lookup"><span data-stu-id="f96c2-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="f96c2-138">Давление в шинах</span><span class="sxs-lookup"><span data-stu-id="f96c2-138">Tire pressure</span></span> |<span data-ttu-id="f96c2-139">загрузку велосипеда Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="f96c2-140">Случайно сгенерированное число от 0 до 50 (указывает уровень давления в шинах в процентах)</span><span class="sxs-lookup"><span data-stu-id="f96c2-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="f96c2-141">odometer</span><span class="sxs-lookup"><span data-stu-id="f96c2-141">Odometer</span></span> |<span data-ttu-id="f96c2-142">считывание одометра Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="f96c2-143">Случайно сгенерированное число от 0 до 200 000</span><span class="sxs-lookup"><span data-stu-id="f96c2-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="f96c2-144">accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="f96c2-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="f96c2-145">Hello сочетаний клавиш педали положение hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="f96c2-146">Случайно сгенерированное число от 0 до 100 (указывает уровень, соответствующий положению педали газа, в процентах)</span><span class="sxs-lookup"><span data-stu-id="f96c2-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="f96c2-147">parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="f96c2-147">Parking_brake_status</span></span> |<span data-ttu-id="f96c2-148">Указывает ли hello vehicle выполнены в нерабочем или нет</span><span class="sxs-lookup"><span data-stu-id="f96c2-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="f96c2-149">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-149">True or False</span></span> |
| <span data-ttu-id="f96c2-150">headlamp_status</span><span class="sxs-lookup"><span data-stu-id="f96c2-150">Headlamp_status</span></span> |<span data-ttu-id="f96c2-151">Указывает, где Прожектор hello на или нет</span><span class="sxs-lookup"><span data-stu-id="f96c2-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="f96c2-152">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-152">True or False</span></span> |
| <span data-ttu-id="f96c2-153">brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="f96c2-153">Brake_pedal_status</span></span> |<span data-ttu-id="f96c2-154">Указывает, нажата ли педаль тормоза hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="f96c2-155">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-155">True or False</span></span> |
| <span data-ttu-id="f96c2-156">transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="f96c2-156">Transmission_gear_position</span></span> |<span data-ttu-id="f96c2-157">положение шестеренки передачи Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="f96c2-158">Состояния: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="f96c2-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="f96c2-159">ignition_status</span><span class="sxs-lookup"><span data-stu-id="f96c2-159">Ignition_status</span></span> |<span data-ttu-id="f96c2-160">Указывает, является ли hello vehicle запущенной или остановленной</span><span class="sxs-lookup"><span data-stu-id="f96c2-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="f96c2-161">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-161">True or False</span></span> |
| <span data-ttu-id="f96c2-162">windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="f96c2-162">Windshield_wiper_status</span></span> |<span data-ttu-id="f96c2-163">Указывает, включено ли wiper ветровое hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="f96c2-164">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-164">True or False</span></span> |
| <span data-ttu-id="f96c2-165">ABS</span><span class="sxs-lookup"><span data-stu-id="f96c2-165">ABS</span></span> |<span data-ttu-id="f96c2-166">Указывает, включена ли антиблокировочная система тормозов</span><span class="sxs-lookup"><span data-stu-id="f96c2-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="f96c2-167">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="f96c2-167">True or False</span></span> |
| <span data-ttu-id="f96c2-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f96c2-168">Timestamp</span></span> |<span data-ttu-id="f96c2-169">Hello отметка времени, когда создается точка данных hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="f96c2-170">Дата</span><span class="sxs-lookup"><span data-stu-id="f96c2-170">Date</span></span> |
| <span data-ttu-id="f96c2-171">City</span><span class="sxs-lookup"><span data-stu-id="f96c2-171">City</span></span> |<span data-ttu-id="f96c2-172">расположение Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="f96c2-172">hello location of hello vehicle</span></span> |<span data-ttu-id="f96c2-173">В этом решении представлены 4 города: Бельвью, Редмонд, Саммамиш и Сиэтл</span><span class="sxs-lookup"><span data-stu-id="f96c2-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="f96c2-174">Hello vehicle модели эталонный набор данных содержит сопоставление модели VIN toohello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="f96c2-175">VIN</span><span class="sxs-lookup"><span data-stu-id="f96c2-175">VIN</span></span> | <span data-ttu-id="f96c2-176">Модель</span><span class="sxs-lookup"><span data-stu-id="f96c2-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="f96c2-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="f96c2-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="f96c2-178">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-178">Sedan</span></span> |
| <span data-ttu-id="f96c2-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="f96c2-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="f96c2-180">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-180">Hybrid</span></span> |
| <span data-ttu-id="f96c2-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="f96c2-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="f96c2-182">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-182">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="f96c2-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="f96c2-184">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-184">Sedan</span></span> |
| <span data-ttu-id="f96c2-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="f96c2-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="f96c2-186">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-186">Hybrid</span></span> |
| <span data-ttu-id="f96c2-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="f96c2-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="f96c2-188">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-188">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="f96c2-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="f96c2-190">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-190">Sedan</span></span> |
| <span data-ttu-id="f96c2-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="f96c2-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="f96c2-192">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-192">Hybrid</span></span> |
| <span data-ttu-id="f96c2-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="f96c2-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="f96c2-194">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-194">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="f96c2-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="f96c2-196">Автомобиль с откидным верхом</span><span class="sxs-lookup"><span data-stu-id="f96c2-196">Convertible</span></span> |
| <span data-ttu-id="f96c2-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="f96c2-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="f96c2-198">Автомобиль с кузовом «универсал»</span><span class="sxs-lookup"><span data-stu-id="f96c2-198">Station Wagon</span></span> |
| <span data-ttu-id="f96c2-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="f96c2-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="f96c2-200">Малогабаритный автомобиль</span><span class="sxs-lookup"><span data-stu-id="f96c2-200">Compact Car</span></span> |
| <span data-ttu-id="f96c2-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="f96c2-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="f96c2-202">Небольшой внедорожник</span><span class="sxs-lookup"><span data-stu-id="f96c2-202">Small SUV</span></span> |
| <span data-ttu-id="f96c2-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="f96c2-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="f96c2-204">Спортивный автомобиль</span><span class="sxs-lookup"><span data-stu-id="f96c2-204">Sports Car</span></span> |
| <span data-ttu-id="f96c2-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="f96c2-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="f96c2-206">Внедорожник среднего размера</span><span class="sxs-lookup"><span data-stu-id="f96c2-206">Medium SUV</span></span> |
| <span data-ttu-id="f96c2-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="f96c2-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="f96c2-208">Автомобиль с кузовом «универсал»</span><span class="sxs-lookup"><span data-stu-id="f96c2-208">Station Wagon</span></span> |
| <span data-ttu-id="f96c2-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="f96c2-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="f96c2-210">Большой внедорожник</span><span class="sxs-lookup"><span data-stu-id="f96c2-210">Large SUV</span></span> |
| <span data-ttu-id="f96c2-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="f96c2-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="f96c2-212">Большой внедорожник</span><span class="sxs-lookup"><span data-stu-id="f96c2-212">Large SUV</span></span> |
| <span data-ttu-id="f96c2-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="f96c2-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="f96c2-214">Двухместный легковой автомобиль</span><span class="sxs-lookup"><span data-stu-id="f96c2-214">Coupe</span></span> |
| <span data-ttu-id="f96c2-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="f96c2-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="f96c2-216">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-216">Sedan</span></span> |
| <span data-ttu-id="f96c2-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="f96c2-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="f96c2-218">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-218">Hybrid</span></span> |
| <span data-ttu-id="f96c2-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="f96c2-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="f96c2-220">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-220">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="f96c2-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="f96c2-222">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-222">Sedan</span></span> |
| <span data-ttu-id="f96c2-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="f96c2-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="f96c2-224">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-224">Hybrid</span></span> |
| <span data-ttu-id="f96c2-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="f96c2-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="f96c2-226">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-226">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="f96c2-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="f96c2-228">Седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-228">Sedan</span></span> |
| <span data-ttu-id="f96c2-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="f96c2-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="f96c2-230">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="f96c2-230">Hybrid</span></span> |
| <span data-ttu-id="f96c2-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="f96c2-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="f96c2-232">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="f96c2-232">Family Saloon</span></span> |
| <span data-ttu-id="f96c2-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="f96c2-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="f96c2-234">Автомобиль с откидным верхом</span><span class="sxs-lookup"><span data-stu-id="f96c2-234">Convertible</span></span> |
| <span data-ttu-id="f96c2-235">…….</span><span class="sxs-lookup"><span data-stu-id="f96c2-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="f96c2-236">Ссылки</span><span class="sxs-lookup"><span data-stu-id="f96c2-236">References</span></span>
[<span data-ttu-id="f96c2-237">Решение Visual Studio "Симулятор телематики автомобиля"</span><span class="sxs-lookup"><span data-stu-id="f96c2-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="f96c2-238">Концентратор событий Azure</span><span class="sxs-lookup"><span data-stu-id="f96c2-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="f96c2-239">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="f96c2-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="f96c2-240">Прием</span><span class="sxs-lookup"><span data-stu-id="f96c2-240">Ingestion</span></span>
<span data-ttu-id="f96c2-241">Комбинация концентраторов событий Azure Stream Analytics и фабрики данных является hello vehicle использовать tooingest сигналов, hello события диагностики и в режиме реального времени и пакетной аналитике.</span><span class="sxs-lookup"><span data-stu-id="f96c2-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="f96c2-242">Все эти компоненты создаются и настраиваются как часть развертывания решения hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="f96c2-243">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="f96c2-243">Real-time analysis</span></span>
<span data-ttu-id="f96c2-244">Hello события, создаваемые hello симулятор Telematics Vehicle публикуются toohello концентратора событий с помощью пакета SDK концентратор событий "hello".</span><span class="sxs-lookup"><span data-stu-id="f96c2-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="f96c2-245">Задание Stream Analytics Hello принимает эти события из концентратора событий hello и процессы hello данные в реальном времени tooanalyze hello vehicle работоспособности.</span><span class="sxs-lookup"><span data-stu-id="f96c2-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Панель мониторинга концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="f96c2-247">*Рис. 4. Панель мониторинга концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="f96c2-247">*Figure 4 - Event Hub dashboard*</span></span>

![Обработка данных заданием Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="f96c2-249">*Рис. 5. Обработка данных заданием Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="f96c2-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="f96c2-250">Задание Stream Analytics Hello;</span><span class="sxs-lookup"><span data-stu-id="f96c2-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="f96c2-251">принимает данные из hello концентратора событий</span><span class="sxs-lookup"><span data-stu-id="f96c2-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="f96c2-252">выполняется соединение с hello ссылка toomap hello vehicle VIN toohello соответствующей модели данных</span><span class="sxs-lookup"><span data-stu-id="f96c2-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="f96c2-253">сохраняет эти данные в хранилище BLOB-объектов для расширенного пакетного анализа.</span><span class="sxs-lookup"><span data-stu-id="f96c2-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="f96c2-254">приветствия при следующем запросе Stream Analytics является данных используется toopersist hello в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f96c2-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Запрос задания Stream Analytics для приема данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="f96c2-256">*Рис. 6. Запрос задания Stream Analytics для приема данных*</span><span class="sxs-lookup"><span data-stu-id="f96c2-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="f96c2-257">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="f96c2-257">Batch analysis</span></span>
<span data-ttu-id="f96c2-258">Для расширенного пакетного анализа необходимо создать дополнительное количество имитированных сигналов автомобиля и набор диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="f96c2-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="f96c2-259">Это обязательный tooensure тома хорошо репрезентативных данных для пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="f96c2-260">Для этой цели используется конвейер с именем «PrepareSampleDataPipeline» в рабочий процесс toogenerate hello фабрики данных Azure за один год имитацию vehicle сигналов и набор диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="f96c2-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="f96c2-261">Нажмите кнопку [фабрики данных пользовательского действия](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello пользовательское действие DotNet решения Visual Studio для настройки фабрики данных на основе требований.</span><span class="sxs-lookup"><span data-stu-id="f96c2-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Подготовка образца данных для рабочего процесса пакетной обработки](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="f96c2-263">*Рис. 7. Подготовка образца данных для рабочего процесса пакетной обработки*</span><span class="sxs-lookup"><span data-stu-id="f96c2-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="f96c2-264">конвейер Hello состоит из пользовательских .net ADF действия, здесь показаны:</span><span class="sxs-lookup"><span data-stu-id="f96c2-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Действие PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="f96c2-266">*Рис. 8. PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="f96c2-267">После конвейера hello выполняется успешно и набор данных «RawCarEventsTable» помечен «Готово», один год стоит имитацию vehicle сигналов и диагностических данных создаются.</span><span class="sxs-lookup"><span data-stu-id="f96c2-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="f96c2-268">Вы видите следующее hello папок и файлов, созданных в учетной записи хранения в контейнере «connectedcar» hello:</span><span class="sxs-lookup"><span data-stu-id="f96c2-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Выходные данные PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="f96c2-270">*Рис. 9. Выходные данные PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="f96c2-271">Ссылки</span><span class="sxs-lookup"><span data-stu-id="f96c2-271">References</span></span>
[<span data-ttu-id="f96c2-272">Пакет SDK концентратора событий Azure для приема потока</span><span class="sxs-lookup"><span data-stu-id="f96c2-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="f96c2-273">[Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md)
[Использование настраиваемых действий в конвейере фабрики данных Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="f96c2-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="f96c2-274">Решение Visual Studio "Действие DotNet фабрики данных Azure" для подготовки примера данных</span><span class="sxs-lookup"><span data-stu-id="f96c2-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="f96c2-275">Разделение набора данных hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-275">Partition hello dataset</span></span>
<span data-ttu-id="f96c2-276">сигналы необработанные полуструктурированные vehicle Hello и набор диагностических данных секционируются на этапе подготовки данных hello в формат года и МЕСЯЦА.</span><span class="sxs-lookup"><span data-stu-id="f96c2-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="f96c2-277">Такое секционирование обеспечивает более эффективно опрашивать и масштабируемых долговременного хранения, позволяя сбоя переход из одного большого двоичного объекта учетной записи toohello Далее hello первой учетной записи может заполниться до конца.</span><span class="sxs-lookup"><span data-stu-id="f96c2-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="f96c2-278">Этот шаг в решении hello является применимо только toobatch обработки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="f96c2-279">Управление входными и выходными данными:</span><span class="sxs-lookup"><span data-stu-id="f96c2-279">Input and output data data management:</span></span>

* <span data-ttu-id="f96c2-280">Hello **выходных данных** (с меткой *PartitionedCarEventsTable*) toobe сохраняется длительное время как hello фундаментальные / «rawest» формы данных в hello клиента» Озера данных».</span><span class="sxs-lookup"><span data-stu-id="f96c2-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="f96c2-281">Hello **входные данные** конвейера toothis бы обычно удаляется как hello выходных данных имеет toohello полноценная входных данных — просто хранится (секционировать) лучше для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="f96c2-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Рабочий процесс секционирования событий автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="f96c2-283">*Рис. 10. Рабочий процесс секционирования событий автомобиля*</span><span class="sxs-lookup"><span data-stu-id="f96c2-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="f96c2-284">Hello необработанные данные секционируются с использованием действия Hive HDInsight в «PartitionCarEventsPipeline».</span><span class="sxs-lookup"><span data-stu-id="f96c2-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="f96c2-285">Hello образец данных, созданного на шаге 1 за год, секционирована по года и МЕСЯЦА.</span><span class="sxs-lookup"><span data-stu-id="f96c2-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="f96c2-286">Hello разделы являются используется toogenerate vehicle сигналов и диагностических данных для каждого месяца (всего 12 разделов) года.</span><span class="sxs-lookup"><span data-stu-id="f96c2-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Действие PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="f96c2-288">*Рис. 11. PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="f96c2-289">***Сценарий Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="f96c2-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="f96c2-290">Hello следующий сценарий Hive, с именем «partitioncarevents.hql» используется для секционирования и находится в папке «\demo\src\connectedcar\scripts» hello hello загружен zip.</span><span class="sxs-lookup"><span data-stu-id="f96c2-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="f96c2-291">После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Секционированные выходные данные](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="f96c2-293">*Рис. 12. Секционированные выходные данные*</span><span class="sxs-lookup"><span data-stu-id="f96c2-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="f96c2-294">Hello данных теперь оптимизирован, управляемость и готов для дальнейшей обработки toogain широкие возможности пакета аналитики.</span><span class="sxs-lookup"><span data-stu-id="f96c2-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="f96c2-295">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="f96c2-295">Data Analysis</span></span>
<span data-ttu-id="f96c2-296">В этом разделе, показано, как расширенный toocombine Azure Stream Analytics, машинного обучения Azure, фабрики данных Azure и Azure HDInsight для форматированного привычки аналитика на автомобиль работоспособности и управление им.</span><span class="sxs-lookup"><span data-stu-id="f96c2-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="f96c2-297">Здесь содержатся три подраздела:</span><span class="sxs-lookup"><span data-stu-id="f96c2-297">There are three subsections here:</span></span>

1. <span data-ttu-id="f96c2-298">**Машинное Обучение**: в этом подразделе рассказывается о эксперимента обнаружение аномалий hello, мы использовали в это решение toopredict автомобилей, требующие обслуживания, обслуживания и средств, требующие попыток из-за проблем с toosafety.</span><span class="sxs-lookup"><span data-stu-id="f96c2-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="f96c2-299">**В режиме реального времени анализа**: в этом подразделе содержит сведения о аналитики hello в реальном времени с помощью hello язык запросов Stream Analytics и ввод в эксплуатацию hello машинного обучения поэкспериментировать в режиме реального времени с помощью пользовательского приложения.</span><span class="sxs-lookup"><span data-stu-id="f96c2-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="f96c2-300">**Анализ пакета**: этот подраздел содержит сведения, касающиеся hello, преобразования и обработки данных пакета hello, с помощью Azure HDInsight и машинного обучения Azure, введенную фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f96c2-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="f96c2-301">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="f96c2-301">Machine Learning</span></span>
<span data-ttu-id="f96c2-302">Наша цель — toopredict hello автомобилей, требующие обслуживания или отзыв на основе определенных состоянием статистики.</span><span class="sxs-lookup"><span data-stu-id="f96c2-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="f96c2-303">Корпорация Microsoft hello, следуя предположения</span><span class="sxs-lookup"><span data-stu-id="f96c2-303">We make hello following assumptions</span></span>

* <span data-ttu-id="f96c2-304">Если один из следующих трех условий hello верны, требуют hello автомобилей **обслуживания обслуживания**:</span><span class="sxs-lookup"><span data-stu-id="f96c2-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="f96c2-305">низкое давление в шине;</span><span class="sxs-lookup"><span data-stu-id="f96c2-305">Tire pressure is low</span></span>
  * <span data-ttu-id="f96c2-306">низкий уровень моторного масла;</span><span class="sxs-lookup"><span data-stu-id="f96c2-306">Engine oil level is low</span></span>
  * <span data-ttu-id="f96c2-307">высокая температура двигателя.</span><span class="sxs-lookup"><span data-stu-id="f96c2-307">Engine temperature is high</span></span>
* <span data-ttu-id="f96c2-308">Если одно из следующих условий hello имеют значение true, возможно, hello автомобилей **проблему безопасности** и требуют **отзыва**:</span><span class="sxs-lookup"><span data-stu-id="f96c2-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="f96c2-309">высокая температура двигателя, но низкая наружная температура;</span><span class="sxs-lookup"><span data-stu-id="f96c2-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="f96c2-310">низкая температура двигателя, но высокая наружная температура.</span><span class="sxs-lookup"><span data-stu-id="f96c2-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="f96c2-311">В зависимости от требований предыдущих hello, мы создали аномалий toodetect две отдельные модели, один для обнаружения транспортного средства обслуживания и один для обнаружения транспортного средства повторного вызова.</span><span class="sxs-lookup"><span data-stu-id="f96c2-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="f96c2-312">В обоих этих моделей hello встроенный алгоритм анализа главных компонентов (PCA) используется для обнаружения аномалий.</span><span class="sxs-lookup"><span data-stu-id="f96c2-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="f96c2-313">**Модель определения необходимости в обслуживании**</span><span class="sxs-lookup"><span data-stu-id="f96c2-313">**Maintenance detection model**</span></span>

<span data-ttu-id="f96c2-314">Если один из трех индикаторов - нагрузка для велосипеда, нефти engine или температуры ядра - удовлетворяет его соответствующие условию, модель обнаружения обслуживания hello сообщает аномалий.</span><span class="sxs-lookup"><span data-stu-id="f96c2-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="f96c2-315">В результате нам требуется только tooconsider эти три переменные для построения модели hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="f96c2-316">В нашем эксперименты в машинном обучении Azure, сначала используется **Выбор столбцов в наборе данных** модуль tooextract эти три переменные.</span><span class="sxs-lookup"><span data-stu-id="f96c2-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="f96c2-317">Далее мы используем hello аномалий на основе PCA обнаружения модуль toobuild hello модель обнаружения аномалий.</span><span class="sxs-lookup"><span data-stu-id="f96c2-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="f96c2-318">Анализ главных компонентов (PCA) — это общепринятая методика машинного обучения, который может быть применен toofeature выбора, классификации и аномалий обнаружения.</span><span class="sxs-lookup"><span data-stu-id="f96c2-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="f96c2-319">Этот тип анализа предусматривает преобразование набора сценариев с предположительно коррелированными переменными в набор значений, которые называются основными компонентами.</span><span class="sxs-lookup"><span data-stu-id="f96c2-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="f96c2-320">Идея ключа Hello моделирования на основе PCA данные tooproject на нижнем мерный пространство, чтобы компоненты и аномалии, можно легко определить.</span><span class="sxs-lookup"><span data-stu-id="f96c2-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="f96c2-321">Для каждого нового входного слишком hello модель обнаружения, обнаружения аномалий hello сначала вычисляет его проекции на собственных векторов hello, а затем вычисляет hello нормализовать реконструкции ошибки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="f96c2-322">Нормализованный ошибки, оценка аномалий hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="f96c2-323">Ошибка выше hello Hello, hello более hello экземпляр является.</span><span class="sxs-lookup"><span data-stu-id="f96c2-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="f96c2-324">В проблема обнаружения обслуживания hello каждая запись можно считать, что точки в пространстве с 3-мерная определяется велосипеда давление, engine нефти и температуры ядра координатами.</span><span class="sxs-lookup"><span data-stu-id="f96c2-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="f96c2-325">toocapture эти аномалии мы проекта hello исходных данных в пространстве объемного hello на двухмерного пространство с помощью PCA.</span><span class="sxs-lookup"><span data-stu-id="f96c2-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="f96c2-326">Таким образом рекомендуется задать для параметра hello количество компонентов toouse в PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="f96c2-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="f96c2-327">Этот параметр играет важную роль в обнаружении аномалий на основе анализа главных компонентов.</span><span class="sxs-lookup"><span data-stu-id="f96c2-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="f96c2-328">Спроецировав данные с использованием этого анализа, определить соответствующие аномалии намного проще.</span><span class="sxs-lookup"><span data-stu-id="f96c2-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="f96c2-329">**Модель обнаружения аномалий выборка** в модели обнаружения аномалий выборка hello, мы используем hello Выбор столбцов в наборе данных и аномалий на основе PCA модулей обнаружения аналогичным образом.</span><span class="sxs-lookup"><span data-stu-id="f96c2-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="f96c2-330">В частности, мы сначала извлечь три переменные - температуры ядра, вне температуры и скорости — с помощью hello **Выбор столбцов в наборе данных** модуля.</span><span class="sxs-lookup"><span data-stu-id="f96c2-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="f96c2-331">Также мы включаем скорость hello переменной, поскольку обычно является температуры ядра hello коррелированных toohello скорости.</span><span class="sxs-lookup"><span data-stu-id="f96c2-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="f96c2-332">Далее мы используем данные hello tooproject модуля обнаружения аномалий на основе PCA из 3-мерная пространства hello на двухмерного пространство.</span><span class="sxs-lookup"><span data-stu-id="f96c2-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="f96c2-333">удовлетворяются условия отзыва Hello и hello vehicle требует повторного вызова при температуры ядра и внешними температуры высокой отрицательно связаны.</span><span class="sxs-lookup"><span data-stu-id="f96c2-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="f96c2-334">Используя алгоритм обнаружения аномалий на основе PCA, можно свести аномалий hello после выполнения PCA.</span><span class="sxs-lookup"><span data-stu-id="f96c2-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="f96c2-335">При обучении любой модели, нам нужна обычные данные toouse, которая не требует обслуживания или отзыве как модель обнаружения аномалий на основе PCA hello tootrain hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="f96c2-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="f96c2-336">В hello оценки экспериментов мы используем toodetect модели обнаружения аномалий hello обучена ли hello vehicle требуется обслуживание или отзыва.</span><span class="sxs-lookup"><span data-stu-id="f96c2-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="f96c2-337">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="f96c2-337">Real-time analysis</span></span>
<span data-ttu-id="f96c2-338">использовать следующие SQL запросов Stream Analytics Hello tooget hello среднее всех hello важным средством таких параметров, как vehicle скорость, уровень топлива, температуры ядра, одометра чтения, нехватку велосипеда, нефти уровня ядра и другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="f96c2-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="f96c2-339">Hello средние значения, используемые toodetect аномалий, выдавать предупреждения, а также определить hello общей работоспособности условий эксплуатации в определенном регионе автомобилей и сопоставить его toodemographics.</span><span class="sxs-lookup"><span data-stu-id="f96c2-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Запрос Stream Analytics для обработки в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="f96c2-341">*Рис. 13. Запрос Stream Analytics для обработки в реальном времени*</span><span class="sxs-lookup"><span data-stu-id="f96c2-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="f96c2-342">Средние значения все hello вычисляются TumblingWindow 3 секунды.</span><span class="sxs-lookup"><span data-stu-id="f96c2-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="f96c2-343">Мы применили TubmlingWindow, так как необходимо использовать непересекающиеся последовательные интервалы времени.</span><span class="sxs-lookup"><span data-stu-id="f96c2-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="f96c2-344">Щелкните toolearn Дополнительные сведения о всеми возможностями «Над окнами» hello в Azure Stream Analytics [управления окнами (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="f96c2-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="f96c2-345">**Прогнозирование в режиме реального времени**</span><span class="sxs-lookup"><span data-stu-id="f96c2-345">**Real-time prediction**</span></span>

<span data-ttu-id="f96c2-346">Приложение включен в состав решения toooperationalize hello машинного обучения модели hello в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="f96c2-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="f96c2-347">Это приложение, называется «RealTimeDashboardApp» создается и настраивается в ходе развертывания решения hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="f96c2-348">приложение Hello выполняет hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f96c2-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="f96c2-349">Выполняет прослушивание экземпляр tooan концентратора событий, где Stream Analytics публикация hello событий в шаблоне постоянно.</span><span class="sxs-lookup"><span data-stu-id="f96c2-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="f96c2-350">![Запросов Stream Analytics для публикации данных hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *рис. 14 – запросов Stream Analytics для публикации данных tooan hello вывода экземпляра концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="f96c2-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="f96c2-351">Для каждого события, которое получает это приложение:</span><span class="sxs-lookup"><span data-stu-id="f96c2-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="f96c2-352">Процессы hello данные с помощью машины оценки запроса-ответа обучения (RR) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="f96c2-353">Конечная точка Hello записей Ресурсов, автоматически публикуется как часть развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="f96c2-354">выходные данные записи Ресурсов Hello — опубликованных tooa набора данных Power BI с помощью принудительной hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="f96c2-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="f96c2-355">Этот шаблон также является применимо tooscenarios, в котором нужно toointegrate строке из бизнес-приложения с потоком hello аналитика в реальном времени, для сценариев, таких как оповещения, уведомления и обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="f96c2-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="f96c2-356">Нажмите кнопку [RealtimeDashboardApp загрузки](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello решения RealtimeDashboardApp Visual Studio для настройки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="f96c2-357">**hello tooexecute приложении панели мониторинга в реальном времени**</span><span class="sxs-lookup"><span data-stu-id="f96c2-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="f96c2-358">Извлеките его и сохраните на локальном компьютере ![Папка RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Рис. 16. Папка RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="f96c2-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="f96c2-359">Выполните приложение hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="f96c2-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="f96c2-360">Укажите действительные учетные данные Power BI, войдите и нажмите кнопку "Принять".</span><span class="sxs-lookup"><span data-stu-id="f96c2-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Панель мониторинга в реальном времени приложения вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Приложение с панелью мониторинга в реальном времени окончания tooPower входа бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="f96c2-363">*Рисунок 17 — RealtimeDashboardApp: Вход tooPower бизнес-Аналитики*</span><span class="sxs-lookup"><span data-stu-id="f96c2-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="f96c2-364">Если вы хотите tooflush набора данных Power BI hello, выполните hello RealtimeDashboardApp с параметром «flushdata» hello:</span><span class="sxs-lookup"><span data-stu-id="f96c2-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="f96c2-365">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="f96c2-365">Batch analysis</span></span>
<span data-ttu-id="f96c2-366">Hello цель — tooshow как Contoso моторов использует hello вычислений Azure возможности tooharness больших данных toogain подробные сведения о на шаблон, использование поведения и работоспособности автомобиля.</span><span class="sxs-lookup"><span data-stu-id="f96c2-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="f96c2-367">Это позволяет:</span><span class="sxs-lookup"><span data-stu-id="f96c2-367">This makes it possible to:</span></span>

* <span data-ttu-id="f96c2-368">Повышение качества hello и сделать его дешевле, предоставляя аналитические данные на привычки и топливо эффективный определяющим поведения</span><span class="sxs-lookup"><span data-stu-id="f96c2-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="f96c2-369">Ознакомьтесь с заранее клиентов и определяющим шаблонов toogovern бизнес-решения и предоставьте hello лучше всего в класс продукты и услуги</span><span class="sxs-lookup"><span data-stu-id="f96c2-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="f96c2-370">В данном решении мы ожидаем hello следующие метрики:</span><span class="sxs-lookup"><span data-stu-id="f96c2-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="f96c2-371">**Агрессивная пешком поведение**: Определяет тренд hello hello моделей, расположения, определяющим условия и время средств анализа toogain год hello агрессивной определяющим шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f96c2-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="f96c2-372">Contoso Motors сможет использовать ее в маркетинговых кампаниях, чтобы предлагать новые персонализированные функции и умное страхование.</span><span class="sxs-lookup"><span data-stu-id="f96c2-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="f96c2-373">**Задают ритм для эффективного определяющим поведение**: Определяет тренд hello hello моделей, расположения, определяющим условия и время hello аналитики toogain год на топливо эффективный определяющим шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f96c2-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="f96c2-374">Contoso моторов можно использовать эти знания для маркетинговых кампаний, пешком новые функции и упреждающее отчетов toohello драйверы для стоимости начала и среде понятное определяющим привычки.</span><span class="sxs-lookup"><span data-stu-id="f96c2-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="f96c2-375">**Отозвать моделей**: Определяет моделей требуется отзывы, ввод в эксплуатацию эксперимента машинного обучения для обнаружения аномалий hello</span><span class="sxs-lookup"><span data-stu-id="f96c2-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="f96c2-376">Давайте посмотрим hello Дополнительные сведения о каждой из этих метрик</span><span class="sxs-lookup"><span data-stu-id="f96c2-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="f96c2-377">**Шаблон агрессивного вождения**</span><span class="sxs-lookup"><span data-stu-id="f96c2-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="f96c2-378">Hello секционированы vehicle сигналов и диагностических данных обрабатываются в конвейере hello с именем «AggresiveDrivingPatternPipeline» с использованием моделей hello toodetermine Hive, расположение, автомобиль, пешком условия и другие параметры, которые видно агрессивной определяющим шаблон.</span><span class="sxs-lookup"><span data-stu-id="f96c2-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="f96c2-379">![Рабочий процесс для шаблона агрессивного вождения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Рис. 18. Рабочий процесс для шаблона агрессивного вождения*</span><span class="sxs-lookup"><span data-stu-id="f96c2-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="f96c2-380">***Запрос Hive для шаблона агрессивного вождения***</span><span class="sxs-lookup"><span data-stu-id="f96c2-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="f96c2-381">Hello скрипта Hive с именем «aggresivedriving.hql», используемое для анализа агрессивной определяющим условие шаблон находится в папке «\demo\src\connectedcar\scripts» hello загружен zip.</span><span class="sxs-lookup"><span data-stu-id="f96c2-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="f96c2-382">Она использует сочетание hello автомобилей передачи шестеренки позиции, педали состояние тормоза и скорость toodetect бы безрассудным/агрессивной пешком поведение в зависимости от тормозным шаблон с высокой скоростью.</span><span class="sxs-lookup"><span data-stu-id="f96c2-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="f96c2-383">После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Выходные данные AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="f96c2-385">*Рис. 19. Выходные данные AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="f96c2-386">**Шаблон вождения для экономии топлива**</span><span class="sxs-lookup"><span data-stu-id="f96c2-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="f96c2-387">Hello секционированы vehicle сигналов и диагностических данных обрабатываются в конвейере hello с именем «FuelEfficientDrivingPatternPipeline».</span><span class="sxs-lookup"><span data-stu-id="f96c2-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="f96c2-388">Куст — моделей используется toodetermine hello, расположение, vehicle, определяющим условия и другие свойства, которые демонстрировал топливо эффективный определяющим.</span><span class="sxs-lookup"><span data-stu-id="f96c2-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Шаблон вождения для экономии топлива](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="f96c2-390">*Рис. 20. Рабочий процесс для шаблона вождения, позволяющего экономить топливо*</span><span class="sxs-lookup"><span data-stu-id="f96c2-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="f96c2-391">***Запрос Hive для шаблона вождения, позволяющего экономить топливо***</span><span class="sxs-lookup"><span data-stu-id="f96c2-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="f96c2-392">Hello скрипта Hive с именем «fuelefficientdriving.hql», используемое для анализа агрессивной определяющим условие шаблон находится в папке «\demo\src\connectedcar\scripts» hello загружен zip.</span><span class="sxs-lookup"><span data-stu-id="f96c2-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="f96c2-393">Он использует сочетание hello передачи шестеренки положение автомобилей, тормоза педали состояния, скорость и сочетаний клавиш педали позиции toodetect топливо эффективный определяющим поведение на основании ускорение, тормозным, и ускорить шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f96c2-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="f96c2-394">После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Выходные данные FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="f96c2-396">*Рис. 21. Выходные данные FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="f96c2-397">**Прогнозы для отзыва**</span><span class="sxs-lookup"><span data-stu-id="f96c2-397">**Recall Predictions**</span></span>

<span data-ttu-id="f96c2-398">Подготовленная и опубликованы как веб-службы в ходе развертывания решения hello Hello эксперимента машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="f96c2-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="f96c2-399">Hello массовой оценки конечной точки используется в этом рабочем процессе, регистрируются в качестве данных связанной службы фабрики и введенную, используя действие оценки пакета фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="f96c2-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Конечная точка машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="f96c2-401">*Рис. 22. Конечная точка машинного обучения, зарегистрированная в качестве связанной службы в фабрике данных*</span><span class="sxs-lookup"><span data-stu-id="f96c2-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="f96c2-402">Hello зарегистрированной связанной службы используется в hello DetectAnomalyPipeline tooscore hello данных с помощью модели обнаружения аномалий hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Пакетная оценка в фабрике данных в рамках Машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="f96c2-404">*Рис. 23. Пакетная оценка в фабрике данных в рамках Машинного обучения Azure*</span><span class="sxs-lookup"><span data-stu-id="f96c2-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="f96c2-405">Существуют несколько шагов, выполненных в этом конвейере для подготовки данных, чтобы его можно введенную с hello массовой оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f96c2-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="f96c2-407">*Рис. 24. DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей*</span><span class="sxs-lookup"><span data-stu-id="f96c2-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="f96c2-408">***Запрос Hive для обнаружения аномалий***</span><span class="sxs-lookup"><span data-stu-id="f96c2-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="f96c2-409">После завершения оценки hello действие HDInsight — используется tooprocess и hello статистические данные, которые классифицируются как аномалии hello модели с оценкой вероятности 0.60 или выше.</span><span class="sxs-lookup"><span data-stu-id="f96c2-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="f96c2-410">После успешного выполнения конвейера hello можно увидеть hello, следуя секций, создаваемых в вашей учетной записи хранения в контейнере «connectedcar» hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Выходные данные DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="f96c2-412">*Рис. 25. Выходные данные DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="f96c2-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="f96c2-413">Опубликовать</span><span class="sxs-lookup"><span data-stu-id="f96c2-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="f96c2-414">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="f96c2-414">Real-time analysis</span></span>
<span data-ttu-id="f96c2-415">Один из запросов hello в задании Stream Analytics hello публикует выход tooan hello события экземпляра концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f96c2-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Задание Stream Analytics публикует выход tooan экземпляра концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="f96c2-417">*Рис. 26 — задание Stream Analytics публикует выход tooan экземпляра концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="f96c2-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Stream Analytics запроса toopublish toohello вывода экземпляра концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="f96c2-419">*Рис. 27 — экземпляр концентратора событий вывода toohello toopublish запросов Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="f96c2-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="f96c2-420">Этот поток событий используются hello RealTimeDashboardApp, включенный в решении hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="f96c2-421">Это приложение использует hello машины обучения запрос-ответ веб-службы для оценки в режиме реального времени и публикует hello результирующие данные tooa Power BI набор данных для потребления.</span><span class="sxs-lookup"><span data-stu-id="f96c2-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="f96c2-422">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="f96c2-422">Batch analysis</span></span>
<span data-ttu-id="f96c2-423">результаты Hello hello пакета и в режиме реального времени обработки, toohello опубликованных таблиц базы данных SQL Azure для потребления.</span><span class="sxs-lookup"><span data-stu-id="f96c2-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="f96c2-424">Hello Azure SQL Server, базы данных и таблицы hello автоматически создаются как часть сценария установки hello.</span><span class="sxs-lookup"><span data-stu-id="f96c2-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Результаты пакетной обработки скопировать рабочий процесс Киоск toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="f96c2-426">*Рис. 28 – пакетной обработки toodata Киоск результаты копирование рабочего процесса*</span><span class="sxs-lookup"><span data-stu-id="f96c2-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Задание Stream Analytics публикует toodata киоска](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="f96c2-428">*Рис. 29 — задание Stream Analytics публикует toodata киоска*</span><span class="sxs-lookup"><span data-stu-id="f96c2-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Настройка киоска данных в задании Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="f96c2-430">*Рис. 30. Настройка киоска данных в задании Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="f96c2-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="f96c2-431">Использование</span><span class="sxs-lookup"><span data-stu-id="f96c2-431">Consume</span></span>
<span data-ttu-id="f96c2-432">Power BI предоставляет для этого решения расширенную панель мониторинга, предназначенную для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="f96c2-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="f96c2-433">Подробные инструкции по настройке hello Power BI отчеты и панели мониторинга hello, щелкните здесь.</span><span class="sxs-lookup"><span data-stu-id="f96c2-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="f96c2-434">Окончательный мониторинга Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f96c2-434">hello final dashboard looks like this:</span></span>

![Информационная панель Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="f96c2-436">*Рис. 31. Информационная панель Power BI*</span><span class="sxs-lookup"><span data-stu-id="f96c2-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="f96c2-437">Сводка</span><span class="sxs-lookup"><span data-stu-id="f96c2-437">Summary</span></span>
<span data-ttu-id="f96c2-438">Этот документ содержит подробные детализация hello решения для анализа телеметрии автомобиля.</span><span class="sxs-lookup"><span data-stu-id="f96c2-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="f96c2-439">Здесь показан шаблон лямбда-архитектуры для анализа в режиме реального времени и пакетного анализа с прогнозами и действиями.</span><span class="sxs-lookup"><span data-stu-id="f96c2-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="f96c2-440">Эта схема применяется tooa разнообразные варианты использования, которые требуют Горячий путь (в реальном времени) и аналитика холодного путь (пакет).</span><span class="sxs-lookup"><span data-stu-id="f96c2-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

