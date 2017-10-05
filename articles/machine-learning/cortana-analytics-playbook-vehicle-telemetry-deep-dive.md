---
title: "Подробный обзор прогнозирования исправности автомобиля и манеры вождения с помощью Azure | Документация Майкрософт"
description: "Используйте возможности Cortana Intelligence, чтобы получить прогнозы и актуальную информацию об исправности и манере вождения автомобиля в режиме реального времени."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="d86d6-103">Сборник тренировочных заданий по решению для аналитики телеметрии автомобиля. Подробный обзор решения</span><span class="sxs-lookup"><span data-stu-id="d86d6-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="d86d6-104">В этом **меню** содержатся ссылки на разделы сборника тренировочных заданий:</span><span class="sxs-lookup"><span data-stu-id="d86d6-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="d86d6-105">В этом разделе детально рассматривается каждый этап, входящий в архитектуру решения, с инструкциями и ссылками для настройки.</span><span class="sxs-lookup"><span data-stu-id="d86d6-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="d86d6-106">Источники данных</span><span class="sxs-lookup"><span data-stu-id="d86d6-106">Data Sources</span></span>
<span data-ttu-id="d86d6-107">Это решение предусматривает использование двух разных источников данных:</span><span class="sxs-lookup"><span data-stu-id="d86d6-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="d86d6-108">**имитированные сигналы автомобиля и набор диагностических данных** ;</span><span class="sxs-lookup"><span data-stu-id="d86d6-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="d86d6-109">**каталог автомобилей.**</span><span class="sxs-lookup"><span data-stu-id="d86d6-109">**vehicle catalog**</span></span>

<span data-ttu-id="d86d6-110">В это решение входит симулятор телематики автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="d86d6-111">Он выдает диагностическую информацию и сигналы, соответствующие состоянию автомобиля и манере вождения в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="d86d6-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="d86d6-112">Щелкните [здесь](http://go.microsoft.com/fwlink/?LinkId=717075) , чтобы скачать **решение Visual Studio симулятора телематики автомобиля** для настройки в соответствии со своими требованиями.</span><span class="sxs-lookup"><span data-stu-id="d86d6-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="d86d6-113">Каталог автомобилей содержит справочный набор данных для сопоставления идентификационного номера (VIN) с моделью автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Симулятор телематики автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="d86d6-115">*Рис. 1. Симулятор телематики автомобиля*</span><span class="sxs-lookup"><span data-stu-id="d86d6-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="d86d6-116">Это набор данных в формате JSON, содержащий следующую схему.</span><span class="sxs-lookup"><span data-stu-id="d86d6-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="d86d6-117">столбец</span><span class="sxs-lookup"><span data-stu-id="d86d6-117">Column</span></span> | <span data-ttu-id="d86d6-118">Описание</span><span class="sxs-lookup"><span data-stu-id="d86d6-118">Description</span></span> | <span data-ttu-id="d86d6-119">Значения</span><span class="sxs-lookup"><span data-stu-id="d86d6-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d86d6-120">VIN</span><span class="sxs-lookup"><span data-stu-id="d86d6-120">VIN</span></span> |<span data-ttu-id="d86d6-121">Случайно сгенерированный идентификационный номер автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="d86d6-122">Его можно получить из главного списка 10 000 случайно сгенерированных идентификационных номеров автомобилей</span><span class="sxs-lookup"><span data-stu-id="d86d6-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="d86d6-123">outsideTemperature</span><span class="sxs-lookup"><span data-stu-id="d86d6-123">Outside temperature</span></span> |<span data-ttu-id="d86d6-124">Наружная температура, при которой движется автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="d86d6-125">Случайно сгенерированное число от 0 до 100</span><span class="sxs-lookup"><span data-stu-id="d86d6-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="d86d6-126">engineTemperature</span><span class="sxs-lookup"><span data-stu-id="d86d6-126">Engine temperature</span></span> |<span data-ttu-id="d86d6-127">Температура двигателя автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="d86d6-128">Случайно сгенерированное число от 0 до 500</span><span class="sxs-lookup"><span data-stu-id="d86d6-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="d86d6-129">Speed</span><span class="sxs-lookup"><span data-stu-id="d86d6-129">Speed</span></span> |<span data-ttu-id="d86d6-130">Частота вращения двигателя, с которой движется автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="d86d6-131">Случайно сгенерированное число от 0 до 100</span><span class="sxs-lookup"><span data-stu-id="d86d6-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="d86d6-132">fuel</span><span class="sxs-lookup"><span data-stu-id="d86d6-132">Fuel</span></span> |<span data-ttu-id="d86d6-133">Уровень топлива в автомобиле</span><span class="sxs-lookup"><span data-stu-id="d86d6-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="d86d6-134">Случайно сгенерированное число от 0 до 100 (указывает уровень топлива в процентах)</span><span class="sxs-lookup"><span data-stu-id="d86d6-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="d86d6-135">engineoil</span><span class="sxs-lookup"><span data-stu-id="d86d6-135">EngineOil</span></span> |<span data-ttu-id="d86d6-136">Уровень моторного масла в автомобиле</span><span class="sxs-lookup"><span data-stu-id="d86d6-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="d86d6-137">Случайно сгенерированное число от 0 до 100 (указывает уровень моторного масла в процентах)</span><span class="sxs-lookup"><span data-stu-id="d86d6-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="d86d6-138">Давление в шинах</span><span class="sxs-lookup"><span data-stu-id="d86d6-138">Tire pressure</span></span> |<span data-ttu-id="d86d6-139">Давление в шинах автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="d86d6-140">Случайно сгенерированное число от 0 до 50 (указывает уровень давления в шинах в процентах)</span><span class="sxs-lookup"><span data-stu-id="d86d6-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="d86d6-141">odometer</span><span class="sxs-lookup"><span data-stu-id="d86d6-141">Odometer</span></span> |<span data-ttu-id="d86d6-142">Показания одометра автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="d86d6-143">Случайно сгенерированное число от 0 до 200 000</span><span class="sxs-lookup"><span data-stu-id="d86d6-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="d86d6-144">accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="d86d6-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="d86d6-145">Положение педали газа автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="d86d6-146">Случайно сгенерированное число от 0 до 100 (указывает уровень, соответствующий положению педали газа, в процентах)</span><span class="sxs-lookup"><span data-stu-id="d86d6-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="d86d6-147">parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="d86d6-147">Parking_brake_status</span></span> |<span data-ttu-id="d86d6-148">Указывает, припаркован ли автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="d86d6-149">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-149">True or False</span></span> |
| <span data-ttu-id="d86d6-150">headlamp_status</span><span class="sxs-lookup"><span data-stu-id="d86d6-150">Headlamp_status</span></span> |<span data-ttu-id="d86d6-151">Указывает, включена ли головная фара</span><span class="sxs-lookup"><span data-stu-id="d86d6-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="d86d6-152">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-152">True or False</span></span> |
| <span data-ttu-id="d86d6-153">brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="d86d6-153">Brake_pedal_status</span></span> |<span data-ttu-id="d86d6-154">Указывает, нажата ли педаль тормоза</span><span class="sxs-lookup"><span data-stu-id="d86d6-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="d86d6-155">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-155">True or False</span></span> |
| <span data-ttu-id="d86d6-156">transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="d86d6-156">Transmission_gear_position</span></span> |<span data-ttu-id="d86d6-157">Включенная передача коробки передач автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="d86d6-158">Состояния: first, second, third, fourth, fifth, sixth, seventh, eighth</span><span class="sxs-lookup"><span data-stu-id="d86d6-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="d86d6-159">ignition_status</span><span class="sxs-lookup"><span data-stu-id="d86d6-159">Ignition_status</span></span> |<span data-ttu-id="d86d6-160">Указывает, движется ли автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="d86d6-161">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-161">True or False</span></span> |
| <span data-ttu-id="d86d6-162">windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="d86d6-162">Windshield_wiper_status</span></span> |<span data-ttu-id="d86d6-163">Указывает, включен ли стеклоочиститель ветрового стекла</span><span class="sxs-lookup"><span data-stu-id="d86d6-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="d86d6-164">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-164">True or False</span></span> |
| <span data-ttu-id="d86d6-165">ABS</span><span class="sxs-lookup"><span data-stu-id="d86d6-165">ABS</span></span> |<span data-ttu-id="d86d6-166">Указывает, включена ли антиблокировочная система тормозов</span><span class="sxs-lookup"><span data-stu-id="d86d6-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="d86d6-167">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="d86d6-167">True or False</span></span> |
| <span data-ttu-id="d86d6-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="d86d6-168">Timestamp</span></span> |<span data-ttu-id="d86d6-169">Метка времени создания точки данных</span><span class="sxs-lookup"><span data-stu-id="d86d6-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="d86d6-170">Дата</span><span class="sxs-lookup"><span data-stu-id="d86d6-170">Date</span></span> |
| <span data-ttu-id="d86d6-171">City</span><span class="sxs-lookup"><span data-stu-id="d86d6-171">City</span></span> |<span data-ttu-id="d86d6-172">Расположение автомобиля</span><span class="sxs-lookup"><span data-stu-id="d86d6-172">The location of the vehicle</span></span> |<span data-ttu-id="d86d6-173">В этом решении представлены 4 города: Бельвью, Редмонд, Саммамиш и Сиэтл</span><span class="sxs-lookup"><span data-stu-id="d86d6-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="d86d6-174">Справочный набор данных модели автомобиля позволяет сопоставить VIN с моделью.</span><span class="sxs-lookup"><span data-stu-id="d86d6-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="d86d6-175">VIN</span><span class="sxs-lookup"><span data-stu-id="d86d6-175">VIN</span></span> | <span data-ttu-id="d86d6-176">Модель</span><span class="sxs-lookup"><span data-stu-id="d86d6-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="d86d6-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="d86d6-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="d86d6-178">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-178">Sedan</span></span> |
| <span data-ttu-id="d86d6-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="d86d6-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="d86d6-180">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-180">Hybrid</span></span> |
| <span data-ttu-id="d86d6-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="d86d6-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="d86d6-182">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-182">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="d86d6-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="d86d6-184">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-184">Sedan</span></span> |
| <span data-ttu-id="d86d6-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="d86d6-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="d86d6-186">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-186">Hybrid</span></span> |
| <span data-ttu-id="d86d6-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="d86d6-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="d86d6-188">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-188">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="d86d6-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="d86d6-190">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-190">Sedan</span></span> |
| <span data-ttu-id="d86d6-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="d86d6-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="d86d6-192">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-192">Hybrid</span></span> |
| <span data-ttu-id="d86d6-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="d86d6-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="d86d6-194">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-194">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="d86d6-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="d86d6-196">Автомобиль с откидным верхом</span><span class="sxs-lookup"><span data-stu-id="d86d6-196">Convertible</span></span> |
| <span data-ttu-id="d86d6-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="d86d6-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="d86d6-198">Автомобиль с кузовом «универсал»</span><span class="sxs-lookup"><span data-stu-id="d86d6-198">Station Wagon</span></span> |
| <span data-ttu-id="d86d6-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="d86d6-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="d86d6-200">Малогабаритный автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-200">Compact Car</span></span> |
| <span data-ttu-id="d86d6-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="d86d6-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="d86d6-202">Небольшой внедорожник</span><span class="sxs-lookup"><span data-stu-id="d86d6-202">Small SUV</span></span> |
| <span data-ttu-id="d86d6-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="d86d6-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="d86d6-204">Спортивный автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-204">Sports Car</span></span> |
| <span data-ttu-id="d86d6-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="d86d6-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="d86d6-206">Внедорожник среднего размера</span><span class="sxs-lookup"><span data-stu-id="d86d6-206">Medium SUV</span></span> |
| <span data-ttu-id="d86d6-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="d86d6-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="d86d6-208">Автомобиль с кузовом «универсал»</span><span class="sxs-lookup"><span data-stu-id="d86d6-208">Station Wagon</span></span> |
| <span data-ttu-id="d86d6-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="d86d6-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="d86d6-210">Большой внедорожник</span><span class="sxs-lookup"><span data-stu-id="d86d6-210">Large SUV</span></span> |
| <span data-ttu-id="d86d6-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="d86d6-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="d86d6-212">Большой внедорожник</span><span class="sxs-lookup"><span data-stu-id="d86d6-212">Large SUV</span></span> |
| <span data-ttu-id="d86d6-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="d86d6-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="d86d6-214">Двухместный легковой автомобиль</span><span class="sxs-lookup"><span data-stu-id="d86d6-214">Coupe</span></span> |
| <span data-ttu-id="d86d6-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="d86d6-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="d86d6-216">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-216">Sedan</span></span> |
| <span data-ttu-id="d86d6-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="d86d6-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="d86d6-218">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-218">Hybrid</span></span> |
| <span data-ttu-id="d86d6-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="d86d6-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="d86d6-220">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-220">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="d86d6-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="d86d6-222">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-222">Sedan</span></span> |
| <span data-ttu-id="d86d6-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="d86d6-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="d86d6-224">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-224">Hybrid</span></span> |
| <span data-ttu-id="d86d6-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="d86d6-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="d86d6-226">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-226">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="d86d6-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="d86d6-228">Седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-228">Sedan</span></span> |
| <span data-ttu-id="d86d6-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="d86d6-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="d86d6-230">Гибридная среда</span><span class="sxs-lookup"><span data-stu-id="d86d6-230">Hybrid</span></span> |
| <span data-ttu-id="d86d6-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="d86d6-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="d86d6-232">Семейный седан</span><span class="sxs-lookup"><span data-stu-id="d86d6-232">Family Saloon</span></span> |
| <span data-ttu-id="d86d6-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="d86d6-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="d86d6-234">Автомобиль с откидным верхом</span><span class="sxs-lookup"><span data-stu-id="d86d6-234">Convertible</span></span> |
| <span data-ttu-id="d86d6-235">…….</span><span class="sxs-lookup"><span data-stu-id="d86d6-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="d86d6-236">Ссылки</span><span class="sxs-lookup"><span data-stu-id="d86d6-236">References</span></span>
[<span data-ttu-id="d86d6-237">Решение Visual Studio "Симулятор телематики автомобиля"</span><span class="sxs-lookup"><span data-stu-id="d86d6-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="d86d6-238">Концентратор событий Azure</span><span class="sxs-lookup"><span data-stu-id="d86d6-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="d86d6-239">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="d86d6-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="d86d6-240">Прием</span><span class="sxs-lookup"><span data-stu-id="d86d6-240">Ingestion</span></span>
<span data-ttu-id="d86d6-241">Для принятия сигналов автомобиля, событий диагностики, анализа в режиме реального времени и пакетного анализа используется сочетание концентраторов событий Azure, Stream Analytics и фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d86d6-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="d86d6-242">Все эти компоненты создаются и настраиваются как часть развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="d86d6-243">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="d86d6-243">Real-time analysis</span></span>
<span data-ttu-id="d86d6-244">События, создаваемые симулятором телематики автомобиля, публикуются в концентраторе событий с помощью пакета SDK для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="d86d6-245">Задание Stream Analytics принимает эти события из концентратора событий и обрабатывает данные в режиме реального времени для анализа работоспособности автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Панель мониторинга концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="d86d6-247">*Рис. 4. Панель мониторинга концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="d86d6-247">*Figure 4 - Event Hub dashboard*</span></span>

![Обработка данных заданием Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="d86d6-249">*Рис. 5. Обработка данных заданием Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="d86d6-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="d86d6-250">Задания Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="d86d6-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="d86d6-251">принимает данные из концентратора событий;</span><span class="sxs-lookup"><span data-stu-id="d86d6-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="d86d6-252">объединяет их со справочными данными для сопоставления VIN автомобиля с соответствующей моделью;</span><span class="sxs-lookup"><span data-stu-id="d86d6-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="d86d6-253">сохраняет эти данные в хранилище BLOB-объектов для расширенного пакетного анализа.</span><span class="sxs-lookup"><span data-stu-id="d86d6-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="d86d6-254">Следующий запрос Stream Analytics используется для хранения данных в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d86d6-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Запрос задания Stream Analytics для приема данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="d86d6-256">*Рис. 6. Запрос задания Stream Analytics для приема данных*</span><span class="sxs-lookup"><span data-stu-id="d86d6-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="d86d6-257">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="d86d6-257">Batch analysis</span></span>
<span data-ttu-id="d86d6-258">Для расширенного пакетного анализа необходимо создать дополнительное количество имитированных сигналов автомобиля и набор диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="d86d6-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="d86d6-259">Это необходимо для предоставления достаточного объема репрезентативных данных для пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="d86d6-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="d86d6-260">С этой целью в рабочем процессе фабрики данных Azure используется конвейер PrepareSampleDataPipeline для создания имитированных сигналов автомобиля и набора диагностических данных за год.</span><span class="sxs-lookup"><span data-stu-id="d86d6-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="d86d6-261">Щелкните [здесь](http://go.microsoft.com/fwlink/?LinkId=717077) , чтобы скачать решение Visual Studio настраиваемого действия DotNet фабрики данных для настройки в соответствии со своими требованиями.</span><span class="sxs-lookup"><span data-stu-id="d86d6-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Подготовка образца данных для рабочего процесса пакетной обработки](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="d86d6-263">*Рис. 7. Подготовка образца данных для рабочего процесса пакетной обработки*</span><span class="sxs-lookup"><span data-stu-id="d86d6-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="d86d6-264">Конвейер состоит из настраиваемого действия .NET фабрики данных Azure, указанного ниже.</span><span class="sxs-lookup"><span data-stu-id="d86d6-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Действие PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="d86d6-266">*Рис. 8. PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="d86d6-267">После того как конвейер успешно выполнит это действие и набор данных RawCarEventsTable будет помечен как Ready, создаются имитированные сигналы автомобиля и диагностические данные за год.</span><span class="sxs-lookup"><span data-stu-id="d86d6-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="d86d6-268">Затем в вашей учетной записи хранения в контейнере connectedcar будут созданы следующие папка и файл:</span><span class="sxs-lookup"><span data-stu-id="d86d6-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![Выходные данные PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="d86d6-270">*Рис. 9. Выходные данные PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="d86d6-271">Ссылки</span><span class="sxs-lookup"><span data-stu-id="d86d6-271">References</span></span>
[<span data-ttu-id="d86d6-272">Пакет SDK концентратора событий Azure для приема потока</span><span class="sxs-lookup"><span data-stu-id="d86d6-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="d86d6-273">[Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md)
[Использование настраиваемых действий в конвейере фабрики данных Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="d86d6-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="d86d6-274">Решение Visual Studio "Действие DotNet фабрики данных Azure" для подготовки примера данных</span><span class="sxs-lookup"><span data-stu-id="d86d6-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="d86d6-275">Секционирование набора данных</span><span class="sxs-lookup"><span data-stu-id="d86d6-275">Partition the dataset</span></span>
<span data-ttu-id="d86d6-276">На этапе подготовки данных необработанные полуструктурированные сигналы автомобиля и набор диагностических данных секционируются по годам и месяцам.</span><span class="sxs-lookup"><span data-stu-id="d86d6-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="d86d6-277">Секционирование обеспечивает более эффективное выполнение запросов и долговременное масштабируемое хранение, позволяя переходить от одной учетной записи хранения больших двоичных объектов к другой после заполнения первой.</span><span class="sxs-lookup"><span data-stu-id="d86d6-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="d86d6-278">Этот этап решения применяется только для пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="d86d6-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="d86d6-279">Управление входными и выходными данными:</span><span class="sxs-lookup"><span data-stu-id="d86d6-279">Input and output data data management:</span></span>

* <span data-ttu-id="d86d6-280">**Выходные данные** (с меткой *PartitionedCarEventsTable*) в течение длительного периода времени хранятся в виде фундаментальных данных или данных rawest в Data Lake заказчика.</span><span class="sxs-lookup"><span data-stu-id="d86d6-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="d86d6-281">**Входные данные** для этого конвейера обычно отклоняются, так как выходные данные полностью с ними совпадают — они лучше хранятся (секционируются) для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="d86d6-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Рабочий процесс секционирования событий автомобиля](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="d86d6-283">*Рис. 10. Рабочий процесс секционирования событий автомобиля*</span><span class="sxs-lookup"><span data-stu-id="d86d6-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="d86d6-284">Необработанные данные секционируются с помощью действия Hive HDInsight в PartitionCarEventsPipeline.</span><span class="sxs-lookup"><span data-stu-id="d86d6-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="d86d6-285">Образец данных, созданный на шаге 1 для параметра года, секционируется по годам и месяцам.</span><span class="sxs-lookup"><span data-stu-id="d86d6-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="d86d6-286">Секции используются для создания сигналов транспортного средства и диагностических данных для каждого месяца (всего 12 секций) года.</span><span class="sxs-lookup"><span data-stu-id="d86d6-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Действие PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="d86d6-288">*Рис. 11. PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="d86d6-289">***Сценарий Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="d86d6-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="d86d6-290">Следующий скрипт Hive с именем partitioncarevents.hql используется для секционирования и расположен в папке \demo\src\connectedcar\scripts скачанного ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="d86d6-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="d86d6-291">После успешного выполнения конвейера отобразятся следующие секции, созданные в учетной записи хранения в контейнере connectedcar.</span><span class="sxs-lookup"><span data-stu-id="d86d6-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Секционированные выходные данные](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="d86d6-293">*Рис. 12. Секционированные выходные данные*</span><span class="sxs-lookup"><span data-stu-id="d86d6-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="d86d6-294">Теперь данные оптимизированы, более управляемы и готовы для дальнейшей обработки и выполнения расширенного пакетного анализа.</span><span class="sxs-lookup"><span data-stu-id="d86d6-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="d86d6-295">Анализ данных</span><span class="sxs-lookup"><span data-stu-id="d86d6-295">Data Analysis</span></span>
<span data-ttu-id="d86d6-296">В этом разделе рассматривается использование сочетания Azure Stream Analytics, Машинного обучения Azure, фабрики данных Azure и Azure HDInsight для расширенного анализа работоспособности и манер вождения автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="d86d6-297">Здесь содержатся три подраздела:</span><span class="sxs-lookup"><span data-stu-id="d86d6-297">There are three subsections here:</span></span>

1. <span data-ttu-id="d86d6-298">**Машинное обучение.** В этом подразделе содержатся сведения об эксперименте обнаружения аномалий, проведенном в этом решении для прогнозирования необходимости технического обслуживания и отзывов из-за проблем безопасности для автомобилей.</span><span class="sxs-lookup"><span data-stu-id="d86d6-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="d86d6-299">**Анализ в режиме реального времени.** В этом подразделе содержатся сведения об аналитике в режиме реального времени с использованием языка запросов Stream Analytics и выполнении эксперимента машинного обучения в режиме реального времени с помощью пользовательского приложения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="d86d6-300">**Пакетный анализ.** В этом подразделе содержатся сведения о преобразовании и обработке данных пакета с помощью Azure HDInsight и Машинного обучения Azure, используемых в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d86d6-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="d86d6-301">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="d86d6-301">Machine Learning</span></span>
<span data-ttu-id="d86d6-302">Здесь наша цель заключается в прогнозировании того, для каких автомобилей необходимо провести обслуживание или какие из них нужно отозвать на основе определенных статистических данных о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="d86d6-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="d86d6-303">Предположим следующее.</span><span class="sxs-lookup"><span data-stu-id="d86d6-303">We make the following assumptions</span></span>

* <span data-ttu-id="d86d6-304">**Техническое обслуживание**автомобиля требуется при одном из условий:</span><span class="sxs-lookup"><span data-stu-id="d86d6-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="d86d6-305">низкое давление в шине;</span><span class="sxs-lookup"><span data-stu-id="d86d6-305">Tire pressure is low</span></span>
  * <span data-ttu-id="d86d6-306">низкий уровень моторного масла;</span><span class="sxs-lookup"><span data-stu-id="d86d6-306">Engine oil level is low</span></span>
  * <span data-ttu-id="d86d6-307">высокая температура двигателя.</span><span class="sxs-lookup"><span data-stu-id="d86d6-307">Engine temperature is high</span></span>
* <span data-ttu-id="d86d6-308">Может возникнуть **проблема безопасности** автомобиля, что требует **отзыва** при одном из условий:</span><span class="sxs-lookup"><span data-stu-id="d86d6-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="d86d6-309">высокая температура двигателя, но низкая наружная температура;</span><span class="sxs-lookup"><span data-stu-id="d86d6-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="d86d6-310">низкая температура двигателя, но высокая наружная температура.</span><span class="sxs-lookup"><span data-stu-id="d86d6-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="d86d6-311">Чтобы выявить аномалии, мы создали две отдельные модели на основе предыдущих условий: для определения необходимости в обслуживании и необходимости в отзыве автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="d86d6-312">Для обнаружения аномалий обе модели используют встроенный алгоритм анализа главных компонентов.</span><span class="sxs-lookup"><span data-stu-id="d86d6-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="d86d6-313">**Модель определения необходимости в обслуживании**</span><span class="sxs-lookup"><span data-stu-id="d86d6-313">**Maintenance detection model**</span></span>

<span data-ttu-id="d86d6-314">Эта модель сообщает об аномалии, если один из трех показателей, а именно давление в шинах, уровень моторного масла или температура двигателя, отвечает соответствующему условию.</span><span class="sxs-lookup"><span data-stu-id="d86d6-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="d86d6-315">Поэтому при создании модели необходимо учесть только эти три переменные.</span><span class="sxs-lookup"><span data-stu-id="d86d6-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="d86d6-316">В эксперименте в Машинном обучении Azure сначала мы используем модуль **Выбор столбцов в наборе данных** , чтобы извлечь эти три переменные.</span><span class="sxs-lookup"><span data-stu-id="d86d6-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="d86d6-317">Затем мы используем модуль обнаружения аномалий на основе алгоритма анализа главных компонентов, чтобы создать модель обнаружения аномалий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="d86d6-318">Анализ главных компонентов — это общепринятый метод машинного обучения, который можно использовать при выборе признаков, классификации и обнаружении аномалий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="d86d6-319">Этот тип анализа предусматривает преобразование набора сценариев с предположительно коррелированными переменными в набор значений, которые называются основными компонентами.</span><span class="sxs-lookup"><span data-stu-id="d86d6-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="d86d6-320">Основная идея моделирования на основе анализа главных компонентов заключается в том, чтобы проецировать данные в пространстве меньшей размерности, упростив определение признаков и аномалий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="d86d6-321">Для каждого нового фрагмента входных данных в модели обнаружения сначала рассчитывается проекция на основе собственных векторов, а затем вычисляется нормализованная ошибка восстановления.</span><span class="sxs-lookup"><span data-stu-id="d86d6-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="d86d6-322">Нормализованная ошибка представляет собой показатель аномалии.</span><span class="sxs-lookup"><span data-stu-id="d86d6-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="d86d6-323">Чем больше значение ошибки, тем больше аномалий в экземпляре.</span><span class="sxs-lookup"><span data-stu-id="d86d6-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="d86d6-324">При обнаружении необходимости в обслуживании каждую запись можно рассматривать в качестве точки в трехмерном пространстве. Ее определяют показатели давления в шинах, уровня моторного масла и температуры двигателя.</span><span class="sxs-lookup"><span data-stu-id="d86d6-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="d86d6-325">Чтобы выявить эти аномалии, можно проецировать исходные данные трехмерного пространства в двухмерном пространстве, используя анализ главных компонентов.</span><span class="sxs-lookup"><span data-stu-id="d86d6-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="d86d6-326">Поэтому мы установим значение «2» для параметра количества компонентов в анализе.</span><span class="sxs-lookup"><span data-stu-id="d86d6-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="d86d6-327">Этот параметр играет важную роль в обнаружении аномалий на основе анализа главных компонентов.</span><span class="sxs-lookup"><span data-stu-id="d86d6-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="d86d6-328">Спроецировав данные с использованием этого анализа, определить соответствующие аномалии намного проще.</span><span class="sxs-lookup"><span data-stu-id="d86d6-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="d86d6-329">**Модель обнаружения аномалий для отзыва.** Эта модель предусматривает аналогичное использование модулей Select Columns in Dataset (Выбор столбцов в наборе данных) и PCA-based anomaly detection (Обнаружение аномалий на основе анализа главных компонентов).</span><span class="sxs-lookup"><span data-stu-id="d86d6-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="d86d6-330">В частности, сначала нужно извлечь три переменные — температуру двигателя, наружную температуру и скорость, используя модуль **Select Columns in Dataset** (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="d86d6-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="d86d6-331">Мы также учитываем переменную скорости, так как температура двигателя обычно зависит от скорости.</span><span class="sxs-lookup"><span data-stu-id="d86d6-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="d86d6-332">Далее мы используем модуль обнаружения аномалий на основе анализа главных компонентов, чтобы проецировать данные трехмерного пространства в двухмерном пространстве.</span><span class="sxs-lookup"><span data-stu-id="d86d6-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="d86d6-333">Если температура двигателя и наружная температура подверглись сильной отрицательной корреляции, значит автомобиль отвечает условиям для отзыва и его необходимо отозвать.</span><span class="sxs-lookup"><span data-stu-id="d86d6-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="d86d6-334">Алгоритм обнаружения аномалий на основе анализа главных компонентов позволяет выявлять аномалии после выполнения соответствующего анализа.</span><span class="sxs-lookup"><span data-stu-id="d86d6-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="d86d6-335">При обучении любой модели в качестве входных данных необходимо использовать обычные данные, полученные в условиях, когда не требуется обслуживание или отзыв, как и при обучении модели обнаружения аномалий на основе анализа главных компонентов.</span><span class="sxs-lookup"><span data-stu-id="d86d6-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="d86d6-336">В оценивающем эксперименте мы используем обученную модель обнаружения аномалий, чтобы определить, нужно ли провести обслуживание или отозвать автомобиль.</span><span class="sxs-lookup"><span data-stu-id="d86d6-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="d86d6-337">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="d86d6-337">Real-time analysis</span></span>
<span data-ttu-id="d86d6-338">Следующий SQL-запрос Stream Analytics используется, чтобы получить средние значения таких важных параметров автомобиля, как скорость, уровень топлива, температура двигателя, показания одометра, давление в шинах, уровень моторного масла и др.</span><span class="sxs-lookup"><span data-stu-id="d86d6-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="d86d6-339">Средние значения используются для обнаружения аномалий, выдачи предупреждений и определения общих условий работоспособности автомобилей в определенном регионе, а также сопоставления их с демографическими данными.</span><span class="sxs-lookup"><span data-stu-id="d86d6-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Запрос Stream Analytics для обработки в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="d86d6-341">*Рис. 13. Запрос Stream Analytics для обработки в реальном времени*</span><span class="sxs-lookup"><span data-stu-id="d86d6-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="d86d6-342">Все средние значения вычисляются в 3-секундном окне TumblingWindow.</span><span class="sxs-lookup"><span data-stu-id="d86d6-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="d86d6-343">Мы применили TubmlingWindow, так как необходимо использовать непересекающиеся последовательные интервалы времени.</span><span class="sxs-lookup"><span data-stu-id="d86d6-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="d86d6-344">Дополнительные сведения обо всех возможностях окон в Azure Stream Analytics см. [здесь](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="d86d6-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="d86d6-345">**Прогнозирование в режиме реального времени**</span><span class="sxs-lookup"><span data-stu-id="d86d6-345">**Real-time prediction**</span></span>

<span data-ttu-id="d86d6-346">Для ввода в эксплуатацию модели машинного обучения в режиме реального времени в решение включено отдельное приложение.</span><span class="sxs-lookup"><span data-stu-id="d86d6-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="d86d6-347">Оно называется RealTimeDashboardApp. Это приложение создано и настроено как часть развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="d86d6-348">RealTimeDashboardApp выполняет такие задачи.</span><span class="sxs-lookup"><span data-stu-id="d86d6-348">The application performs the following:</span></span>

1. <span data-ttu-id="d86d6-349">Прослушивает экземпляр концентратора событий, в котором Stream Analytics непрерывно публикует события.</span><span class="sxs-lookup"><span data-stu-id="d86d6-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="d86d6-350">![Запрос Stream Analytics на публикацию данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Рис. 14. Запрос Stream Analytics на публикацию в выходном экземпляре концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="d86d6-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="d86d6-351">Для каждого события, которое получает это приложение:</span><span class="sxs-lookup"><span data-stu-id="d86d6-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="d86d6-352">обрабатывает данные с использованием конечной точки оценки «запрос-ответ» (RRS) системы машинного обучения,</span><span class="sxs-lookup"><span data-stu-id="d86d6-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="d86d6-353">при этом публикация конечной точки происходит автоматически в рамках развертывания;</span><span class="sxs-lookup"><span data-stu-id="d86d6-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="d86d6-354">выходные данные RRS публикуются в наборе данных Power BI при помощи API push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d86d6-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="d86d6-355">Этот шаблон также можно применять в сценариях, когда нужно интегрировать бизнес-приложение с потоком анализа в режиме реального времени для предупреждений, уведомлений и сообщений.</span><span class="sxs-lookup"><span data-stu-id="d86d6-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="d86d6-356">Щелкните [здесь](http://go.microsoft.com/fwlink/?LinkId=717078) , чтобы скачать решение Visual Studio RealtimeDashboardApp для настройки.</span><span class="sxs-lookup"><span data-stu-id="d86d6-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="d86d6-357">**Чтобы запустить приложение панели мониторинга в реальном времени:**</span><span class="sxs-lookup"><span data-stu-id="d86d6-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="d86d6-358">Извлеките его и сохраните на локальном компьютере ![Папка RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Рис. 16. Папка RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="d86d6-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="d86d6-359">Запустите приложение RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="d86d6-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="d86d6-360">Укажите действительные учетные данные Power BI, войдите и нажмите кнопку "Принять".</span><span class="sxs-lookup"><span data-stu-id="d86d6-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Вход в приложение информационной панели в Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Завершение входа в приложение информационной панели в Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="d86d6-363">*Рис. 17. RealtimeDashboardApp: вход в Power BI*</span><span class="sxs-lookup"><span data-stu-id="d86d6-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="d86d6-364">Если необходимо очистить набор данных Power BI, запустите RealtimeDashboardApp с использованием параметра flushdata:</span><span class="sxs-lookup"><span data-stu-id="d86d6-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="d86d6-365">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="d86d6-365">Batch analysis</span></span>
<span data-ttu-id="d86d6-366">Цель этого задания состоит в том, чтобы продемонстрировать, как Contoso Motors использует вычислительные возможности Azure для работы с большими данными и получения исчерпывающих сведений о шаблоне вождения, манере использования и работоспособности автомобиля.</span><span class="sxs-lookup"><span data-stu-id="d86d6-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="d86d6-367">Это позволяет:</span><span class="sxs-lookup"><span data-stu-id="d86d6-367">This makes it possible to:</span></span>

* <span data-ttu-id="d86d6-368">улучшить обслуживание клиентов и снизить его цену, предоставив им сведения о манерах вождения, в том числе тех, которые позволяют оптимизировать расход топлива;</span><span class="sxs-lookup"><span data-stu-id="d86d6-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="d86d6-369">заранее изучить данные о клиентах и их манеры вождения, чтобы принимать правильные бизнес-решения и обеспечивать предоставление лучших в своем классе продуктов и услуг.</span><span class="sxs-lookup"><span data-stu-id="d86d6-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="d86d6-370">В этом решении необходимо получить такие метрики.</span><span class="sxs-lookup"><span data-stu-id="d86d6-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="d86d6-371">**Агрессивная манера вождения**: определяет характеристики модели, расположение, условия вождения и время, чтобы предоставить подробные сведения о шаблоне агрессивного вождения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="d86d6-372">Contoso Motors сможет использовать ее в маркетинговых кампаниях, чтобы предлагать новые персонализированные функции и умное страхование.</span><span class="sxs-lookup"><span data-stu-id="d86d6-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="d86d6-373">**Манера вождения, позволяющая экономить топливо**: определяет характеристики модели, расположение, условия вождения и время года, чтобы предоставить подробные сведения о шаблоне вождения, позволяющем экономить топливо.</span><span class="sxs-lookup"><span data-stu-id="d86d6-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="d86d6-374">Contoso Motors сможет использовать это, чтобы предлагать новые функции, предоставляя сведения о том, как водить с учетом экономии и не вредить окружающей среде.</span><span class="sxs-lookup"><span data-stu-id="d86d6-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="d86d6-375">**Модели определения необходимости в отзыве**: определяет необходимость отзыва модели с помощью эксперимента по выявлению аномалий в рамках машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="d86d6-376">Рассмотрим эти метрики подробнее.</span><span class="sxs-lookup"><span data-stu-id="d86d6-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="d86d6-377">**Шаблон агрессивного вождения**</span><span class="sxs-lookup"><span data-stu-id="d86d6-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="d86d6-378">Секционированные сигналы автомобиля и диагностические данные обрабатываются в конвейере AggresiveDrivingPatternPipeline. При этом используется скрипт Hive, чтобы определить модель, расположение автомобиля, условия вождения и другие параметры, которые характерны для агрессивного вождения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="d86d6-379">![Рабочий процесс для шаблона агрессивного вождения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Рис. 18. Рабочий процесс для шаблона агрессивного вождения*</span><span class="sxs-lookup"><span data-stu-id="d86d6-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="d86d6-380">***Запрос Hive для шаблона агрессивного вождения***</span><span class="sxs-lookup"><span data-stu-id="d86d6-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="d86d6-381">Сценарий Hive aggresivedriving.hql, который используется для анализа шаблона агрессивного вождения, находится в скачанном ZIP-файле в папке \demo\src\connectedcar\scripts.</span><span class="sxs-lookup"><span data-stu-id="d86d6-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="d86d6-382">В нем учитывается включенная передача, положение педали тормоза и скорость автомобиля, которые позволяют идентифицировать неосторожное или агрессивное поведение во время вождения на основе шаблона торможения при высокой скорости.</span><span class="sxs-lookup"><span data-stu-id="d86d6-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="d86d6-383">После успешного выполнения конвейера отобразятся следующие секции, созданные в учетной записи хранения в контейнере connectedcar.</span><span class="sxs-lookup"><span data-stu-id="d86d6-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Выходные данные AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="d86d6-385">*Рис. 19. Выходные данные AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="d86d6-386">**Шаблон вождения для экономии топлива**</span><span class="sxs-lookup"><span data-stu-id="d86d6-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="d86d6-387">Секционированные сигналы автомобиля и диагностические данные обрабатываются в конвейере FuelEfficientDrivingPatternPipeline.</span><span class="sxs-lookup"><span data-stu-id="d86d6-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="d86d6-388">При этом используется скрипт Hive, чтобы определить модель, расположение автомобиля, условия вождения и другие параметры, которые характерны для агрессивного вождения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Шаблон вождения для экономии топлива](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="d86d6-390">*Рис. 20. Рабочий процесс для шаблона вождения, позволяющего экономить топливо*</span><span class="sxs-lookup"><span data-stu-id="d86d6-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="d86d6-391">***Запрос Hive для шаблона вождения, позволяющего экономить топливо***</span><span class="sxs-lookup"><span data-stu-id="d86d6-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="d86d6-392">Сценарий Hive fuelefficientdriving.hql, который используется для анализа шаблона агрессивного вождения, находится в скачанном ZIP-файле в папке \demo\src\connectedcar\scripts.</span><span class="sxs-lookup"><span data-stu-id="d86d6-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="d86d6-393">В нем учитывается включенная передача, положение педали тормоза, педали газа и скорость автомобиля, что дает возможность определить манеру вождения, позволяющую экономить топливо, на основе шаблонов ускорения, торможения и скорости.</span><span class="sxs-lookup"><span data-stu-id="d86d6-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="d86d6-394">После успешного выполнения конвейера отобразятся следующие секции, созданные в учетной записи хранения в контейнере connectedcar.</span><span class="sxs-lookup"><span data-stu-id="d86d6-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Выходные данные FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="d86d6-396">*Рис. 21. Выходные данные FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="d86d6-397">**Прогнозы для отзыва**</span><span class="sxs-lookup"><span data-stu-id="d86d6-397">**Recall Predictions**</span></span>

<span data-ttu-id="d86d6-398">Эксперимент по машинному обучению подготавливается и публикуется в качестве веб-службы в рамках развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="d86d6-399">В этом рабочем процессе используется конечная точка пакетной оценки, регистрируемая в качестве службы, связанной с фабрикой данных. Для ввода в эксплуатацию используется пакетная оценка в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="d86d6-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Конечная точка машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="d86d6-401">*Рис. 22. Конечная точка машинного обучения, зарегистрированная в качестве связанной службы в фабрике данных*</span><span class="sxs-lookup"><span data-stu-id="d86d6-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="d86d6-402">Зарегистрированная связанная служба используется в DetectAnomalyPipeline для оценки данных с использованием модели обнаружения аномалий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Пакетная оценка в фабрике данных в рамках Машинного обучения](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="d86d6-404">*Рис. 23. Пакетная оценка в фабрике данных в рамках Машинного обучения Azure*</span><span class="sxs-lookup"><span data-stu-id="d86d6-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="d86d6-405">В контейнере выполняется несколько шагов по подготовке данных, чтобы их можно было использовать в веб-службе пакетной оценки.</span><span class="sxs-lookup"><span data-stu-id="d86d6-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="d86d6-407">*Рис. 24. DetectAnomalyPipeline для прогнозирования необходимости в отзыве автомобилей*</span><span class="sxs-lookup"><span data-stu-id="d86d6-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="d86d6-408">***Запрос Hive для обнаружения аномалий***</span><span class="sxs-lookup"><span data-stu-id="d86d6-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="d86d6-409">По завершении оценки выполняется действие HDInsight по обработке и агрегации данных, которые с помощью модели отнесены к категории аномалий с вероятностью 0,6 или выше.</span><span class="sxs-lookup"><span data-stu-id="d86d6-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="d86d6-410">После успешного выполнения конвейера отобразятся следующие секции, созданные в учетной записи хранения в контейнере connectedcar.</span><span class="sxs-lookup"><span data-stu-id="d86d6-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Выходные данные DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="d86d6-412">*Рис. 25. Выходные данные DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="d86d6-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="d86d6-413">Опубликовать</span><span class="sxs-lookup"><span data-stu-id="d86d6-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="d86d6-414">Анализ в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="d86d6-414">Real-time analysis</span></span>
<span data-ttu-id="d86d6-415">Один из запросов в задании Stream Analytics предусматривает публикацию событий в выходном экземпляре концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="d86d6-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Публикация данных задания Stream Analytics в выходном экземпляре концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="d86d6-417">*Рис. 26. Публикация данных задания Stream Analytics в выходном экземпляре концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="d86d6-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Запрос Stream Analytics на публикацию в выходном экземпляре концентратора событий](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="d86d6-419">*Рис. 27. Запрос Stream Analytics на публикацию в выходном экземпляре концентратора событий*</span><span class="sxs-lookup"><span data-stu-id="d86d6-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="d86d6-420">Этот поток событий использует приложение RealTimeDashboardApp, которое входит в состав решения.</span><span class="sxs-lookup"><span data-stu-id="d86d6-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="d86d6-421">Приложение RealTimeDashboardApp использует веб-службу машинного обучения типа "ответ на запрос" для оценки в режиме реального времени и публикует результаты в наборе данных Power BI.</span><span class="sxs-lookup"><span data-stu-id="d86d6-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="d86d6-422">Пакетный анализ</span><span class="sxs-lookup"><span data-stu-id="d86d6-422">Batch analysis</span></span>
<span data-ttu-id="d86d6-423">Результаты пакетной обработки и обработки в режиме реального времени публикуются в таблицах Базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d86d6-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="d86d6-424">Сервер, база данных и таблицы SQL Azure создаются автоматически при настройке.</span><span class="sxs-lookup"><span data-stu-id="d86d6-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Копирование результатов пакетной обработки в рабочий процесс киоска данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="d86d6-426">*Рис. 28. Копирование результатов пакетной обработки в рабочий процесс киоска данных*</span><span class="sxs-lookup"><span data-stu-id="d86d6-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Публикация данных задания Stream Analytics в киоске данных](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="d86d6-428">*Рис. 29. Публикация данных задания Stream Analytics в киоске данных*</span><span class="sxs-lookup"><span data-stu-id="d86d6-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Настройка киоска данных в задании Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="d86d6-430">*Рис. 30. Настройка киоска данных в задании Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="d86d6-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="d86d6-431">Использование</span><span class="sxs-lookup"><span data-stu-id="d86d6-431">Consume</span></span>
<span data-ttu-id="d86d6-432">Power BI предоставляет для этого решения расширенную панель мониторинга, предназначенную для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="d86d6-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="d86d6-433">Чтобы получить подробные инструкции по настройке отчетов Power BI и информационной панели, щелкните здесь.</span><span class="sxs-lookup"><span data-stu-id="d86d6-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="d86d6-434">Окончательная панель мониторинга выглядит так:</span><span class="sxs-lookup"><span data-stu-id="d86d6-434">The final dashboard looks like this:</span></span>

![Информационная панель Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="d86d6-436">*Рис. 31. Информационная панель Power BI*</span><span class="sxs-lookup"><span data-stu-id="d86d6-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="d86d6-437">Сводка</span><span class="sxs-lookup"><span data-stu-id="d86d6-437">Summary</span></span>
<span data-ttu-id="d86d6-438">Этот документ содержит подробные сведения о решении для аналитики телеметрии автомобилей.</span><span class="sxs-lookup"><span data-stu-id="d86d6-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="d86d6-439">Здесь показан шаблон лямбда-архитектуры для анализа в режиме реального времени и пакетного анализа с прогнозами и действиями.</span><span class="sxs-lookup"><span data-stu-id="d86d6-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="d86d6-440">Этот шаблон подходит для самых разнообразных сценариев использования, в которых требуется использование «горячего» (в режиме реального времени) и «холодного» (пакетного) анализа.</span><span class="sxs-lookup"><span data-stu-id="d86d6-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

